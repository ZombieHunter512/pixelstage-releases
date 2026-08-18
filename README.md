# Pixel Stage

**An LED wall, a lighting rig and a stage — on your desk, at real size.**

[**Download the latest build →**](https://github.com/ZombieHunter512/pixelstage-releases/releases/latest)

Build the venue in 3D, map every panel the way a real processor does, feed it live from
Resolume, and run the show. Nothing here is a mock-up: a 12″ box truss is 305 mm, a 128 px
panel at P3.9 is 500 mm across, and the pixel map you export is the one you would hand a
screens tech.

One HTML file, or an app for Windows, macOS and Linux. MIT licensed.

> **This repo holds the built app and nothing else. No source lives here.**
> See [Why downloads have a repo of their own](#why-downloads-have-a-repo-of-their-own).

---

## What it is

A rehearsal room for people who work with LED and light: VJs, screens techs, lighting
designers, production managers, and anyone who has to explain a rig to somebody before it
is built.

- **Build the rig.** Walls, wings, circles, strips, cylinders, discs and spheres of real LED
  panels. Truss in the lengths people actually hire. Moving heads, lekos, PARs, washes,
  blinders, strobes, vipers, lasers, CO₂, pyro and cold sparks. Stage decks, PA, backline,
  people, and a shapes library for everything else.
- **Map it.** Each wall gets a rectangle on the video signal — the same processor mapping a
  real wall tech does, with overlap and off-signal warnings as you drag.
- **Send it to Resolume.** One button writes a complete Advanced Output preset — slices,
  input and output rectangles, warper grids and all — built from your Resolume's own
  settings so there is no version to get wrong. A map PNG and a CSV come with it.
- **Run the show.** Capture Resolume's output and it plays on the virtual panels. A
  front-of-house desk across the bottom of the 3D view runs beams, looks, strobes, lasers,
  blasts, the kinetic wall and the rigging motors, and it only ever shows you buttons for
  things that are actually on stage.
- **Drive it from real gear.** Art-Net and sACN in, so a grandMA — or any console — runs the
  lights here. A MIDI controller can take the desk. Import a manufacturer's `.gdtf` fixture,
  or a `.obj` model.

## What it is not

None of these are modelled, and the app says so on first run:

- **Rigging and structure.** No weight, no span limit, no bridle angle, no safety factor. A
  truss run that looks fine here may be nowhere near fine in the air.
- **Pyro, CO₂ and lasers.** Purely visual. No fallout zones, no safe distances, no laser MPE.
- **Photometrics.** Beam angles are plausible, not measured.

The sizes are real. The physics and the safety are not. Map with it, plan looks with it, and
let the people whose job it is sign off the rigging and the effects.

---

## Install

Newest build: **[Releases](https://github.com/ZombieHunter512/pixelstage-releases/releases/latest)**.

| Your machine | File |
|---|---|
| Windows | `Pixel-Stage-x.x.x.exe` — no install, just double-click |
| Mac (M1–M4) | `Pixel-Stage-x.x.x-mac-arm64.dmg` |
| Mac (older Intel) | `Pixel-Stage-x.x.x-mac-x64.dmg` |
| Linux | `Pixel-Stage-x.x.x-linux.AppImage` |
| Anywhere, no install | `Pixel-Stage-x.x.x-portable.html` — the whole app as one document |
| Raspberry Pi and friends | `Pixel-Stage-x.x.x-lite-portable.html` — same app on the CSS renderer |

Stuck? **[HELPME.md](HELPME.md)** walks through every install and first-run problem in plain
language.

### First run

The app has no Apple or Microsoft certificate behind it, so both systems stop it once.
Normal for independent apps, and only the first time.

- **Windows** — a blue "protected your PC" screen. **More info → Run anyway**.
- **Mac** — drag it to Applications, then **System Settings → Privacy & Security**, scroll to
  the bottom, and click **Open Anyway** beside Pixel Stage. Right-click → Open used to work
  and no longer does on recent macOS; the Settings route is the one that does.

**Mac says "Pixel Stage is damaged and can't be opened"?** It is not damaged, and do not move
it to the Trash. That exact wording means the copy you have carries no code signature at all,
which an Apple Silicon Mac refuses outright. Builds from 0.36.1 on are ad-hoc signed and do
not do this — download the current release. To rescue a copy you already have, one line in
Terminal clears it:

```sh
xattr -cr "/Applications/Pixel Stage.app" && codesign --force --deep --sign - "/Applications/Pixel Stage.app"
```

The first half removes the download quarantine flag, the second gives the app the signature
the build should have shipped with. Then open it normally.

---

## The single file

Every release also carries the whole app as one document — `Pixel-Stage-x.x.x-portable.html`.
No install, no Electron, nothing to unpack. Double-click it, or email it to somebody.

### What the installed app gives you that the single file cannot

The HTML file is the whole program — every wall, every fixture, the 3D room, the slice map,
the Resolume preset. What it cannot do is the handful of things that need a real operating
system underneath, because a browser tab is not allowed to:

| Only in the installed app | Why |
|---|---|
| Art-Net and sACN in | Listening on UDP 6454 / 5568 needs a socket. A browser has none, so a lighting desk cannot drive the previz from the HTML file. |
| Writing the preset into Resolume's folder | The app writes `Pixel-Stage.xml` straight into Documents › Resolume Arena › Presets › Advanced Output. Chrome can, once you grant the folder; every other browser downloads it and you move it by hand. |
| Reading your `AdvancedOutput.xml` | The app finds Resolume's own settings and moulds the preset on them, which is the version-proof path. In a browser you pick the file yourself. |
| The capture picker with thumbnails | Choosing which screen or window by looking at it, and the macOS screen-recording permission flow that goes with it. |
| Auto-update | The app checks for a release, downloads it, and shows you where it went. A downloaded HTML file is updated by downloading it again. |

Everything else — building the rig, mapping it, exporting the XML, the CSV and the map PNG —
is identical in both. Build in the browser if that suits you; the app is for the day you plug
it into a real rig.

---

## Quick start

1. **Build** — add Walls, Wings, Circles and Strips from the left shelf. Arrange them on the
   Stage and 3D tabs.
2. **Map** — on the Slice tab, place each wall's rectangle on the video signal. That is the
   same processor mapping a real wall tech does.
3. **Send to Resolume** — Signal → Send to Resolume → Build preset from scratch.
4. **Go live** — fullscreen Resolume's output on a display, click **Capture output…** here,
   pick that display. Your show is now running on the virtual wall.

There is a **Help drawer** in the app with tutorials for each of these, and a Quick start that
walks the whole thing in two minutes.

### Nothing here can damage your Resolume setup

This matters if you are handing the app to somebody, or trying it on a show machine.

- **Your own setup is never written to.** Pixel Stage only ever adds one preset file,
  `Pixel-Stage.xml`. You choose whether to load it, from Resolume's own top-left dropdown →
  **Load…**. (Not the Presets list under it: Resolume only rescans that folder when it starts,
  so a file added to a running Resolume appears in Load… immediately but in the list only
  after a restart.)
- **Undo is one click, and it stays available.** Signal → Remove Pixel Stage from Resolume
  deletes the one file it wrote and nothing else. Pick your own preset again first and you are
  exactly where you started.
- **It fits whatever Resolume you run.** The preset is built from your own
  `AdvancedOutput.xml`, so it inherits your build's version and keeps whatever that build puts
  inside a slice.

---

## Good to know

- **Save your stages.** File → Save writes a small `.json`. Ctrl+S, Ctrl+Z, the usual. A venue
  library is a folder of them.
- **Panels are real sizes.** A panel is its pixel count times its pitch — the mm between LEDs.
  The picker is named for the tile you would actually hire (500×1000 P3.9), not for a pixel
  count, so the wall in 3D is the size the wall will really be.
- **Mixed-panel walls.** A row of half panels over fulls: select both, Edit → Group as one
  screen, and they export as a single slice.
- **A prop is one object.** Drag, turn and colour it as one. To get at a single part — one leg
  of a truss, a laser's yoke — unlock its parts first, from the prop's row in the Collection.
- **Kinetic walls.** A wall's tiles can ride in and out on their own actuators, in a wave, a
  ripple, a diagonal or at random — a look on the show desk, with travel, speed and spread.
  The video does not move with the tile, which is how the real thing behaves and why the
  mapping never changes.
- **Rigging motors and hinges, for anything.** A truss, a prop or a wall can hang on a motor
  and be flown from FOH → Rigging: hold Up or Down and the chain runs at a real speed, with a
  real ramp, and stops where you let go. **Home** puts everything back to the trim it was last
  left at. Anything on a hinge swings instead — an LED door, a turning panel — on its own clock.
- **A show desk that says what it will reach.** FOH is one strip across the bottom of the 3D
  view: LED, Lights, Lasers, Blast and Rigging. Every button carries the number of fixtures it
  would actually drive, and a family with nothing on stage does not get a page at all.
- **The Processor drawer.** On the LED page: the composition size, what your map actually
  needs, and one button to make the first equal the second.
- **Drive it from a real desk.** Signal → DMX in listens for Art-Net and sACN (desktop app
  only — a browser cannot open a UDP socket). A small MIDI controller can take the show desk
  instead: Settings → Keys, press Learn, touch the pad.
- **Only what really moves, moves.** A movement effect reaches fixtures with motors in them. A
  leko can be pointed by hand and a PAR is a can on a hook, so neither follows a Sweep.
- **Slice transforms.** A wall can read a different piece of the composition than it occupies
  on the output — the whole comp stretched across it, fitted with bars, cropped to fill,
  mirrored or flipped — written into both rectangles and the warper grid on export.
- **Import.** One File → Import takes a show, a prop pack, a `.gdtf` fixture, a Resolume
  preset, a `.obj` model or a test image, and works out which from the file. Or drop it on the
  window.
- **Updates.** Checked on launch, or Help → Check for updates. Windows and Linux replace the
  app in place and restart; macOS downloads a fresh `.dmg`.

---

## The two-copy rule

> **Every release exists in BOTH repos. No exceptions, in either direction.**
>
> Anything published here has its master in the private source repo, and any version cut
> there must be mirrored here. A release that exists in only one of them is a fault to be
> fixed, not a state to leave.

The two copies do different jobs, which is why neither is optional:

| | Source repo (private) | **This repo** (public) |
|---|---|---|
| Role | **Master** — the tag sits on the commit it was built from | **Mirror** — the copy users download |
| Read by the updater | **Never** — the app carries no credentials | **Always** |
| If it is missing | No archive and nothing to re-mirror from | **Nobody can update. This is an outage.** |

CI does both on every release, master first, and fails the run if either copy comes up short
of its files. The trap worth naming: the master succeeding makes the run *look* fine, while a
missing mirror throws no error anywhere — it just means every copy in the world quietly stops
finding updates.

Releases from before the split (**v0.2.0 – v0.38.1**) were published in the source repo and
have been copied here, so this repo holds the full history rather than only what came after.
Their tags do not correspond to commits in this repo; the attached files are the originals.

If you are publishing by hand for any reason, you are not finished until both repos have it.

## Why downloads have a repo of their own

The app updates itself, and the updater is a plain anonymous HTTPS request with no login
attached. A GitHub release inherits the visibility of the repo it sits in, so releases kept
beside private source would be unreachable to the very thing that needs to download them.
Hence this repo: **public, binaries only.**

`update-pointer.json` is the other half. Every installed copy reads it before checking for
updates and follows the repo it names, so the project can move house without stranding copies
already out in the world. It is mastered in the source repo and pushed here by CI — **edit it
there, not here**, or the next release will overwrite your change.

**This repository must stay public, permanently.** If it is ever made private, every installed
copy of Pixel Stage in the world loses its update channel and its download links at the same
moment, and it cannot be undone from the app's side. See **[GOTCHAS.md](GOTCHAS.md)** before
changing anything about this repo's visibility.

---

## Licence

MIT. Do what you like with it; there is no warranty, and the **What it is not** section above
is not a formality.
