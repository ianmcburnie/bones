# BONES

> Widgets are stronger with bones. Does *your* widget have bones?

## Contents

1. [Introduction](#user-content-introduction)
1. [Accordion](#user-content-accordion)
1. [Alert Dialog](#user-content-alert-dialog)
1. [Breadcrumbs](#user-content-breadcrumbs)
1. [Carousel](#user-content-carousel)
1. [Checkbox](#user-content-checkbox)
1. [Combobox](#user-content-combobox)
1. [Confirm Dialog](#user-content-confirm-dialog)
1. [Details](#user-content-details)
1. [Fake Menu](#user-content-fake-menu)
1. [Fake Tabs](#user-content-fake-tabs)
1. [Flyout](#user-content-flyout)
1. [Fullscreen Dialog](#user-content-fullscreen-dialog)
1. [Icon Button](#user-content-icon-button)
1. [Infotip](#user-content-infotip)
1. [Inline Notice](#user-content-inline-notice)
1. [Input Dialog](#user-content-input-dialog)
1. [Input Validation](#user-content-input-validation)
1. [Lightbox Dialog](#user-content-lightbox-dialog)
1. [Listbox](#user-content-listbox)
1. [Listbox Button](#user-content-listbox-button)
1. [Menu](#user-content-menu)
1. [Menu Button](#user-content-menu-button)
1. [Page Notice](#user-content-page-notice)
1. [Pagination](#user-content-pagination)
1. [Panel Dialog](#user-content-panel-dialog)
1. [Radio](#user-content-radio)
1. [Select](#user-content-select)
1. [Switch](#user-content-switch)
1. [Tabs](#user-content-tabs)
1. [Toast Dialog](#user-content-toast-dialog)
1. [Tooltip](#user-content-tooltip)
1. [Tourtip](#user-content-tourtip)

## Introduction

Bones provides lean, mean, semantic HTML markup for widgets; ensuring maximum Accessibility, SEO and Site Speed performance. Bones markup uses [ARIA](http://www.w3.org/WAI/intro/aria) only where strictly necessary.

Bones is not intended to be an exhaustive set of instructions for creating accessible components. The primary intention of bones is to detail the structural and semantic markup requirements. For further guidance, please visit [eBay MIND Patterns](https://ebay.gitbook.io/mindpatterns) and/or [WAI-ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices-1.1).

Bones advocates the [Progressive Enhancement](http://en.wikipedia.org/wiki/Progressive_enhancement) web-design strategy; building the web in a layered fashion that allows **everyone** to access the **most important** content and functionality.

Bones favors the the [BEM](http://getbem.com) (block, element, modifier) methodology and naming convention.

## [Accordion](https://ebay.gitbooks.io/mindpatterns/content/disclosure/accordion.html)

The accordion is simply a list of [details](#user-content-details) widgets. Each details summary should include a relevant heading-level tag.

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

## [Alert Dialog](https://ebay.gitbooks.io/mindpatterns/content/messaging/alert-dialog.html)

A [lightbox dialog](#user-content-lightbox-dialog) with a single button to acknowledge the alert content.

Try to bucket the main page content in an element that is *not* an ancestor of the dialog. This will vastly simplify the amount of DOM manipulation when implementing modal behaviour.

```html
<body>
    <div>
        <!-- main page content -->
    </div>
    <div class="alert-dialog" role="alertdialog" aria-labelledby="alert-dialog-title" aria-modal="true" hidden>
        <div class="alert-dialog__window">
            <div class="alert-dialog__header">
                <h2 class="alert-dialog__title" id="dialog-title">Alert Dialog Title</h2>
            </div>
            <div class="alert-dialog__main">
                <!-- alert dialog content goes here -->
            </div>
            <div class="alert-dialog__footer">
                <button class="alert-dialog__acknowledge" type="button">OK</button>
            </div>
        </div>
    </div>
</body>
```

## [Breadcrumbs](https://ebay.gitbooks.io/mindpatterns/content/navigation/breadcrumbs.html)

The content is an ordered list of links inside a navigation landmark region.

```html
<nav class="breadcrumbs" aria-labelledby="breadcrumbs_heading" role="navigation">
    <h2 class="clipped" id="breadcrumbs_heading">You are here</h2>
    <ol>
        <li>
            <a href="http://www.ebay.com">Great Grandparent Page</a>
            <svg focusable="false" height="10" width="10" aria-hidden="true">
                <use xlink:href="#icon-breadcrumb"></use>
            </svg>
        </li>
        <li>
            <a href="http://www.ebay.com">Grandparent Page</a>
            <svg focusable="false" height="10" width="10" aria-hidden="true">
                <use xlink:href="#icon-breadcrumb"></use>
            </svg>
        </li>
        <li>
            <a href="http://www.ebay.com">Parent Page</a>
            <svg focusable="false" height="10" width="10" aria-hidden="true">
                <use xlink:href="#icon-breadcrumb"></use>
            </svg>
        </li>
        <li>
            <a aria-current="page">Current Page</a>
        </li>
    </ol>
</nav>
```

While CSS can be used to generate a separator image or glyph using the `::after` pseudo element, we find that inline SVG offers a more accessible and flexible approach.

## [Carousel](https://ebay.gitbooks.io/mindpatterns/content/disclosure/carousel.html)

A carousel is a list of items. These items may contain anything - text, images, links, tiles, cards, etc. - but each item is responsible for managing its own markup and accessibility (e.g. tab-order, semantics, etc).

```html
<div class="carousel" role="group" aria-labelledby="carousel-title" aria-roledescription="carousel">
    <button aria-label="Previous slide">
        <!-- SVG icon -->
    </button>
    <ul>
        <!-- onscreen items -->
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        <li aria-hidden="false">...</li>
        <!-- offscreen items -->
        <li aria-hidden="true">...</li>
        <li aria-hidden="true">...</li>
        <li aria-hidden="true">...</li>
        <li aria-hidden="true">...</li>
        <li aria-hidden="true">...</li>
    </ul>
    <button aria-label="Next slide">
        <!-- SVG icon -->
    </button>
</div>
```

JavaScript must maintain the tabindex and aria-hidden state of items as they scroll in and out of view.

## [Checkbox](https://ebay.gitbooks.io/mindpatterns/content/input/checkbox.html)

Native HTML checkboxes are 100% accessible by default.

To ensure correct grouping semantics, checkboxes should be placed inside of a fieldset with legend.

```html
<fieldset>
    <legend>Auction Type</legend>
    <span>
        <input id="freeshipping" type="checkbox" name="freeshipping" />
        <label for="freeshipping">Free Shipping</label>
    </span>
    <span>
        <input id="endssoon" type="checkbox" name="endssoon" />
        <label for="endssoon">Ends soon</label>
    </span>
    <span>
        <input id="zerobids" type="checkbox" name="zerobids" />
        <label for="zerobids">Zero bids</label>
    </span>
</fieldset>
```

For vertically stacked checkboxes, simply switch the spans to divs.

### Custom Checkbox Icon

A foreground SVG, combined with CSS, can be used as a facade over the real checkbox.

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

This markup assumes that the symbol definitions for `#icon-checkbox-unchecked` and `#icon-checkbox-checked` exist on the page. The hidden property ensures that the SVG icon is not visible alongside the native icon when the page is in a non-CSS state. This hidden property should be over-ridden by CSS.

## [Combobox](https://ebay.gitbooks.io/mindpatterns/content/input/combobox.html)

A textbox plus listbox combination.

### Collapsed State

```html
<div class="combobox" id="combobox-1">
    <span class="combobox__control">
        <input name="combobox-1-name" type="text" role="combobox" autocomplete="off" aria-expanded="false" aria-owns="combobox-1-listbox" />
    </span>
    <div class="combobox__overlay">
        <ul id="combobox-1-listbox" role="listbox">
            <li role="option" id="combobox-1-option-1">Option 1</li>
            <li role="option" id="combobox-1-option-2">Option 2</li>
            <li role="option" id="combobox-1-option-3">Option 3</li>
            ...
        </ul>
    </div>
</div>
```

### Expanded State

```html
<div class="combobox combobox--expanded" id="combobox-1">
    <span class="combobox__control">
        <input name="combobox-1-name" type="text" role="combobox" autocomplete="off" aria-expanded="true" aria-owns="combobox-1-listbox" />
    </span>
    <div class="combobox__overlay">
        <ul id="combobox-1-listbox" role="listbox">
            <li role="option" id="combobox-1-option-1">Option 1</li>
            <li role="option" id="combobox-1-option-2">Option 2</li>
            <li role="option" id="combobox-1-option-3">Option 3</li>
            ...
        </ul>
    </div>
</div>
```

JavaScript must update the `aria-activedescendant` attribute on the textbox to reflect the state of the currently active descendant listbox item.

## [Confirm Dialog](https://ebay.gitbooks.io/mindpatterns/content/messaging/confirm-dialog.html)

A [lightbox dialog](#user-content-lightbox-dialog) with buttons to cancel or confirm an action.

Try to bucket the main page content in an element that is *not* an ancestor of the dialog. This will vastly simplify the amount of DOM manipulation when implementing modal behaviour.

```html
<body>
    <div>
        <!-- main page content -->
    </div>
    <div class="confirm-dialog" role="dialog" aria-labelledby="confirm-dialog-title" aria-modal="true" hidden>
        <div class="confirm-dialog__window">
            <div class="confirm-dialog__header">
                <h2 class="confirm-dialog__title" id="confirm-dialog-title">Confirm Dialog Title</h2>
            </div>
            <div class="confirm-dialog__main">
                <!-- confirm dialog content goes here -->
            </div>
            <div class="confirm-dialog__footer">
                <button class="confirm-dialog__cancel" type="button">Cancel</button>
                <button class="confirm-dialog__confirm" type="button">OK</button>
            </div>
        </div>
    </div>
</body>
```

## [Details](https://ebay.gitbooks.io/mindpatterns/content/disclosure/details.html)

Uses the native HTML `<details>` tag.

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

## [Fake Menu](https://ebay.gitbooks.io/mindpatterns/content/navigation/fake-menu.html)

A fake menu is styled like a regular menu, but it contains a list of links and/or buttons instead of menu items.

```html
<ul>
    <li>
        <a href="http://www.ebay.com">Link Text</a>
    </li>
    <li>
        <button type="button">Button Text</button>
    </li>
    <li>
        <a href="http://www.ebay.com">Link Text</a>
    </li>
</ul>
```

If the `href` value of a fake menu item matches the current page url, then add `aria-current="page"` to that anchor tag.

## [Fake-Menu Button](https://ebay.gitbooks.io/mindpatterns/content/navigation/fake-menu-button.html)

A button that opens a fake menu.

```html
<div class="fake-menu">
    <button aria-expanded="false">Fake Menu</button>
    <div>
        <ul>
            <li>
                <a href="http://www.ebay.com">Link Text</a>
            </li>
            <li>
                <button type="button">Button Text</button>
            </li>
            <li>
                <a href="http://www.ebay.com">Link Text</a>
            </li>
        </ul>
    </div>
</div>
```

## [Fake Tabs](https://ebay.gitbooks.io/mindpatterns/content/navigation/fake-tabs.html)

Fake tabs are simply a list of links styled to look like tabs.

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

## [Flyout](https://ebay.gitbooks.io/mindpatterns/content/disclosure/flyout.html)

A flyout might open on click, focus or hover, on any kind of host button, input or link.

For correct reading order, and to minimize accessibility defects, the overlay element and its content should always immediately follow the host element in the DOM.

```html
<div class="flyout">
    <button class="flyout__host" aria-expanded="false">Host Button</button>
    <div class="flyout__overlay">
        <!-- overlay content -->
    </div>
</div>
```

If the overlay element cannot be immediately adjacent to the button element, then an additional class will be required for styling purposes:

```html
<div class="flyout flyout--expanded">
    <div>
        <button class="flyout__host" aria-expanded="true">Host Button</button>
    </div>
    <div class="flyout__overlay">
        <!-- overlay content -->
    </div>
</div>
```

## [Fullscreen Dialog](https://ebay.gitbooks.io/mindpatterns/content/disclosure/fullscreen-dialog.html)

A fullscreen dialog takes over the entire screen.

Try to bucket the main page content in an element that is *not* an ancestor of the dialog. This will vastly simplify the amount of DOM manipulation when implementing modal behaviour.

```html
<body>
    <div>
        <!-- main page content -->
    </div>
    <div class="fullscreen-dialog" role="dialog" aria-labelledby="dialog-title" aria-modal="true" hidden>
        <div class="fullscreen-dialog__window">
            <div id="dialog-title" class="fullscreen-dialog__header">
                <button aria-label="Close dialog" class="fullscreen-dialog__close" type="button">
                    <svg aria-hidden="true" focusable="false" height="16" width="16">
                        <use xlink:href="#icon-close"></use>
                    </svg>
                </button>
                <h2 class="large-text-1 bold-text">Fullscreen Dialog Title</h2>
            </div>
            <div class="fullscreen-dialog__main">
                <!-- dialog copy -->
            </div>
        </div>
    </div>
</body>
```

Note that Menu Button, Listbox Button, Tooltip & Combobox are special instances of flyouts, but follow the same general pattern and rules.

## [Icon Button](https://ebay.gitbooks.io/mindpatterns/content/input/icon-button.html)

Using a hamburger menu as an example, for button behaviour:

```html
<button class="icon-btn" type="button" aria-label="Menu">
    <svg class="icon icon--menu" focusable="false" width="16" height="16" aria-hidden="true">
        <use xlink:href="icons.svg#icon-menu"></use>
    </svg>
</button>
```

For link behaviour:

```html
<a class="icon-link" href="http://www.ebay.com" aria-label="Menu">
    <svg class="icon icon--menu" focusable="false" width="16" height="16" aria-hidden="true">
        <use xlink:href="icons.svg#icon-menu"></use>
    </svg>
</a>
```

## [Infotip](https://ebay.gitbooks.io/mindpatterns/content/disclosure/infotip.html)

An infotip is expanded and visible on click event of host element.

Infotip is a specific type of [flyout](#user-content-flyout). The markup becomes a little more convoluted due to the presence of a visual "pointer". This additional markup allows enough hooks for styling & masking with CSS.

```html
<span class="infotip">
    <button class="infotip__host" type="button" aria-expanded="false" aria-label="Help">
        <svg focusable="false" width="16" height="16" aria-hidden="true">
            <use xlink:href="#icon-information-small"></use>
        </svg>
    </button>
    <div class="infotip__overlay">
        <span class="infotip__pointer infotip__pointer--bottom-center"></span>
        <div class="infotip__mask">
            <div class="infotip__cell">
                <span class="infotip__content">
                    <h3 class="infotip__heading">Infotip Title</h3>
                    <p>Infotip Copy</p>
                </span>
                <button class="infotip__close" type="button" aria-label="Dismiss infotip">
                    <svg focusable="false" height="24" width="24" aria-hidden="true">
                        <use xlink:href="#icon-close"></use>
                    </svg>
                </button>
            </div>
        </div>
    </div>
</span>
```

## [Inline-Notice](https://ebay.gitbooks.io/mindpatterns/content/messaging/inline-notice.html)

If the inline notice is rendered or updated on the client, wrap it within a [live-region](https://ebay.gitbook.io/mindpatterns/techniques/live-region) element.

```html
<div class="inline-notice inline-notice--confirmation">
    <span class="inline-notice__header">
        <svg focusable="false" class="icon icon--confirmation-filled" height="16" width="16" role="img" aria-label="Confirmation">
            <use xlink:href="#icon-confirmation-filled"></use>
        </svg>
    </span>
    <span class="inline-notice__main">
        <p>Notice Copy</p>
    </span>
</div>
```

## [Input Dialog](https://ebay.gitbooks.io/mindpatterns/content/disclosure/input-dialog.html)

A [lightbox dialog](#user-content-lightbox-dialog) with one or more form inputs.

Try to bucket the main page content in an element that is *not* an ancestor of the dialog. This will vastly simplify the amount of DOM manipulation when implementing modal behaviour.

```html
<body>
    <div>
        <!-- main page content -->
    </div>
    <div class="input-dialog" role="dialog" aria-labelledby="input-dialog-title" aria-modal="true">
        <div class="input-dialog__window">
            <div class="input-dialog__header">
                <h2 class="input-dialog__title" id="input-dialog-title">Input Dialog Title</h2>
            </div>
            <div class="input-dialog__main">
                <label for="foo">Input Label</label>
                <input id="foo" type="text" name="foo" />
            </div>
            <div class="input-dialog__footer">
                <button class="input-dialog__cancel" type="button">Cancel</button>
                <button class="input-dialog__submit" type="button">Submit</button>
            </div>
        </div>
    </div>
</body>
```

## [Input Validation](https://ebay.gitbooks.io/mindpatterns/content/messaging/input-validation.html)

Input validation messages rendered on the client are considered an *enhancement* to full, server-side form validation.

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

Notice that the `aria-described` attribute supplements the live-region, by using the same live-region content as a *description* for the input.

## [Lightbox Dialog](https://ebay.gitbooks.io/mindpatterns/content/disclosure/lightbox-dialog.html)

A lightbox dialog is always modal. Other types of lightbox dialog include: [alert dialog](#user-content-alert-dialog), [confirm dialog](#user-content-confirm-dialog) & [input dialog](#user-content-input-dialog).

Try to bucket the main page content in an element that is *not* an ancestor of the dialog. This will vastly simplify the amount of DOM manipulation when implementing modal behaviour.

```html
<div class="lightbox-dialog" role="dialog" aria-labelledby="lightbox-dialog-title" aria-modal="true">
    <div class="lightbox-dialog__window">
        <div class="lightbox-dialog__header">
            <h2 class="lightbox-dialog__title" id="lightbox-dialog-title">Dialog Title</h2>
            <button aria-label="Close dialog" class="lightbox-dialog__close" type="button"></button>
        </div>
        <div class="lightbox-dialog__main">
            <!-- lightbox dialog content goes here -->
        </div>
    </div>
</div>
```

## [Listbox](https://ebay.gitbooks.io/mindpatterns/content/input/listbox.html)

The listbox pattern is intended as a JavaScript alternative to the `multiselect` state of the HTML select.

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

Opens a [listbox](#user-content-listbox) via a host button.

```html
<span class="listbox-button">
    <button class="listbox-button__button" aria-expanded="false" aria-haspopup="listbox">
        <span>
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

A menu contains one or more groups of commands (`menuitem`, `menuitemradio`, or `menuitemcheckbox`) that execute JavaScript.

### Single Group

```html
<div class="menu">
    <div role="menu">
        <div role="menuitem" tabindex="0">Button 1</div>
        <div role="menuitem" tabindex="-1">Button 2</div>
    </div>
</div>
```

### Multiple Groups

```html
<div class="menu">
    <div role="menu">
        <div role="presentation">
            <div role="menuitem" tabindex="0">Button 1</div>
            <div role="menuitem" tabindex="-1">Button 2</div>
        </div>
        <hr />
        <div role="presentation">
            <div aria-checked="true" role="menuitemradio" tabindex="-1">Radio Button 1</div>
            <div aria-checked="false" role="menuitemradio" tabindex="-1">Radio Button 2 </div>
            <div aria-checked="false" role="menuitemradio" tabindex="-1">Radio Button 3</div>
        </div>
        <hr />
        <div role="presentation">
            <div aria-checked="true" role="menuitemcheckbox" tabindex="-1">Checkbox 1</div>
            <div aria-checked="true" role="menuitemcheckbox"  tabindex="-1">Checkbox 2</div>
        </div>
    </div>
</div>
```

## [Menu Button](https://ebay.gitbooks.io/mindpatterns/content/input/menu-button.html)

A menu button opens a [menu](#user-content-menu) in a [flyout](#user-content-flyout).

```html
<div class="menu-button">
    <button aria-expanded="false" aria-haspopup="true" class="menu-button__button">
        <span>
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

Page notices are common and prominent visual landmarks on any website. A labelled landmark element (i.e. `<section>`) increases affordance for assistive technology.

A live-region ensure dynamic updates on the client are picked up by assistive technology. This live-region can be removed or set to "off" if the page notice is only ever rendered once on the server without any further client-side changes or updates.

```html
<span aria-live="polite">
    <section class="page-notice page-notice--information" role="region" aria-label="Information">
        <div class="page-notice__header">
            <svg focusable="false" height="24" width="24" role="img" aria-label="Information">
                <use xlink:href="#icon-information"></use>
            </svg>
        </div>
        <div class="page-notice__main">
            <h2 class="page-notice__title">Title</h2>
            <p>Copy</p>
        </div>
        <div class="page-notice__footer">
            <a href="https://www.ebay.com" class="page-notice__cta">Call to action</a>
        </div>
    </section>
</span>
```

## [Pagination](http://ianmcburnie.github.io/mindpatterns/pagination/)

Pagination is an important means of site navigation. A labelled landmark element (i.e. `<nav>`) increases affordance for assistive technology.

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

**NOTE:** The ARIA live-region need only be enabled (set from "off" to "polite") if client-side pagination is implemented.

## [Panel Dialog](https://ebay.gitbooks.io/mindpatterns/content/disclosure/panel-dialog.html)

A modal dialog that sits flush to one side of the screen.

Try to bucket the main page content in an element that is *not* an ancestor of the dialog. This will vastly simplify the amount of DOM manipulation when implementing modal behaviour.

```html
<div aria-labelledby="dialog-title" aria-modal="true" class="panel-dialog" hidden id="dialog-left-panel-0" role="dialog">
    <div class="panel-dialog__window">
        <div class="panel-dialog__header">
            <h2 id="dialog-title" class="panel-dialog__title">Panel Dialog Title</h2>
            <button aria-label="Close dialog" class="icon-btn panel-dialog__close" type="button">
                <svg aria-hidden="true" class="icon icon--close" focusable="false" height="16" width="16">
                    <use xlink:href="#icon-close"></use>
                </svg>
            </button>
        </div>
        <div class="panel-dialog__main">
            <!-- content -->
        </div>
        <!-- optional -->
        <div class="panel-dialog__footer">
            <!-- content -->
        </div>
    </div>
</div>
```

## [Radio](https://ebay.gitbooks.io/mindpatterns/content/input/radio.html)

Native HTML radio buttons are 100% accessible by default.

To ensure correct grouping semantics, radio buttons should be placed inside of a fieldset with legend.

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

Foreground SVG can be used as a facade over the real radio.

```HTML
<span class="radio" hidden>
    <input class="radio__control" id="radio-group1_input1" type="radio" value="3" name="radio-group-1" />
    <svg aria-hidden="true" class="radio__unchecked" focusable="false">
        <use xlink:href="#icon-radio-unchecked"></use>
    </svg>
    <svg aria-hidden="true" class="radio__checked" focusable="false">
        <use xlink:href="#icon-confirmation"></use>
    </svg>
</span>
```

The hidden property ensures that the SVG icon is not visible alongside the native icon when the page is in a non-CSS state. This hidden property should be overriden by CSS.

## [Select](https://ebay.gitbooks.io/mindpatterns/content/input/select.html)

A native HTML select is 100% accessible by default. The "button" can be styled with CSS; the "dropdown" not so much.

```html
<span class="select">
    <select name="options">
        <option value="item1">Option 1</option>
        <option value="item2">Option 2</option>
        <option value="item3">Option 3</option>
    </select>
    <svg class="icon icon--dropdown" focusable="false" height="8" width="8" aria-hidden="true">
        <use xlink:href="#icon-dropdown"></use>
    </svg>
</span>
```

## [Switch](https://ebay.gitbooks.io/mindpatterns/content/input/switch.html)

A switch is not a true form control. It typically executes JavaScript on the client when toggled (i.e. without a full page reload).

```html
<span class="switch">
    <span class="switch__control" role="switch" tabindex="0" aria-checked="false"></span>
    <span class="switch__button"></span>
</span>
```

The following version of the switch uses a checkbox under the hood. It should be used if you require the switch to store data inside of a form. As mentioned above however, this is not the intended purpose of a switch. You may wish to consider using an actual checkbox instead.

```html
<span class="switch">
    <input class="switch__control" role="switch" type="checkbox" aria-checked="false" />
    <span class="switch__button"></span>
</span>
```

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
            <!-- panel content -->
        </div>
        <div aria-labelledby="tabs1_tab2" class="tabs__panel" role="tabpanel" hidden id="tabs-1-panel-2">
            <h3>Panel 2 heading</h3>
            <!-- panel content -->
        </div>
        <div aria-labelledby="tabs1_tab3" class="tabs__panel" role="tabpanel" hidden id="tabs-1-panel-3">
            <h3>Panel 3 heading</h3>
            <!-- panel content -->
        </div>
    </div>
</div>
```

## [Toast Dialog](https://ebay.gitbooks.io/mindpatterns/content/messaging/toast-dialog.html)

Toast dialog is non-modal and should not steal or trap keyboard focus.

Try to position the dialog immediately after the currently focussed element (i.e. the `document.activeElement`).

```html
<aside aria-label="Notification" aria-live="polite" aria-modal="false" class="toast-dialog" hidden role="dialog">
    <div class="toast-dialog__window">
        <div class="toast-dialog__header">
            <h2 class="toast-dialog__title">
                <!-- heading -->
            </h2>
            <button class="toast-dialog__close" type="button" aria-label="Close notification dialog">
                <svg focusable="false" height="24" width="24" aria-hidden="true">
                    <use xlink:href="#icon-close"></use>
                </svg>
            </button>
        </div>
        <div class="toast-dialog__main">
            <!-- content -->
        </div>
        <!-- optional footer with cta -->
        <div class="toast-dialog__footer">
            <a accesskey="a" class="toast-dialog__cta" href="http://www.ebay.com">Action</a>
        </div>
    </div>
</aside>
```

If using the optional footer with call-to-action link or button, the first letter of the CTA will define the `accesskey` property.

## [Tooltip](https://ebay.gitbooks.io/mindpatterns/content/disclosure/tooltip.html)

A tooltip is expanded and visible on hover and focus of host element.

Tooltip structure is almost identical to [flyout](#user-content-flyout) structure. The markup becomes a little more convoluted due to the presence of a visual "pointer". This additional markup allows enough hooks for styling & masking with CSS.

```html
<span class="tooltip">
    <button class="tooltip__host" aria-describedby="tooltip-0" aria-expanded="false" aria-label="Settings">
        <svg focusable="false" height="16" width="16" aria-hidden="true">
            <use xlink:href="#icon-settings"></use>
        </svg>
    </button>
    <div class="tooltip__overlay" id="tooltip-0" role="tooltip">
        <span class="tooltip__pointer"></span>
        <div class="tooltip__mask">
            <div class="tooltip__cell">
                <div class="tooltip__content">
                    <!-- content -->
                </div>
            </div>
        </div>
    </div>
</span>
```

## [Tourtip](https://ebay.gitbooks.io/mindpatterns/content/messaging/tourtip.html)

A tourtip is expanded and visible on page load.

Tourtip structure is almost identical to [flyout](#user-content-flyout) structure. The markup becomes a little more convoluted due to the presence of a visual "pointer". This additional markup allows enough hooks for styling & masking with CSS.

```html
<div class="tourtip tourtip--expanded">
    <button class="tourtip__host" aria-label="Settings">
        <svg focusable="false" height="16" width="16" aria-hidden="true">
            <use xlink:href="#icon-settings"></use>
        </svg>
    </button>
    <div class="tourtip__overlay" role="region" aria-labelledby="tourtip-label">
        <span class="tourtip__pointer"></span>
        <div class="tourtip__mask">
            <div class="tourtip__cell">
                <span class="tourtip__content">
                    <h2 class="tourtip__heading" id="tourtip-label">Tourtip Title</h2>
                    <!-- content -->
                </span>
                <button class="tourtip__close" type="button" aria-label="Dismiss tip">
                    <svg focusable="false" height="24" width="24" aria-hidden="true">
                        <use xlink:href="#icon-close"></use>
                    </svg>
                </button>
            </div>
        </div>
    </div>
</div>
```
