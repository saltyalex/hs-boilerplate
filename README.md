# Introduction

### Purpose
This is a skeleton framework designed for rallying developers around a common starting point on Hubspot CMS. Through this documentation, these topics will be covered: file organization; guiding principles for successful application of the framework; and optimizations that need to be accounted for.

## File Organization
The following is a overview description of the common directories and key places. More specific documentation is available in README.md in each sub-directory, if available. Please use these directory specific documents to leave notes for other team members regarding appropriate topics.
It is important to maintain a folder structure that is as similar as possible to this standard:

#### `css`
 - `css` contains our common css global; usually named *main.css*
 --> `components` keep common constructs such as cards, modal, and carousel styles here
 --> `elements` holds styles for lower level elements like forms, tables, buttons, colors, etc
 --> `generic` resets, weird optimizations, and other odd global styles go here
 --> `modules` styles specific to custom modules are stored here
 --> `objects` these styles are used for powering the site layout engine
 --> `templates` are styles specific to page templates
 --> `tools` contains macros and pertinent code samples for css specifically
 
#### `js`
 - javascript goes here; keep scripts in separate files as often as it makes sense to for optimization purposes

#### `modules`
 - our custom modules go here; refer to [Guiding Philosophies](#guiding%20philosophies) for useful details regarding where we should employ custom modules
 
#### `templates`
 - `templates` straightforwardly is used to store our template files
 --> `layouts` generally just needs a single file; sets up page structure
 --> `partials` is used to store static constructs that require their own editing screen
 --> `sections` contains pre-defined DND area layouts; build most content from these
 --> `system` these templates are used to run HubSpot features; edit sparingly

#### `tools`
- `tools` this is a good place general code samples, macros, etc
 -->`macros` general use macros; keep organized away from other files here

>**!IMPORTANT!** -- Files that begin with an underscore ("_normalize.css," for example) are used to denote that the file is included somewhere else. Please maintain this convention to provide useful information at a glance to fellow developers!

## Guiding Philosophies
This framework is not meant to restrict any developer, but simply to reduce repetitious development constructs. As such, when extending the framework and building functionality within it, it's important to consider the principles that underpin it.

### Mobile-first, but just a little bit more
Common, but often overlooked. Our most important consideration is to develop from a mobile screen-size first; adding styles as needed while also making sure styles that are specific to a viewport are only written for those viewports.

>A common example of this is main menu styles. If there are borders only on mobile, do not override the border to hide it on desktop; place these styles in a mobile only media query instead.

### Make use of DND areas for layout
Hubspot DND areas are now very capable and can be safely considered a visual layout generator. Manually defined layout should primarily be considered for layout within custom modules, but even that should be used sparingly. The following is an example of legacy layout structures and beside it is its representation in DND area syntax:
| Legacy | DND Area |
|--|--|
|`<section><div class="page-center"><div class="row-fluid"><div class="col-6">`|`{% dnd_section %}{% dnd_column %}{% dnd_row %}{% dnd_column %}` |

In addition to this more simplified syntax, block-specific settings are available to provide defaults when creating pre-defined section layouts for end-users. The following is a simple example:

`{% dnd_section background_color={{ context.background_color or "#f8fafc" }}, vertical_alignment="MIDDLE" %}`

### Build from existing section layouts first
A number of default section layouts are included to facilitate faster content production. In general, try to build as much page/content structure as possible within the DND area layouts before resorting to using a custom module to accomplish development of the design.

### Use custom modules sparingly
Following on this sentiment, custom modules should be used to accomplish rich functionality that does not already exist in the theme OR if the development goal would be impossible otherwise. Put more simply, custom modules should be used for carousel sliders, calculators, and similar functionality. That's the key word here: *functionality.*

## Optimizations
There are a few optimizations that must be accounted for. Altering these may negatively impact Google Core Web Vital scores.

 - `templates/layout/base.html` header css injected directly into head to speed above-fold rendering
 --> `modules/menu-section` the second part of the related optimization above
 --> `modules/megamenu-section` this mirrors the menu-section optimization
 
 - Custom modules have their own specific considerations
 -- Shared component functionality should be included using the "**Linked Files**" panel in the custom module settings. This helps to keep updates and fixes consistent while also separating module-specific overrides to the module CSS/JS. Further overrides on the module level can be accomplished with [scoping](https://developers.hubspot.com/docs/cms/building-blocks/modules/files#require-css-block).
 
 # Introduction