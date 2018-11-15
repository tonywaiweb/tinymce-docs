---
layout: default
title: Advanced Code Editor
title_nav: Advanced Code Editor
description: How to setup TinyMCE's Advanced Code Editor plugin.
keywords: code advcode codemirror
controls: toolbar button, menu item
---

## Introduction (from Enterprise)

The [Advanced Code Editor]({{ site.baseurl }}/plugins/advcode/) plugin (`advcode`) brings a more advanced code editor to TinyMCE. This code editor makes it easier to modify the HTML, and it's a very useful add-on for power users. It comes with many features often found in IDEs, all enabled by default:

* Syntax color highlighting
* Bracket matching
* Code folding
* Multiple selections/carets

### How to get the Advanced Code Editor plugin

The Advanced Code feature is a [premium feature](https://www.tinymce.com/pricing/) available from as little as $4 per month.


## Introduction (from docs)

This plugin adds a toolbar button that allows a user to edit the HTML code using a more advanced [code editor]({{ site.baseurl }}/enterprise/advcode/) than the default textarea.

If you are using Advanced Code Editor `advcode` plugin, make sure you do not use Code `code` plugin.

##### Example

```js
tinymce.init({
  selector: "textarea",  // change this value according to your HTML
  plugins: "advcode",
  toolbar: "code"
});
```

> The Advanced Code Editor plugin is included with a [TinyMCE Enterprise](https://www.tinymce.com/pricing/) subscription. Please [click here](https://www.tinymce.com/pricing/) to learn more about our flexible subscriptions plans.
