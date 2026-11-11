# AI Desktop RTL Companion

<!-- Public releases repository: installers, user guide and problem reports.
     The source code is kept in a private repository. -->

**Persian / Farsi and Arabic RTL for desktop AI apps on Windows:
ChatGPT, Claude, Antigravity, Hermes, OpenCode, Cline and T3 Code.**

A Windows tray app that makes Persian (Farsi) and other right-to-left text read
correctly in desktop AI chat apps: paragraphs and lists get the right
direction, and English words, units (`4 mm²`, `12.5 bar`) and code such as
`List<T*>` keep their order inside Persian sentences.

راهنمای فارسی: [README.fa.md](README.fa.md)

If this tool helps you, please give this repository a ⭐ Star (top right of this page) so other Persian and Arabic speakers can find it.

> **Status: pre-release (v0.3.0-alpha18).** Every app below was tested in
> real use, but only on one Windows PC. Please report anything that does not
> work (tray menu → *app* → **Report a problem...**).

## Supported apps

| App | Install type that was tested | Last tested version | Notes |
|---|---|---|---|
| ChatGPT | Microsoft Store | 26.1106.51428 | |
| Claude | Microsoft Store | 5.1231.2 | Needs one click in Claude per session (below) |
| Antigravity | Per-user installer | 2.29.0 | |
| Hermes | Built from source | 0.23.0 | **Experimental**: the official installer's path is not yet verified |
| OpenCode Desktop | Per-user installer | 2.2.6 | |
| Cline Desktop | Per-user installer | 0.0.49 | Needs Windows UAC on (below) |
| T3 Code | Per-user installer | 0.1.9 | **Experimental**; see the security note below |

Besides the tested
install folders, the companion also looks in *Program Files*, in the app's
entry in Windows *Installed apps* and at the running app. If an app is still
"not found", choose *app → Set app location...* in the tray menu and pick its
exe (the publisher is checked). Gemini Desktop is not supported: it refuses to start with a
debugging port, and the companion does not work around that.

## Download and install

From the [Releases](https://github.com/ehsanpazoki-lab/Persian-Farsi-Arabic-RTL-AI-Desktop-Releases/releases) page, download **one** of:

- `AI-Desktop-RTL-Companion-Setup-v<version>.exe`: all apps. Setup looks for
  the supported apps on your PC, marks each one "found" or "not found" and
  ticks the found ones; change the ticks if you like. Only the ticked apps
  appear in the tray menu.
- `AI-Desktop-RTL-Companion-<App>-Setup-v<version>.exe`: a single app. Running
  another single-app installer later adds that app to the same installation.

Setup installs for the current user only (no administrator rights) into
`%LOCALAPPDATA%\Programs\AI Desktop RTL Companion`. The program is
self-contained: it carries its own .NET 8 runtime, so .NET does not need to be
installed (that runtime is most of its size on disk). A new version first
removes the previous one; your settings and app choices are kept. Run the full
installer again to change the app selection, or uninstall from
*Settings → Apps*.

**Updates:** when it starts, the companion asks GitHub's public releases list
whether a newer version exists and, if so, shows it at the top of the tray
menu. Nothing is downloaded or installed automatically, and nothing about you
or your PC is sent beyond that one HTTPS request. Turn it off in
*Updates → Check at Start*.

The installers are not code-signed yet, so Windows SmartScreen may show
"Windows protected your PC" (choose *More info → Run anyway*). Compare the
file with `SHA256SUMS.txt` from the same release if you want to check it.

## Requirements

- Windows 10 (1809 or later) or Windows 11, 64-bit. Windows on ARM is untested.
- Run the companion as a **normal user**, not "as administrator".
- **Cline only:** Windows UAC must be on. With UAC off every app runs elevated
  and WebView2 ignores the debugging switch. Any UAC level, including
  "Never notify", works.
- **T3 Code:** its agents can run commands on your PC. While T3 Code is open
  with the debugging port, other software on this PC could reach it through
  that port. Use RTL in T3 Code only on a PC you trust, and quit T3 Code when
  you no longer need it.
- **Claude only:** after Claude starts, choose *Developer → Enable Main
  Process Debugger* in Claude once per session. The companion turns on
  Claude's Developer Mode for this and restores your own setting on
  *Disable RTL* (and on uninstall).

## How it works and what to know

1. Choose *Enable RTL* for an app in the tray menu. If the app is not running,
   the companion starts it with a local debugging port
   (`127.0.0.1`, ports 9229–9235) and attaches the RTL runtime. If the app is
   already open without that port, the companion asks you to quit it yourself:
   **it never closes your apps**, so unsent text is never lost.
2. *Disable RTL* removes everything the companion added and checks each window.
3. Before anything is sent, the companion checks that the program listening on
   the port is the expected app in your own Windows session (Store package
   identity for ChatGPT and Claude, exe path and publisher for the others).

Security note: while an app runs with a debugging port, other software on the
same PC can also connect to that port. The port is bound to 127.0.0.1 only and
closes when you quit the app. Do not forward these ports or expose them
through a proxy or tunnel.

### Copying

Copied text is not changed: copy and the app's own Copy buttons give what the
app gives. Word does not always keep the order of mixed Persian/English text
from a plain copy; better support for Word is planned as a separate tool.

Known limits: inside message boxes (composers) only the direction of each line
is set, by CSS only; mixed words inside one draft line keep plain Unicode order
(for example `mm² 4`). An app update can change its layout and stop RTL from
applying; the tray then shows the version as "newer than tested". Please
report it.

## Report a problem

Tray menu → *app* → **Report a problem...** (also offered when Enable fails).
The report shows Windows, companion and app versions and the companion's own
status lines; it never includes chat text, and your user name, PC name, paths
and links are masked. You see the full text and send it yourself, to Telegram
or as a GitHub issue. Nothing is sent automatically. The in-app *Help* has the same guide in English and Persian (section "فارسی").

## Trademarks

This is an independent project. It is not affiliated with, endorsed by or
sponsored by OpenAI, Anthropic, Google, Nous Research, the OpenCode project,
Cline or T3 Tools. ChatGPT, Claude, Antigravity, Gemini, Hermes, OpenCode, Cline and T3 Code are
trademarks or names of their respective owners and are used here only to say
which apps this tool works with.

## Privacy and security

See [SECURITY.md](SECURITY.md). Third-party components:
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). This repository holds the
installers and the user guide; the source code is not published.
