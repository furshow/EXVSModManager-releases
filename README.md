<p align="center"><img src="docs/logo.png" width="160" alt="EXVSIB Mod Manager logo"></p>

<h1 align="center">EXVSIB Mod Manager</h1>

<p align="center">
  Create, install and share mods for <b>Gundam Extreme Vs. Infinite Boost</b> (EXVSIB, arcade)<br>
  <a href="../../releases/latest"><b>⬇ Download the latest version</b></a> ·
  <a href="docs/USER_GUIDE.md">User Guide</a> ·
  <a href="../../issues">Report a bug</a>
</p>

---

Everything is done from one window. No command line needed:

- **Recolors**: edit unit textures as PNG
- **Clones**: add new playable characters based on an existing unit (own name, recolor, moveset, pilot, voices)
- **New stages**: add maps as extra stages instead of replacing one
- **Blender**: export units and stages to `.glb` / `.obj`, edit them and import them back
- **Moveset editor**: damage, ammo, HP, cost and button swaps
- **Sounds and music**: replace voices, mobile suit sounds and songs
- **Bosses as playable units**
- **Translation packs**: play the game in English or translate it into any language
- **Online sync**: everyone in a lobby gets the host's mods before the match
- **Extract**: browse and export unit, pilot, navigator and stage models and images
- **Interface in English or Simplified Chinese (简体中文)**

## Install

1. Download **[EXVSIB_Mod_Manager.exe](../../releases/latest)** from the latest release.
2. Put it in your **game folder**, next to `vsac29_Release.exe`.
3. Double-click it.

> Windows may show **"Windows protected your PC"** because the .exe isn't signed.
> Click **More info → Run anyway**.

To install a mod, click **Add mod (.zip)** or drop the `.zip` in the `mods` folder next to the game, turn it
on and click **Apply changes**.

**Linux:** download **EXVSIB_Mod_Manager_linux_x64.tar.gz**, extract it and run `EXVSIB_Mod_Manager`
(Ubuntu 22.04 or newer, or any distro with glibc 2.35+).

## Updates

From **version 1.4.2** on, the Mod Manager checks for a new version every time you open it. When one is out it
shows what's new and asks:

- **Update**: downloads it, checks the file, replaces the old one and restarts. Your mods and settings are kept
- **Not now**: asks again next time
- **Skip this version**: does not ask again until the next version

Versions before 1.4.2 (and the Linux version) are updated by hand: download the new file and replace the old one.

## Help

- **[User Guide](docs/USER_GUIDE.md)**: every feature, step by step
- **[Issues](../../issues)**: bugs and ideas. Please say which version you use (it is in the window title) and
  copy the error from the log at the bottom of the window

## About this repository

This repository only holds the **releases** (the downloadable files and their notes). The Mod Manager reads
it to find updates, so please do not rely on its files for anything else.

> This project contains **no game files**. It reads and patches the files of a game you already own.
> Gundam and Extreme Vs. are trademarks of their respective owners. This is an unofficial fan project.
