# Congegno

**Many natures, one environment.**

Congegno is a desktop application to draw and simulate machines together with their control. Block diagrams,
multibody mechanics, physical networks and state machines live in one model, in one workspace, and run together.

*Congegno* is Italian for "mechanism" (con-JEN-yo).

![A pendulum's model, its 3D view and the Library](images/workspace.png)

This repository holds Congegno's **downloads**, its **release notes** and its **issue reports**. Congegno is free to
try under the [Congegno Preview Licence](LICENSE.md). It is not open source.

## What it does

- **Block diagrams**: sources, sinks, math, continuous and discrete blocks, lookup tables, buses, subsystems,
  several sample rates in one model, and Python Function and C Function blocks. The control diagram is compiled to
  native code.
- **Multibody mechanics as blocks**: frames, rigid transforms, solids from simple shapes or CAD files, joints,
  forces, contact and flexible beams. You never declare a body: Congegno finds the bodies from how the frames are
  connected.
- **Multiphysics**: physical networks with conserving ports, from 1-D mechanics to electrical, thermal, gas and
  propulsion, compiled by OpenModelica; a whole Modelica model, or equations typed in, as a block.
- **State machines**: modes, sequences and fault handling drawn as states and transitions on a canvas of their own.
- **Two engines**: the *Accurate* profile runs on Drake, the *Fast* profile on MuJoCo.
- **Results you can look at**: a 3D view with playback and overlays, scopes, dashboards, Matplotlib figures, video
  export.
- **Scripting**: a Python console and an editor in the app; run a model from a script.
- **Agents**: run your own AI coding agent in a terminal inside the app, acting on the models you see.
- **Everything is a file**: a model is a plain text file you can read, compare and keep under Git.

![A cart-pole balanced by an LQR controller, with its scope](images/control.png)
![A dashboard built from the model's probes](images/dashboard.png)
![Two robot arms picking and placing, one of the examples](images/panda.png)

The examples that come with Congegno (Help ▸ Examples…) are a good place to start.

## Download

Get the latest build from [Releases](../../releases). Congegno is a preview: expect rough edges, and tell us about
them.

| System | File |
|---|---|
| macOS, Apple Silicon | `Congegno-<version>-arm64.dmg` |
| macOS, Intel | `Congegno-<version>-x64.dmg` |
| Linux x86_64 | `Congegno-<version>-linux-x86_64.AppImage` |
| Linux aarch64 | `Congegno-<version>-linux-aarch64.AppImage` (newer and less tested: tell us how it goes) |
| Windows | coming: it will be added to this release once tested |

Each file has a `.sha256` beside it, and each is complete: its own Python, the engines, OpenModelica with the Modelica
Standard Library and a C compiler. Nothing is downloaded when Congegno first starts, and you need no Xcode, Homebrew
or Python of your own.

## System requirements

- **macOS, Apple Silicon**: macOS 15 or later; about 2 GB of disk for the app.
- **macOS, Intel**: macOS 13 or later. Simulations run in a small Linux system that the app carries and starts by
  itself: the download is about 1.5 GB larger, and Linux takes more disk once prepared. The first launch of a new
  version takes a minute or two to prepare it, and each launch about twenty seconds to start it. By default it gets
  all the cores and half the memory, at least 4 GB; File ▸ Back-End Settings… changes that.
- **Linux**: x86_64 or aarch64, glibc 2.34 or later (Debian 12, Ubuntu 22.04, Fedora 35 and later), and FUSE
  (`fuse3`; most desktops have it). No root access is needed. The AppImage is one file of under 1 GB.

## Install on macOS

The app is not notarized by Apple yet, so macOS refuses to open a copy that comes straight from a downloaded `.dmg`:
it says it cannot check the app for malicious software. On macOS 15 and later, right-click ▸ Open no longer gets
around this. The `.dmg` window shows two steps that do:

1. Open the `.dmg` and drag Congegno to Applications.
2. Open Terminal and paste the line the window shows:

   ```sh
   bash /Volumes/Congegno/install.sh
   ```

   The script checks that Congegno in Applications is the `.dmg`'s app, whole and with its signature intact, removes
   the download mark from `/Applications/Congegno.app` only, and opens it. It asks for no password and changes no
   setting of macOS. If you skipped step 1, it says so. The line is the same for every release.

Without Terminal: open Congegno, let macOS refuse it, then go to System Settings ▸ Privacy & Security and choose
**Open Anyway**.

With the GitHub CLI, one command downloads a release, checks its SHA-256 and installs it:

```sh
gh release download <tag> --repo msavox/congegno-releases --pattern install_release.sh && bash install_release.sh <tag>
```

## Install on Linux

Make the AppImage executable and open it:

```sh
chmod +x Congegno-<version>-linux-x86_64.AppImage
./Congegno-<version>-linux-x86_64.AppImage
```

Where FUSE is missing, `./Congegno-<version>-linux-x86_64.AppImage --appimage-extract-and-run` opens it.

To install it with a desktop entry, icons and the file types of `.cgn` and `.cgnproj`, download
`install_release_linux.sh` from the release, keep the AppImage's `.sha256` beside the AppImage, and run:

```sh
bash install_release_linux.sh ./Congegno-<version>-linux-x86_64.AppImage
```

It checks the checksum, copies the AppImage to `~/Applications/Congegno.AppImage` and adds Congegno to your
applications.

## First launch

Congegno first shows its terms, the Congegno Preview Licence: **Accept** to go on, or **Quit**. It asks once, and
again only when a new version of the terms comes. Then it opens the folder `~/Congegno` as its project.

## The licence, in short

Congegno is free to download, install and use to try it, evaluate it, learn and teach with it, and for personal
projects. It is not for production or commercial use yet: final terms will come. There is no warranty. What you make
with it is yours, and you may share it. Congegno collects no telemetry and needs no account, licence key or
activation. It is not open source; it runs open-source engines and libraries (Drake, MuJoCo, OpenModelica and
others) under their own licences, listed in Help ▸ About Congegno ▸ Licences.

The full text is in [LICENSE.md](LICENSE.md), and it is the one that counts.

## Reporting a problem

In Congegno, Help ▸ Report a Problem… opens a new [issue](../../issues/new/choose) here. Say what you did, what you
expected and what happened, and paste what Help ▸ About Congegno ▸ This Installation copies (version, system,
engines). A small model that shows the problem helps most; the session log is `~/.congegno/logs/session.log`. Please
attach only what you are free to share.

© 2026 Matteo Savoia.
