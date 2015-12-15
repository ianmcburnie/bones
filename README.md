# BONES

> Widgets are stronger with bones. Does *your* widget have bones?

## Contents

1. [Introduction](#user-content-introduction)
1. [Accordion](#user-content-accordion)
1. [Breadcrumbs](#user-content-breadcrumbs)
1. [Carousel](#user-content-carousel)
1. [Combobox](#user-content-combobox)
1. [Dialog](#user-content-dialog)
1. [Input Validation](#user-content-input-validation)
1. [Pagination](#user-content-pagination)
1. [Popup Menu](#user-content-popup-menu)
1. [Popup Nav](#user-content-popup-nav)
1. [Radio](#user-content-radio)
1. [Tabs](#user-content-tabs)

## Introduction

Bones provides lean, mean, semantic HTML markup for widgets; ensuring maximum Accessibility, SEO and Site Speed performance. Bones markup has full support for <a href="http://www.w3.org/WAI/intro/aria"> WAI-ARIA</a> roles, states and properties.

Bones favors the <a href="http://en.wikipedia.org/wiki/Convention_over_configuration">convention over configuration</a> paradigm. A convention for widget structure allows us to add only a minimal amount of CSS and JavaScript 'hooks' to the base markup.<sup>1</sup>

Bones advocates the [Progressive Enhancement](http://en.wikipedia.org/wiki/Progressive_enhancement) web-design strategy; building the web in a layered fashion that allows **everyone** to access the **most important** content and functionality. We supply HTML markup for both the *before* and *after*  JavaScript initialisation states of a widget, i.e. before-enhancement and after-enhancement. If you do not wish to support progressive enhancement we also provide alternatives.<sup>2</sup>

<sub><sup>1</sup> Bones has a class naming convention similar to the <a href="http://smacss.com">SMACSS</a> architecture, whereby we define a single module name on our root node, alongside any additional *modifier* class names, such as states & themes. If additional classes are needed in the inner HTML, we encourage a BEM-style (block-level-element) naming convention and syntax.</sub>

<sub><sup>2</sup> Building an app that is rendered entirely on the client-side? If so, you will only need to refer to the enhanced/initialised code. However, best practice is to build apps in an <a href="http://nerds.airbnb.com/isomorphic-javascript-future-web-apps/">isomorphic</a> fashion so that first page load is rendered by the server then *enhanced* on the client.</sub>

## [Accordion](https://github.corp.ebay.com/pages/accessibility/patterns/disclosure/accordion.html)

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

## [Breadcrumbs](https://github.corp.ebay.com/pages/accessibility/patterns/navigation/breadcrumbs.html)

The content is an ordered list of links inside a navigation landmark region. Breadcrumbs do not require JavaScript initialisation. CSS can be used to generate → separator content.

```html
<nav class="crumbs" aria-labelledby="crumbs_heading">
    <h3 id="crumbs_heading">You are here</h3>
    <ol>
        <li><a href="http://www.ebay.com">Great Grandparent Page</a></li>
        <li><a href="http://www.ebay.com">Grandparent Page</a></li>
        <li><a href="http://www.ebay.com">Parent Page</a></li>
        <li><span>Current Page</span></li>
    </ol>
</nav>
```

## [Carousel](https://github.corp.ebay.com/pages/accessibility/patterns/disclosure/carousel.html)

### Before JavaScript Initialisation

A carousel is a list of *stuff*. This stuff can be anything - text, links, tiles, cards, widgets, you name it.

```html
<div class="carousel">
    <h2>List of Stuff</h2>
    <ul>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        ...
    </ul>
</div>
```

### After JavaScript Initialisation

JavaScript wraps the list of stuff in a new div and adds the pagination controls.

```html
<div class="carousel">
    <h2>List of Stuff</h2>
    <div>
        <button aria-disabled="false" aria-label="Show previous n items of stuff"></button>
        <ul>
            <li aria-hidden="false">...</li>
            <li aria-hidden="false">...</li>
            <li aria-hidden="false">...</li>
            ...
        </ul>
        <button aria-disabled="false" aria-label="Show next n items of stuff"></button>
    </div>
    <!-- additional pagination controls can go here as desired -->
</div>
```

JavaScript must maintain the aria-hidden state of items as they scroll in and out of view.

## Combobox

### Before JavaScript Initialisation

Without JavaScript, the combobox markup is a simple text input with label.

```html
<div class="combobox" id="combobox-1">
    <label for="combobox-1-input">Combobox Label</label>
    <input id="combobox-1-input" name="combobox-1-name" type="text">
</div>
```

### After JavaScript Initialisation

JavaScript adds the button, instructions and listbox to the markup.

```html
<div class="combobox" id="combobox-1">
    <label for="combobox-1-input">Combobox Label</label>
    <input id="combobox-1-input" name="combobox-1-name" type="text" role="combobox" aria-expanded="false" autocomplete="off" aria-owns="combobox-1-listbox" aria-describedby="combobox-1-instructions">
    <button type="button" tabindex="-1" aria-label="Expand Options"></button>
    <span id="combobox-1-instructions">Use up and down arrow keys to navigate options</span>
    <ul id="combobox-1-listbox" role="listbox">
        <li role="option" id="combobox-1-activedescendant">Option 1</li>
        <li role="option">Option 2</li>
        <li role="option">Option 3</li>
        ...
    </ul>
</div>
```

## [Dialog](https://github.corp.ebay.com/pages/accessibility/patterns/structure/dialog.html)

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

## [Input Validation](https://github.corp.ebay.com/pages/accessibility/patterns/messaging/inputvalidation.html)

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
## [Listbox](https://github.corp.ebay.com/pages/accessibility/patterns/input/listbox.html)

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

## [Pagination](https://github.corp.ebay.com/pages/accessibility/examples/pagination/)

### Stateless Pagination

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

## [Popup Menu](https://github.corp.ebay.com/pages/accessibility/patterns/input/menu.html)

A popup menu contains commands (menuitem, menuitemradio, or menuitemcheckbox) that execute JavaScript. If you require a non-JavaScript fallback, consider using native form controls (e.g. regular buttons, radios and checkboxes).

```html
<div class="popupmenu" id="popupmenu_0">
    <button aria-controls="popupmenu_0_flyout" aria-expanded="false" aria-haspopup="true" disabled>Open Menu</button>
    <div id="popupmenu_0_flyout">
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

Remember that the popup button will not work without JavaScript. Therefore we mark it as disabled in our markup and then enable it with JavaScript.

If you only require a flat list of menu items, with no groups or separators, you can instead use a more compact form of markup:

```html
<div class="popupmenu" id="popupmenu_1">
    <button aria-controls="popupmenu_1_flyout" aria-expanded="false" aria-haspopup="true">Open Menu</button>
    <div id="popupmenu_1_flyout">
        <div role="menu">
            <div role="menuitem" tabindex="0">Button 1</div>
            <div role="menuitem" tabindex="-1">Button 2</div>
        </div>
    </div>
</div>
```

In all cases, a popup menu requires a [rovingtabindex](http://www.w3.org/TR/wai-aria-practices/#focus_tabindex) for it's menu items.

## [Popup Nav](https://github.corp.ebay.com/pages/accessibility/patterns/navigation/navmenu.html)

### Before JavaScript Initialisation

The content is a button and a list of links. Use an ordered list if the items are semantically ordered in any way.

```html
<div class="popupnav">
    <button disabled>Open Nav</button>
    <div>
        <ul>
            <li><a href="http://www.ebay.com">Link Text</a></li>
            <li><a href="http://www.ebay.com">Link Text</a></li>
            <li><a href="http://www.ebay.com">Link Text</a></li>
        </ul>
    </div>
</div>
```

Remember that this button will not work without JavaScript. Therefore we disable it in our markup and then enable it with JavaScript.

### After JavaScript Initialisation

```html
<div class="popupnav popupnav--js" id="popupnav_0">
    <button aria-controls="popupnav_0_flyout" aria-expanded="false">Open Nav</button>
    <div id="popupnav_0_flyout">
        <ul>
            <li><a href="http://www.ebay.com">Link Text</a></li>
            <li><a href="http://www.ebay.com">Link Text</a></li>
            <li><a href="http://www.ebay.com">Link Text</a></li>
        </ul>
    </div>
</div>
```

If you require a popup nav that is opened by hovering on a link, rather than clicking on a button, then append an offscreen popup button immediately after the anchor tag. This button will appear, and receive focus, as soon as the user tabs past the hyperlink.

## [Radio](https://github.corp.ebay.com/pages/accessibility/patterns/input/radio.html)

```html
<div class="radiogroup" id="radiogroup1">
    <fieldset>
        <legend>Radio Group Title</legend>
        <span>
            <input id="radiogroup1_input1" name="radiogroup1" type="radio" value="1" checked />
            <label for="radiogroup1_input1">Input 1</label>
        </span>
        <span>
            <input id="radiogroup1_input2" name="radiogroup1" type="radio" value="2" />
            <label for="radiogroup1_input2">Input 2</label>
        </span>
        <span>
            <input id="radiogroup1_input3" name="radiogroup1" type="radio" value="3" />
            <label for="radiogroup1_input3">Input 3</label>
        </span>
    </fieldset>
</div>
```

If for whatever reason you cannot use the correct &lt;fieldset&gt; and &lt;legend&gt; structural elements, then you must create the grouping semantics with ARIA instead:

```html
<div class="radiogroup" id="radiogroup1">
    <div aria-labelledby="radiogroup1_label" class="radiogroup-fieldset" role="radiogroup">
        <div class="radiogroup-legend" id="radiogroup1_label">Radio Group Title</div>
        <!-- radio buttons go here, same as in example above -->
    </div>
</div>
```

Classes 'radiogroup-fieldset' and 'radiogroup-legend' can be added for additional CSS and JS hooks.

Radio button elements are traditionally difficult to style the way we want them to be. Modern CSS however, gives us the ability to 'hide' the native radio button element and generate font icon content for both the checked and unchecked states. The only caveat with this approach is that the focus indicator is also masked, meaning we must create our own custom focus indicator.

<!--
### After JavaScript Initialisation

Using JavaScript we insert custom radio elements which allow for greater styling flexibility. The native elements are now hidden.

```html
<div class="radiogroup radiogroup--js" id="radiogroup1">
    <fieldset aria-labelledby="radiogroup1_label" role="radiogroup">
        <legend id="radiogroup1_label">Radio Group Title</legend>
        <span>
            <input aria-hidden="true" id="radiogroup1_input1" name="radiogroup1" type="radio" value="1" checked />
            <span aria-checked="true" aria-labelledby="radiogroup1_label1" role="radio" tabindex="0" />
            <label aria-hidden="true" for="radiogroup1_input1" id="radiogroup1_label1">Input 1</label>
        </span>
        <span>
            <input aria-hidden="true" id="radiogroup1_input2" name="radiogroup1" type="radio" value="2" />
            <span aria-checked="false" aria-labelledby="radiogroup1_label2" role="radio" tabindex="-1" />
            <label aria-hidden="true" for="radiogroup1_input2" id="radiogroup1_label2">Input 2</label>
        </span>
        <span>
            <input aria-hidden="true" id="radiogroup1_input3" name="radiogroup1" type="radio" value="3" />
            <span aria-checked="false" aria-labelledby="radiogroup1_label3" role="radio" tabindex="-1" />
            <label aria-hidden="true" for="radiogroup1_input3" id="radiogroup1_label3">Input 3</label>
        </span>
    </fieldset>
</div>
```

Notice that aria-hidden is now applied to the labels. This is to prevent an issue in Voiceover which treats the labels as members of the radiogroup role, thus doubling the number of reported radio items in the group. Don't worry, the label will still be read when focus and virtual cursor is on the custom radio button.

-->

## [Tabs](https://github.corp.ebay.com/pages/accessibility/patterns/disclosure/tabs.html)

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
    <h2>Tabs Heading</h2>
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
    <h2>Tabs Heading</h2>
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

## More to Come...
