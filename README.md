# BONES

> Widgets are stronger with bones. Does *your* widget have bones?

## Contents

1. [Introduction](#user-content-introduction)
1. [Accordion](#user-content-accordion)
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
1. [Listbox Button](#user-content-listbox-button)
1. [Menu](#user-content-menu)
1. [Menu Button](#user-content-menu-button)
1. [Page Notice](#user-content-page-notice)
1. [Pagination](#user-content-pagination)
1. [Radio](#user-content-radio)
1. [Tabs](#user-content-tabs)
1. [Tooltip](#user-content-tooltip)

## Introduction

Bones provides lean, mean, semantic HTML markup for widgets; ensuring maximum Accessibility, SEO and Site Speed performance. Bones markup uses ARIA only where strictly <a href="http://www.w3.org/WAI/intro/aria"> WAI-ARIA</a> necessary.

Bones advocates the [Progressive Enhancement](http://en.wikipedia.org/wiki/Progressive_enhancement) web-design strategy; building the web in a layered fashion that allows **everyone** to access the **most important** content and functionality.

Bones favors the the [BEM](http://getbem.com) (block, element, modifier) methodology for naming its classes.

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

## [Breadcrumbs](https://ebay.gitbooks.io/mindpatterns/content/navigation/breadcrumbs.html)

The content is an ordered list of links inside a navigation landmark region.

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

CSS can be used to generate a separator image or glyph using the `::after` pseudo element.

## [Carousel](https://ebay.gitbooks.io/mindpatterns/content/disclosure/carousel.html)

A carousel is a list of items. These items can contain anything - text, images, links, tiles, cards, etc. - but we advise against using complex widgets. The usual accessibility rules apply to the contents of these items (tab-order, semantics, etc).

For the server rendered markup you can choose to render as little or as much of the full list as you wish. Client-side script can lazy-load in additional items as desired.

```html
<div class="carousel">
    <span aria-live="polite" role="status">
        <h2 class="carousel__title">
            <span>Title</span>
            <span class="clipped"> - Carousel - slide n of n</span>
        </h2>
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

### Custom Checkbox Icon

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

This latter markup assumes that the symbol definitions for `#icon-checkbox-unchecked` and `#icon-checkbox-checked` exist on the page. The hidden property ensures that the SVG icon is not visible alongside the native icon when the page is in a non-CSS state. This hidden property should be overriden by CSS.

In both cases, don't forget to add a label for the checkbox!

## [Combobox](https://ebay.gitbooks.io/mindpatterns/content/input/combobox.html)

```html
<div class="combobox" id="combobox-1">
    <span class="combobox__control">
        <input name="combobox-1-name" type="text" role="combobox" autocomplete="off" aria-expanded="false" aria-owns="combobox-1-listbox" />
    </span>
    <button type="button" tabindex="-1" aria-label="Expand Options"></button>
    <ul id="combobox-1-listbox" role="listbox">
        <li role="option" id="combobox-1-option-1">Option 1</li>
        <li role="option" id="combobox-1-option-2">Option 2</li>
        <li role="option" id="combobox-1-option-3">Option 3</li>
        ...
    </ul>
</div>
```

JavaScript must update the `aria-activedescendant` attribute on the textbox to reflect the state of the currently active descendant listbox item.

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
</div>
```

## [Fake Menu](https://ebay.gitbooks.io/mindpatterns/content/navigation/fake-menu.html)

A fake menu is styled like a regular menu, but it contains a list of links and/or buttons instead of menu items. No ARIA roles are required. If the `href` value of a fake menu item matches the current page url, then add `aria-current="page"` to that anchor tag.

```html
<ul>
    <li><a href="http://www.ebay.com">Link Text</a></li>
    <li><a href="http://www.ebay.com">Link Text</a></li>
    <li><a href="http://www.ebay.com">Link Text</a></li>
</ul>
```

## [Fake-Menu Button](https://ebay.gitbooks.io/mindpatterns/content/navigation/fake-menu-button.html)

A button that opens a fake menu.

```html
<div class="fake-menu">
    <button aria-expanded="false">Fake Menu</button>
    <div>
        <ul>
            <li><a href="http://www.ebay.com">Link Text</a></li>
            <li><a href="http://www.ebay.com">Link Text</a></li>
            <li><a href="http://www.ebay.com">Link Text</a></li>
        </ul>
    </div>
</div>
```

## [Fake Tabs](https://ebay.gitbooks.io/mindpatterns/content/navigation/fake-tabs.html)

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
    <button class="flyout__host" aria-expanded="false">Button</button>
    <div class="flyout__content">
        <!-- overlay content -->
    </div>
</div>
```

Note that Menu, Fake Menu, Tooltip & Combobox are special instances of flyouts, but follow the same general pattern in that their overlay element must immediately follow the trigger element.

## [Input Validation](https://ebay.gitbooks.io/mindpatterns/content/messaging/input-validation.html)

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
            <!-- this content should be empty in a valid state, populated in an invalid state -->
        </span>
    </span>
</div>
```

For Voiceover to correctly detect live-region updates, the updates must happen on direct-descendant(s) of the live-region, not on the live-region itself.

### Invalid State

Changing the content of a directly-descendant element will trigger a live-region update.

```html
<div class="input-validation">
    <span>
        <label for="input1">Input 1</label>
        <input aria-describedby="input1-description" aria-invalid="true" id="input1" name="input1" type="text" />
    </span>
    <span aria-live="polite" class="input-validation__status" role="status">
        <span class="input-validation__description" id="input1-description">
            <!-- this content should be empty in a valid state, populated in an invalid state -->
        </span>
    </span>
</div>
```

Notice that the `aria-described` attribute supplements the live-region, by using the same live-region content as a *description* for the input. Descriptions can be read at any time, live-regions only once at the time they are triggered.

Be warned that even a hidden description (using display: none or `hidden` property) will be announced. Therefore if you plan on simply toggling the display of an error message, be sure to also toggle the presence of the `aria-describedby` attribute.

## [Listbox](https://ebay.gitbooks.io/mindpatterns/content/input/listbox.html)

The listbox pattern is intended as a JavaScript alternative to the HTML select element. It can be single-select or multi-select.

```html
<span class="listbox">
    <div role="listbox" tabindex="0">
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

When a single-select listbox receives focus for the first time, the first option should be selected if the user does not specify a selection.

An initial selection can be specified by applying the `aria-selected` state to one or more options.

## [Listbox Button](https://ebay.gitbooks.io/mindpatterns/content/input/listbox-button.html)

Opens a [listbox](#user-content-listbox) via a button flyout.

```html
<span class="listbox-button">
    <button class="listbox-button__button" aria-expanded="false" aria-haspopup="listbox">
        <span> <!-- flex container -->
            <span>Option 1</span>
            <span class="listbox-button__icon-expand"></span>
        </span>
    </button>
    <div class="listbox-button__listbox" hidden>
        <div role="listbox" tabindex="0">
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

In all cases, a menu requires a [rovingtabindex](http://www.w3.org/TR/wai-aria-practices/#focus_tabindex) for its menu items.

## [Menu Button](https://ebay.gitbooks.io/mindpatterns/content/input/menu-button.html)

A menu button opens a [menu](#user-content-menu) in a flyout.

```html
<div class="menu-button">
    <button aria-expanded="false" aria-haspopup="true" class="menu-button__button">
        <span> <!-- flex container (optional) -->
            <span>Open Menu</span>
            <span class="menu-button__icon-expand"></span>
        </span>
    </button>
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

## [Page Notice](http://ianmcburnie.github.io/mindpatterns/messaging/page-notice/)

Use `role=region` and `aria-label` to mark the page notice as a landmark for assistive technology.

```html
<section class="page-notice" role="region" aria-label="Page notice: high priority">
    <p>Something went wrong. Please try again.</p>
</section>
```

If the page notice content or display will be dynamically updated on the client, wrap the notice with `role="alert"` or `role="status"` to create a live region for assistive technology.

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

```html
<div class="tabs" id="tabs-1">
    <h2 class="clipped">Tabs Heading</h2>
    <div class="tabs__items" role="tablist">
        <div class="tabs__item" role="tab" aria-controls="tabs-1-panel-1" aria-selected="true" id="tabs1_tab1" tabindex="0">
            <span>Tab 1</span>
        </div>
        <div class="tabs__item" role="tab" aria-controls="tabs-1-panel-2" aria-selected="false" id="tabs1_tab2" tabindex="-1">
            <span>Tab 2</span>
        </div>
        <div class="tabs__item" role="tab" aria-controls="tabs-1-panel-3" aria-selected="false" id="tabs1_tab3" tabindex="-1">
            <span>Tab 3</span>
        </div>
    </div>
    <div class="tabs__content">
        <div aria-labelledby="tabs1_tab1" class="tabs__panel" role="tabpanel" id="tabs-1-panel-1">
            <h3>Panel 1 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div aria-labelledby="tabs1_tab2" class="tabs__panel" role="tabpanel" hidden id="tabs-1-panel-2">
            <h3>Panel 2 heading</h3>
            <!-- panel content goes here -->
        </div>
        <div aria-labelledby="tabs1_tab3" class="tabs__panel" role="tabpanel" hidden id="tabs-1-panel-3">
            <h3>Panel 3 heading</h3>
            <!-- panel content goes here -->
        </div>
    </div>
</div>
```

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
