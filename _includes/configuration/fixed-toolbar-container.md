## fixed_toolbar_container

Use this option to render the toolbar into a fixed positioned HTML element. For example, you could fix the toolbar to the top of the browser viewport.

**Type:** `String`

This example takes the CSS ID selector `'#mytoolbar'` and renders any inline toolbars into this element.

##### Example

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your HTML
  inline: true,
  fixed_toolbar_container: '#mytoolbar'
});
```
