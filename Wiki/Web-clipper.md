# Web-clipper
![](Web-clipper_chrome-trilium-web.png)

Trilium Web Clipper is a web browser extension which allows user to clip text, screenshots, whole pages and short notes and save them directly to Trilium Notes.

Project is hosted [here](https://github.com/zadam/trilium-web-clipper). Firefox and Chrome are supported browsers, but the chrome build should work on other chromium based browsers as well.

Functionality
-------------

*   select text and clip it with context menu (right click)
*   click on an image or link and save it through context menu
*   save whole page from the popup or context menu
*   save screenshot (with crop tool) from either popup or context menu
*   create short text note from popup

Trilium will save these clippings as a new child note under a "clipper inbox" note. Clipper inbox is:

*   if there's a note with [label](Attributes.md) `clipperInbox`, then this note is used as parent for the clipped notes
*   otherwise, [day note](Day-notes.md) is used as a parent

If there's multiple clippings from the same page (and on the same day), then they will be added to the same note.

Get it
------

Extension is available from:

*   [Project release page](https://github.com/zadam/trilium-web-clipper/releases) - .xpi for Firefox and .zip for Chromium based browsers.
*   [Chrome Web Store](https://chrome.google.com/webstore/detail/trilium-web-clipper/dfhgmnfclbebfobmblelddiejjcijbjm?hl=en&authuser=0)

Configuration
-------------

The extension needs to connect to a running Trilium instance. By default, it scans a port range on the local computer to find a desktop Trilium instance.

It's also possible to configure [server](Server-installation.md) address for cases when the desktop application is not currently running.

Username
--------

Older versions of Trilium (before 0.50) required username & password to authenticate, but this was reduced to just password. Web Clipper UI still contains the username field, just use arbitrary string.