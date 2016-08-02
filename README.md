# Load tracker
To load tracker on your page, include this code into your <head> or <body> tag:

    <script type="text/javascript">
    window.addEventListener("intempt.YOUR_TRACKER_NAME.ready", function() {
      //do something when tracker has been loaded;
      //the tracker object becomes accessible at window._intempt["site"] after loading;
    });
    !function(a,b){if(window.__intempt&&window._intempt)a&&(window.__intempt.init_tracker?window.__intempt.init_tracker(a):window.__intempt.startup_configs.push(a));else{window.__intempt={},window.__intempt.startup_configs=[],a&&window.__intempt.startup_configs.push(a);var c=document.createElement("script");c.type="text/javascript",c.async=!0,c.src=b||"https://cdn.intempt.co/intempt.min.js";var d=document.getElementsByTagName("script")[0];d.parentNode.insertBefore(c,d)}}({orgId:"YOUR_ORG_NAME",trackerId:"YOUR_TRACKER_NAME",token:"YOUR_TRACKER_TOKEN"});
    </script>

This code is auto-generated on your tracker's settings page and upon tracker's creation for convenience.

Notifications mechanism is also auto-loaded onto the page, so once your visitor is compliant with campaign requirements, he will see notification ribbon appearing for him without any need to change anything from your side.
However, if you want to display notifications somehow differently, for instance, use very custom design, you would need to do some modifications to the way tracker is loaded. Check [API Notifications Client](API Notifications Client) for details.


# Identify and track visitors
Once the tracker is loaded and tracker initialization is complete, you would receive `intempt.YOUR_TRACKER_NAME.ready` event. After this, you can start identifying your visitors and track their activity with custom events using populated tracker object.
#### Warning:
Before tracker initialization has been finished, tracker object does not exist! So, for safety, you might want to include a check, that tracker object has been sucessfully populated, for safety:

    if (window._intempt && window._intempt['YOUR_TRACKER_NAME']) {
        // Perform your tracker operations here
    }

## Identify a visitor
To identify a visitor, embed the following call in your page scripts:

    window._intempt["YOUR_TRACKER_NAME"].identify({
        identifier: 'your_user_identifier'
    })

You can add any additional fields to the idnetify call, but `identifier` is mandatory, as that is how our backend distinguishes an identified visitior from anonymous one.

## Track custom event
While our tracker automatically tracks all visitor's interactions with your page, you might find it necessary to track custom events, you can totally do it! In general, to perform custom event tracking, all you need to do is to implement a call like that:

    window._intempt["YOUR_TRACKER_NAME"].track("YOUR_COLLECTION_NAME", {
        "your.property": "your value"
    })

One of the cases that you might find particulary useful is tracking purchases on your site. To perform such special tracking operation, use the following code:

        window._intempt["YOUR_TRACKER_NAME"].track("purchase", {
            "item": "Your item name",
            "price": "31.99",
            "timestamp": new Date().getTime(),
            "fixed.name": "John Smith",
            "fixed.age": 28,
            "fixed.color": ["255", "255", "255"],
            "intempt.visit.trackcharge": "31.99"
        })

Notice some special features about our tracking. First, for tracking site purchases (and thus, monetary conversion) we have set up a special collection called `purchase` which you should track your event into. In order for purchase amount to be automatically tracked, you need to include `intempt.visit.trackcharge` field in your object.

This example has also some additional important features about this call.
In your custom event object you can include not only completely custom fields (`item`, `price` and `timestamp` in this example), but also any properties of our `fixed` collection. If these properties are included, they will be automatically processed by our system and taken into consideration in respective reports and segments.

#API Notifications Client
In case you want some really custom display of notifications your visitor recieves, you can use our notifications API.
To disable default notifications display and enable API, first you need to modify your tracker insertion call to include `apiMode: true` in initialization parameters like this:

    <script type="text/javascript">
    window.addEventListener("intempt.YOUR_TRACKER_NAME.ready", function() {
      //do something when tracker has been loaded;
      //the tracker object becomes accessible at window._intempt["site"] after loading;
    });
    !function(a,b){if(window.__intempt&&window._intempt)a&&(window.__intempt.init_tracker?window.__intempt.init_tracker(a):window.__intempt.startup_configs.push(a));else{window.__intempt={},window.__intempt.startup_configs=[],a&&window.__intempt.startup_configs.push(a);var c=document.createElement("script");c.type="text/javascript",c.async=!0,c.src=b||"https://cdn.intempt.co/intempt.min.js";var d=document.getElementsByTagName("script")[0];d.parentNode.insertBefore(c,d)}}({orgId:"YOUR_ORG_NAME",trackerId:"YOUR_TRACKER_NAME",token:"YOUR_TRACKER_TOKEN",apiMode:true});
    </script>

Once that has been done, events to handle incoming notifications are activated.
To recieve notification payload, you need to subscribe to `intempt.notifications.notification` event like this:

    window.addEventListener('intempt.notifications.notification', function(event) {
        // event.detail contains object payload, that looks like this:
        // {
        //     id: "abcdef12345",
        //     html: "<div class="intempt-api-notificaiton-container" intempt-notification-id="8ce51fe2727fb" style="animation-name: intemptInsertNotificationMessage;"><div class="intempt-api-notification-message"><p>YOUR NOTIFICATION MESSAGE/p></div><div class="intempt-api-notification-btn-group"><button type="button" onclick="window._intempt.__td('8ce51fe2727fb')">Dismiss</button></div></div>"
        // }
    })

And now all you need to do is insert the `html` whereever you might want on your page! Tracking clicks, embedded in the message and whether or not your visitor saw your notification and even dismisses (and removing notification html from the page) is done completely automatically!

You can also get list of currently received and non-dismissed notification objects by calling `window._intempt.getNotificationsList`.
To get a specific notification object, we provided also `window._intempt.getNotificationById(notificationId)` method, that would return you exactly the same object that you have earlier recieved in an event.

Also, HTML in notificaiton is always structured identically, so that you could apply any custom styling to it with ease:

    <div class="intempt-api-notificaiton-container" intempt-notification-id="8ce51fe2727fb" style="animation-name: intemptInsertNotificationMessage;">
      <div class="intempt-api-notification-message">
        <p>YOUR NOTIFICATION MESSAGE/p>
      </div>
      <div class="intempt-api-notification-btn-group"><button type="button" onclick="window._intempt.__td('8ce51fe2727fb')">Dismiss</button></div>
    </div>

As you can see, all necessary data (including Dismiss button) is already there and namespaced.

#### Warning:
Do not change HTML content of notification, as it is not guaranteed, that tracking clicks, views and dismisses would still be working properly afterwards!

Once the visitor dismisses your notification, we automatically find it in the page and remove it from there. In order to allow you handle dismisses in a special way, `intempt.notifications.dismissed` is emitted:

    window.addEventListener('intempt.notifications.dismissed', function(event) {
        // event.detail contains object payload, that looks like this:
        // {
        //     id: "abcdef12345",
        //     html: "<div class="intempt-api-notificaiton-container" intempt-notification-id="8ce51fe2727fb" style="animation-name: intemptInsertNotificationMessage;"><div class="intempt-api-notification-message"><p>YOUR NOTIFICATION MESSAGE/p></div><div class="intempt-api-notification-btn-group"><button type="button" onclick="window._intempt.__td('8ce51fe2727fb')">Dismiss</button></div></div>"
        // }
        //
    })

Payload of this event contains dismissed notification content, both `id` and `html`