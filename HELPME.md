# Help — Pixel Stage won't install, won't open, or won't update

Plain answers to the things that actually go wrong. Work down the list; the first few cover
almost everything.

**[Download the latest build →](https://github.com/ZombieHunter512/pixelstage-releases/releases/latest)**

---

## Which file do I download?

| Your machine | Download this |
|---|---|
| Windows PC | `Pixel-Stage-x.x.x.exe` |
| Mac bought 2021 or later (M1/M2/M3/M4) | `Pixel-Stage-x.x.x-mac-arm64.dmg` |
| Older Intel Mac | `Pixel-Stage-x.x.x-mac-x64.dmg` |
| Linux | `Pixel-Stage-x.x.x-linux.AppImage` |
| Anything at all, no install, borrowed machine | `Pixel-Stage-x.x.x-portable.html` |
| Raspberry Pi or an old/slow machine | `Pixel-Stage-x.x.x-lite-portable.html` |

**Not sure which Mac you have?** Apple menu → About This Mac. If the Chip line says "Apple
M-something", take `mac-arm64`. If it says Intel, take `mac-x64`.

**Just want to look at it right now?** Take the `portable.html` file. It is the entire program
in one document — double-click it and it opens in your browser. Nothing to install, nothing
to uninstall.

---

## Windows: blue "Windows protected your PC" box

Expected. It happens once.

1. Click **More info** (small link, easy to miss — it is above the OK button).
2. Click **Run anyway**.

This appears because the app has no Microsoft code-signing certificate behind it, which costs
several hundred pounds a year. It is not a virus warning; Windows shows this for every
independent app that has not paid for one.

---

## Mac: "Pixel Stage can't be opened because Apple cannot check it"

Expected. It happens once.

1. Drag Pixel Stage to your **Applications** folder first.
2. Open **System Settings → Privacy & Security**.
3. Scroll right to the bottom.
4. Click **Open Anyway** beside the Pixel Stage message.
5. Confirm.

**Right-click → Open no longer works** on recent macOS versions, even though older guides
still say to do it. Use the Settings route above.

---

## Mac: "Pixel Stage is damaged and can't be opened. You should move it to the Trash."

**It is not damaged. Do not move it to the Trash.**

That exact wording means your copy carries no code signature at all, which an Apple Silicon
Mac refuses outright. Builds from **0.36.1** onwards are signed and do not do this.

**Easiest fix:** download the current release. It will just open.

**If you need to rescue the copy you already have,** open Terminal (Applications → Utilities →
Terminal) and paste this one line, then press Return:

```sh
xattr -cr "/Applications/Pixel Stage.app" && codesign --force --deep --sign - "/Applications/Pixel Stage.app"
```

The first half clears the download quarantine flag. The second gives the app the signature it
should have shipped with. Then open it normally.

---

## Linux: the AppImage won't run

An AppImage needs permission to run as a program. Either:

- Right-click → **Properties** → **Permissions** → tick **Allow executing file as program**, or
- In a terminal: `chmod +x Pixel-Stage-*.AppImage` then `./Pixel-Stage-*.AppImage`

---

## It opens, but it's slow, or the picture is torn / blank

Press **G**, or go to **Settings → GPU view**, to switch between the two ways the app draws.

- If the app feels dead under a big rig, you are probably on the slower path — switch it on.
- If shapes look wrong or the view is blank, switch it off; some machines and remote-desktop
  sessions cannot do the fast path.

The choice is remembered. On a Raspberry Pi or a very old machine, use the
`lite-portable.html` download instead.

---

## The app won't update / "Check for updates" does nothing

1. **Check you are online**, and that a work firewall is not blocking `github.com`.
2. **Update by hand** — download the newest file from
   [Releases](https://github.com/ZombieHunter512/pixelstage-releases/releases/latest) and
   install it over the top. Your saved stages are not touched.
3. On **macOS**, updates are not installed in place — the app downloads a fresh `.dmg` and you
   drag it over the old one.
4. If you downloaded the **portable HTML** file, there is nothing to update automatically.
   Download the new one when you want it.

---

## Where are my saved stages?

Wherever you saved them. **File → Save** writes an ordinary `.json` file to a folder you
choose — the app does not keep a hidden library. Back them up like any other document; a venue
library is just a folder of them.

Updating or reinstalling the app does not touch them.

---

## Will this mess up my Resolume?

No, and that is deliberate.

- Pixel Stage only ever **adds one file**, `Pixel-Stage.xml`, to your Advanced Output presets.
  It never writes to your own setup.
- You decide whether to load it, from Resolume's own top-left dropdown → **Load…**
- **Signal → Remove Pixel Stage from Resolume** deletes that one file and nothing else.

If the preset does not appear in the Presets *list*, that is normal — Resolume only rescans
that folder when it starts. It appears in **Load…** straight away.

---

## Something else is wrong

Open an issue on the **[source repository](https://github.com/ZombieHunter512/pixelstage)**,
and include:

- Which file you downloaded and which version
- What machine and operating system
- What you did, what you expected, and what happened

The app also has a **Help drawer** built in, with tutorials, the shortcut list and an FAQ.
