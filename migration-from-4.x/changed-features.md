---
layout: default
title: Deprecated Features
title_nav: Deprecated Features
description: These features have either changed or have been deleted in TinyMCE 5.
keywords: deleted removed changedfeatures migration 4
---

Each release of TinyMCE adds new features and functionality. We also occasionally remove features and functionality, usually because we've added a better option.

Here are the details about the features removed or changed in TinyMCE 5.

## Removed Features

### Listbox toolbar button type

**Listbox** is no longer a supported toolbar button type. Functionality provided by listbox toolbar buttons can be retained by switching to a different type of toolbar button. The recommended toolbar button type to switch to is the [Split button]({{site.baseurl}}/ui-elements/typesoftoolbarbuttons/#splitbutton).

### Modern theme

The Modern theme is no longer supported. The modern theme's UI library `tinymce.ui.*` has also been deleted. This change may impact integrations depending upon the level of customization.

For changes required, refer to the following table:

| Customization Level | Description | Impact |
| ------------------- | ----------- | ------ |
| Minor | Some custom buttons | no UI fixes required, update `addButton` configuration to TinyMCE 5 format |
| Moderate | A dialog created using `editor.windowManager.open` configuration objects | Convert TinyMCE 4 configuration to TinyMCE 5 configuration |
| Major | Completely custom dialogs and extended use of the Modern UI framework | Not all API use cases are covered by our new TinyMCE 5 components. However, we will strive to create supported workarounds or a new component to resolve the use case. |

> Note: Please provide feedback on your use case and your TinyMCE 4 configuration containing the UI component that you wish to be supported or need a workaround.

> Note: The Silver theme contains a set of configurable UI components that could be used to replace the old customizations (modern, inline, and inlite theme). The Silver theme is enabled by default and will load if you do not specify a theme.


## Changed Features

### Inlite theme

The "Inlite" theme provided a lightweight context toolbars similar to the popular Medium blogging service. The Inlite theme is no longer supported and its features are now available via the [Inlite plugin]({{site.baseurl}}/plugins/inlite). To load the plugin, use the following configuration:
```
{
  theme: 'silver',
  inline: true,
  toolbar: false,
  plugins: [ 'inlite' ]
}
 ```


### Responsive dialog height and width

Plugins that use dialogs no longer have `height` or `width` properties. Dialogs now use a predefined `small`, `medium`, and `large` template to specify the dimensions that responds to the user's screen size.

Specifically, the following plugins no longer require height or width options to be specified:

* [Code]({{site.baseurl}}/plugins/code/)
* [Codesample]({{site.baseurl}}plugins/codesample/)
* [Preview]({{site.baseurl}}plugins/preview/)
* [Template]({{site.baseurl}}plugins/template/)


### Improved table editing experience

* The **Styles** text input has been removed from the **Advanced** section of the dialogs. This simplifies the user experience and enables stricter control over table styles.

* More CSS is used for table styling, and legacy data attributes have been removed from the dialogs. This makes the output HTML cleaner and more modern.

* When opening a properties dialog with a single table/row/cell selected, the dialog will autofill with the relevant existing values. If you select multiple rows or cells and open the relevant properties dialog, TinyMCE 4 would leave all the dialog fields blank. In TinyMCE 5, any fields which have the same values for all the selected rows or cells will autofill, and the fields which have no existing value or have differing values will be empty.

* `Border` input field in the `tableprops` dialog is now called `Border width`, for better clarity.


### Context Menu

The Context Menu is no longer a plugin, it is part of the core and always enabled. 

The [`contextmenu` configuration]({{site.baseurl}}/components/contextmenu) can include menu items as before, but now also plugin menu "sections". These sections are dynamic and may show or hide depending on the cursor position when the context menu is opened. For example, the default context menu config now includes the sections `'link image editimage table spelling'`.


### Context Toolbar

The [Context Toolbar]({{site.baseurl}}/components/contexttoolbar) buttons are added using `addButton`, `addToggleButton`, `addSplitButton` or `addMenuButton`.

The method for creating custom context toolbars has been moved from `editor.addContextToolbar()` to `editor.ui.registry.addContextToolbar()`.

### Context Form

Context Forms are a generalisation of the `Insert Link` form that existed in the original `inlite` theme from [TinyMCE 4.x]((https://www.tiny.cloud/docs/themes/inlite/#quicklink)).

### Toolbar buttons

1. SVG icons for a better crisp look.
2. Buttons are now added via methods in `editor.ui.registry` rather than `editor` e.g. `editor.ui.registry.addButton()` instead of `editor.addButton()`
3. New methods were added for split, toggle and menu toolbar buttons with configuration options specific to the button type, to make the creation of custom toolbar buttons easier.

### Custom Menu Items

* editor.menuitems, [see configuration]({{site.baseurl}}/components/toolbarbuttons/components/menu/)

### Custom Sidebars

* editor.addSidebar, Docs coming soon.

### Toolbar Menus

* New buttons are added to the global `editor.settings.menus` which is an enhancement since, it now shows the toggled state.
* Improved mouse and keyboard navigation.

### Mobile Support
* TinyMCE 4.7 introduced mobile support, via a new theme and configuration settings
* TinyMCE 5.0 bundles mobile support out-of-the-box



