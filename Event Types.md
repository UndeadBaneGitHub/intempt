# Event types

An event type defines, what type of interaction you would like to capture (page/views visits, clicks and touches etc.). For each event type (or rather, *collection*) there is a set of related properties that you can use to refine your events.

Properties for every event type and collection are dynamic (which is especially important for custom collections) and once you add some property by API, you would see them in the list.

## Web
### View page
*Captures visitor's viewing a specific page on your website.*

You can capture it by specifying an exact path (`/shop/my-category/my-product`), wildcard path to cover a group of pages (`/shop/my-category/*`, `/shop/*/my-product` etc.) in provided input field or by using `Filter` button and picking any other [page-related properties](page-properties).

### Interaction

All event types from interaction group are focusing interaction with specific elements (buttons, forms, inputs etc.) on the page.

You can capture it by specifying an exact form CSS path or path with wildcard in provided input field.

You can also omit specifying exact path, and go for `Filter` button, and pick more page-agnostic input attributes to track, like `id`, `class` and so on. [Here](interaction-properties) you can find the entire list of the properties we track for elements

**WARNING**: the path is specific for this particular input on this particular page, and is built so that it does not include ids or class names. The best tool to acquire a path like that is to use our **Event visualizer** tool. 
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

#### Page element exists
*Captures existence (appearance or disappearance) of an element on a page. Once an element appears (or a page with it is first opened), its state is captured and sent as an event, and until element disappears (or the respective page has been left).*

Any changes to element *after* it has appeared on the page are **not** tracked via this event type

#### Page element changed
*Captures changes of an element on a page. Once any property of the element is changed (which can be text, style, attributes and so on), its new state is captured and sent as an event.*

This event is not triggered for the first appearance of an element - only once it has been changed after appearance this event would be received.

To track page element changes, you should specify CSS selector for this element. This CSS selector can be in any form you might choose: it could be a specific path to a specific element, or it can be a more generic class-based selector.

***WARNING***: tracking too many page elements can affect performace of your pages. While very handy and convenient, try to restrict number of elements simultaneously tracked.

### Custom

Our client-side API allows creation of any event type you might desire to be tracked for your page or application.

This event type was designed to allow you viewing statistics for these event types and some Intempt-built event types (like `Visitor` and `Visit`), that did not get their own event type.

After you select this event type, next to it you can see a dropdown list with all the collections, that have not been covered by our other event types. After a collection has been selected, by clicking `Filter` button you can add filters for and of the properties that you (or we for Intempt-defined collections) might have tracked for this collection.
