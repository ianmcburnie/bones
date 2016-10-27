# BONES

> Widgets are stronger with bones. Does *your* widget have bones?

## Contents

1. [Introduction](#user-content-introduction)
1. [Accordion](#user-content-accordion)
1. [Breadcrumbs](#user-content-breadcrumbs)
1. [Carousel](#user-content-carousel)
1. [Combobox](#user-content-combobox)
1. [Dialog](#user-content-dialog)
1. [Faux Menu](#user-content-faux-menu)
1. [Faux Tabs](#user-content-faux-tabs)
1. [Flyout](#user-content-flyout)
1. [Input Validation](#user-content-input-validation)
1. [Menu](#user-content-menu)
1. [Page Alert](#user-content-page-alert)
1. [Pagination](#user-content-pagination)
1. [Radio](#user-content-radio)
1. [Tabs](#user-content-tabs)
1. [Tooltip](#user-content-tooltip)

## Introduction

Bones provides lean, mean, semantic HTML markup for widgets; ensuring maximum Accessibility, SEO and Site Speed performance. Bones markup has full support for <a href="http://www.w3.org/WAI/intro/aria"> WAI-ARIA</a> roles, states and properties.

Bones favors the <a href="http://en.wikipedia.org/wiki/Convention_over_configuration">convention over configuration</a> paradigm. A convention for widget structure allows us to add only a minimal amount of CSS and JavaScript 'hooks' to the base markup.<sup>1</sup>

Bones advocates the [Progressive Enhancement](http://en.wikipedia.org/wiki/Progressive_enhancement) web-design strategy; building the web in a layered fashion that allows **everyone** to access the **most important** content and functionality. We supply HTML markup for both the *before* and *after*  JavaScript initialisation states of a widget, i.e. before-enhancement and after-enhancement. If you do not wish to support progressive enhancement we also provide alternatives.<sup>2</sup>

<sub><sup>1</sup> Bones has a class naming convention similar to the <a href="http://smacss.com">SMACSS</a> architecture, whereby we define a single module name on our root node, alongside any additional *modifier* class names, such as states & themes. If additional classes are needed in the inner HTML, we encourage a BEM-style (block-level-element) naming convention and syntax.</sub>

<sub><sup>2</sup> Building an app that is rendered entirely on the client-side? If so, you will only need to refer to the enhanced/initialised code. However, best practice is to build apps in an <a href="http://nerds.airbnb.com/isomorphic-javascript-future-web-apps/">isomorphic</a> fashion so that first page load is rendered by the server then *enhanced* on the client.</sub>

## [Accordion](https://ebay.gitbooks.io/mindpatterns/content/disclosure/accordion.html)

### Before JavaScript Initialisation

An accordion requires 2 or more panels of content.

```html
<div class="accordion" id="accordion1">
    <h2>Accordion Title</h2>
    <div>
        <h3>Panel 1 Title</h3>
        <div>
            <!-- panel contents go here -->
        </div>
    </div>
    <div>
        <h3>Panel 2 Title</h3>
        <div>
            <!-- panel contents go here -->
        </div>
    </div>
    <div>
        <h3>Panel 3 Title</h3>
        <div>
            <!-- panel contents go here -->
        </div>
    </div>
</div>
```

### After JavaScript Initialisation

Tree structure remains identical, but many new attributes are added. Zero or more panels can be selected & visible at any time.

```html
<div class="accordion accordion--js" role="tablist">
    <h2>Accordion Title</h2>
    <div>
        <h3 aria-controls="accordion1_panel1" aria-selected="false" id="accordion1_tab1" role="tab" tabindex="0">Panel 1 Title</h3>
        <div aria-hidden="true" aria-labelledby="accordion1_tab1" id="accordion1_panel1" role="tabpanel">
            <!-- panel contents go here -->
        </div>
    </div>
    <div>
        <h3 aria-controls="accordion1_panel2" aria-selected="false" id="accordion1_tab2" role="tab" tabindex="-1">Panel 2 Title</h3>
        <div aria-hidden="true" aria-labelledby="accordion1_tab2" id="accordion1_panel2" role="tabpanel">
            <!-- panel contents go here -->
        </div>
    </div>
    <div>
        <h3 aria-controls="accordion1_panel3" aria-selected="false" id="accordion1_tab3" role="tab" tabindex="-1">Panel 3 Title</h3>
        <div aria-hidden="true" aria-labelledby="accordion1_tab3" id="accordion1_panel3" role="tabpanel">
            <!-- panel contents go here -->
        </div>
    </div>
</div>
```

## [Breadcrumbs](https://ebay.gitbooks.io/mindpatterns/content/navigation/breadcrumbs.html)

The content is an ordered list of links inside a navigation landmark region. Breadcrumbs do not require JavaScript initialisation. CSS can be used to generate → separator content.

```html
<nav class="crumbs" aria-labelledby="crumbs_heading" role="navigation">
    <h2 id="crumbs_heading">You are here</h2>
    <ol>
        <li><a href="http://www.ebay.com">Great Grandparent Page</a></li>
        <li><a href="http://www.ebay.com">Grandparent Page</a></li>
        <li><a href="http://www.ebay.com">Parent Page</a></li>
        <li><span>Current Page</span></li>
    </ol>
</nav>
```

## [Carousel](https://ebay.gitbooks.io/mindpatterns/content/disclosure/carousel.html)

### Before JavaScript Initialisation

A carousel is a list of items. These items can contain anything - text, images, links, tiles, cards, etc. - but we advise against using complex widgets. The usual accessibility rules apply to the contents of these items (tab-order, semantics, etc).

For the server rendered markup you can choose to render as little or as much of the full list as you wish. Client-side script can lazy-load in additional items as desired.

```html
<div class="carousel">
    <h2 class="carousel__title">Items<span class="clipped"> - Carousel</span></h2>
    <ul>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        ...
    </ul>
</div>
```

### After JavaScript Initialisation

JavaScript adds a live status region after the heading, and two pagination buttons either side of the list.

```html
<div class="carousel">
    <h2 class="carousel__title">List of Stuff<span class="clipped"> - Carousel</span></h2>
    <p aria-live="polite" class="clipped" role="status">Showing slide 1 of n - Items - Carousel</p>
    <button aria-disabled="false" aria-label="Show previous n items of stuff"></button>
    <ul>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        ...
    </ul>
    <button aria-disabled="false" aria-label="Show next n items of stuff"></button>
</div>
```

JavaScript must maintain the tabindex and aria-hidden state of items as they scroll in and out of view. Items that are not in view need a tabindex value of "-1" an aria-hidden value of "true" to ensure items are hidden from keyboard users and screen reader users respectively.

JavaScript must also maintain the state of the status region.

For small touch screens, you may wish to utilise swipe gestures. In which case pagination buttons can be hidden offscreen, appearing only on keyboard focus (i.e. 'stealth' buttons) for keyboard users.

## Combobox

### Before JavaScript Initialisation

Without JavaScript, the combobox markup is a simple text input with label:

```html
<div class="combobox" id="combobox-1">
    <label for="combobox-1-input">Combobox Label</label>
    <input id="combobox-1-input" name="combobox-1-name" type="text">
</div>
```

### After JavaScript Initialisation

JavaScript adds the button, instructions and listbox to the markup.

```html
<div class="combobox" id="combobox-1" role="application">
    <label for="combobox-1-input">Combobox Label</label>
    <input id="combobox-1-input" name="combobox-1-name" type="text" role="combobox" aria-expanded="false" autocomplete="off" aria-owns="combobox-1-listbox" aria-describedby="combobox-1-instructions">
    <button type="button" tabindex="-1" aria-label="Expand Options"></button>
    <span id="combobox-1-instructions">Use up and down arrow keys to navigate options</span>
    <ul id="combobox-1-listbox" role="listbox">
        <li role="option" id="combobox-1-option-1">Option 1</li>
        <li role="option" id="combobox-1-option-2">Option 2</li>
        <li role="option" id="combobox-1-option-3">Option 3</li>
        ...
    </ul>
</div>
```

After arrow key up or down, JavaScript must update the `aria-activedescendant` attribute to reflect the state of the currently active descendant item. For example, if arrow key down is pressed:

```html
<div class="combobox" id="combobox-1" role="application">
    <label for="combobox-1-input">Combobox Label</label>
    <input id="combobox-1-input" name="combobox-1-name" type="text" role="combobox" aria-activedescendant="combobox-1-option-1" aria-expanded="true" autocomplete="off" aria-owns="combobox-1-listbox" aria-describedby="combobox-1-instructions">
    <button type="button" tabindex="-1" aria-label="Expand Options"></button>
    <span id="combobox-1-instructions">Use up and down arrow keys to navigate options</span>
    <ul id="combobox-1-listbox" role="listbox">
        <li role="option" id="combobox-1-option-1" aria-selected="true">Option 1</li>
        <li role="option" id="combobox-1-option-2">Option 2</li>
        <li role="option" id="combobox-1-option-3">Option 3</li>
        ...
    </ul>
</div>
```

Notice that `role="application"` is required to prevent JAWS virtual cursor from leaving listbox when up/down arrow keys are used. This role essentially forces JAWS into application mode, and is one of the few valid use cases we have for this role.

## [Dialog](https://ebay.gitbooks.io/mindpatterns/content/structure/dialog.html)

```html
<div aria-labelledby="dialog_title" class="dialog" role="dialog">
    <div role="document">
        <header role="banner">
            <button aria-label="Close Dialog" class="dialog__close"></button>
            <h2 id="dialog_title">Dialog Title</h2>
        </header>
        <div>
            <!-- dialog content goes here -->
        </div>
    </div>
</div>
```

**NOTE:** header tag is not supported in IE8 and below - use HTML5Shiv or substitute for a div tag instead.

## [Faux Menu](https://ebay.gitbooks.io/mindpatterns/content/navigation/fauxmenu.html)

### Before JavaScript Initialisation

The content is a button and a list of links. Use an ordered list if the items are semantically ordered in any way.

```html
<div class="fauxmenu">
    <button disabled>Open Nav</button>
    <ul>
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
    </ul>
</div>
```

Remember that this button will not work without JavaScript. Therefore we disable it in our markup and then enable it with JavaScript.

### After JavaScript Initialisation

```html
<div class="fauxmenu fauxmenu--js" id="fauxmenu_0">
    <button aria-controls="fauxmenu_0_flyout" aria-expanded="false">Open Nav</button>
    <ul id="fauxmenu_0_flyout">
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
    </ul>
</div>
```

If you require a faux menu that is opened by hovering on a link, rather than clicking on a button, then append an offscreen popup button immediately after the anchor tag. This button will appear, and receive focus, as soon as the user tabs past the hyperlink.

## Faux Tabs

Faux tabs appear like regular tabs, but behave like a regular list of links. No JavaScript or ARIA is required.

```html
<div class="faux-tabs" id="faux-tabs-1">
    <h2 class="clipped">Faux Tabs Heading</h2>
    <ul>
        <li>
            <a href="http://www.ebay.com/1">Page 1</a>
        </li>
        <li>
            <a href="http://www.ebay.com/2">Page 2</a>
        </li>
        <li>
            <a href="http://www.ebay.com/3">Page 3</a>
        </li>
    </ul>
</div>
```

NOTE: You may wish to use `role="navigation"` on the root div if these links are prominent navigation links.

## [Flyout](https://ebay.gitbooks.io/mindpatterns/content/disclosure/flyout.html)

A flyout might open on click, focus or hover, on any kind of button, input or link. Regardless of what type of element or interaction is used to trigger the flyout, the overlay element must immediately follow the trigger element. This structure ensures a seamless and natural reading order and focus order.

```html
<div class="flyout">
    <button aria-expanded="false|true">Button</button>
    <div class="flyout__overlay-container" aria-live="off|polite|assertive">
        <div class="flyout__overlay">
            <!-- flyout contents -->
        </div>
    </div>
</div>
```

In order for live-region support to work correctly in Voiceover, any hide/show operation (i.e. display:none|block) must be performed on the `flyout__overlay`, not the `flyout__overlay-container`.

Note that Menu, Faux Menu, Tooltip & Combobox are special instances of flyouts, but follow the same general pattern in that their overlay element must immediately follow the trigger element.

## [Input Validation](https://ebay.gitbooks.io/mindpatterns/content/messaging/inputvalidation.html)

Input validation messages depend fully on JavaScript; they are considered an enhancement in *addition* to full form validation (form validation does not require JavaScript).

### Before JavaScript Initialisation

```html
<div class="inputvalidation">
    <span>
        <label for="input1">Input 1</label>
        <input aria-invalid="false" aria-required="false" id="input1" name="input1" type="text" value="" />
    </span>
    <!-- error container will be inserted here -->
</div>
```

### After JavaScript Initialisation

```html
<div class="inputvalidation inputvalidation--js">
    <span>
        <label for="input1">Input 1</label>
        <input aria-describedby="input1_elementnotice" aria-invalid="false" aria-required="false" id="input1" name="input1" type="text" value="" />
    </span>
    <span id="input1_elementnotice" aria-live="polite">
        <!-- error message will be inserted here -->
    </span>
</div>
```

<!--
## [Listbox](https://ebay.gitbooks.io/mindpatterns/content/input/listbox.html)

### Before JavaScript Initialisation

A scrolling listbox is created by using a select tag and specifying an arbitrary size attribute value.

```html
<span class="listbox">
    <label for="listbox">Select an option</label>
    <select id="listbox" name="listbox" size="4">
        <option value="1" selected>Option 1</option>
        <option value="2">Option 2</option>
        <option value="3">Option 3</option>
        <option value="4">Option 4</option>
    </select>
</span>
```

### After JavaScript Initialisation

```html
<span class="listbox">
    <label for="listbox" id="listbox_0_label">Select an option</label>
    <select aria-hidden="true" id="listbox" name="listbox" size="4">
        <option value="1" selected>Option 1</option>
        <option value="2">Option 2</option>
        <option value="3">Option 3</option>
        <option value="4">Option 4</option>
    </select>
    <div role="listbox" tabindex="0" aria-activedescendant="listbox_0_option_0" aria-labelledby="listbox_0_label">
        <div aria-selected="true" role="option" id="listbox_0_option_0">Option 1</div>
        <div aria-selected="false" role="option" id="listbox_0_option_1">Option 2</div>
        <div aria-selected="false" role="option" id="listbox_0_option_2">Option 3</div>
        <div aria-selected="false" role="option" id="listbox_0_option_3">Option 4</div>
    </div>
</span>
```
-->

## [Menu](https://ebay.gitbooks.io/mindpatterns/content/input/menu.html)

A menu contains commands (menuitem, menuitemradio, or menuitemcheckbox) that execute JavaScript. If you require a non-JavaScript fallback, consider using native form controls (e.g. regular buttons, radios and checkboxes).

```html
<div class="menu" id="menu_0">
    <button aria-controls="menu_0_flyout" aria-expanded="false" aria-haspopup="true" disabled>Open Menu</button>
    <div id="menu_0_flyout" role="menu">
        <div role="presentation">
            <div role="menuitem" tabindex="0">Button 1</div>
            <div role="menuitem" tabindex="-1">Button 2</div>
        </div>
        <hr />
        <div role="presentation">
            <div aria-checked="true" role="menuitemradio" tabindex="-1">Radio Button 1 (checked)</div>
            <div aria-checked="false" role="menuitemradio" tabindex="-1">Radio Button 2 </div>
            <div aria-checked="false" role="menuitemradio" tabindex="-1">Radio Button 3</div>
        </div>
        <hr />
        <div role="presentation">
            <div aria-checked="true" role="menuitemcheckbox" tabindex="-1">Checkbox 1 (checked)</div>
            <div aria-checked="true" role="menuitemcheckbox"  tabindex="-1">Checkbox 2 (checked)</div>
        </div>
    </div>
</div>
```

Remember that the popup button will not work without JavaScript. Therefore we mark it as disabled in our markup and then enable it with JavaScript.

If you only require a flat list of menu items, with no groups or separators, you can instead use a more compact form of markup:

```html
<div class="menu" id="menu_1">
    <button aria-controls="menu_1_flyout" aria-expanded="false" aria-haspopup="true">Open Menu</button>
    <div id="menu_1_flyout" role="menu">
        <div role="menuitem" tabindex="0">Button 1</div>
        <div role="menuitem" tabindex="-1">Button 2</div>
    </div>
</div>
```

If you wish to provide a semantic fallback for browser & screen reader combos that do not support menu roles, you can use list markup instead of divs:

```html
<div class="menu" id="menu_2">
    <button aria-controls="menu_2_flyout" aria-expanded="false" aria-haspopup="true">Open Menu</button>
    <ul id="menu_2_flyout" role="menu">
        <li role="menuitem" tabindex="0">Button 1</li>
        <li role="menuitem" tabindex="-1">Button 2</li>
    </ul>
</div>
```

In all cases, a popup menu requires a [rovingtabindex](http://www.w3.org/TR/wai-aria-practices/#focus_tabindex) for it's menu items.

## [Page Alert](http://ianmcburnie.github.io/mindpatterns/pagealert/)

Use `role=region` and `aria-label` to mark the page alert as a landmark for assistive technology.

```html
<div class="page-alert" role="region" aria-label="Page alert: high priority">
    <p>Something went wrong. Please try again.</p>
</div>
```

If the page alert content or display will be dynamically updated on the client, wrap the alert with `role=alert` or `role=status` to create a live region for assistive technology.

```html
<div role="alert">
    <div class="page-alert" role="region" aria-label="Page alert: high priority">
        <p>Oops. Something is still wrong. Please try again later.</p>
    </div>
</div>
```

## [Pagination](http://ianmcburnie.github.io/mindpatterns/pagination/)

### Server-Side Pagination

Assuming current page is 1.

```html
<nav class="pagination" aria-labelledby="pagination_heading" role="navigation">
    <h2 id="pagination_heading" class="clipped">Results pagination</h2>
    <span class="icon-chevron-left-disabled"></span>
    <ol>
        <li>
            <span>1</span>
        </li>
        <li>
            <a href="2.html">2</a>
        </li>
        <li>
            <a href="3.html">3</a>
        </li>
    </ol>
    <a class="icon-chevron-right" href="2.html" aria-label="Next results"></a>
</nav>
```

### Client-Side Pagination

Assuming current page is 1.

```html
<nav class="pagination" aria-labelledby="pagination_heading" role="navigation">
    <h2 id="pagination_heading" class="clipped">Results pagination</h2>
    <a class="icon-chevron-left-disabled" aria-disabled="true" href="index.html" aria-label="Previous results" tabindex="-1"></a>
    <ol>
        <li>
            <a href="index.html" aria-disabled="true" tabindex="-1">1</a>
        </li>
        <li>
            <a href="2.html">2</a>
        </li>
        <li>
            <a href="3.html">3</a>
        </li>
    </ol>
    <a class="icon-chevron-right" href="2.html" aria-label="Next results"></a>
</nav>
```

## [Radio](https://ebay.gitbooks.io/mindpatterns/content/input/radio.html)

Native HTML radio buttons are 100% accessible by default. To ensure correct grouping and group label semantics, radio buttons should always be placed inside of a fieldset with legend.

```html
<div class="radio-group" id="radio-group1">
    <fieldset>
        <legend>Radio Group Title</legend>
        <span>
            <input id="radio-group1_input1" name="radio-group1" type="radio" value="1" checked />
            <label for="radio-group1_input1">Input 1</label>
        </span>
        <span>
            <input id="radio-group1_input2" name="radio-group1" type="radio" value="2" />
            <label for="radio-group1_input2">Input 2</label>
        </span>
        <span>
            <input id="radio-group1_input3" name="radio-group1" type="radio" value="3" />
            <label for="radio-group1_input3">Input 3</label>
        </span>
    </fieldset>
</div>
```

For vertically stacked radios, simply switch the spans to divs.

Using CSS and icon fonts it is possible to 'replace' the natively styled radio button with a custom look and feel, with zero JavaScript required.

### ARIA Radios

For full control over styling of the element, or perhaps if your radio buttons are 'dumb' (i.e. they do not store or post form data) you may wish to consider custom ARIA radio buttons.

```html
<div class="aria-radio-group" id="aria-radios1">
    <div class="aria-radio-group__legend" id="aria-radios1__legend">Auction Type</div>
    <div class="aria-radio-group__fieldset" role="radiogroup" aria-labelledby="aria-radio-group__label">
        <div class="aria-radio__container" role="presentation">
            <span role="radio" aria-checked="false" aria-describedby="aria-radios1__legend" aria-labelledby="aria-radios1_label1"></span>
            <span class="aria-radio__label" id="aria-radios1_label1" aria-hidden="true">All Listings</span>
        </div>
        <div class="aria-radio__container" role="presentation">
            <span role="radio" aria-checked="false" aria-describedby="aria-radios1__legend" aria-labelledby="aria-radios1_label2"></span>
            <span class="aria-radio__label" id="aria-radios1_label2" aria-hidden="true">Auction</span>
        </div>
        <div class="aria-radio__container" role="presentation">
            <span role="radio" aria-checked="false" aria-describedby="aria-radios1__legend" aria-labelledby="aria-radios1_label3"></span>
            <span class="aria-radio__label" id="aria-radios1_label3" aria-hidden="true">Buy it Now</span>
        </div>
    </div>
</div>
```

Notice that aria-hidden is applied to the labels. This is to prevent an issue in Voiceover which treats the labels as members of the radiogroup role, thus doubling the number of reported radio items in the group. Don't worry, the label will still be read when focus and virtual cursor is on the custom radio button. Likewise, the 'legend' is also placed outside of the radiogroup.

Be warned: JavaScript will be required, and you will need to recreate the exact behaviour of native HTML radio buttons in full. It is no easy task. Perhaps a better approach is to progressively enhance the native radios into ARIA radios. This way, the under-the-hood native radios continue to provide all accessibility benefits, whilst the ARIA buttons provide the custom look and feel.

## [Tabs](https://ebay.gitbooks.io/mindpatterns/content/disclosure/tabs.html)

Tabs require 2 or more panels of content.

### With Progressive Enhancement

If you wish to support progressive enhancement, your markup should start out as a list of links.

#### Before JavaScript Initialisation

```html
<div class="tabs" id="tabs1">
    <h2>Tabs Heading</h2>
    <ul>
        <li>
            <a href="#tabs1_panel1">Tab 1</a>
        </li>
        <li>
            <a href="#tabs1_panel2">Tab 2</a>
        </li>
        <li>
            <a href="#tabs1_panel3">Tab 3</a>
        </li>
    </ul>
    <div>
        <div id="tabs1_panel1" tabindex="-1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div id="tabs1_panel2" tabindex="-1">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div id="tabs1_panel3" tabindex="-1">
            <h3>Panel 3 heading</h3>
            <!-- panel content goes here -->
        </div>
    </div>
</div>
```

#### After JavaScript Initialisation

Tree structure remains identical, but many new attributes are added. Only one panel can be selected & visible at any time.

```html
<div class="tabs tab--js" id="tabs1">
    <h2 class="clipped">Tabs Heading</h2>
    <ul role="tablist">
        <li role="tab" aria-controls="tabs1_panel1" aria-selected="true" id="tabs1_tab1" tabindex="0">
            <a role="presentation">Tab 1</a>
        </li>
        <li role="tab" aria-controls="tabs1_panel2" aria-selected="false" id="tabs1_tab2" tabindex="-1">
            <a role="presentation">Tab 2</a>
        </li>
        <li role="tab" aria-controls="tabs1_panel3" aria-selected="false" id="tabs1_tab3" tabindex="-1">
            <a role="presentation">Tab 3</a>
        </li>
    </ul>
    <div>
        <div role="tabpanel" aria-hidden="false" aria-labelledby="tabs1_tab1" id="tabs1_panel1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div role="tabpanel" aria-hidden="true" aria-labelledby="tabs1_tab2" id="tabs1_panel2">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div role="tabpanel" aria-hidden="true" aria-labelledby="tabs1_tab3" id="tabs1_panel3">
            <h3>Panel 3 heading</h3>
            <!-- panel content goes here -->
        </div>
    </div>
</div>
```

If the content of each tabpanel is only a small amount of unstructured text, then you may wish to convert the container of the tab panels into a live region using aria-live="polite".

### Without Progressive Enhancement

If you do not wish to support progressive enhancement, simply replace the list of links in the markup with div tags. You can choose to apply the ARIA attributes with JavaScript or add them directly to the rendered markup.

```html
<div class="tabs tab--js" id="tabs1">
    <h2 class="clipped">Tabs Heading</h2>
    <div role="tablist">
        <div role="tab" aria-controls="tabs1_panel1" aria-selected="true" id="tabs1_tab1" tabindex="0">
            <span>Tab 1</span>
        </div>
        <div role="tab" aria-controls="tabs1_panel2" aria-selected="false" id="tabs1_tab2" tabindex="-1">
            <span>Tab 2</span>
        </div>
        <div role="tab" aria-controls="tabs1_panel3" aria-selected="false" id="tabs1_tab3" tabindex="-1">
            <span>Tab 3</span>
        </div>
    </div>
    <div>
        <div role="tabpanel" aria-hidden="false" aria-labelledby="tabs1_tab1" id="tabs1_panel1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div role="tabpanel" aria-hidden="true" aria-labelledby="tabs1_tab2" id="tabs1_panel2">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div role="tabpanel" aria-hidden="true" aria-labelledby="tabs1_tab3" id="tabs1_panel3">
            <h3>Panel 3 heading</h3>
            <!-- panel content goes here -->
        </div>
    </div>
</div>
```

If the content of each tabpanel is only a small amount of unstructured text, then you may wish to convert the container of the tab panels into a live region using aria-live="polite".

## [Tooltip](https://ebay.gitbooks.io/mindpatterns/content/disclosure/tooltip.html)

Tooltip structure is almost identical to [flyout](#user-content-flyout) structure:

```html
<span class="tooltip">
    <input aria-describedby="tooltip0" class="tooltip__trigger" type="submit" value="Submit" />
    <span class="tooltip__overlay" id="tooltip0" role="tooltip">Hint content</span>
</span>
```

The main difference is that a modifier class must be used instead of aria-expanded attribute:

```html
<span class="tooltip tooltip--expanded">
    <input aria-describedby="tooltip0" class="tooltip__trigger" type="submit" value="Submit" />
    <span class="tooltip__overlay" id="tooltip0" role="tooltip">Hint content</span>
</span>
```

In this example we have chosen the name `tooltip--expanded` for our modifier class.

Role of `tooltip` is required on the overlay, and `aria-describedby` attribute is required on the trigger element.
