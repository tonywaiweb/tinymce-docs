---
layout: default
title: Quick Start
description_short: Setup TinyMCE in less than 5 minutes.
description: Get an instance of TinyMCE up and running in less than 5 minutes.
keywords: tinymce script textarea
---

TinyMCE is a powerful and flexible WYSIWYG HTML editor that you can embed in your web application for editing rich text. 

The Developer Preview is perfect for developers who want to see how version 5.0 integrates into their application prior to its full release.


## Step 1: Include the TinyMCE script

Include this line of code in the `<head>` of your HTML page and link to `tinymce.min.js`:

```html
<script src='https://devpreview.tiny.cloud/demo/tinymce.min.js'></script>
```

Alternatively, download and unzip the [Developer Preview zip](https://devpreview.tiny.cloud/download/tinymce.zip) or build your own from the TinyMCE [Github repository](https://github.com/tinymce/tinymce/tree/5.x).


## Step 2: Initialize TinyMCE as part of a web form

With the script included, initialize TinyMCE on any element (or elements) in your web page.

Identify the elements for TinyMCE to replace via a `selector` value in the JSON configuration passed to `tinymce.init()`.

As an example, replace `<textarea id='mytextarea'>` with a TinyMCE editor instance by passing the selector `'#mytextarea'` to `tinymce.init()`.

```html
<!DOCTYPE html>
<html>
<head>
  <script src='https://devpreview.tiny.cloud/demo/tinymce.min.js'></script>
  <script>
  tinymce.init({
    selector: '#mytextarea'
  });
  </script>
</head>

<body>
<h1>TinyMCE Quick Start Guide</h1>
  <form method="post">
    <textarea id="mytextarea">Hello, World!</textarea>
  </form>
</body>
</html>
```


## Step 3: Saving content with a form POST

When the `<form>` is submitted the TinyMCE editor mimics the behavior of a normal HTML `<textarea>` during the form `POST` action. In your form handler, you can process the content submitted as if it had come from a regular `<textarea>`.

That is all there is to it!

If you prefer to download TinyMCE and install it locally the [Advanced Install]({{  site.baseurl }}/general-configuration-guide/advanced-install/#packagemanagerinstalloptions) page in the [General Configuration Guide]({{  site.baseurl }}/general-configuration-guide) has instructions. This document also provides information about TinyMCE features such as advanced installation options, working with plugins, learning about content filtering, and spell checking.
