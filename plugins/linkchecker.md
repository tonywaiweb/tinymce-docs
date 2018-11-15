---
layout: default
title: Link Checker Plugin
title_nav: Link Checker
description: Validate links, as you type.
keywords: url urls link linkchecker_service_url linkchecker_content_css
---

# Introduction (from Enterprise)



The [Link Checker plugin]({{ site.baseurl }}/plugins/linkchecker/) provides a link checking service right within the TinyMCE editor.

Think of Link Checker as "spell-checking for URLs". But instead of checking spelling, it will let you know if a URL in the editor is valid, invalid or questionable. This is a huge time-saver for anyone who creates content — no more having to double-check URLs, especially in imported content. Not to mention the benefit of no longer frustrating readers with broken hyperlinks.

Link Checker is available as a stand-alone plugin or as part of our Pro Bundle. To learn more about your options, check out our [pricing and plans here](https://www.tinymce.com/pricing/).

Your have two deployment options. One is super easy with TinyMCE Cloud, the other is to go the more traditional Self-hosted route, requiring an additional [server-side component]({{ site.baseurl }}/enterprise/server/) to be installed and configured.

## Link Checker Cloud Quick Setup

[TinyMCE Cloud]({{ site.baseurl }}/cloud-deployment-guide/editor-and-features/) makes setting up Link Checker a breeze. Simply include the `linkchecker` parameter in your `tinymce.init` and have our Cloud services do the work for you.

## Link Checker Self-hosted Quick Setup

If you'd rather deploy Link Checker via the Self-hosted package, you have a little more work to do. Once you've got the [server-side component]({{ site.baseurl }}/enterprise/server/) installed, additional configuration to your `application.conf` file is required. (Don't forget to restart the Java application server after updating the configuration.)

This element configures the Link Checker service's built-in cache. When a hyperlink is checked and confirmed valid, the result is cached to save unnecessary network traffic in the future.

Default settings are automatically configured, meaning these settings are optional.

- `capacity` - sets the capacity of the cache. The default setting is 500.
- `timeToLiveInSeconds` - sets the time-to-live of elements of the cache, measured in seconds. This is the maximum total amount of time that an element is allowed to remain in the cache. The default setting is 86400 seconds, which is one day.
- `timeToIdleInSeconds` - sets the time-to-idle of elements of the cache, measured in seconds. This is the maximum amount of time that an element will remain in the cache if it is not being accessed. The default setting is 3600 seconds, which is one hour.

Example:

```
ephox {
  link-checking.cache {
    capacity = 500
    timeToLiveInSeconds = 86400
    timeToIdleInSeconds = 3600
  }
}
```

You will also find more Self-hosted setup information on the [Link Checker plugin page]({{ site.baseurl }}/plugins/linkchecker/).

> **Important note:** The Link Checker server currently does not support integration with IBM WebSphere Application Server.



# Introduction (from docs)

The `linkchecker` does what it says &ndash; validates URLs, as you type them. URLs considered invalid will be highlighted with red and will have a dedicated context menu with options to either edit the link, try and open it in a separate tab, remove the link, or ignore it.

> Please note that Link Checker is a **premium** plugin and relies on a server-side service, which is included as a part of a [premium TinyMCE plugin](https://www.tinymce.com/pricing/) subscription.


## Cloud Instructions

If you are using [TinyMCE Cloud]({{ site.baseurl }}/cloud-deployment-guide/editor-and-features/), simply add `"linkchecker"` to your plugins list, and the service will be automatically configured.

##### Example

```js
tinymce.init({
  selector: "textarea",  // change this value according to your HTML
  plugins: "linkchecker"
});
```

## Self-hosted Instructions

Customers using a Self-hosted environment will need to provide a URL to their deployment of the link checking service via the `linkchecker_service_url` parameter

##### Example

```js
tinymce.init({
  selector: "textarea",  // change this value according to your HTML
  plugins: "linkchecker",
  linkchecker_service_url: "http://mydomain.com/linkchecker"
});
```

## Options

Link Checker has the following settings.

### `linkchecker_content_css`

After a link is checked for validity, a result of the validation is added to it via `data-mce-linkchecker-status` attribute. There are three possible outcomes of the validation: `valid`, `invalid` and `unknown`. Link Checker visually reflects `invalid` outcome by injecting the following CSS styles into the editor:

```css
a[data-mce-linkchecker-status="invalid"] {
    outline-color: rgba(231, 76, 60, 0.25);
    background-color: rgba(231, 76, 60, 0.25)
}

a[data-mce-linkchecker-focus="true"] {
    outline: 1px solid rgba(231, 76, 60, 0.75)
}
```

`data-mce-linkchecker-focus` attribute is set to *true* every time a dedicated context menu is shown on a link. This only happens for `invalid` links.

It is possible to replace or extend those styles, by providing a URL to custom stylesheet via `linkchecker_content_css` option.


### `linkchecker_service_url`

A URL of the server-side link validation service. This is required option, without it plugin will fail to operate and will throw a corresponding warning on the screen.

**Type:** `String`

##### Example

```js
tinymce.init({
    selector: "textarea",
    plugins: "linkchecker",
    linkchecker_service_url: "http://mydomain.com/linkchecker"
});
```
