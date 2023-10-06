# Firefox

## Download media from GET requests

To download media when no downloader is present on the website:

1. Open the Developer Tools (`Ctrl+Shift+I`).
2. Switch to the 'Network' tab.
3. Play the media.
4. Monitor the network log for GET requests.
5. Right-click the log entry and open the stream in a new tab.
6. Save (`Ctrl+s`) to disk.

## Disable "Private browsing" text label in tab bar

In the `about:config` menu, disable:

```
browser.privatebrowsing.enable-new-indicator
```

## Disable DNS over HTTPS

Firefox can proxy DNS requests to CloudFlare. This behavior is not the default
but may be activated by some Add-ons. The rationale for the feature is to block
man-in-the-middle attacks that redirect normal traffic and the DNS resolution
step. However, this will cause DNS leaks, should one want to proxy network
connections (including name resolution) through a specific server.

Disable this setting by:

1. De-selecting 'Enable DNS over HTTPS' in the Connection Settings submenu in
   `about:preferences`, or
2. Setting `network.dns.disablePrefetch` to `true` in `about:config`.

## Re-enable scrolling on websites where scrolling is disabled

In the web console, enable pasting by typing (`allow pasting`) and then enter:

```js
var r = "html,body{overflow:auto !important;}";
var s = document.createElement("style");
s.type = "text/css";
s.appendChild(document.createTextNode(r));
document.body.appendChild(s);
void 0;
```

## Delete element in website

1. Hover over the element and right-click.
2. Select 'Inspect (Q)' from the context menu.
3. In the 'Search HTML' pane of the Inspector menu, hover over the HTML node
   that contains the element to be deleted and right-click.
4. Select 'Delete Node' in the context menu.

Combine this information with the above instructions for force-enabling
scrolling to bypass login or other un-closable pop-ups that freeze websites.

## Fonts are rendered poorly in PDF viewer

Disallow pages from choosing their own fonts. Either do this through the font
menu in `about:preferences` or by setting `browser.display.use_document_fonts=0`
in `about:config`.
