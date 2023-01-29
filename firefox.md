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

Firefox by default will proxy DNS requests to CloudFlare. The idea is to block
man-in-the-middle attacks that redirect normal traffic and the DNS resolution
step. However, this will cause DNS leaks, should network connections need to
proxied through a specific server.

Disable this setting by:
1. De-selecting 'Enable DNS over HTTPS' in the Connection Settings submenu in
   `about:preferences`, or
2. Setting `network.dns.disablePrefetch` to `true` in `about:config`.
