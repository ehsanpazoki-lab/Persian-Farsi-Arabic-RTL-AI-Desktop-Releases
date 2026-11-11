# Security

## What the companion does

- It talks to an app only through a local debugging port on `127.0.0.1` (ports 9229 to 9235, one per app). HTTP requests ignore proxies and redirects, and WebSocket addresses are accepted only for `ws://127.0.0.1` on the app's port, without credentials or fragments.
- Before each pass, the single listener on the port must be the expected app in the current Windows session: Store package identity for ChatGPT and Claude, exact exe path and publisher for Antigravity, Hermes, OpenCode and T3 Code, and the app's own WebView2 process for Cline. Otherwise nothing is sent.
- It never closes, kills or restarts an app. It starts an app with the debugging switch only when that app is not running.
- No app files, MSIX packages or `app.asar` are patched. No certificate is installed and no elevation is needed. App security controls are never bypassed.
- Claude: Developer Mode is switched on for the current user only. The previous values are saved first and restored by Disable RTL or by uninstalling. A damaged snapshot is kept for manual recovery, not deleted.
- Logs, if any, hold fixed event names and exception types, never chat text, prompts, tokens or CDP payloads.
- Problem reports are built locally, show everything before sending, mask user name, PC name, paths and links, and are sent only by the user.
- The only request to the internet is the update check at start: an HTTPS GET of GitHub's public releases list of this repository (can be turned off in *Updates → Check at Start*). Nothing is downloaded or run.
- An exe found outside the known install folders (Windows *Installed apps*, the running app, or *Set app location...*) is used only with the expected file name and publisher.
- Copied text and the clipboard are not read or changed.

## What to know

- A debugging port is not authenticated. While an app runs with it, other programs on the same PC can connect. Never forward or tunnel these ports.
- The port stays open after Disable RTL or after the companion exits, until the app itself is closed.
- The installers are not code-signed yet.

## Reporting a vulnerability

Please open a private security advisory in this repository (Security tab), or contact the maintainer on Telegram: https://t.me/EhsanGitlab
