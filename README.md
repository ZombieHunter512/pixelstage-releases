# Pixel Stage — downloads

**[Get the latest build →](../../releases)**

This repo holds the built app and nothing else. No source lives here.

| Your machine | File |
|---|---|
| Windows | `Pixel-Stage-x.x.x.exe` — no install, just double-click |
| Mac (M1–M4) | `Pixel-Stage-x.x.x-mac-arm64.dmg` |
| Mac (older Intel) | `Pixel-Stage-x.x.x-mac-x64.dmg` |
| Linux | `Pixel-Stage-x.x.x-linux.AppImage` |
| Any machine, no install | `Pixel-Stage-x.x.x-portable.html` — one file, opens in Chrome |
| Raspberry Pi and friends | `Pixel-Stage-x.x.x-lite-portable.html` — same app on the CSS renderer |

**Pixel Stage** is LED-wall previz: build a venue's walls in 3D, feed them live from
Resolume, and watch the show run on the panels the way a real LED processor would drive
them.

## Why downloads have a repo of their own

The app updates itself, and the updater is a plain anonymous HTTPS request with no login
attached. A GitHub release inherits the visibility of the repo it sits in, so releases
kept beside private source would be unreachable to the very thing that needs to download
them. Hence this repo: public, binaries only.

`update-pointer.json` is the other half. Every installed copy reads it before checking for
updates and follows the repo it names, so the project can move house without stranding
copies already out in the world. It is mastered in the source repo and pushed here by CI —
edit it there, not here, or the next release will overwrite your change.
