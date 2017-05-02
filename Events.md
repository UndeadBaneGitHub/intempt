# Event capturing

Our system automatically collects various events from your page or your app, and every event belongs to an `event collection`. The collections have hierarchical tree-like structure, that allows events "down the line" to acquire and use information from parent events, thus allowing better data slicing later during even definition. The collections tree looks as following:

    visit
    ├── visitor
    ├── page
    │   ├── interaction
    │   ├── page_element_exists
    │   ├── page_element_changed*
    │   ├── page_property_changed
    │   ├── category_changed
    │   └── product_changed
    ├── identify
    ├── view
    │   └── interaction
    └── custom

Some events in addition to `collection` are specified by internal `type` property (like `click`, `change`, `touch` etc).
    
After events have been collected, this data can be sliced in console via creating event definitions there. And these definitions correspond to collections.

# Event definitions

An event type defines, what type of interaction you would like to capture (page/views visits, clicks and touches etc.). For each event type (or rather, *collection*) there is a set of related properties that you can use to refine your events.

Properties for every event type and collection are dynamic (which is especially important for custom collections) and once you add some property by API, you would see them in the list.

## Web
### View page (`page` collection)
*Captures visitor's viewing a specific page on your website.*

You can capture it by specifying an exact path (`/shop/my-category/my-product`), wildcard path to cover a group of pages (`/shop/my-category/*`, `/shop/*/my-product` etc.) in provided input field or by using `Filter` button and picking any other [page-related properties](page-properties).

### Interaction (`interaction` collection)

All event types from interaction group are focusing interaction with specific elements (buttons, forms, inputs etc.) on the page.

You can capture it by specifying an exact element's CSS path or path with wildcard in provided input field.

You can also omit specifying exact path, and go for `Filter` button, and pick more page-agnostic attributes to track, like `id`, `class` and so on. [Here](interaction-properties) you can find the entire list of the properties we track for elements

**WARNING**: the path is specific for this particular element on this particular page, and is built so that it does not include ids or class names. The best tool to acquire a path like that is to use our **Event visualizer** tool. 
However, we recommend going for more generic attributes.

#### Click on
*Captures visitor's clicking on any element on the page. This can be a button, link or even "passive" variant (like image with no action).*

#### Submit on
*Captures visitor's submitting a selected form.*

#### Change on
*Captures visitor's changing an input like text input, radio button, checkboxes and text areas.* 

### Page element

Page element types are desiged to capture changes in elements on your page. That can be element existence (e.g. a message appeared, or dynamic cart element has been shown) or changes of an element (items count in cart, filter value on the page etc.).

Page element event type is, unlike [`view page`](view-page) and [`interaction`](interaction) types is **non-retrospective** event type.
This means, that until you have defined an event of `Page Element` type, no data capturing is being done.

#### Page element exists (`page_element_exists` collection)

*Captures existence (appearance or disappearance) of an element on a page. Once an element appears (or a page with it is first opened), its state is captured and sent as an event, and until element disappears (or the respective page has been left).*

Any changes to element *after* it has appeared on the page are **not** tracked via this event type

*IMPORTANT*: This event type captures the appearance of *the first element*, picked by specified selector and disappearance of *the last one*, left on the page. So, if your logic adds consequently 10 elements, *only* once the first one appears the event would be triggered. Similarly, if you have 10 elements on the page that you logic is removing, *only* once the last one is removed the disappearance event would be triggered.

#### Page element changed (`page_element_changed` collection)
*Captures changes of an element on a page. Once any property of the element is changed (which can be text, style, attributes and so on), its new state is captured and sent as an event.*

This event is not triggered for the first appearance of an element - only once it has been changed after appearance this event would be received.

To track page element changes, you should specify CSS selector for this element. This CSS selector can be in any form you might choose: it could be a specific path to a specific element, or it can be a more generic class-based selector.

***WARNING***: tracking too many page elements can affect performace of your pages. While very handy and convenient, try to restrict number of elements simultaneously tracked.

## iOS

Much like for Web tracking, for iOS tracking we also generate unique path for each element and each view with start at the main window.
As iOS does not have "common" unique path mechanism, we devised a CSS-like path ourselves to improve quality of tracked data and prevent miscaptures.

This however means, that it is very hard to write down this path manually, so if you plan on using view element path to track interaction with specific element in specific view, it is almost essential to use our **Event Stream** tool.

### View open (`view` collection)
*Captures visitor's viewing a specific view in your app.*

You can capture it by specifying an exact path, wildcard path to cover a group of views in provided input field or by using `Filter` button and picking any other [view-related properties](view-properties).

### Interaction (`interaction` collection)

Captures touches, slides, zoom-ins and changes for all elements in all views.

You can capture specific interaction with specific element by specifying an exact path or path with wildcard to this element in provided input field.

You can also omit specifying exact path, and go for `Filter` button, and pick more element-agnostic attributes to track, like `UIViewController`, `class` and so on. [Here](ios-interaction-properties) you can find the entire list of the properties we track for elements

**WARNING**: the path is specific for this particular element on this particular view. The best tool to acquire a path like that is to use our **Event Stream** tool. 
However, we recommend going for more generic attributes.

#### Touch on
*Captures visitor's touching on any element on the page. This can be a button, link or even "passive" variant (like image with no action).*

#### Change on
*Captures visitor's changing an input like text input, radio button, checkboxes and text areas.*

### Interaction Action
*Captures any action, that happens within your app, caused by user's action or automatic*

You can capture specific action by providing its full name in the given input (e.g. `someAction:withParams:andSomeMore:`), or by omiting it and adding `target` or `sender`-specific properties in `Filter` section.

For `target` and `sender` minimal tracked property is `class` - only this property is tracked for non-visual `target`s and `sender`s. However, if either of them is visual, for such more properties would be tracked, similar to [Interaction](interaction) event type elements

## Common
### Custom (`visitor`, `visit`, `identify` and custom collections)

Our client-side API allows creation of any event type you might desire to be tracked for your page or application.

This event type was designed to allow you viewing statistics for these event types and some Intempt-built event collections (like `visitor` and `visit`), that did not get their own event type.

After you select this event type, next to it you can see a dropdown list with all the collections, that have not been covered by our other event types. After a collection has been selected, by clicking `Filter` button you can add filters for and of the properties that you (or we for Intempt-defined collections) might have tracked for this collection.
