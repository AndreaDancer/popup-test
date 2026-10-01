# Popup Test: Squarespace setup

Two snippets, one per page:
- `launcher-codeblock.html` goes on the page that opens popups
- `popup-codeblock.html` goes on the page that loads inside the popup

## Setup
1. JavaScript in Code Blocks needs a Squarespace plan that allows custom code (Core/Business or higher). On lower plans the block shows up but the buttons won't do anything.
2. Create two pages under **Not Linked**, so they stay out of navigation:
   - **Popup Test**: any slug (e.g. `/popup-test`)
   - **Popup Test Window**: slug **`/popup-test-window`** (the launcher opens this by default)
3. On each page, add a **Code Block**, set it to **HTML**, paste the full contents of the matching file, and turn **Display Source** off. Save and publish.
4. Test on the **live site** (log out or use a private window), not in the editor. The editor shows pages inside an iframe, which changes how `window.open` behaves.
5. Optional: add a page password to keep the pages private.

## Using it
- Pick a preset, or set the size, position, and features and click **Open popup**. The exact `window.open(...)` call is shown under the buttons.
- To test your new feature's page instead, change the **URL** field. Messaging only works when that page has the popup snippet on it and is on the same domain.
- The popup shows its actual size so you can compare it with what you asked for. It also shows whether `window.opener` and `document.referrer` came through.
- Both sides can send messages. Each window keeps its own log.
- **Popup blocking** buttons open the popup 0.5, 2, or 5 seconds after your click, or after a network request finishes. The log says BLOCKED or OPENED for each. To test a popup with no click at all, check "Try to open a popup on page load" and reload the page. Uncheck it when you're done.

## Local test before uploading
```
cd ~/Desktop/popup-test && python3 -m http.server 8000
```
Open http://localhost:8000/launcher-codeblock.html. The URL field switches to `popup-codeblock.html` automatically when you run it locally.

## Hosting on GitHub Pages (github.com)
1. On github.com, create a new **public** repository (e.g. `popup-test`). Free accounts need the repository to be public for Pages.
2. Click **uploading an existing file**, drag in `index.html`, `launcher-codeblock.html`, `popup-codeblock.html`, and `README.md`, then **Commit changes**.
3. Go to **Settings → Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, Branch to **main**, folder **/ (root)**, then **Save**.
4. After a minute or two the site is live at `https://<your-username>.github.io/popup-test/`. That address opens the launcher, and the launcher opens `popup-codeblock.html` from the same folder.
