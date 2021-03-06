# Unwritten Future

Platform-agnostic HTML5 Boilerplate

Designed to be used as a base for any CMS or single-page app. Used as the basis of the [Unwritten Future Wordpress Base Theme](https://github.com/jkissam/uwf-wp). I am also planning to build an Unwritten Future base theme for Drupal.

Built-in CSS includes:

* reset.css
* Bootstrap grid system (but no other bootstrap styling)
* .section-wrapper > .section > .section-inner structure for building parallax-style sites/themes
* Special "utility" section which can be placed anywhere in HTML (to render in any arbitrary place on mobile) but which is placed in upper-right-hand corner on tablets & desktop by media query

Javascript/CSS functionality includes:

* Responsive menu with touch-friendly drop-downs
* Dismissable messages
* Modals, which are openable by linking to their ids or programatically through Javascript
* Option to fix footer to the bottom of the page when content doesn't push it that far
* Option to fix secondary column so that it will not scroll off the page entirely (but will scroll if its height is greater than the window height)
* adding the `uwf-input-label` class to an `input` or `textarea` element, or to any parent of an input or textarea element, will display the label over the element (i.e., like a placeholder), but use css transitions to move it to smaller text immediately above the input when the input/textarea has focus or content. Will not affect checkbox, radio or submit input types

Additional optional Javascript functionality:

* create on-the-fly "on this page" navigation based on `h2` elements (or any other selector, as set in `uwfOptions.onThisPageHeading`) in `#content` section
* shorten links that are wider than their parents (i.e., when long URLs are used as the link text, which can break mobile layouts)
* open links to external URLs in a new window, optionally excluding by jQuery selectors
* make links to anchors in the same page scroll rather than jump (do this by adding a class)
* helper functions to set and get cookies
* populate inputs with the value of their labels
* prepare pop-ups
* add class "fixed" to a particular element when the page scrolls past a certain number of pixels
* equalize the height of a set of matched elements
* scroll the page to include a particular element
* vertically center an element relative to another element
* smartresize event

Javascript behavior can be configured through the `uwfOptions` object, and all text used by Javascript functions is in `uwfText` object for internationalization and localization

## Usage notes:

1. In order to be able to apply updates from the basic HTML framework, do not modify screen.scss, any of its component files, or uwfutil.js
2. For css, rename child-template.scss to child.scss (and create component files as necessary) in the sass folder to generate child.css, and uncomment line 19 in index.html
3. For javascript, rename script-template.js to script.js and uncomment line 201 in index.html
4. For google analytics, replace "UA-XXXXX-X" with your site's ID on line 211 of index.html, and then uncomment lines 204-213

## Version Log

### Version 1.2.2
_January 24, 2019_

* Updated `uwfUtil.prepareNavigation` so that when mobile menu is closed, all submenus are also closed
* Fixed bug in `uwfUtil.init` that was throwing a Javascript error when `uwfOptions.fixSecondary` was set to true but `#secondary` didn't exist in the DOM

### Version 1.2.1
_December 28, 2018_

* Added `jQuery(window).trigger('resize')` to `uwfUtil.prepareOnThisPage` so that any additional height created by on this page navigation is taken into account by scripts that fix elements based on scrolling

### Version 1.2
_December 27, 2018_

* Adds `uwfUtil.fixOnMaxScroll` function to "fix" any arbitrary element so that it will not scroll off the page entirely (but will scroll if its height is greater than the window height). Takes four arguments:
  * `sel` : jQuery selector for element
  * `maxScroll` : controls the maximum amount at the bottom (increase this to leave space for a footer).
  * `breakPoint` : Only implemented when window width is greater than this number (defaults to 768, assuming we don't want this behavior on "xs" devices)
  * `maxTop` : controls maximum amount at the top (increase this to leave space for a fixed header/navigation)
* Adds `uwfOptions` to apply `fixOnMaxScroll` to the `#secondary` column: `fixSecondary` (boolean), `fixSecondaryMax` (integer), `fixSecondaryBreakPoint` (integer), and `fixSecondaryTop` (integer)
* Adds `uwfUtil.registerGAevent` function as a wrapper for Google Analytics' `ga.send`
* Updates css for fieldsets and legends to a more flat look

### Version 1.1.4
_December 15, 2018_

* Fixed bug in `uwfUtil.shortenLinks` that triggered link shortening when the link is enclosed within an inline element (rewrote to find the closest non-inline element to compare the width to, instead of just using the immediate parent)

### Version 1.1.3
_July 20, 2018_

A number of updates in preparation for the unwritten_future Drupal theme:

* made a couple of changes to `prepareOnThisPage`:
    1. it will now use the _class_ `on-this-page` as well as the _id_ to find elements to populate with the menu (so you can populate multiple elements). This can be changed in `uwfOptions`
    2. new `uwfOptions.onThisPageContent` option controls what element to _search_ for headers
    3. new `on-this-page-mobile` class will place the links in a modal-like menu which is opened when any element inside the `on-this-page-mobile` element with the class of `on-this-page-mobile-trigger` is clicked (_Note:_ the developer will need to create the trigger element, and also add any classes and css media queries to make this type of menu appear/disappear if you only want to use it for mobile devices)
* `prepareNavigation` now adds `has-open-submenu` class to `#navigation-wrapper` when there is an open submenu

### Version 1.1.2
_January 6, 2018_

* changed `prepareNavigation` so only one drop-down menu can be open at a time
* changed `prepareSectionNavigation` so that it _won't_ attempt to scroll to non-existent ids, but _will_ recognize anchors (i.e., `<a name="some-id"></a>`)

### Version 1.1.1
_December 24, 2017_

* fixed `uwf-input-label` class to deal with instances where input is pre-filled

### Version 1.1
_December 18, 2017_

* added `uwf-input-label` class
* added jquery to /js/vendor so framework can be used for development in situations without access to the web

### Version 1.0
_October 2, 2017_

* added option `uwfOptions.mobileMenuDirection` to `uwfutil.js` to set direction of mobile menu (slides in from right or left). Could also be set to 'up' or 'down' if you add custom css to handle the transitions (see `_navigation.scss` lines 34-37, but you would also need to give `.menu-mobile #navigation .main-menu > ul` an absolute height, remove the absolute width, etc.).

### Version 1.0-rc9
_September 27, 2017_

* updated `uwfutil.js` to translate text for '(link)'
* created `child-template.scss` as a template for child.scss to indicate all color and font styles that might need to be changed in a child theme

### Version 1.0-rc8
_September 26, 2017_

* replaced css-only navigation icon with inline svg
* added test in `uwfUtil.fixFooter` so it doesn't throw an error if the footer HTML has been removed but `uwfOptions.fixFooter` is still set to true

### Version 1.0-rc7
_June 27, 2017_

* cleaned up a few duplicatations in `_elements.scss`
* made `a.button` elements display as `inline-block`
* improvements to `uwfUtil.shortenLinks`
* added `uwfOptions.shortenLinksSelector` option, which defaults to `a` but can be modified to limit link-shortening
* added `print.css` which only prints header and main content, prints text as black, and increases text side on the content

### Version 1.0-rc6
_June 15, 2017_

* simplified sass component files
* improved display of checkboxes, radio buttons & selects on webkit browsers on Macs
* changed navigation so that display of "mobile" vs. "full" menu is controlled by `uwfOptions.mobileBreakPoint` instead of hard-wired css selectors
* added line-height to `input[type="submit"]` elements so they are the same height as `button` and `a.button` elements
* moved modal-dismiss buttons into modal divs and added "[ESC]" text to them on non-touch devices

### Version 1.0-rc5
_June 15, 2017_

* updated to latest version of `hammerjs`
* fixed bug where prepareNavigation will throw an error if `#navigation .main-menu ul` doesn't exist
* added usage notes and script-example.js for local script

### Version 1.0-rc4

* added `width: 100%` to `button-mobile-block` class to make it, um, actually work

### Version 1.0-rc3
_May 25, 2017_

Added a new `prepareOnThisPage` function to `uwfUtil`, which will create "sections" of `#content` based on the header structure (defaulting to Header 2). This allows content editors to create "sections" of content simply by using the appropriate header element in the HTML, CMS or WYSIWYG. The function creates a menu with links which scroll to the appropriate section of the page, and "Back to top" links at the bottom of each "section."

`prepareOnThisPage` is called automatically by `uwfUtil.init` and configured by properties of the `uwfOptions` variable:
* `onThisPageHeading` : header (or other) elements which will be treated as the beginning of a new section inside `#content` (defaults to `h2`)
* `onThisPageNav` : jQuery selector for container to place on-this-page navigation inside (defaults to `#on-this-page`)
* `onThisPageMinimumSections` : minimum number of sections that must exist on the page before "on this page" navigation is implemented (defaults to 2)
* the "Back to top" text is set (and can be configured by modifying) `uwfText.backToTop`
* also note that `prepareOnThisPage` will _only_ work if `uwfOptions.sectionNavigationSelector` is set, as it relies on `uwfUtil.prepareSectionNavigation`

This version also contains a few minor fixes:
* fixed bugs in `uwfUtil.scrollToInclude()` function
* fixed bug where some of the javascript for modals used `widget` class instead of `modal`
* finished removing javascript for "reveals"
* changed `p:last-of-type` selector to `p:last-child` to remove bottom margin on last paragraph in a container, so that bottom margin is only removed if there are no other elements after it
* added `text-align: center` to `button-block` class
* added `button-mobile-block` class for buttons that should display as block buttons on mobile, but can display as regular buttons on larger devices
* made `.button-block` buttons inside `p.read-more` display as block buttons on mobile (continue to float right on larger devices)

### Version 1.0-rc2
_April 11, 2017_

Fixed & added a few things:
* added `{ margin-bottom: 0; }` to `p:last-of-type` so last paragraph within any given container will have no bottom margin, so it doesn't get added to the container's padding
* added `p.read-more` class (aligns text to the right)
* adde `button-block` class for buttons (submit inputs, buttons and links with "button" class), to create buttons which will display as a block
* added `-webkit-overflow-scrolling: touch;` to mobile menu, and changed transition from linear to ease, for improved experience on webkit touch devices

### Version 1.0-rc1
_April 7, 2017_

