# BONES

> Widgets are stronger with bones. Does *your* widget have bones?

## Contents

1. [Introduction](#user-content-introduction)
1. [Accordion](#user-content-accordion)
1. [Accordion (Legacy)](#user-content-accordion-legacy)
1. [Breadcrumbs](#user-content-breadcrumbs)
1. [Carousel](#user-content-carousel)
1. [Checkbox](#user-content-checkbox)
1. [Combobox](#user-content-combobox)
1. [Details](#user-content-details)
1. [Dialog](#user-content-dialog)
1. [Fake Menu](#user-content-fake-menu)
1. [Fake Tabs](#user-content-fake-tabs)
1. [Flyout](#user-content-flyout)
1. [Input Validation](#user-content-input-validation)
1. [Listbox](#user-content-listbox)
1. [Menu](#user-content-menu)
1. [Menu Button](#user-content-menu-button)
1. [Page Notice](#user-content-page-notice)
1. [Pagination](#user-content-pagination)
1. [Radio](#user-content-radio)
1. [Tabs](#user-content-tabs)
1. [Tooltip](#user-content-tooltip)

## Introduction

Bones provides lean, mean, semantic HTML markup for widgets; ensuring maximum Accessibility, SEO and Site Speed performance. Bones markup has full support for <a href="http://www.w3.org/WAI/intro/aria"> WAI-ARIA</a> roles, states and properties.

Bones advocates the [Progressive Enhancement](http://en.wikipedia.org/wiki/Progressive_enhancement) web-design strategy; building the web in a layered fashion that allows **everyone** to access the **most important** content and functionality. We supply HTML markup for both the *before* and *after*  JavaScript initialisation states of a widget, i.e. before-enhancement and after-enhancement. If you do not wish to support progressive enhancement we also provide alternatives.<sup>1</sup>

<strike>Bones favors the <a href="http://en.wikipedia.org/wiki/Convention_over_configuration">convention over configuration</a> paradigm. A convention for widget structure allows us to add only a minimal amount of CSS and JavaScript 'hooks' to the base markup. Typically, we define a single module name on our root node, alongside any additional *modifier* class names, such as states & themes.</strike>

**UPDATE**: Bones is evolving from it's original  ultra-minimalist "convention over configuration" paradigm, to the [BEM](http://getbem.com) (block, element, modifier) naming methodology. With this change we hope to strike the right balance between lean HTML and performant, flexible CSS. Not all patterns have been updated yet. Please bear with us.

<sub><sup>1</sup> Building an app that is rendered entirely on the client-side? If so, you will only need to refer to the enhanced/initialised code. However, best practice is to build apps in an <a href="http://nerds.airbnb.com/isomorphic-javascript-future-web-apps/">isomorphic</a> fashion so that first page load is rendered by the server then *enhanced* on the client.</sub>

## [Accordion](https://ebay.gitbooks.io/mindpatterns/content/disclosure/accordion.html)

The accordion is simply a list of [details](#user-content-details) widgets. Each details summary should include a relevant heading level tag.

```html
<ul class="accordion" role="list" aria-roledescription="accordion">
    <li>
        <details class="details">
            <summary><h3>Panel 1</h3></summary>
            <ul>
                <li><a href="http://www.ebay.com">Item 1</a></li>
                <li><a href="http://www.ebay.com">Item 2</a></li>
                <li><a href="http://www.ebay.com">Item 3</a></li>
            </ul>
        </details>
    </li>
    <li>
        <details class="details">
            <summary><h3>Panel 2</h3></summary>
            <ul>
                <li><a href="http://www.ebay.com">Item 1</a></li>
                <li><a href="http://www.ebay.com">Item 2</a></li>
                <li><a href="http://www.ebay.com">Item 3</a></li>
            </ul>
        </details>
    </li>
</ul>
```

## [Accordion (Legacy)](https://ebay.gitbooks.io/mindpatterns/content/disclosure/accordionlegacy.html)

This accordion markup is considered "legacy" as it followed an old, outdated version of the WAI-ARIA Authoring Practices.

### Before JavaScript Initialisation

An accordion requires 2 or more panels of content.

```html
<div class="accordion" id="accordion1">
    <h2>Accordion Title</h2>
    <div class="accordion__item">
        <h3 class="accordion__tab">Panel 1 Title</h3>
        <div class="accordion__panel">
            <!-- panel contents go here -->
        </div>
    </div>
    <div class="accordion__item">
        <h3 class="accordion__tab">Panel 2 Title</h3>
        <div class="accordion__panel">
            <!-- panel contents go here -->
        </div>
    </div>
    <div class="accordion__item">
        <h3 class="accordion__tab">Panel 3 Title</h3>
        <div class="accordion__panel">
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
    <div class="accordion__item">
        <h3 class="accordion__tab" aria-controls="accordion1_panel1" aria-selected="false" id="accordion1_tab1" role="tab" tabindex="0">Panel 1 Title</h3>
        <div class="accordion__panel" aria-hidden="true" aria-labelledby="accordion1_tab1" id="accordion1_panel1" role="tabpanel">
            <!-- panel contents go here -->
        </div>
    </div>
    <div class="accordion__item">
        <h3 class="accordion__tab" aria-controls="accordion1_panel2" aria-selected="false" id="accordion1_tab2" role="tab" tabindex="-1">Panel 2 Title</h3>
        <div class="accordion__panel" aria-hidden="true" aria-labelledby="accordion1_tab2" id="accordion1_panel2" role="tabpanel">
            <!-- panel contents go here -->
        </div>
    </div>
    <div class="accordion__item">
        <h3 class="accordion__tab" aria-controls="accordion1_panel3" aria-selected="false" id="accordion1_tab3" role="tab" tabindex="-1">Panel 3 Title</h3>
        <div class="accordion__panel" aria-hidden="true" aria-labelledby="accordion1_tab3" id="accordion1_panel3" role="tabpanel">
            <!-- panel contents go here -->
        </div>
    </div>
</div>
```

## [Breadcrumbs](https://ebay.gitbooks.io/mindpatterns/content/navigation/breadcrumbs.html)

The content is an ordered list of links inside a navigation landmark region. Breadcrumbs do not require JavaScript initialisation. CSS can be used to generate a separator image or glyph using the `::after` pseudo element.

```html
<nav class="crumbs" aria-labelledby="crumbs_heading" role="navigation">
    <h2 id="crumbs_heading">You are here</h2>
    <ol>
        <li><a href="http://www.ebay.com">Great Grandparent Page</a></li>
        <li><a href="http://www.ebay.com">Grandparent Page</a></li>
        <li><a href="http://www.ebay.com">Parent Page</a></li>
        <li><a aria-current="location">Current Page</a></li>
    </ol>
</nav>
```

## [Carousel](https://ebay.gitbooks.io/mindpatterns/content/disclosure/carousel.html)

### Before JavaScript Initialisation

A carousel is a list of items. These items can contain anything - text, images, links, tiles, cards, etc. - but we advise against using complex widgets. The usual accessibility rules apply to the contents of these items (tab-order, semantics, etc).

For the server rendered markup you can choose to render as little or as much of the full list as you wish. Client-side script can lazy-load in additional items as desired.

```html
<div class="carousel">
    <span aria-live="polite" role="status">
        <h2 class="carousel__title">Title</h2>
    </span>
    <ul>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        ...
    </ul>
</div>
```

### After JavaScript Initialisation

JavaScript adds a description and state to the heading inside of live region, and two pagination buttons either side of the list.

```html
<div class="carousel">
    <span aria-live="polite" role="status">
        <h2 class="carousel__title">Title<span class="clipped"> - Carousel - slide n of n</span></h2>
    </span>
    <button aria-disabled="false" aria-label="Previous slide - Title"></button>
    <ul>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        ...
    </ul>
    <button aria-disabled="false" aria-label="Next slide - Title"></button>
</div>
```

JavaScript must maintain the tabindex and aria-hidden state of items as they scroll in and out of view. Items that are not in view need a tabindex value of "-1" an aria-hidden value of "true" to ensure items are hidden from keyboard users and screen reader users respectively.

JavaScript must also maintain the state of the heading inside the live region.

For small touch screens, you may wish to utilise swipe gestures. In which case pagination buttons can be hidden offscreen, appearing only on keyboard focus (i.e. 'stealth' buttons) for keyboard users.

## [Checkbox](https://ebay.gitbooks.io/mindpatterns/content/input/checkbox.html)

Native HTML checkboxes are 100% accessible by default. To ensure correct grouping and group label semantics, groups of checkboxes should always be placed inside of a fieldset with legend.

```html
<fieldset>
    <legend>Auction Type</legend>
    <div>
        <input id="freeshipping" type="checkbox" name="freeshipping" />
        <label for="freeshipping">Free Shipping</label>
    </div>
    <div>
        <input id="endssoon" type="checkbox" name="endssoon" />
        <label for="endssoon">Ends soon</label>
    </div>
    <div>
        <input id="zerobids" type="checkbox" name="zerobids" />
        <label for="zerobids">Zero bids</label>
    </div>
</fieldset>
```

For vertically stacked checkboxes, simply switch the spans to divs.

### Custom Icon

To create a custom checkbox style, either background or foreground SVG can be used as a facade over the real checkbox.

Background SVG:

```html
<span class="checkbox">
    <input class="checkbox__control" id="freeshipping" type="checkbox" name="freeshipping" />
    <span class="checkbox__icon"></span>
</span>
```

Foreground SVG:

```html
<span class="checkbox">
  <input class="checkbox__control" id="freeshipping" type="checkbox" name="freeshipping" />
  <span class="checkbox__icon" hidden>
    <svg aria-hidden="true" class="checkbox__unchecked" focusable="false">
      <use xlink:href="#icon-checkbox-unchecked"></use>
    </svg>
    <svg aria-hidden="true" class="checkbox__checked" focusable="false">
      <use xlink:href="#icon-checkbox-checked"></use>
    </svg>
  </span>
</span>
```

This latter markup assumes that the symbol definitions for #icon-checkbox-unchecked and #icon-checkbox-checked exist on the page. The hidden property ensures that the SVG icon is not visible alongside the native icon when the page is in a non-CSS state. This hidden property should be overriden by CSS.

In both cases, don't forget to add a label!

## [Combobox](https://ebay.gitbooks.io/mindpatterns/content/input/combobox.html)

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

## [Details](https://ebay.gitbooks.io/mindpatterns/content/disclosure/details.html)

Uses the native HTML `<details>` tag. IE and Edge browsers require a CSS and JavaScript polyfill.

```html
<details class="details">
    <summary>Details</summary>
    <ul>
        <li><a href="http://www.ebay.com">Link 1</a></li>
        <li><a href="http://www.ebay.com">Link 2</a></li>
        <li><a href="http://www.ebay.com">Link 3</a></li>
    </ul>
</details>
```

## [Dialog](https://ebay.gitbooks.io/mindpatterns/content/structure/dialog.html)

```html
<div aria-labelledby="dialog_title" class="dialog" role="dialog">
    <div class="dialog__window" role="document">
        <header role="banner">
            <h2 id="dialog_title">Dialog Title</h2>
            <button aria-label="Close dialog" class="dialog__close" type="button"></button>
        </header>
        <div>
            <!-- dialog content goes here -->
        </div>
    </div>
    <div class="dialog__mask"></div>
</div>
```

## [Fake Menu](https://ebay.gitbooks.io/mindpatterns/content/navigation/fakemenu.html)

### Before JavaScript Initialisation

The content is a button and a list of links.

```html
<div class="fake-menu">
    <button disabled>Open Nav</button>
    <ul>
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
    </ul>
</div>
```

If the href value of a fake menu item matches the current page url, then add `aria-current="page"` to that anchor tag.

Remember that this button will not work without JavaScript. Therefore we disable it in our markup and then enable it with JavaScript.

### After JavaScript Initialisation

```html
<div class="fake-menu fake-menu--js" id="fake-menu-0">
    <button aria-controls="fake-menu-0-flyout" aria-expanded="false">Open Nav</button>
    <ul id="fake-menu-0-flyout">
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
        <li><a href="http://www.ebay.com">Link Text</a></li>
    </ul>
</div>
```

The `aria-controls` attribute should only be present when aria-expanded state is true.

If you require a fake menu that is opened by hovering on a link, rather than clicking on a button, then append a stealth button immediately after the anchor tag. This button will appear, and receive focus, as soon as the user tabs past the hyperlink.

## [Fake Tabs](https://ebay.gitbooks.io/mindpatterns/content/navigation/faketabs.html)

Fake tabs *look* like regular tabs, but behave like a list of links. No JavaScript is required.

```html
<nav aria-labelledby="fake-tabs-title" class="fake-tabs" role="navigation">
    <h2 class="clipped" id="fake-tabs-title">Fake Tabs Heading</h2>
    <ul>
        <li>
            <a aria-current="page" href="http://www.ebay.com/1">Page 1</a>
        </li>
        <li>
            <a href="http://www.ebay.com/2">Page 2</a>
        </li>
        <li>
            <a href="http://www.ebay.com/3">Page 3</a>
        </li>
    </ul>
</nav>
```

NOTE: We say 'Current Page', rather than 'Current Tab', because the controls are links, not tabs.

## [Flyout](https://ebay.gitbooks.io/mindpatterns/content/disclosure/flyout.html)

A flyout might open on click, focus or hover, on any kind of button, input or link. Regardless of what type of element or interaction is used to trigger the flyout, the overlay element must immediately follow the host element in the DOM. This structure ensures a seamless and natural reading order and focus order.

```html
<div class="flyout">
    <button class="flyout__host" aria-expanded="false|true">Button</button>
    <div class="flyout__overlay-container">
        <div class="flyout__overlay">
            <!-- overlay content -->
        </div>
    </div>
</div>
```

The `flyout__overlay-container` element acts as a hook for an ARIA live-region (see below), this element can be dropped if live-region support is not required.

Note that Menu, Fake Menu, Tooltip & Combobox are special instances of flyouts, but follow the same general pattern in that their overlay element must immediately follow the trigger element.

### Live Region

Live region support is optional. We have added support for live-region based on feedback from users who want the contents of flyouts to be announced when opened in certain cases (not all cases).

```html
<div class="flyout">
    <button class="flyout__host" aria-expanded="false|true">Button</button>
    <div class="flyout__overlay-container" aria-live="polite">
        <div class="flyout__overlay">
            <!-- overlay content -->
        </div>
    </div>
</div>
```

In order for live-region support to work correctly in Voiceover, any hide/show operation (i.e. display:none|block) or content update must be performed on the `flyout__overlay`, not the `flyout__overlay-container`.


## [Input Validation](https://ebay.gitbooks.io/mindpatterns/content/messaging/inputvalidation.html)

Input validation messages depend on client-side JavaScript and are considered an *enhancement* to full, server-side form validation.

### Valid State

The error message container is a live-region, and can be primed and ready in the server-side code, or injected dynamically at error-time with client-side JavaScript.

```html
<div class="input-validation">
    <span>
        <label for="input1">Input 1</label>
        <input aria-describedby="input1-description" aria-invalid="false" id="input1" name="input1" type="text" />
    </span>
    <span aria-live="polite" class="input-validation__status" role="status">
        <span class="input-validation__description" id="input1-description" >
            <!-- this content should be empty in a valid state -->
        </span>
    </span>
</div>
```

For Voiceover to correctly detect live-region updates, the updates must happen on direct-descendant(s) of the live-region, not on the live-region itself.

### Invalid State

Changing the content of a directly-descendant element will trigger a live-region update.

```html
<div class="input-validation input-validation--js">
    <span>
        <label for="input1">Input 1</label>
        <input aria-describedby="input1-description" aria-invalid="true" id="input1" name="input1" type="text" />
    </span>
    <span aria-live="polite" class="input-validation__status" role="status">
        <span class="input-validation__description" id="input1-description">
            <!-- this content should be populated in an invalid state -->
        </span>
    </span>
</div>
```

Notice that the `aria-described` attribute supplements the live-region, by using the same live-region content as a *description* for the input. Descriptions can be read at any time, live-regions only once at the time they are triggered.

Be warned that even a hidden description (using display: none or `hidden` property) will be announced. Therefore if you plan on simply toggling the display of an error message, be sure to also toggle the presence of the `aria-describedby` attribute.

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

## [Listbox](https://ebay.gitbooks.io/mindpatterns/content/input/listbox.html)

The listbox pattern is intended for use as a custom, progressive enhancement of the native HTML select element.

Because the single-select listbox pattern uses a button element, it's value will not be submitted along with other form data without the assistance of JavaScript.

```html
<span class="listbox">
    <button class="expand-btn" aria-expanded="false" aria-haspopup="listbox">
        <span class="expand-btn__cell">
            <span>Option 1</span>
            <span class="expand-btn__icon"></span>
        </span>
    </button>
    <div class="listbox__options" role="listbox" tabindex="-1">
        <div class="listbox__option" role="option">
            <span>Option 1</span>
            <span class="listbox__status"></span>
        </div>
        <div class="listbox__option" role="option">
            <span>Option 2</span>
            <span class="listbox__status"></span>
        </div>
        <div class="listbox__option" role="option">
            <span>Option 3</span>
            <span class="listbox__status"></span>
        </div>
    </div>
</span>
```

By default, the first option should be selected if the user does not specify a selection.

An initial selection can be specified by applying the `aria-selected` state to a single option.

```html
<span class="listbox">
    <button class="expand-btn" aria-expanded="false" aria-haspopup="listbox">
        <span class="expand-btn__cell">
            <span>Option 1</span>
            <span class="expand-btn__icon"></span>
        </span>
    </button>
    <div class="listbox__options" role="listbox" tabindex="-1">
        <div class="listbox__option" role="option">
            <span>Option 1</span>
            <span class="listbox__status"></span>
        </div>
        <div aria-selected="true" class="listbox__option" role="option">
            <span>Option 2</span>
            <span class="listbox__status"></span>
        </div>
        <div class="listbox__option" role="option">
            <span>Option 3</span>
            <span class="listbox__status"></span>
        </div>
    </div>
</span>
```

For multi-select, the button element is dropped. Again, this behaves similar to the native HTML select element.

```html
<span class="listbox">
    <div class="listbox__options" role="listbox" tabindex="-1">
        <div class="listbox__option" role="option">
            <span>Option 1</span>
            <span class="listbox__status"></span>
        </div>
        <div class="listbox__option" role="option">
            <span>Option 2</span>
            <span class="listbox__status"></span>
        </div>
        <div class="listbox__option" role="option">
            <span>Option 3</span>
            <span class="listbox__status"></span>
        </div>
    </div>
</span>
```

## [Menu](https://ebay.gitbooks.io/mindpatterns/content/input/menu.html)

A menu contains commands (`menuitem`, `menuitemradio`, or `menuitemcheckbox`) that execute JavaScript. If you require a non-JavaScript fallback, consider using native form controls (e.g. regular buttons, radios and checkboxes).

```html
<div class="menu">
    <div role="menu">
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

If you only require a flat list of menu items, with no groups or separators, you can instead use a more compact form of markup:

```html
<div class="menu">
    <div role="menu">
        <div role="menuitem" tabindex="0">Button 1</div>
        <div role="menuitem" tabindex="-1">Button 2</div>
    </div>
</div>
```

If you wish to provide a semantic fallback for browser & screen reader combos that do not support menu roles, you can use list markup instead of divs:

```html
<div class="menu">
    <ul role="menu">
        <li role="menuitem" tabindex="0">Button 1</li>
        <li role="menuitem" tabindex="-1">Button 2</li>
    </ul>
</div>
```

In all cases, a menu requires a [rovingtabindex](http://www.w3.org/TR/wai-aria-practices/#focus_tabindex) for its menu items.

## [Menu Button](https://ebay.gitbooks.io/mindpatterns/content/input/menu.html)

A menu button opens a [menu](#user-content-menu) in a flyout.

```html
<div class="menu-button">
    <button aria-expanded="false" aria-haspopup="true" class="menu-button__button">Open Menu</button>
    <div class="menu-button__menu" hidden>
        <div role="menu">
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
</div>
```

## [Page Notice](http://ianmcburnie.github.io/mindpatterns/messaging/pagenotice/)

Use `role=region` and `aria-label` to mark the page notice as a landmark for assistive technology.

```html
<section class="page-notice" role="region" aria-label="Page notice: high priority">
    <p>Something went wrong. Please try again.</p>
</section>
```

If the page notice content or display will be dynamically updated on the client, wrap the notice with `role=alert` or `role=status` to create a live region for assistive technology.

```html
<span role="alert">
    <section class="page-notice" role="region" aria-label="Page notice: high priority">
        <p>Oops. Something is still wrong. Please try again later.</p>
    </section>
</span>
```

## [Pagination](http://ianmcburnie.github.io/mindpatterns/pagination/)

The pagination pattern allows a user to navigate back and forwards through a URL based dataset, or jump directly to any specific URL in that set.

Pagination links may update the results immediately on the client via AJAX, or on the server via a full page reload. In both cases, the browser's URL will be updated.

The example below assumes that the first result set item is the current page (hence the 'Previous' link would appear 'disabled' in this state).

```html
<nav class="pagination" aria-labelledby="pagination-heading" role="navigation">
    <span aria-live="off">
        <h2 id="pagination-heading" class="clipped">Results Pagination - Page 1</h2>
    </span>
    <a aria-disabled="true" aria-label="Previous Page" class="pagination__previous" href="1.html">
        <svg aria-hidden="true">
            <use xlink:href="#icon-chevron-light-left"></use>
        </svg>
    </a>
    <ol>
        <li>
            <a aria-current="page" href="1.html">1</a>
        </li>
        <li>
            <a href="2.html">2</a>
        </li>
        <li>
            <a href="3.html">3</a>
        </li>
    </ol>
    <a aria-label="Next Page" class="pagination__next" href="2.html">
        <svg aria-hidden="true">
            <use xlink:href="#icon-chevron-light-right"></use>
        </svg>
    </a>
</nav>
```

**NOTE:** The heading need only be wrapped in an ARIA live-region if client-side pagination is implemented (i.e. partial page updates).

## [Radio](https://ebay.gitbooks.io/mindpatterns/content/input/radio.html)

Native HTML radio buttons are 100% accessible by default. To ensure correct grouping and group label semantics, radio buttons should always be placed inside of a fieldset with legend.

```html
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
```

For vertically stacked radios, simply switch the spans to divs.

### Custom Radios

To create a custom radio style, either background or foreground SVG can be used as a facade over the real radio.

Background SVG:

```HTML
<span class="radio">
    <input class="radio__control" id="radio-group1_input1" type="radio" value="3" name="radio-group-1" />
    <span class="radio__icon"></span>
</span>
```

Foreground SVG:

```HTML
<span class="radio__icon" hidden>
    <input class="radio__control" id="radio-group1_input1" type="radio" value="3" name="radio-group-1" />
    <svg aria-hidden="true" class="radio__unchecked" focusable="false">
        <use xlink:href="#icon-radio-unchecked"></use>
    </svg>
    <svg aria-hidden="true" class="radio__checked" focusable="false">
        <use xlink:href="#icon-confirmation"></use>
    </svg>
</span>
```

This latter markup assumes that the symbol definitions for #icon-radio-unchecked and #icon-radio-checked exist on the page. The hidden property ensures that the SVG icon is not visible alongside the native icon when the page is in a non-CSS state. This hidden property should be overriden by CSS.

In both cases, don't forget to add a label!

## [Tabs](https://ebay.gitbooks.io/mindpatterns/content/disclosure/tabs.html)

Tabs require 2 or more panels of content.

### With Progressive Enhancement

If you wish to support progressive enhancement, your markup should start out as a list of links.

#### Before JavaScript Initialisation

```html
<div class="tabs" id="tabs1">
    <h2>Tabs Heading</h2>
    <ul class="tabs__items">
        <li class="tabs__item">
            <a href="#tabs1_panel1">Tab 1</a>
        </li>
        <li class="tabs__item">
            <a href="#tabs1_panel2">Tab 2</a>
        </li>
        <li class="tabs__item">
            <a href="#tabs1_panel3">Tab 3</a>
        </li>
    </ul>
    <div class="tabs__content">
        <div class="tabs__panel" id="tabs1_panel1" tabindex="-1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div class="tabs__panel" id="tabs1_panel2" tabindex="-1">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div class="tabs__panel" id="tabs1_panel3" tabindex="-1">
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
    <ul class="tabs__items" role="tablist">
        <li class="tabs__item" role="tab" aria-controls="tabs1_panel1" aria-selected="true" id="tabs1_tab1" tabindex="0">
            <a role="presentation">Tab 1</a>
        </li>
        <li class="tabs__item" role="tab" aria-controls="tabs1_panel2" aria-selected="false" id="tabs1_tab2" tabindex="-1">
            <a role="presentation">Tab 2</a>
        </li>
        <li class="tabs__item" role="tab" aria-controls="tabs1_panel3" aria-selected="false" id="tabs1_tab3" tabindex="-1">
            <a role="presentation">Tab 3</a>
        </li>
    </ul>
    <div class="tabs__content">
        <div aria-labelledby="tabs1_tab1" class="tabs__panel" role="tabpanel" id="tabs1_panel1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div aria-labelledby="tabs1_tab2" class="tabs__panel" role="tabpanel" hidden id="tabs1_panel2">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div aria-labelledby="tabs1_tab3" class="tabs__panel" role="tabpanel" hidden id="tabs1_panel3">
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
    <div class="tabs__items" role="tablist">
        <div class="tabs__item" role="tab" aria-controls="tabs1_panel1" aria-selected="true" id="tabs1_tab1" tabindex="0">
            <span>Tab 1</span>
        </div>
        <div class="tabs__item" role="tab" aria-controls="tabs1_panel2" aria-selected="false" id="tabs1_tab2" tabindex="-1">
            <span>Tab 2</span>
        </div>
        <div class="tabs__item" role="tab" aria-controls="tabs1_panel3" aria-selected="false" id="tabs1_tab3" tabindex="-1">
            <span>Tab 3</span>
        </div>
    </div>
    <div class="tabs__content">
        <div aria-labelledby="tabs1_tab1" class="tabs__panel" role="tabpanel" id="tabs1_panel1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div aria-labelledby="tabs1_tab2" class="tabs__panel" role="tabpanel" hidden id="tabs1_panel2">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div aria-labelledby="tabs1_tab3" class="tabs__panel" role="tabpanel" hidden id="tabs1_panel3">
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
