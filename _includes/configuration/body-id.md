## body_id

This option enables you to specify a CSS ID selector for the body of each editor instance. This ID can then be used to do TinyMCE specific overrides in your `content_css`.

**Type:** `String`

##### Example

This will add the same ID to all editors that gets created by the `init` call.

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your HTML
  body_id: 'my_id'
});
```

This will set specific IDs on the bodies of specific editors.

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your HTML
  body_id: 'elm1=my_id, elm2=my_id2'
});
```
