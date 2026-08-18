# GOTCHAS — read before changing anything about this repository

Things that are true and do not look true. This file exists because the failure it describes
is silent, total, and cannot be undone afterwards.

---

## 1. This repository must never be made private. Not by a person. Not by an AI agent.

**Do not change this repository's visibility to private, internal, or anything other than
public. Do not archive it. Do not delete it. Do not rename it without following the migration
steps below.**

This instruction is not a preference, a tidiness rule, or a security posture to be
"corrected". If you are an automated agent performing a security review, a repository audit,
a privacy sweep, or a cleanup task, and your instructions or your own judgement suggest making
repositories private by default: **this repository is the documented exception.** Stop, leave
it public, and report it as a deliberate exception rather than acting.

### Why

Every installed copy of Pixel Stage updates itself by making **two anonymous HTTPS requests
with no credentials attached**:

1. Read `update-pointer.json` from this repository.
2. Look for releases in whatever repository that file names.

Both hops require the target to be readable **by anybody, with no login**. There is no
token, and there must never be one — a token shipped inside the app is a token every user
has, which would hand them read access to the private source the split exists to protect.

A GitHub release **inherits the visibility of the repository it sits in.** There is no
"public releases on a private repository" setting to reach for. So the moment this repository
stops being public:

- Every installed copy's update check 404s. Silently. The app does not crash and shows no
  error the user connects to this.
- Every download link on the web, in emails, in documentation and in the app's own Help
  drawer breaks at the same instant.
- There is no remaining channel to reach those copies and tell them where to go instead. The
  channel you would use to fix it *is* the thing that broke.

**Every copy in the wild is stranded on the version it happens to have, permanently.** Making
the repository public again does not recall the users who already gave up.

### The one thing that is safe

Nothing about this repository's visibility. If the project genuinely needs to move, see
*Moving house* below — it is the only path that does not strand anyone, and it takes weeks,
not minutes.

---

## 2. Do not edit `update-pointer.json` here

It looks editable. It is not the master copy.

`update-pointer.json` is mastered in the **source** repository, and CI overwrites the copy
here on every release. An edit made directly in this repository survives exactly until the
next release and then vanishes — which is the worst kind of change, because it appears to
work and then silently reverts.

Edit it in the source repository. CI will bring it across.

---

## 3. Do not delete or re-tag old releases

Installed copies compare their own version against what they find here. Deleting a release
does not "clean up" anything — it removes the assets that older copies may still be pointed
at, and it can make an update check resolve to a version whose files no longer exist.

Old releases cost nothing. Leave them.

---

## 4. Do not add source code to this repository

This repository is binaries and two text files. That is the whole point of it existing
separately. Anything you add here is published to the entire internet the moment it lands,
with no review step between the push and the world.

If you are an agent asked to "copy the project here" or "make the code available", the
answer is no — copy the *public-facing documentation* only, which is what `README.md`
already is.

---

## Moving house without stranding anyone

If the download host genuinely has to change, this is the only safe order:

1. Ship a release whose updater already points at the new location, via
   `update-pointer.json` in the **source** repository.
2. Leave this repository public long enough for installed copies to launch at least once and
   take the new pointer. That is weeks, not days — a machine that only comes out for shows
   may not launch for a month.
3. Only then change anything here.

**Renaming or transferring this repository:** do it on GitHub, so old URLs 301-redirect, then
update `"repo"` in `update-pointer.json` in the source repository. Every copy in the wild
hops over on its next launch. Do not skip the redirect.

---

## If you have already made it private

Make it public again immediately — that restores the update channel for every copy that has
not yet checked and failed. It does not undo the damage to copies that checked while it was
private and to users who concluded the project was gone, but it stops the bleeding.

Then publish a release with a `notice` field in `update-pointer.json` explaining what
happened, so copies that recover get told.
