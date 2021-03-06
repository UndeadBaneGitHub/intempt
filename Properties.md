# Properties overview

Properties are tools by which you can properly slice the data that we have automatically collected from your website or application. Using them in our event and segment constructors via applying filters (`Filter` button) you can slice out pretty precise behaviors, like "new visitors who have seen the page twice and clicked some Add To Cart button" or "recurring male visitors from Brazil who have not made a new purchase withing the last month". To allow identifying such wide variety of actions, default property structure has to be really complex (and it is, as you can see in [structure](properties-structure) section).

However, if you find, that you somehow cannot slice desired actions well enough, or it is too inconvenient, you can also dynamically define new properties and even new event collections via our [API](https://github.com/intempt/intempt/blob/master/API.md).

## Property name structure

Our properties are hierarchical, split into collections for convenience in the interface, and are also filtered by [event collections](https://github.com/intempt/intempt/blob/master/Events.md) (for example, properties for `timeseries.element` are visible only while creating elements-related events, like `interaction` or `page_element_changed`).

For convenience in UI, our hierarchy is flattened with parent collections preceeding child in property names. So, for example, name for property `value` for `background-color` in collection `style`, in collection `timeseries` would look in query constructor like `timeseries.style.background-color.value`.

Every property in constructor is also decorated with human-readable title and description, allowing easier navigation amongst them. So while there are many various properties in many various collections displayed in the list, entering desired "background" or "Element" would filter the wide list to a much more usable and relative selection.

# Properties collections details

## `fixed` collection

Non-event-specific properties that are always tracked and populated for every event. They describe things like browser or operating system properties, timezone, whether visitor is identified and when was this visitor first to the website and so on.
Properties from this collection are also the only ones, available for being used in **segment** filters directly (all others are limited to events).

In this category also fall `visitor` and `visit`-related properties (as they are pretty static) like geolocation or browser data.

## `timeseries` collection

Event-specific properties, subsets of which are collected, varying by [event collections](https://github.com/intempt/intempt/blob/master/Events.md). This high-level collection also would contain whatever custom collection might be created on client side. In sub-collections of `timeseries` one can find various information, like `element` properties (`id`, `class` etc.), style attributes for `page_element_exists` and `page_element_failed` events, ID of campaign, which the visitor has qualified for and so on.

# Properties structure

    fixed
    ├── browser
    │   ├── device
    │   │   ├── family
    │   │   └── name
    │   ├── os
    │   │   ├── extension
    │   │   ├── family
    │   │   ├── major
    │   │   ├── minor
    │   │   └── patch
    │   └── user_agent
    │       ├── family
    │       ├── major
    │       ├── minor
    │       └── patch
    ├── first_seen
    ├── geo
    │   ├── city
    │   ├── country
    │   │   ├── iso_code
    │   │   └── name
    │   ├── location
    │   │   ├── lat
    │   │   └── lon
    │   ├── postal
    │   └── subdivision
    │       ├── iso_code
    │       └── name
    ├── identified
    ├── identifier
    ├── initial_referrer
    │   ├── domain
    │   ├── hash
    │   ├── href
    │   ├── origin
    │   ├── path
    │   ├── port
    │   └── query
    ├── landing_page
    ├── lang
    ├── platform
    ├── screen
    │   ├── color_depth
    │   └── resolution
    ├── timezone
    ├── utm
    │   ├── campaign
    │   ├── content
    │   ├── medium
    │   ├── source
    │   └── term
    └── visitorid

    timeseries
    ├── applicationid
    ├── campaign_id
    ├── campaign_name
    ├── clicked
    ├── client_ip
    ├── control
    ├── element
    │   ├── classList
    │   ├── className
    │   ├── exists
    │   ├── href
    │   ├── id
    │   ├── number
    │   ├── path
    │   ├── tag
    │   ├── tagName
    │   ├── text
    │   ├── type
    │   └── value
    ├── email
    ├── eventid
    ├── fixed
    ├── href
    ├── identified
    ├── identifier
    ├── ids
    │   ├── id
    │   ├── org
    │   ├── session
    │   └── tracker
    ├── intempt
    │   └── visit
    │       └── trackcharge
    ├── keyword
    ├── message
    ├── messageVariant
    ├── received
    ├── referrer
    │   ├── domain
    │   ├── hash
    │   ├── host
    │   ├── hostname
    │   ├── href
    │   ├── origin
    │   ├── path
    │   ├── port
    │   ├── protocol
    │   └── query
    ├── sent
    ├── style
    │   ├── -webkit-app-region
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-appearance
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-background-clip
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-background-origin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-border-horizontal-spacing
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-border-image
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-border-vertical-spacing
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-align
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-decoration-break
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-direction
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-flex-group
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-flex
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-lines
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-ordinal-group
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-orient
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-pack
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-box-reflect
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-clip-path
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-font-smoothing
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-highlight
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-hyphenate-character
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-line-break
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-line-clamp
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-locale
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-margin-after-collapse
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-margin-before-collapse
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-box-image-outset
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-box-image-repeat
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-box-image-slice
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-box-image-source
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-box-image-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-box-image
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-clip
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-composite
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-image
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-origin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-position
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-repeat
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-mask-size
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-print-color-adjust
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-rtl-ordering
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-tap-highlight-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-combine
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-decorations-in-effect
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-emphasis-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-emphasis-position
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-emphasis-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-fill-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-orientation
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-security
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-stroke-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-text-stroke-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-user-drag
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-user-modify
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── -webkit-writing-mode
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── align-content
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── align-items
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── align-self
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── alignment-baseline
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-delay
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-direction
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-duration
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-fill-mode
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-iteration-count
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-name
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-play-state
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── animation-timing-function
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── backface-visibility
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-attachment
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-blend-mode
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-clip
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-image
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-origin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-position
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-repeat
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── background-size
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── baseline-shift
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-bottom-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-bottom-left-radius
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-bottom-right-radius
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-bottom-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-bottom-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-collapse
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-image-outset
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-image-repeat
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-image-slice
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-image-source
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-image-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-left-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-left-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-left-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-right-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-right-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-right-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-top-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-top-left-radius
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-top-right-radius
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-top-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── border-top-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── bottom
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── box-shadow
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── box-sizing
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── break-after
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── break-before
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── break-inside
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── buffered-rendering
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── caption-side
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── clear
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── clip-path
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── clip-rule
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── clip
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── color-interpolation-filters
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── color-interpolation
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── color-rendering
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-count
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-gap
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-rule-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-rule-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-rule-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-span
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── column-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── content
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── cursor
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── cx
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── cy
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── d
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── direction
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── display
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── dominant-baseline
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── empty-cells
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── fill-opacity
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── fill-rule
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── fill
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── filter
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flex-basis
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flex-direction
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flex-grow
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flex-shrink
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flex-wrap
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── float
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flood-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── flood-opacity
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-family
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-kerning
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-size
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-stretch
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-variant-caps
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-variant-ligatures
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-variant-numeric
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-variant
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── font-weight
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── height
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── image-rendering
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── isolation
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── justify-content
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── left
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── letter-spacing
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── lighting-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── line-height
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── list-style-image
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── list-style-position
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── list-style-type
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── margin-bottom
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── margin-left
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── margin-right
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── margin-top
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── marker-end
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── marker-mid
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── marker-start
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── mask-type
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── mask
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── max-height
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── max-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── min-height
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── min-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── mix-blend-mode
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── motion-offset
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── motion-path
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── motion-rotation
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── object-fit
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── object-position
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── opacity
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── order
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── orphans
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── outline-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── outline-offset
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── outline-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── outline-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── overflow-wrap
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── overflow-x
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── overflow-y
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── padding-bottom
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── padding-left
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── padding-right
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── padding-top
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── paint-order
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── perspective-origin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── perspective
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── pointer-events
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── position
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── r
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── resize
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── right
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── rx
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── ry
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── shape-image-threshold
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── shape-margin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── shape-outside
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── shape-rendering
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── speak
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stop-color
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stop-opacity
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-dasharray
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-dashoffset
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-linecap
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-linejoin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-miterlimit
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-opacity
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke-width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── stroke
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── tab-size
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── table-layout
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-align-last
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-align
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-anchor
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-decoration
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-indent
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-overflow
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-rendering
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-shadow
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-size-adjust
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── text-transform
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── top
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── touch-action
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transform-origin
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transform-style
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transform
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transition-delay
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transition-duration
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transition-property
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── transition-timing-function
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── unicode-bidi
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── user-select
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── vector-effect
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── vertical-align
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── visibility
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── white-space
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── widows
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── width
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── will-change
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── word-break
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── word-spacing
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── word-wrap
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── writing-mode
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── x
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── y
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   ├── z-index
    │   │   ├── number
    │   │   ├── unit
    │   │   └── value
    │   └── zoom
    │       ├── number
    │       ├── unit
    │       └── value
    ├── title
    ├── trackerid
    ├── treated
    ├── treater_id
    ├── treater_name
    ├── treatment_name
    ├── treatment_value
    ├── type
    ├── url
    │   ├── hash
    │   ├── host
    │   ├── hostname
    │   ├── href
    │   ├── origin
    │   ├── path
    │   ├── port
    │   ├── protocol
    │   ├── query
    │   └── domain
    ├── uuid
    ├── visitid
    └── visitorid
