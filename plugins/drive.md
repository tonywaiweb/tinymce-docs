---
layout: default
title: Drive
title_nav: Drive
description: Cloud-based file and image management for TinyMCE.
keywords: tinydrive storage media tiny drive
---




### Cloud-based File and Image Management for TinyMCE

Tiny Drive is a premium TinyMCE plugin for cloud-based asset management and storage solution. Tiny Drive is a solution for creating rich text by attaching and embedding images, videos, and other files in your document.

Drive presents a cloud-based asset management and storage solution that provides the ease of use of Google Drive without the server requirements of a self-hosted asset manager such as our own MoxieManager.

### Getting Started

#### Creating an Account

If you would like to try out Drive and our Cloud-delivered editor, the first step is to create a free [Tiny account](https://www.tiny.cloud/download/).  When you create an account, you are assigned an API key, which is required for the implementation of Drive.

> The API key is also provisioned with a free 30-day trial of all of our [premium plugins](https://apps.tiny.cloud/product-category/tiny-cloud-extensions/), with no credit card information or commitment required.

#### Configuring the Editor for Drive

Once you have the API key, or if you are a current Cloud user who already has an API key, then you have access to Drive.  In order to get the service up and running, you’ll need to complete a few more steps. See our [documentation]({{site.baseurl}}/plugins/drive) for more information.

> We are launching the service with a complimentary 100MB of storage and up to 1 GB of bandwidth.

### Security & Performance

We know security is a primary concern when it comes to cloud storage.  Drive uses an [Amazon Web Services S3](https://aws.amazon.com/s3/) bucket, the same storage solution used by companies like Netflix, Thomson Reuters, and Zillow.  (You can read about Amazon’s comprehensive security approach [here](https://aws.amazon.com/security/).)

As your assets are passed back and forth between your TinyMCE editor instance and the S3 bucket, Drive uses both your API key and a [JSON Web Token](https://jwt.io/introduction/) (JWT) to authenticate each data transaction.  Each Drive user will need to create their own JWT, and we walk you through the whole process [here]({{site.baseurl}}/configure/jwt-authentication/).

And to make sure your assets are delivered as fast as possible, we utilize the [CloudFront CDN](https://aws.amazon.com/cloudfront/), which is Amazon’s global content delivery network, known for its low latency and high data transfer speeds.

For more information on Drive see our full [documentation]({{site.baseurl}}/plugins/drive/).

We also have a demo for you to explore the Drive capabilities [here]({{site.baseurl}}/demo/drive/).




****

The Tiny Drive plugin adds the functionality to upload and manage files and images to the cloud. This plugin is only available in [Tiny Cloud](https://www.tiny.cloud/download/) and requires you to register for an API key.

To enable this functionality, add `tinydrive` to the list of plugins in the `tinymce.init` call. You also need to authenticate the user using a [JSON Web Token]({{site.baseurl}}/configure/jwt-authentication) (JWT).

Once you enable Drive it integrates as the default file picker for the Image, Link, and Media dialogs and as the default upload handler for local images being pasted or inserted into the document.


### Example

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your html
  plugins: 'tinydrive'
});
```

## Options

These settings are necessary to make Drive work:

### `tinydrive_token_provider`

This setting could take one of the following two forms:

* A URL to a page that takes an HTTP JSON POST request and produces a JSON structure with a valid JWT. It uses a POST request to avoid caching by browsers and proxies.
* A function that provides the same token through a callback. This allows you to make your own HTTP request in any format you like. The provider function is a function that has a success and failure callback where the success takes an object with a token property containing the JWT, and the failure callback takes a string to present as an error message if the token could not be produced.

You can read more about how to create these tokens in the [JWT authentication]({{site.baseurl}}/configure/jwt-authentication/) guide.

**Type:** `String` or `Function`

**Required:** yes

#### Example Using a JWT Provider URL

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your HTML
  plugins: 'tinydrive',
  tinydrive_token_provider: '/jwt'
});
```

#### Example Using a JWT Provider Callback

```js
tinymce.init({
  selector: "textarea",  // change this value according to your HTML
  plugins: "tinydrive",
  tinydrive_token_provider: function (success, failure) {
     success({ token: 'jwt-token' });
     // failure('Could not create a jwt token')
  }
});
```

### `tinydrive_upload_path`

This setting enables you to change the default upload path for files that get uploaded when pasted into the editor, uploaded directly through the Image dialog, or when you drag-and-drop images into the editor. It will produce a date-based structure within this path like this `/uploads/{year}{month}{day}`. This is to avoid having thousands of files in the same directory.

**Type:** `String`

**Default Value:** `"/uploads"`

#### Example

```js
tinymce.init({
  selector: "textarea",  // change this value according to your HTML
  plugins: "tinydrive",
  tinydrive_upload_path: '/some/other/path'
});
```

## Insert File toolbar button

Drive will automatically integrate into the Image, Link, and Media dialogs as a file picker. You can also configure it to insert files directly into your content using the `insertfile` button. To enable this button, add it to your toolbar editor setting.

The Insert File toolbar button will insert images as `img` elements or other files as links to that file.

### Example of toolbar button

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your HTML
  plugins: 'tinydrive',
  toolbar: 'insertfile'
});
```

## Insert File menu item

Drive will automatically integrate into the Image, Link, and Media dialogs as a file picker. You can also configure it to insert files directly into your content using the `insertfile` menu item. To enable this menu item, add it to your menus editor setting or the insert_button_items setting.

The Insert File menu item will insert images as `img` elements or other files as links to that file.

### Example of menu item

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your HTML
  plugins: 'tinydrive',
  toolbar: 'insert',
  menu: {
    insert: { title: 'Insert', items: 'insertfile' }
  },
  insert_button_items: 'insertfile'
});
```

## Restrictions and Quotas

Drive has restrictions on what files can be uploaded and how large these files can be:

* The maximum file size is 100MB
* Allowed image extensions: gif, jpeg, jpg, png, tif, tiff, bmp
* Allowed document extensions: doc, xls, ppt, pps, docx, xlsx, pptx, pdf, rtf, txt, keynote, pages, numbers
* Allowed audio extensions: wav, wave, mp3, ogg, ogv, oga, ogx, ogm, spx, opus
* Allowed video extensions: mp4, m4v, ogv, webm, mov
* Allowed archive extensions: zip
* The Copy operation is limited to single files due to technical reasons.

Your storage and bandwidth quota varies based upon the [Tiny Cloud Plan](https://www.tiny.cloud/pricing/) you are subscribed to.

## Upload Files URL

All files are uploaded to a central storage with a CDN endpoint that means that we are hosting your files and they are publicly available in read-only mode for anyone that has access to the URL of that file.
The URL format for each file is `https://drive.tiny.cloud/1/{your-api-key}/{uuid}` and gets generated when a file is uploaded.
If you move or rename a file, it will still have the same unique URL, so the restructuring of your files using Drive won't affect where they are being used. However, deleting a file will mark the URL as being unused, and the URL will not continue to work.

