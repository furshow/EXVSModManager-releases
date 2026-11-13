# EXVSIB Mod Manager — User & Modding Guide

For **Gundam EXVSIB 1.13.30** (also works on 1.0.4) · `EXVSIB_Mod_Manager.exe` · by Furshow

The Mod Manager installs, combines and removes mods without ever losing your original game files. It also extracts models and images, shows movesets, and keeps mods in sync for online play.

---

## Contents

1. [How it works (the short version)](#1-how-it-works-the-short-version)
2. [The window](#2-the-window)
3. [Mod types](#3-mod-types)
4. [The `mod.json` file](#4-the-modjson-file)
5. [Quick tutorial: your first recolor mod](#5-quick-tutorial-your-first-recolor-mod)
6. [More tutorials](#6-more-tutorials)
7. [Sharing mods (.zip)](#7-sharing-mods-zip)
8. [Online play: syncing mods with the host](#8-online-play-syncing-mods-with-the-host)
9. [Other tabs: Extract, Sounds and Movesets](#9-other-tabs-extract-sounds-and-movesets)
10. [Folders and files](#10-folders-and-files)
11. [Troubleshooting & limits](#11-troubleshooting--limits)
12. [Appendix: creating .bpatch files and naming every file](#12-appendix-creating-bpatch-files-and-naming-every-file)

---

## 1. How it works (the short version)

- The game data is in `data\x64\dplcache_release\` as files named like `0xA78A797D.fhm2d`. Each one is a package holding sub-files (textures, meshes, tables, scripts…).
- A **mod** is a folder in `mods\` with a `mod.json` and the changes, for example edited textures saved as PNGs or binary patches. A mod **never contains full game files**, only the parts that changed. That's why mods are small and can be shared legally.
- When you click **Apply changes**, the Mod Manager:
  1. Copies each original file it's about to touch into `backup_mods\original_fhm2d\` (first time only).
  2. **Rebuilds** each affected game file from that original copy plus every enabled mod that touches it.
  3. Restores the original of any file that no enabled mod touches any more.
- Because every file is always rebuilt from the original, turning mods on and off is safe and fully reversible. Turn everything off, click Apply, and you're back to the original game.
- **Order matters.** If two mods change the same texture, the one **lower in the list wins**. Use the ▲ ▼ buttons to reorder.
- Applying is **incremental**: files whose mods didn't change are skipped ("up to date").

> ⚠️ Close the game before you click **Apply changes**. Windows locks files the game has open.

---

## 2. The window

### Header
- **Apply changes** writes your current selection to the game. The status pill next to it shows whether there are pending (unapplied) changes.
- **Language / 语言** switches the whole Mod Manager between English and Simplified Chinese (简体中文). The window changes right away and keeps everything you had turned on but not applied yet; the choice is remembered. The first time, a Chinese Windows starts in Chinese. It only changes the Mod Manager, not the game (the game's language comes from the translation pack you turn on).

### Mods tab
| Element | What it does |
|---|---|
| **Search mods** | Filters the list by name or author. |
| **Open mods folder** | Opens `mods\`. |
| **＋ Add mod (.zip)** | Installs a mod zip. You can also drop the .zip into `mods\` (it installs itself within ~2 s) or drag it onto the .exe. |
| **Online ▾** | Online sync options (see [section 8](#8-online-play-syncing-mods-with-the-host)). |
| **Create ▾** | **New folder…** (see *Folders* below) · **New recolor mod…** (exports a unit's textures to PNG) · **Mod from extracted files (Extract tab)…** · **Mod from modified .fhm2d files (.bpatch)…** (turns files edited with other tools into a patch mod) · **Edit a 3D model in Blender (.glb)…** · **New stage in Blender (.glb)…** · **Import from Blender (.glb)…** · **Translation template (.xlsx)…** · **Translation from spreadsheet (.xlsx)…** |
| List: **TRANSLATIONS** | Translation packs. Only one can be active at a time (radio button). |
| List: **folders** | Your own folders (e.g. *STAGES*, *CALIBARN*). The switch of a folder turns **all** its mods on or off at once. |
| List: **MODS** / **OTHER MODS** | All other mods, each with an on/off switch, its type and its author. |
| **ACTIVITY** (bottom) | The log. Click *Show* to see what Apply did, plus warnings and errors. |

#### Folders
Folders only organize the list; they don't move or change any file.
- **Create ▾ ▸ New folder…** (or right-click an empty part of the list) and give it a name, for example *Stages* or *Calibarn*.
- Put a mod in a folder: **right-click the mod ▸ Move to folder**, or select it and use **Move to folder…** in the detail card. A mod can be in one folder at a time; *Take out of the folder* puts it back in the main list.
- The **switch of a folder** turns all its mods on or off (then press **Apply changes**). The detail card of a folder lists its mods and has *Turn all on / Turn all off*.
- **Double-click** a folder to fold / unfold it. **Right-click** it to rename or delete it (deleting a folder keeps its mods).
- ▲ / ▼ move a mod among the mods of its own folder. Priority between mods ("lower wins") is still the global order.

### Detail card (right side)
Select a mod to see its description, type, the game files it touches and its folder. Actions:

| Button | What it does |
|---|---|
| **Turn on / Turn off** | Enables or disables the mod. Nothing changes in the game until you Apply. |
| **▲ ▼** | Changes priority. Lower in the list wins. |
| **Mode…** | For unit mods: *Recolor* (changes the original unit) or *New character* (clone). For stage mods: *Replace* or *New stage*. For pilot mods: *Replace*, *For a new character* or *On another pilot* (see [3.9](#39-pilot-and-voice-type-pilot--voice)). |
| **Art templates** | Clones and new stages only: saves the original 2D images (unit select, card, VS screens, loading screens, thumbnails…) as PNGs with the right names and sizes, ready to edit. |
| **Pilot…** | Clones and hidden units only: gives the character a pilot of its own (portraits, cut-ins and name from any pilot of the game, a voice from any pilot, or a pilot mod you make for it). See [6.13](#613-give-a-new-character-its-own-pilot). |
| **Merge into…** | Copies everything in this mod (textures, patches, pilot images, voices, sounds, art…) into another mod, so one mod holds all the changes. See [6.14](#614-one-mod-with-everything-merging-mods). |
| **Remove unchanged** | Deletes the PNGs you didn't edit (textures and art templates), so the mod only keeps what you changed. Do it before exporting. |
| **Export as .zip** | Creates `mods\_exported_zips\<mod>.zip`, ready to share (changed files only). |
| **Open folder** | Opens the mod's folder. |
| **Delete mod** | Deletes the mod folder. |

---

## 3. Mod types

The **Type** column in the list tells you what kind of mod each one is.

### 3.1 Recolor (texture mod)
Replaces textures of a unit, navigator, pilot, stage, etc. with your own PNGs.

```
mods\My Mod\
  mod.json
  0xA78A797D\                         ← the game file the texture belongs to
    tex_01_1024x1024_BC7.png          ← tex_<sub-file number>_<width>x<height>_<format>.png
```

- The file name must keep the `tex_NN_` prefix. `NN` is the sub-file number inside the game file. Keep the same **size** too. A PNG with a different size is resized, and the log says so.
- Only PNGs that **differ from the original** are applied. Unedited PNGs are ignored, so it's fine to leave them, but *Remove unchanged* keeps the mod clean.
- The Mod Manager converts your PNG to the texture's own format. The last part of the name tells you which one it is:

  | Format | Typical use | What is kept from your PNG |
  |---|---|---|
  | `BC7` | Base color (albedo), emissive, most unit textures | Color + alpha, best quality. Takes about a minute per large texture. |
  | `BC3` | Textures with alpha, some normal maps | Color + alpha |
  | `BC1` | Simple color textures | Color only (no alpha) |
  | `BC4` | Grayscale masks (roughness, metal, AO…) | One channel: exported as grayscale; a color PNG is turned into grayscale |
  | `BC5` | Normal maps (2 channels) | Red and green channels only |
  | `RAW` | UI images, icons, portraits, 2D art | Exact pixels, no compression |

- Encoded textures are cached in `mods\<mod>\_cache\`, so later Applies are instant.
- Environment maps (format `0x4D7`) can't be imported.
- A unit often has **several game files** (versions of the same unit with different weapon sets or roles). A recolor of one file doesn't change the others. Include every version's file in the mod if you want the change everywhere.

### 3.2 Model (binary patch mod)
For changes that PNGs can't express: new meshes, skeletons, materials, effects, tables, or added sub-files. These mods hold **binary patches** that store only the differences from the original:

```
mods\My Model Mod\
  mod.json
  0x7B7EAEC9\
    sub_71.bpatch      ← patch for sub-file 71 (any size change is allowed)
  0xA0308811\
    full.bpatch        ← patch for the WHOLE .fhm2d (used when sub-files are added or the index changes)
```

- You don't write these by hand. Edit the `.fhm2d` with any tool, then use **Create ▾ → Mod from modified .fhm2d files (.bpatch)…** and pick your edited files. They must keep their game name, `0xXXXXXXXX.fhm2d`. The Mod Manager compares them to the originals and saves only the differences. You don't need to share your .fhm2d files.
- When a file gets several changes, they're applied in this order: `full.bpatch` → `sub_NN.bpatch` → PNGs.
- A patch only applies to the exact original it was made from. If it doesn't match, the log says it was skipped.
- Full details on creating patches and naming files: [section 12](#12-appendix-creating-bpatch-files-and-naming-every-file).

### 3.3 Clone (new character)
Any unit mod (recolor or model) can be switched with **Mode… → New character**. Instead of changing the original unit, the mod then **adds a new playable unit** with its own name in a **MODS** tab of the unit select screen.

- The clone uses the original's moveset, sounds, effects and animations. It gets its **own** model (original + your changes), its own parameters and unit ID.
- Up to **8 clones** can be on at once. Each gets a slot (0–7), which sets its ID (`base ID // 1000 * 1000 + 901 + slot`, e.g. `66004901`) and MS number (`330 + slot`). The slot is saved in `mod.json`, so everyone who installs the same zip gets the same ID.
- **Own 2D art (optional):** select the mod → **Art templates**. The original unit's images are saved in `mods\<mod>\clone_art\` with the right names and sizes. Edit the ones you want. Images you leave unchanged (or delete) keep using the original art. (Mods made with older versions used a folder called `arte_clon` / `arte_escenario`: they still work and are renamed automatically.) Each PNG must keep its **size**, or it's skipped (the log says which size is needed).

  | File | Size | Used for |
  |---|---|---|
  | `ms_ms_l.png` | 1920×1080 | Large unit-select art |
  | `ms_ms_s.png` | 228×104 | Small unit-select art |
  | `ms_vs_l.png` / `ms_vs_r.png` | 960×900 | VS screen art (left / right) |
  | `ms_card.png` | 458×680 | Card |
  | `ms_igh.png` | 144×48 | In-game HUD image |
  | `ms_tracker.png` | 240×72 | Tracker image |

- **Swapped buttons (optional):** `"swap_buttons": ["A", "B"]` gives the clone its own moveset script with those buttons swapped (A = shoot, B = melee, C = jump/boost). Combinations follow the swap automatically (A+B sub, A+C special shot, B+C special melee). You can also give several pairs: `[["A","B"], ...]`. Note: a CPU-controlled clone may also get the swapped inputs.
- **Own pilot (optional):** by default a clone has the pilot of the unit it was made from (same portraits, cut-ins, voice and name). Select the mod → **Pilot…** to give it another pilot of the game, its own pilot name, or a **pilot mod** made just for it; the original pilot is never changed. See [6.13](#613-give-a-new-character-its-own-pilot).
- **Own sounds and pilot voice (optional):** select the clone mod in the **Mod** box of the **Sounds** tab and replace the sounds of the **original unit** (Mobile suit sounds) and/or the voice lines of its **pilot** (Pilot voices), or import a modified `.nus3audio` / `.nus3bank`. The tab tells you which entries belong to the clone. The clone gets its own copy; the original unit keeps its sounds and voice (see [6.12](#612-change-voices-and-mobile-suit-sounds)).
- **Moveset editor (optional):** damage, ammo, reload, HP and cost of the clone can be changed in the Movesets tab (see [6.8](#68-edit-a-moveset-damage-ammo-hp-cost)).
- **Moveset edits (advanced, optional):** `"moveset"` with `add_rows` (add or modify rows in the clone's parameter tables, e.g. a new projectile) and `replace_consts` (replace a 32-bit constant in the moveset script). See the example in [section 6.4](#64-advanced-clone-with-a-custom-projectile).
- A clone can have **no texture folders at all** (moveset-only clone, e.g. just swapped buttons).

#### Hidden unit (Type: *Hidden unit*)
The game includes some **complete units that it never shows** in the unit select: they have a model, moveset, animations, cost and HP, but no unit-select entry. A hidden-unit mod adds that entry, so the unit becomes playable **in the tab of its own series**, with its real ID. No game file is copied and the game program is not changed. Ready-made mods:

| Mod | Unit | Cost / HP | Series tab | Art, icon and portraits from |
|---|---|---|---|---|
| Hidden unit - Dom | Dom | 1500 / 460 | Mobile Suit Gundam | Doan's Zaku II |
| Hidden unit - Silver SUMO | Silver SUMO | 1500 / 420 | Turn A Gundam | Gold SUMO |
| Hidden unit - Gundam Throne Eins | Gundam Throne Eins | 2000 / 500 | Mobile Suit Gundam 00 | Gundam Throne Zwei |

- The game has no 2D art or pilot portraits for these units, so they're borrowed from the **donor** unit. **Art templates** saves the donor's images to `clone_art` so you can draw your own (same table as above). **Pilot…** works for hidden units too (another pilot of the game, or a pilot mod made for it).
- Online, both players need the same hidden-unit mods (they're synced like clones, see [section 8](#8-online-play-syncing-mods-with-the-host)).
- `mod.json`: `"mode": "clone"` and

  ```json
  "clone": {"hidden": true, "unit": 14019001, "donor": 14020001, "name": "Gundam Throne Eins",
            "short_name": "Throne Eins", "pilot": "Johann Trinity", "pilot_short": "Johann",
            "weapons": ["GN Beam Rifle", "GN Mega Launcher", "GN Launcher [Irradiation]", "GN Beam Saber",
                        "Gundam Throne Zwei (Call)"]}
  ```

  `weapons` = texts of the unit select: main, sub, special shooting, melee, special melee. `pilot` and `weapons` are optional (the donor's are kept). The MS number is set automatically (Dom 15, Silver SUMO 110, Throne Eins 155: the gaps the original numbering left for them).

#### Boss (Type: *Boss*)
The game also has **14 bosses** that only the CPU uses, each with its full moveset (player buttons included), model, animations, sounds, pilot, VS art and card: Zakrello, Zeong (Complete), Quin Mantha, Gundam GP03 Dendrobium, Shamblo, Divinidad, Vagan Gear SID, Zeerach, Graze Ein, Psycho GM, Galvaria B34M3R / H4ND3R / W45P3R and Eldora Dotress (Large).

1. **Create ▾ → Bosses as playable units…**
2. Tick the bosses you want (**Select all** for every one). Bosses that already have a mod are greyed out.
3. Choose the **cost** (3000, 2500, 2000 or 1500) and the **HP**:
   - **Boss HP** (1600-2800): the boss keeps its real HP, so it's very hard to defeat.
   - **Normal HP for that cost**: the usual HP of a unit of that cost (about 680 at 3000), for balanced matches.
   
   In the game bosses cost 6000, so one boss would use the whole team cost. That's why the cost is chosen here.
4. **Create mods** makes one mod per boss, `mods\Boss - <name>\` (off). Turn them on and **Apply changes**. Each boss appears in the **tab of its series** (Galvaria, whose series has no playable unit, goes in the Mobile Suit Gundam tab).

- The boss keeps its own name, pilot (portrait, cut-in and voice), VS picture, card and name plate. The game has no select-screen pictures for bosses, so the Mod Manager makes them from the VS picture and saves them in the mod's `clone_art` folder (`ms_ms_l`, `ms_ms_s`, `ms_vs_l`, `ms_tracker`). Replace them with your own art of the same size and apply again.
- Graze Ein, the Galvarias and Eldora Dotress have no pilot: they get the pilot of a unit of their series. Use **Pilot…** to pick another one.
- The icon and the unit select weapon texts aren't the boss's own (the icon is the donor's; the weapon texts are empty).
- The game program marks bosses as "boss" and leaves them out of the unit select, so while a boss mod is on the Mod Manager marks that boss as a normal playable unit in `vsac29_Release.exe` (one value per boss; close the game before applying). In battle, including CPU route battles, it is then treated like a normal unit. Turning the mod off restores it.
- Bosses are big and some of their moves were made for fighting several players at once, so some moves may look odd in a normal match.
- Online, both players need the same boss mods, like any clone or hidden unit (see [section 8](#8-online-play-syncing-mods-with-the-host)).
- `mod.json`: `"mode": "clone"` and

  ```json
  "clone": {"hidden": true, "boss": true, "unit": 603002001, "donor": 3001001, "name": "Quin Mantha",
            "cost": 3000, "hp": 1600}
  ```

  `donor` = playable unit whose row gives the series tab, the icon and what a boss doesn't have. `short_name`, `pilot`, `pilot_short` and `weapons` work as for hidden units. MS numbers start at 340.

### 3.4 New stage
A mod that changes a stage map file can be switched with **Mode… → New stage**. Instead of replacing the stage, it then **adds a new stage** at the end of the stage select, built from the original stage plus your changes.

- Up to **8 new stages**. Each gets a slot and its own files (`0x5354….fhm2d`).
- **Own images (optional):** select the mod → **Art templates**. The base stage's images are saved in `mods\<mod>\stage_art\` with the right names and sizes. Edit the ones you want. Unchanged or missing ones come from the original stage, and `vs_sn` (the name banner) is drawn automatically from the stage name.

  | File | Size | Used for |
  |---|---|---|
  | `ms_s_s.png` | 300×188 | Stage-select thumbnail |
  | `ms_s_l.png` | 1856×548 | Stage-select large image |
  | `vs_s_l.png` | 1920×1080 | Loading screen |
  | `vs_s_d.png` | 1920×1080 | Dark loading background |
  | `vs_s_s.png` | 491×148 | Stage badge |
  | `vs_sn.png` | 320×32 | Stage name (auto if missing) |

- Optional `"random_weight"` in the `stage` block controls whether the stage can come up when the stage is chosen at random (0 = never).

### 3.5 Game patch (exe patch)
Changes the game program (`vsac29_Release.exe`) with find/replace byte patches. The LM program (`vsac29_Release_LM.exe`) is left original:

```json
"exe_patches": [
  { "description": "Time Rental timer frozen",
    "find":    "ff83c0040000 488d8bd0040000",
    "replace": "660f1f440000 488d8bd0040000" }
]
```

- `find` must appear **exactly once** in the original exe, and `replace` must be the **same length**. Spaces in the hex are ignored.
- The exe is always rebuilt from `backup_mods\original_exe`: original → clone table → exe patches. Turn the mod off and Apply, and the exe goes back to the original.
- Example included: **Infinite Time Rental** (the 30-minute Time Rental timer never runs out).

### 3.6 Generated
A mod with `"generator"` in its `mod.json` holds **no game data**. Its images are generated from **your own** game files the first time you apply it, which can take a few minutes. Example: **Navigator image fix** (`"generator": "navigator_fix"`) removes the thin frame around navigators' eyes and mouths. Exporting a generated mod saves only its `mod.json`.

### 3.7 Sound (Type: *Sound*)
Replaces **pilot voices**, **navigator voices**, **mobile suit sounds** (shots, slashes, explosions…) or the **music (BGM)** with your own WAV files. Made in the **Sounds** tab (see [6.12](#612-change-voices-and-mobile-suit-sounds) and, for music, [6.15](#615-change-the-music-bgm)). Any WAV works: mono or stereo, any sample rate, 8/16/24/32-bit or float; the Mod Manager converts it to the game's format when you apply. A sound mod can be combined with a recolor of the same unit (they can even be the same mod). Turning it off and applying puts the original sounds back.

### 3.8 Translation pack
A folder with `"type": "translation"` and the translation JSONs:

```
mods\English translation v1.0\
  mod.json                       {"name", "version", "type": "translation", "author", "description"}
  traduccion_menus.json          (required)
  traduccion_tabla.json          (required)
  traduccion_unidades.json       (required)
  traduccion_bases_datos.json    (required)
  traduccion_imagenes.json       (optional: texts drawn on images)
  traduccion_oficial.json        (optional: own texts for weapons and options instead of the official English)
```

- You don't write these files by hand: make them from a spreadsheet (see [6.7](#67-translate-the-game-into-any-language)).
- Only **one** translation can be active (radio button). Choosing none and applying restores the original Japanese.
- Packs contain no Japanese text and no game data (the keys are hashes).
- A translation installed with `EXVSIB_English_Patch.exe` shows as *external* and is left alone unless you pick a pack.

### 3.9 Pilot and Voice (Type: *Pilot* / *Voice*)
A mod that only changes **pilot images** (sortie portraits with their lip-sync mouths, cut-ins, and the pilot's body pictures) and/or **pilot voice lines** shows the type *Pilot* (*Voice* if it only has voice lines). You can make one in the **Extract** tab (Pilots → edit → *Make a mod from my edits*), from a clone's **Pilot…** window (*Create pilot mod*), or by hand with the pilot files' PNGs. Use **Mode…** to choose where it goes:

| Mode | What it does |
|---|---|
| **Replace** | Changes that pilot itself, in every unit that has it (like any recolor). |
| **For a new character** | The images go only to one of your clones or hidden units, which gets its **own copy** of the pilot files. The original pilot stays as it is. Turn on both the pilot mod and the character, then Apply. |
| **On another pilot** | Puts this pilot on top of **another pilot of the game**: that pilot's portraits and cut-ins (if the mod has images) and its whole voice (if the mod has voice lines) are replaced by the mod's pilot, in every unit with that pilot. The pilot name stays. |

- **Voices:** each pilot has its own set of lines and its own rules for when each line is said, so a voice is always moved **as a whole**: the character (or the other pilot) speaks with the mod's pilot voice, with your edited lines, from its own copy. The original pilot keeps its voice.

- A pilot file holds the whole picture set with its own mouth positions, so a pilot can be moved onto any unit without adjusting anything.
- `mod.json`: `"mode": "pilot"` and `"pilot": {"mod": "<folder name of the clone mod>"}` or `"pilot": {"unit": <ID of a unit that has the target pilot>}`.
- Turning it off and applying puts everything back.

---

## 4. The `mod.json` file

Every mod needs a `mod.json` in its folder. Minimum:

```json
{
  "name": "My Mod",
  "author": "Your name",
  "description": "What the mod does."
}
```

| Key | Used by | Meaning |
|---|---|---|
| `name` | all | Name shown in the list. The zip installs into `mods\<name>\`. |
| `author` | all | Shown in the list and detail card. |
| `description` | all | Shown in the detail card. |
| `version` | optional | Shown as `vX`. Translation packs install into `<name> v<version>`. |
| `type` | translation | `"translation"`. |
| `mode` | clone / stage / pilot | `"clone"`, `"stage"` or `"pilot"`. Leave it out for recolor/replace. Normally set with **Mode…**. |
| `clone` | clone | `name` (max 40 chars), `unit` (original unit ID), optional `short_name`, `swap_buttons`, `moveset`, and the pilot keys `pilot_from` (ID of the unit whose pilot it uses), `voice_from` (ID of the unit whose pilot voice it uses), `pilot` / `pilot_short` (pilot name; `""` = no name). `slot`, `id` and `ms_number` are filled in automatically. |
| `pilot` | pilot | `{"mod": "<clone mod folder>"}` (pilot of that character) or `{"unit": <unit ID>}` (put on that unit's pilot). |
| `stage` | stage | `name`, `base` (row ID of the original stage), optional `random_weight`. `slot` is filled in automatically. |
| `exe_patches` | game patch | List of `{description, find, replace}`. |
| `generator` | generated | e.g. `"navigator_fix"`. |

Optional extra files in the mod folder: `preview.png` / `preview.jpg` and `readme.txt` (both are included in zips).

---

## 5. Quick tutorial: your first recolor mod

Goal: recolor a mobile suit and see it in the game.

**Step 1 — Find the unit's game file**
Open the **Extract models & images** tab, choose *Mobile suits* and search for the unit. The tab shows its game file (e.g. Gundam Aerial Rebuild = `0xA78A797D`) and a preview. If the unit has several versions, note them all.

**Step 2 — Create the mod**
In the **Mods** tab: **Create ▾ → New recolor mod…**
- *Mod name*: e.g. `Aerial - Red`
- *Game file*: `0xA78A797D`

The Mod Manager exports every texture of the file (color, masks, normal maps…) to `mods\Aerial - Red\0xA78A797D\` and opens the folder. Then it asks whether the mod is a **Recolor** (changes the original unit) or a **New character** (clone). You can change this later with **Mode…**.

**Step 3 — Edit the PNGs**
Open the textures in any image editor (GIMP, Photoshop, Krita, Paint.NET…).
- The large, colorful one is usually the **albedo** (base color). Unit textures often have an **emissive** texture (glowing parts) too; recolor it as well if the glow color should change.
- **Keep the same file name and size.** Save as PNG with transparency (alpha) preserved.
- Tip: use the *Extract* tab with *Also save OBJ files* to get the 3D model and see what each part of the texture maps to.

**Step 4 — Clean up (optional)**
Select the mod and click **Remove unchanged** to delete the PNGs you didn't edit.

**Step 5 — Apply**
Turn the mod **on** and click **Apply changes**. The first time, encoding takes about a minute per edited texture (watch the ACTIVITY log). Then start the game.

**Step 6 — Tweak**
Edit the PNG again and click Apply. Only the changed texture is re-encoded.

**Step 7 — Share**
Click **Export as .zip**. The zip goes to `mods\_exported_zips\` and contains only `mod.json` and your edited textures. Others install it with **＋ Add mod (.zip)**.

---

## 6. More tutorials

### 6.1 Turn a recolor into a new character
1. Select the mod → **Mode… → New character** → type the character's name (e.g. `Calibarn`).
2. Optional: click **Art templates**, then edit the images that appear in `mods\<mod>\clone_art\` (see [3.3](#33-clone-new-character)). Keep their size.
3. Turn the mod on → **Apply changes**. The new unit appears in the **MODS** tab of the unit select, and the original keeps its colors.

### 6.2 Make a mod from files edited with another tool
1. Edit the game's `.fhm2d` files with your tool (model or effect editors, etc.). Keep the original names (`0xXXXXXXXX.fhm2d`).
2. **Create ▾ → Mod from modified .fhm2d files (.bpatch)…** → pick the edited files → choose *Automatic* → give the mod a name. If sub-files were added or removed, a `full.bpatch` is made instead (see [12.4](#124-creating-bpatch-files-in-the-mod-manager)).
3. The Mod Manager saves only the differences as `.bpatch` files. Turn the mod on and Apply. You can delete your edited .fhm2d copies now; the mod doesn't need them.
4. If it's a unit, you can still make it a clone with **Mode…**.

### 6.3 Moveset-only clone (swapped buttons)
Create a folder `mods\Gundam - Swapped Buttons\` containing only this `mod.json`:

```json
{
  "name": "Gundam - Swapped Buttons",
  "author": "You",
  "description": "RX-78-2 with shoot and melee swapped.",
  "mode": "clone",
  "clone": {
    "name": "Gundam (Swapped)",
    "unit": 1001001,
    "swap_buttons": ["A", "B"]
  }
}
```

Restart the Mod Manager so it shows the new folder (mods you create by hand appear on the next start). Then turn the mod on and Apply. You can also zip the folder and add it with **＋ Add mod (.zip)**.
Unit IDs are `SSS·UUU·VVV` (series, unit, variant). For example, `1001001` = RX-78-2 Gundam. The **Movesets** tab lists every unit with its ID.

### 6.4 Advanced: clone with a custom projectile
The `moveset` block edits the clone's own copy of the parameter tables and the moveset script:

```json
"moveset": {
  "add_rows": [
    { "table": 8, "id": "crc:CLONE_VIS_JAVELIN", "base": "0x10d64cb1",
      "set": { "49672094": "crc:eff_001gundam_001gundam_001_jabelin_001" } },
    { "table": 2, "id": "crc:CLONE_PRJ_JAVELIN", "base": "0x180d9a7d",
      "set": { "68cd7942": "crc:CLONE_VIS_JAVELIN", "f33f8630": 120 } }
  ],
  "replace_consts": { "0x93459d29": "crc:CLONE_PRJ_JAVELIN" }
}
```

- `table`: sub-file number of the unit's parameter file (e.g. 2 = attacks/projectiles, 8 = projectile visuals).
- `id`: ID of the new row. `base`: an existing row of the same table to copy first. `from`: `{file, table, row, cols}` copies columns from another unit's table.
- `set`: column hash (hex) → new value.
- Values can be numbers, `"0x…"` hex, or `"crc:NAME"` (CRC32 of the name, the way the game builds its IDs).
- `replace_consts`: replaces every `push` of that 32-bit constant in the moveset script (here, the beam rifle shot now fires the new projectile).

This is the most experimental feature. Test in Training mode, and see the included **Gundam - Javelin Throw** mod.

### 6.5 New stage from a map mod
1. Make or install a mod that changes a stage map file (e.g. *Rocket Arena*, which changes Practice `0xA0308811`).
2. **Mode… → New stage** → type the name.
3. Optional: click **Art templates**, then edit the images in `mods\<mod>\stage_art\` (see [3.4](#34-new-stage)).
4. Turn it on → Apply. The stage is added at the end of the stage select.

### 6.6 Game (exe) patch
Create `mods\<name>\mod.json` with an `exe_patches` list (see [3.5](#35-game-patch-exe-patch)). The detail card lists each patch's description. If `find` isn't found exactly once, Apply reports an error and doesn't write the exe.

### 6.7 Translate the game into any language
1. **Create ▾ → Translation template (.xlsx)…** and choose how the *Translation* column starts:
   - **Empty**: to translate from scratch (you'll see the Japanese and, where the game has it, the official English).
   - **From "<translation>"**: starts with the selected or active translation, to fix it or to translate from English into another language.
2. Save the `.xlsx` and open it in Excel, LibreOffice Calc or Google Sheets. It has a README sheet and one sheet per part of the game (about 6,600 texts):

   | Sheet | What it is |
   |---|---|
   | Menus | Menu and screen texts, descriptions, messages |
   | Weapons / Options | Weapon names and option menus (empty = official English) |
   | Unit names / Pilot names / Unit weapons / Stages | Names shown on the unit and stage select |
   | CPU, route & other | CPU units, bosses, route events, custom chips, series, BGM titles… |
   | Mode titles / Title screen / Burst names / CPU commands / Unit select tabs | Texts drawn as images |
   | Screen labels | Fixed labels of some screens: can't be longer (in bytes) than the Notes column says |

3. Write your text in the yellow **Translation** column. Don't touch the **ID** column.
   - Keep control codes such as `{x10}[time]` exactly as they are. Rows with missing or extra codes are skipped and listed in the log.
   - An empty cell leaves the game text as it is. Write `{empty}` to make a text disappear on purpose.
   - Line breaks inside a cell are kept.
4. Save as `.xlsx`, then **Create ▾ → Translation from spreadsheet (.xlsx)…** → pick the file → name, version and author.
5. The pack appears under **TRANSLATIONS**. Choose it and click **Apply changes**. Check long texts in the game, since some menus have little space.
6. Share it with **Export as .zip**. The pack contains only your texts, with no game data and no Japanese.

Texts drawn as images use a Latin font, so they work best for languages written with Latin letters.

### 6.8 Edit a moveset (damage, ammo, HP, cost)
1. Open the **Movesets** tab and pick a mobile suit.
2. Click **Edit moveset…**. Moves are always edited on a **new character** (clone), so the original unit and online matches against unmodded players stay fair:
   - **New character**: creates a clone mod with the moveset of that unit (asks for its name).
   - Or pick an existing clone of that unit to keep editing it. Picking a clone in the list edits that clone directly.
3. The editor shows:

   | Part | What you can change |
   |---|---|
   | HP / Cost | Health and cost (1500, 2000, 2500, 3000) |
   | Weapons | Ammo and reload time (seconds) of each weapon |
   | Attacks | For every hit: damage, number of hits, correction % (how much it lowers the damage of the following hits), down value (knockdown gauge; 5 or more = knockdown) |

   The **Used by** column tells you which input each hit belongs to (e.g. `B · stage 2`, `↓ A+C · stage 1`). It's read from the game files, like the Movesets tab. Double-click a value to change it; changed values are highlighted. **Reset to original** undoes everything.
4. **Save**, turn the mod on in the **Mods** tab and click **Apply changes**. The character is in the **MODS** section of the unit select.

You can combine this with a recolor of the same unit (the textures of a clone mod) and with `swap_buttons`. The edits are stored in `mod.json` (`clone.moveset.edit`) and travel with the zip and with the online sync.

### 6.9 Edit a unit's 3D model in Blender
You need [Blender](https://www.blender.org/) (free).

1. **Create ▾ → Edit a 3D model in Blender (.glb)…** → mod name → game file of the unit (the *Extract* tab shows it). The model is saved as `mods\<mod>\_blender\0xFILE.glb` and the folder opens.
2. In Blender: **File → Import → glTF 2.0** and open that file. Every mesh is a separate object named like `00|body_normal|SHAPE_ROOTShape|0`:
   - the body is in its place, hands are on their bones, and weapons and other parts are lined up next to the body;
   - textures are shown for reference (to change them, use a recolor: textures and model can be in the same mod).
3. Edit the meshes: move, scale, sculpt, add or delete geometry, change UVs.
   - **Keep the object names.** Objects you duplicate (`.001`) are merged into the original one.
   - Moving or rotating a whole object (or applying its transforms) is fine: its original placement is undone on import.
   - To hide a part, delete all its faces but keep the object.
   - New geometry follows the bones that were closest to it in the original model (weights are copied from the nearest original vertex), so it moves with the animations automatically.
4. **File → Export → glTF 2.0**, format **glTF Binary (.glb)**, default settings (+Y Up on), and save over the same file.
5. **Create ▾ → Import edited 3D model (.glb)…** and pick the file. Only the parts you changed are saved, as `sub_NN.bpatch` patches in the mod. Importing again replaces them.
6. Turn the mod on and **Apply changes**. Use **Mode…** to make it a new character instead of changing the original unit.

The `_blender` folder holds game data, so it is never included in exported zips; only the patches are shared.

Limits: the skeleton, animations and materials are not changed, and parts can't be added to or removed from the model (only their geometry changes). Very large stretches away from the original shape can look odd in animations.

### 6.10 Make a new stage in Blender
1. **Create ▾ → New stage in Blender (.glb)…** → name of the stage. The mod is created as a **new stage**, and a starting map is saved as `mods\<mod>\_blender\stage.glb`. It contains:
   - `ground`: an example floor with a repeating texture;
   - `REFERENCE_play_area_edge`: the edge of the play area, an octagon of ±50 m (±500 game units) with an invisible wall;
   - `REFERENCE_unit_size`: a box the size of a mobile suit (1.8 m tall).
2. Open it in Blender and build your map. **1 meter = 10 game units.**
   - Any meshes and materials with an image texture (or a plain color) work. Textures can repeat.
   - Players appear near the center, so keep ground there.
   - Object name prefixes: `COL_…` = invisible wall (collision only), `NOCOL_…` = visible but you go through it (decoration), `REFERENCE…` = ignored.
   - Surfaces facing up are ground; everything else is wall (solid from both sides).
3. **File → Export → glTF 2.0**, format **glTF Binary (.glb)**, over the same file.
4. **Create ▾ → Import from Blender (.glb)…** and pick it. The Mod Manager builds the stage:
   - the visible geometry;
   - a 2048×2048 texture atlas with all your materials;
   - a matching emission (glow) atlas from the materials' **Emission** color/texture — use it for lit windows, lamps or a self-lit sky dome (materials without emission stay unlit);
   - the Havok collision, generated from your triangles.
5. Optional: **Art templates** for the stage select and loading screen images.
6. Turn the mod on and **Apply changes**. The stage is added at the end of the stage select.

Limits: the stage is built on top of the Practice stage, so it keeps its sky, lighting, spawn points and play-area edge. All textures share one 2048×2048 atlas, so many large textures lose detail; prefer a few small repeating ones.

### 6.11 Import a custom model made by someone else (.glb with its own textures)
Model mods shared as a `.glb` (for example a different robot rigged over a unit) can be turned into a mod directly.

What the `.glb` needs (how these mods are usually made):
- it is **rigged to the game skeleton** of the unit (bone names like `BASE`, `KOSHI`, `MUNE1`, `ATAMA`, `TE_L`…, same pose as the game);
- its meshes keep the names of the unit's parts (`body_normal`, `body_lose`, `wep_handl_ngr00`…, with or without the unit prefix like `015gndmuc_009banorn_001_`), and the materials/textures of the original parts keep their game names, so the Mod Manager can tell which unit it replaces;
- textures are inside the file (glTF Binary).

Steps:
1. **Create ▾ → Import from Blender (.glb)…**, pick the `.glb` and type a mod name.
2. The Mod Manager detects the unit and builds the mod:
   - parts the author **shrank to nothing** (scale 0) are hidden in the game; original pieces left inside a part but shrunk to a tiny size also count as deleted;
   - parts with **new materials** are rebuilt with the new mesh, and each vertex follows the bone it is rigged to. This works for the body **and** for weapons and armaments (backpack, shield, sword, rack…);
   - the color textures of the new materials are packed into atlases (up to 4096×4096) that replace texture sets of the unit that nothing visible uses any more (e.g. the body in one, the weapons in another);
   - the **other maps of the new materials** are used too, each in its own atlas with the same layout: **Normal Map** (normal), **Metallic / Roughness** (metallic, roughness), **Ambient Occlusion** (AO) and **Emission** (emissive), as the glTF exporter writes them (in Blender: Principled BSDF with Image Texture nodes on Normal, Metallic, Roughness, Emission; AO through the glTF Material Output group). A channel that **no** new material has becomes one flat value from the materials' Metallic / Roughness / Emission settings (never the original unit's map), and a new material that lacks a map others have gets its flat value in that atlas;
   - if `body_normal` is replaced and `body_lose` (the defeat pose) was left as the original, it gets the new body too.
3. Turn the mod on and **Apply changes**. Use **Mode…** to make it a new character instead of replacing the original unit.

Limits: a map only shows if the texture set it lands in has that channel (for example `pbr1`/`pbr2` sets have normal, metallic, roughness and AO but no emissive, so an Emission map there is not used; `emiMtl` has all of them). Every map of a set has the size of its color atlas, so a model with many maps takes a little longer to import. Weapons and effects that the game spawns (beams, sabers…) keep their original look unless the author replaced or hid them. A part can only get new textures if one of its original materials is no longer used by anything visible; if, for example, the original hands still show and share their material with a weapon, that weapon stays as in the game and the import log says which material to free (hide or replace the pieces that still use it). Glow materials (with an emissive texture, e.g. a sensor's `emiMtl`) are avoided: a part left with only one of those is moved to a normal material when the unit allows it; otherwise the log warns that it can look too bright. **Transparency (tested in game with Lancelot's energy wings)**: the game has no semi-transparent unit materials. A new material set to Alpha Blend or Alpha Clip in Blender (glass, energy wings…) gets **alpha cut-out**, the mode some units use for holes: each pixel is either drawn or not. Alpha Clip gives clean holes at the material's cut-off. Alpha Blend (e.g. alpha 0.3) becomes a fine dot pattern with that share of pixels drawn, which looks see-through from a distance. The texture alpha and the Base Color alpha both count. This changes one setting in the unit's material files; if the game crashes with it, set those materials back to Opaque.

#### Glowing see-through parts (`_fx` materials)
For a part that should really look translucent and glow (energy wings, beam blades, light effects), draw it as an **effect** instead of part of the model. Effects only show while the game uses a thruster point of the unit (boost dash, steps, jumps, attacks…), **not when standing still**.

1. **Create ▾ → Thruster markers test (for _fx glow parts)…**, pick the unit your `.glb` replaces. It makes a test mod with a **numbered arrow** on every thruster point of the unit.
2. Turn the test on (turn off other mods of that unit), **Apply changes** and play the unit: boost dash in every direction, jump, step and attack. Note the number of the arrow where your glow part should be. Points on the chest or back are the steadiest; points on wing binders or legs move with those parts.
3. Turn the test off. In Blender, put the glow part in its own material whose name ends in **`_fx`** (e.g. `Wing_fx`) and rig it to the body bone it should follow (e.g. `MUNE2`, the chest). Its color comes from the material's Base Color texture (or color); bright colors glow more.
4. **Create ▾ → Import from Blender…** and pick the `.glb`. The Mod Manager asks for the **number** of the thruster point and its **bone** (the most likely one is selected: the thruster bone next to the bone your part is rigged to, e.g. `ATH_V_MUNE_N — thruster, chest, center`). The `_fx` parts leave the model and become an effect on that point; the rest of the model is imported as usual.

Limits: the effect is one rigid piece that follows the bone of the point (it does not bend with the skin). The unit's own effect on that point is replaced. A few units have no effect with a 3D mesh that can be copied; the import then says so.

---

### 6.12 Change voices and mobile suit sounds
The **Sounds** tab works in 4 numbered steps: the list of sounds is on the left and the card **YOUR SOUND MOD** on the right.

1. **Choose the sounds** (left): pick **Pilot voices**, **Navigator voices** or **Mobile suit sounds**, then a name (use *Search*). The list shows every line or sound with its length; **double-click** one (or **▶ Play**) to hear it. Sounds already changed in your mod show **● changed**, and ▶ Play then plays your version as it will sound in the game. Names with sounds changed by the mod chosen in step 2 show **●** and come first in the list; tick **Only the ones my mod changes** to see just those.
2. **Pick the mod** (card): choose the mod where your changes are saved, or press **＋ New** to create one (any mod works, also a clone mod or a recolor of the same unit). The line below says how many sounds the mod changes and whether it is ON.
3. **Change sounds**:
   - One sound: select it in the list → **Replace with WAV…** and choose your file. **Undo** puts the original sound back in the mod.
   - Many at once: **Export to WAV** (bottom left: *Selected* or *All*; *Folder…* chooses where, `extracted\Sounds\…` by default), edit the WAVs in any audio editor or replace them with your own files **keeping the file names**, then **Edited WAV folder…** and pick that folder (or a folder above it). Only the files you changed go into the mod.
   - A `.nus3audio` / `.nus3bank` already modified with another tool (or shared by someone): **.nus3audio / .nus3bank…** and pick one or more files. The Mod Manager finds which game file each one replaces (by its file name, or by the names of the sounds inside), compares every sound with the game and keeps only the different ones. Sounds already in the game's format are kept exactly as they are (no quality loss). `.nus3audio` = pilot / navigator voices, `.nus3bank` = mobile suit sounds.
4. **Put it in the game**: close the game and press **Turn the mod on and apply** (the same as turning the mod on in the **Mods** tab and pressing **Apply changes**).

If you replace a sound before creating a mod, the tab asks for a name and creates it.

Tips:
- New sounds can be longer or shorter than the originals.
- The tick **Play the original sounds** makes the list play and export the untouched game sounds, even the ones your mod changes. Untick it to hear your mod's sounds (marked **● changed**).
- Pilot voices are listed by pilot and the units that use them. A few files used only in special modes have no name (e.g. *Mobile Suit Gundam - voice P49*): play them to know what they are.
- Mobile suit sounds are shared by all versions of a unit (for example every color of the same suit).
- **Clone characters:** every clone has its own entries at the top of the lists: **★ <name> — its own pilot voice** (Pilot voices) and **★ <name> — its own mobile suit sounds** (Mobile suit sounds). Picking one also picks the clone's mod in step 2. Only the clone gets those changes; the original pilot and unit keep theirs (their normal entries don't show the clone's changes and can't be edited for the clone). Example: a *Calibarn* folder with the model clone and an English voice in the same mod.

### 6.13 Give a new character its own pilot
1. Select the clone (or hidden unit) in the list → **Pilot…**.
2. **Portraits and cut-ins:** pick *Same as the original* or any pilot of the game from the list (type in the box to search). The character gets that pilot's sortie portraits, cut-ins, body pictures and voice.
   **Voice:** *Same pilot as the portraits*, or pick another pilot to use only that pilot's voice (e.g. Amuro's portraits with Char's voice).
3. **Pilot name:** fills in by itself with the chosen pilot's name; change it to give the character its own name (leave it empty for no pilot name). The short name is optional.
4. **Save**, then **Apply changes**.

**Draw your own pilot:** in the same window choose the pilot to start from and click **Create pilot mod (images to edit)…**. A new mod (Type *Pilot*, already on and linked to the character) is created with that pilot's images as PNGs, and its folder opens:
- `0x……\tex_01_572x572_BC7.png` in the sortie file is the big portrait; the two small ones next to it are the **mouth** frames for lip-sync (draw them to match the portrait).
- The cut-in file contains the pilot cut-out (the big image); the generic backgrounds are not exported.
- Edit what you want (keep names and sizes), then Apply. Images you leave unchanged keep the original; **Remove unchanged** cleans them up before sharing.

**Already have a pilot mod?** Select it → **Mode…** → **For a new character** and pick the character. Or **On another pilot** to put it on a pilot of the original game instead.

Notes: the character's voice comes from the chosen pilot; to give it its **own voice lines**, use the Sounds tab with the clone (or its pilot mod) selected in the Mod box ([6.12](#612-change-voices-and-mobile-suit-sounds)). Online, the other player sees the character's pilot only if they have the same mods.

### 6.14 One mod with everything (merging mods)
A single mod folder can hold **all kinds of changes at once**: unit textures and patches, pilot images, pilot voice lines, navigator voices, mobile suit sounds, art and exe patches. The detail card lists them under **CONTAINS**.

- In a **new character** (clone) mod, pilot images and voice lines of **any** pilot inside its folder are used by the character: it takes that pilot's portraits / voice with your edits, from its own copy (the original pilot is not changed).
- In a recolor mod, everything replaces the originals, as usual.

To put two mods together: select one → **Merge into…** → pick the other mod. Everything in the first one is copied into the second, which keeps its name (if both have the same file, the one from the first mod wins). Choose **Merge and delete** to end up with a single mod, or **Merge and keep**. If the first mod was a new character or new stage and the second one was a plain recolor, the result becomes that new character / stage. Then **Apply changes**.

Typical use: make the character's pilot with *Create pilot mod*, edit its voice in the Sounds tab, then merge both into the character's mod and share just that one zip.

### 6.15 Change the music (BGM)
The battle, menu and mode music is in the **Sounds** tab too, under **Music (BGM)**. It works like voices (see [6.12](#612-change-voices-and-mobile-suit-sounds)):

1. Pick **Music (BGM)** and a music file: *Battle music 1 / 2*, *Menu and mode music* and the ones added by game updates. The list shows every song with its length; **▶ Play** to hear it.
2. Pick or create a sound mod (**＋ New**). Music only works in a normal sound mod (not in a new character, pilot or new stage mod).
3. Select a song → **Replace with WAV…** (and/or **Rename song…**, see below), or **Export to WAV**, replace or edit the files keeping their names, then **Edited WAV folder…**. A music `.nus3audio` modified with another tool can be imported with **.nus3audio / .nus3bank…**.
4. **Turn the mod on and apply** (with the game closed).

- Any WAV works (mono or stereo, any sample rate, 8/16/24/32-bit or float). It is converted to the game's format: 16-bit stereo at the song's sample rate (48 kHz for almost all). A WAV already in that format is used as it is.
- **Loop:** the game repeats each battle song from a loop start to a loop end. The loop points of your WAV are used (the `smpl` chunk that editors like Wavosaur, Awave Studio or LoopAuditioneer write). Without them the whole song loops from the start. Exported songs keep the game's loop points, so an edited export keeps looping the same way.
- Songs can be longer or shorter than the originals. The only limit: each game music file must stay under 2 GB, and *Battle music 1* is already almost 2 GB. If the new songs don't fit, the log says by how many MB and that file is left original; use shorter songs or put fewer of them in that file.
- Turning the mod off and applying puts back the original music exactly. Only the header of each music file and the songs that were overwritten are backed up (in `backup_mods\original_waveform\BGM\`), not the whole 2 GB file.
- Music mods can be big (about 10 MB per minute of song); an exported zip carries the WAVs.
- **Rename song…** changes the title the game shows when a battle song plays (e.g. *♪ Plazma*). Select the song, press the button and type the new title; leave it empty to go back to the original. The list shows the new title and **● renamed**. It is saved in the mod (`waveform\BGM	itles.json`, carried by exported zips) and written to the game when you apply. Menu music has no title.

## 7. Sharing mods (.zip)

- **Export as .zip** writes `mods\_exported_zips\<mod>.zip` with:
  - `mod.json`, `preview.*`, `readme.txt`
  - **only changed** PNGs, `.bpatch` files, `clone_art\` and `stage_art\` images
  - no game files. Generated and game-patch mods export only their metadata, and translation packs export without Japanese.
- **Installing:** **＋ Add mod (.zip)**, drop the zip into `mods\`, or drag it onto `EXVSIB_Mod_Manager.exe`. It's extracted to `mods\<name>\` (turned **off**), and the zip is moved to `mods\_zips_installed\`.
- Installing a zip with the same name **replaces** the old version.
- Only known file types are extracted from zips; everything else is ignored.

---

## 8. Online play: syncing mods with the host

Some mods change **gameplay** and must be identical on every PC: **clones, new stages and game patches**. If a player picks a clone the other PC doesn't have, the match freezes on the loading screen. Recolors, model mods and translations are personal and are never synced.

**Host:**
1. Online ▾ → **Start the mod server on this PC** (port **38080**, on the same PC as Server-Infinite; it also runs on the Raspberry Pi package as service `exvsib-mods`).
2. Turn on your gameplay mods and Apply.
3. Online ▾ → **Share my mods with players (host)**. This uploads the exported zips plus a manifest.

**Players:**
- The SnowLauncher from the players' package runs the Mod Manager's sync before starting the game. It reads the host's IP from `config.ini` (`Server=`), downloads any missing or changed mods, enables **exactly** the host's gameplay mods (others of that kind are turned off) and applies them.
- It asks for confirmation unless you ticked *Always sync with this server without asking*.
- Manual: Online ▾ → **Sync with the host now**. To use a different server: Online ▾ → **Mod server address…**.
- Sync log: `mods\_sync.log`.

### Move your card to the host's server

If you used to play on your own local Server-Infinite and want to keep your progress on the host's server (PC or Raspberry Pi):
1. Online ▾ → **Move my card to the host server…**
2. Type your card code (the `accessCode` from `card.ini`; it is filled in for you). If several cards share that code, pick yours.
3. Type the host's IP address and confirm. Your whole card is copied: profile, units, navigators, titles, stickers, settings and battle history. The card on your PC is not changed.
4. If the host already has that card (you already played there), you are asked whether to **replace** it. The progress saved on the host for that card is lost, but the host keeps a backup.
5. At the end you can **point your game** to the host: `Server=` in `config.ini`, `lmnfig.ini` and `SnowLauncher.ini` becomes `HOST_IP:28080` (copies of the old files are kept as `.antes_tarjeta`).

The host must have the mod server running (the Raspberry Pi runs it as the `exvsib-mods` service). Every imported card leaves a copy of the host's database in `backups_tarjetas`, next to `ServerInfinite.db`.

### Watch a match from the server's Battle History

The server's web page **Battle History** has a **Download** button on every match the LM saved a replay of (a `.bin` file, a few KB; it is not a video, the game plays the match again).
1. Online ▾ → **Import match replays (.bin)…** and pick one or more downloaded files (the dialog opens in your Downloads folder).
2. Start the game in LM mode and open its replays. The LM reads its list only when it starts: if it was already open, restart it.
3. The list is sorted by date, newest first (No.001), so a match from the server goes where its date puts it.

The files go to `29\replay_store` and are added to the LM's list (`replay_list.json`; the previous list is kept as `replay_list.json.backup`). Importing the same match twice does nothing. A file renamed by the browser (for example `... (1).bin`) still works.

---

## 9. Other tabs: Extract, Sounds and Movesets

### Extract models & images
Exports game content to edit it and turn it into mods (or just to look at it). Your installed mods are included unless you tick *Use the original game files*. For mods, tick that box, so you start from the original.

| Category | Output | What you can edit |
|---|---|---|
| Mobile suits (3D model) | `.glb` (one object per mesh, all materials) + every texture as PNG in `0xFILE\` (+ optional OBJ) | The PNGs, and the `.glb` in Blender |
| Pilots (portraits & cut-ins) | PNGs in `0xFILE\` | The PNGs |
| Navigators (images) | PNGs in `0xFILE\` + full composited images in `complete\` (only for viewing) | The PNGs in `0xFILE\` |
| Stages (3D map) | `.glb` of the map with its objects (+ textures and OBJ with the OBJ option, optional sky dome) | The `.glb` in Blender: it becomes a **new stage**; the textures |
| Effects | `textures\` (PNG, `textures\shared\` = shared effects the unit uses), `particles\NN_<name>.json` + `.efxb` (+ optional ready-to-open `.blend`), 3D effect meshes as `.glb` | The PNGs and the values in the `.json` (see below) |

- *Extract all versions* exports every file of a unit (a recolor of one version doesn't change the others).
- **Mobile suits: bones** (option *Include the bones (skeleton)…*, off by default). The `.glb` also gets the unit's skeleton as an armature with the game bone names (`BASE`, `KOSHI`, `ATAMA`, `TE_L`…). The body is skinned to it with its game weights, and the hand parts follow their hand bone. In Blender you can pose the model to check how it moves, or repaint the weights (**Weight Paint**). When you import the `.glb` back, the body uses the weights from the `.glb` (the heaviest bone of each vertex, like the game); posing the armature changes nothing in the mod. Every other part with bones of its own (a second form such as a mobile armor mode, the damaged body, an assist unit, weapons with moving pieces like claws, legs or shields) gets **its own armature**, named `EXVS bones|<part>`, next to the body. The model is at the real game size (1:1: a mobile suit is about 17 units tall).
- **Mobile suits: animations** (option *Include the animations…*, off by default; it also adds the bones). The `.glb` gets every move of the unit (about 250-450: walks, boosts, shots, melee stages, hit reactions...) as separate animations named like the game files (`landlong_stk_gnd_fr`, `40kaky10a_stk_air_fr`...). The first one, **0 T-pose**, is the game's rest pose: the model opens standing in a T-pose instead of in the middle of a move, and picking it again puts the pose back. In Blender they are Actions of the armature: pick one in the **Action Editor** / **Nonlinear Animation** editor and press Space. They play at the game's 60 fps (set the scene to 60 fps to see the real speed). The other armatures get their own moves too: a second form plays its own moves (e.g. the mobile armor moves), and weapons with moving pieces open, fold or swing. A weapon held in a hand is put in that hand for the move; the others stay lined up next to the body. In Blender 4.4 and later one Action holds the move for every armature: pick the Action and its slot (the armature's name) on each armature you want to see. A form that uses the same bones as the body (e.g. a Z'Gok form) has no moves of its own in the game: give it any body Action. Extract only: edited animations cannot be put back into the game.
- **Mobile suits: hitboxes and hurtboxes** (option *Include the hitboxes and hurtboxes…*, adds the animations). Each melee hit of the unit becomes a red see-through sphere (the game's hit spheres: position, size and the bone they follow) that only shows on the frames where the hit is active, inside the same Action as the move. They are extra bones of the armature, so picking the move's Action on the armature is enough to see them. The **hurtboxes** (where the unit can be hit) are blue spheres on the hands, feet, chest and waist bones: always shown, they follow the pose of every move. Shots and thrown weapons are not included.
- **Mobile suits: ready-to-open .blend** (option *Make ready-to-open .blend files…*, uses your Blender, found by itself or picked with **Blender…**). Next to the `.glb` you also get a `.blend` with the scene at 60 fps and the objects sorted in collections: **Skeleton**, **Body** (with the spare hands), **Other forms** (second form, damaged body...), **Weapons** (also assists), **Hitboxes**, **Hurtboxes**. The bones show as plain Blender bones of an even size. If you import a `.glb` by hand (File > Import > glTF), tick **Disable Bone Shape** in the import options, or Blender draws a sphere per bone sized from its guessed length. Click the eye or the tick of a collection in the Outliner to show or hide that whole group. Every armature starts in the **0 T-pose**; to pose the unit, open the **Animation** tab at the top, select the armature and pick a move in the **Action Editor** list (the timeline is long enough for any move). For mobile suits this option always includes the skeleton, the animations and the hitboxes / hurtboxes (the .blend is for watching the unit move).
- **Stages: collision and spawn points** (option *Include the collision…*, on by default). The `.glb` also gets the game's real collision as see-through objects. These are the heights where units really stand, which can differ from what you see:
  - `COL_ground_floor` (green) and `COL_ground_wall` (red) are the terrain. `COL_ground_tXXXX` (blue) are other surface types.
  - `COL_area_limit_wall` is the invisible edge of the play area.
  - Each building's collision (`COL_<building>_…`) is inside that building, so it moves with it.
  - Yellow markers `REFERENCE_start_N_team1/2` are the start positions (each N is one start variant). Cyan `REFERENCE_respawn_NN` are the respawn drop points.
  - To hide them in Blender, select the `COL_` objects and press **H**.
  - **Editing the floor height:** move the vertices of `COL_ground_…` (or `COL_area_limit_…`) and import the `.glb` as usual. The Mod Manager rebuilds that collision. Unchanged collision is left exactly as in the game.
- **Effects: change their look.** Two things can go back into the game:
  - **Textures:** recolor the PNGs in `textures\` (keep name and size). PNGs in `textures\shared\` belong to the **shared** effects file: changing one changes that effect for **every** unit (thrusters, hits, explosions...). To edit the shared effects directly, extract **Shared effects** (top of the list).
  - **Values:** open a `particles\NN_<name>.json` in any text editor (Notepad works). At the top, `"tint": [1.0, 1.0, 1.0, 1.0]` multiplies the color of the whole effect (red, green, blue, and the last one is the brightness: e.g. `[0.3, 1.0, 0.4, 1.0]` turns a pink beam green, `[1, 1, 1, 2]` makes it twice as bright) and `"size": 1.0` its size. Each emitter has `life` (frames: 60 = 1 second), `count`, `size`, `rotation` and the tracks: lists of `[% of the life, value]` for `red`/`green`/`blue`/`alpha` (above 1 = brighter glow), `scale_x/y/z`, `rot_*`, `vel_*`. You can change values and add or remove keys. Don't change `kind`, `children`, `mesh` or `textures` (they are ignored). If you made the `.blend` files, import the edited `.json` again in Blender (**File > Import > EXVS effect**) to preview it. Experts can also replace the `.efxb` itself.
  - Then **Make a mod from my edits…** as below. The game file is remembered in `effects.json` (extract again with this version if the Mod Manager says the folder is from an older one).
- **Rescan game files** rebuilds the catalog (needed after adding clones).

#### Edit textures while looking at the 3D model
The unit `.glb` doesn't carry its color, AO and emissive textures inside: it **links to the extracted PNGs** (`0xFILE\tex_NN_…png`, same names in Blender). Keep the `.glb` next to its `0xFILE` folder.
- **Paint on the model in Blender:** open the `.glb` and go to the **Texture Paint** workspace. Pick the texture in the image editor (they are named `tex_NN_…`) and paint. Then use **Image → Save All Images**. The PNGs are updated directly.
- **Edit in another program** (Photoshop, GIMP, Krita…): save the PNG, then in Blender press **Alt+R** (Image → Reload) to see it on the model.
- Normal and metal/roughness maps are shown on the model but stay inside the `.glb`, because the game stores them in a different layout. To change them, edit their PNGs in the `0xFILE` folder.

**Create ▾ → Edit a 3D model in Blender** works the same way: the PNGs are saved in `mods\<mod>\_blender\0xFILE\`, and **Import from Blender** also takes the textures you painted.

#### Make a mod from what you extracted
1. Extract, then edit:
   - **PNGs:** keep the same name and size. They can be any format (BC7, BC1, BC3, BC4, BC5, RAW). Leave the ones you don't change as they are.
   - **Unit `.glb`:** in Blender, keep the object names; same rules as [6.9](#69-edit-a-units-3d-model-in-blender). Export it as **glTF Binary (.glb)** over the same file.
   - **Stage `.glb`:** in Blender, change whatever you want; same rules as [6.10](#610-make-a-new-stage-in-blender) (1 m = 10 units, `COL_` / `NOCOL_` prefixes). The sky dome, if you extracted it, has no collision. If the `.glb` has the extracted `COL_…_floor` / `COL_…_wall` objects, **only those** are solid (exactly as you leave them). Your other objects are then only visible: to make one solid, duplicate it and rename the copy `COL_<name>_floor` or `COL_<name>_wall`.
2. Click **Make a mod from my edits…** (in the Extract tab) or **Create ▾ → Mod from extracted files (Extract tab)…**, pick the extracted folder (or a folder that contains several), and type a mod name. Use the name of an existing mod to add the changes to it.
3. The Mod Manager compares everything with the game and keeps only what you changed: edited PNGs, changed meshes and effects as `.bpatch`, and an edited stage as a new stage. Turn the mod on and apply. Use **Mode…** to make a unit mod a new character.

### Sounds
Listen to, export and replace pilot voices, navigator voices, mobile suit sounds and the music (BGM). See [6.12](#612-change-voices-and-mobile-suit-sounds) and [6.15](#615-change-the-music-bgm).

### Movesets
Pick a mobile suit to see its moveset, weapons, damage, cancel routes and sample combos. Everything is read **from your game files**, with arcade button icons. **Export .md** saves it to `movelists\`.

---

## 10. Folders and files

| Path | Contents |
|---|---|
| `mods\<mod>\` | Installed mods |
| `mods\<mod>\_cache\` | Encoded textures (safe to delete; they're rebuilt on the next Apply) |
| `mods\mod_manager.json` | Mod Manager state (enabled mods, order, what was applied) |
| `mods\_exported_zips\` | Zips created with *Export as .zip* |
| `mods\_zips_installed\` | Zips that were already installed |
| `mods\_mod_server\` | Data of the online mod server (host) |
| `mods\_sync.log` | Online sync log |
| `backup_mods\original_fhm2d\` | **Original copies** of every game file a mod ever touched. **Don't delete.** |
| `backup_mods\original_exe\` | Original game exes (for clones and game patches). **Don't delete.** |
| `backup_mods\original_waveform\` | Original copies of every voice file a sound mod touched, and in `BGM\` the original header and overwritten songs of each music file. **Don't delete.** |
| `mods\<mod>\waveform\…`, `mods\<mod>\0x…\snd_NN\` | The WAV files of a sound mod (voices and music in `waveform\voice\` / `waveform\BGM\`, mobile suit sounds in `snd_NN\`) |
| `data\x64\dplcache_release\` | The game's data files (written by Apply) |
| `data\x64\091waveform\voice\` | Pilot and navigator voices (written by Apply when a sound mod is on) |
| `data\x64\091waveform\BGM\` | The music (written by Apply when a sound mod with music is on) |

---

## 11. Troubleshooting & limits

| Problem | Cause / fix |
|---|---|
| Apply fails with "file in use" / permission errors | Close the game (and the launcher) first. |
| `tex_… skipped (sub-file N is not a supported texture)` | That sub-file isn't a texture, or it's an environment map (can't be imported). Check the `NN` in the name. |
| `skipped (name must be tex_NN_...)` | Don't rename the exported PNGs. |
| `clone_art\x.png skipped (must be WxH)` | The art must be exactly the size of the original image. |
| `.bpatch skipped` | The patch was made from a different version of the file than yours. |
| A recolor only shows on some versions of the unit | The unit has several game files; include all of them in the mod. |
| More than 8 clones or 8 new stages | Not supported. Turn some off. |
| `….wav skipped (unsupported WAV format …)` | Save the file again as a 16-bit PCM WAV. MP3/OGG are not accepted: convert them to WAV first. |
| `….wav skipped (no sound N …)` | Don't rename the exported WAVs: the number at the start says which sound it replaces. |
| Online match freezes on the loading screen | The players don't have the same gameplay mods. Sync with the host. |
| I want the original game back | Turn every mod off, choose no translation, and click **Apply changes**. |

**Limits to know**
- Clones share the original unit's sounds, voice, effects and animations, plus its special C++ gimmicks. A clone whose mod changes the effects, the mobile suit sounds or the pilot voice gets its own copy of them.
- New stages keep the base stage's collision unless the mod includes new collision.
- The game can't be modded while it's running. Always apply first, then play.

---

## 12. Appendix: creating .bpatch files and naming every file

### 12.1 What a .bpatch is
A `.bpatch` turns one **original** block of bytes into your **modified** version. It stores only the differences: "copy these bytes from the original" plus "insert these new bytes". That keeps it small, and since it holds no full game files, it can be shared.

Every patch contains the SHA-1 of the original it was made from and the SHA-1 of the expected result. When you Apply, the Mod Manager checks both:
- If your original file isn't the one the patch was made for, the patch is skipped (`the game file is not the version this patch was made for`).
- If the result isn't byte-identical to what the author had, the patch is skipped (`patch result does not match`).

So a patch can never write a half-broken file.

There are two kinds:

| File | Patches | When to use it |
|---|---|---|
| `sub_NN.bpatch` | **One sub-file** (number `NN`) of a `.fhm2d` | Your edit **replaces** sub-files: a new mesh, texture, effect or table. Sub-files can change size. |
| `full.bpatch` | The **whole** `.fhm2d` | Your edit **adds or removes sub-files**, or changes the package index/resource tree (e.g. new objects in a stage). |

### 12.2 Folder and file names

```
mods\
  <Mod name>\                      ← any name (it's the folder; the list shows "name" from mod.json)
    mod.json
    0x7B7EAEC9\                    ← EXACT game file name without ".fhm2d": "0x" + 8 hex digits
      sub_00.bpatch                ← patch for sub-file 0
      sub_71.bpatch                ← patch for sub-file 71
      sub_105.bpatch               ← 3 digits once past 99
      tex_09_1024x1024_BC7.png     ← PNGs can live next to patches
    0xA0308811\
      full.bpatch                  ← whole-file patch (exactly this name)
```

Rules:
- **Game file folder:** `0x` followed by exactly **8 hex digits**, matching the file in `data\x64\dplcache_release\` (e.g. `0x7B7EAEC9.fhm2d` → folder `0x7B7EAEC9`). Uppercase is recommended (zip installs convert it), but lowercase works too. Any other folder name is ignored.
- **Sub-file patch:** `sub_<number>.bpatch`. The number is the **sub-file index inside the .fhm2d, counting from 0**. It's the same number as in `tex_NN_…png`. The Mod Manager writes it with at least 2 digits (`sub_05`), but `sub_5` is read the same.
- **Whole-file patch:** must be named exactly `full.bpatch`. There's only one per game file folder.
- Anything else in the folder (other names, `.fhm2d` copies, notes) is ignored by Apply and left out of zips.

### 12.3 How to know a sub-file's number
You normally **don't need to**: *Mod from modified .fhm2d files* compares the files and names the patches for you. If you want to know what's inside a file:
- **Textures:** export the unit in the *Extract models & images* tab. Each texture comes out as `tex_NN_WxH_FMT.png`, where `NN` is the sub-file number, and `texture_names.txt` lists the in-game name of each one.
- **Other sub-files** (meshes, skeletons, materials, tables…): the number is the sub-file's position in the package index. Other tools may number or sort sub-files differently, so don't rename their output by hand. Let the Mod Manager compare the files instead.

### 12.4 Creating .bpatch files in the Mod Manager
Everything is done from the Mod Manager window.

1. **Have the untouched original.** The Mod Manager compares against `backup_mods\original_fhm2d\0xXXXXXXXX.fhm2d` if it exists; otherwise it uses the file in the game folder (and backs it up first). **That file must still be the original**, so don't overwrite game files by hand before making the mod.
2. **Edit a copy** of the file with your tool, somewhere outside the game folder (e.g. `C:\my_edits\`). Keep the name `0xXXXXXXXX.fhm2d`, because the name is how the Mod Manager knows which game file it is.
3. **Create ▾ → Mod from modified .fhm2d files (.bpatch)…** → select one or more edited files.
4. **Choose how to save the changes:**

   | Option | What it creates | When |
   |---|---|---|
   | **Automatic (recommended)** | `sub_NN.bpatch` for each changed sub-file. If sub-files were **added or removed** (or the package can't be read sub-file by sub-file), it switches to `full.bpatch` by itself and says so in the log. | Almost always. |
   | **Whole file** | Always one `full.bpatch` of the whole .fhm2d. | The tool changed the package **index** but kept the same number of sub-files (e.g. moved objects in a stage tree), and the automatic mode didn't work in the game. |

5. **Type the mod name.** A new name creates `mods\<name>\` with a basic `mod.json`. The **name of an existing mod** adds these files to it, for example to add a model patch to a recolor. For each file you pick, its old `.bpatch` files in that mod are replaced, and its PNGs are kept.
6. The ACTIVITY log shows what was saved. For example:
   ```
   0x7B7EAEC9 sub-file 71: 182400 -> 240128 bytes (patch 35 KB)
   0xA0308811: different number of sub-files (57 vs 77) -> whole-file patch (full.bpatch)
   0xA0308811 whole file -> full.bpatch: 11780604 -> 3181482 bytes (patch 477 KB)
   ```
   Files identical to the original are reported as "nothing to keep". Every patch is verified right after it's created: applied to the original, it must give back exactly your file.
7. Turn the mod on → **Apply**. You can delete your edited `.fhm2d` copies afterwards; the mod doesn't need them.

> 💡 If a whole-file patch comes out almost as big as the file, the log warns you. It means the tool recompressed the entire package, so every byte changed. The mod still works, it's just big. Tools that keep unchanged chunks as they were give much smaller patches.

### 12.5 Notes on whole-file patches
- They're made against the **whole original file**, so they only work on exactly that version of the game file.
- The modified file must be a valid `.fhm2d` the game can load. The patch reproduces your bytes exactly; it doesn't check or fix the package.
- Big files are fine: a 337 MB stage file with 5 MB of changes is patched in about 4 seconds (patch ≈ 5 MB).
- When a file has **only** a `full.bpatch` (no `sub_NN` or PNGs from any mod), Apply writes the patched file directly without reading its index. That's what lets it work with the very large stage files.

### 12.6 Order and combining
When several things change the same game file, Apply builds it in this order:

1. Start from the original in `backup_mods\original_fhm2d\`.
2. Apply the **`full.bpatch`** of each enabled mod, in list order.
3. Apply each mod's **`sub_NN.bpatch`** files, then its **PNGs**, in list order. Patches and PNGs of a later mod replace the same sub-file from an earlier one (lower in the list wins).
4. Fix the package index if sizes changed, then verify every replaced sub-file.

Consequences:
- A `sub_NN.bpatch` is checked against the sub-file **as it is after the full patches**. If another mod's `full.bpatch` changed that sub-file, your sub-file patch is skipped. Two mods with a `full.bpatch` for the same file usually can't be combined either, because the second one no longer sees the original.
- Within one mod, a PNG and a patch for the same sub-file: the PNG wins.
- Clone mode works with patches too: the clone gets its own copy of the model (and of the effects and 2D art files, if the mod changes them).

### 12.7 Sharing
**Export as .zip** includes every `sub_NN.bpatch` and `full.bpatch` together with changed PNGs and `mod.json`. When someone installs the zip, only these names are extracted: `0xXXXXXXXX/sub_N.bpatch`, `0xXXXXXXXX/full.bpatch`, `0xXXXXXXXX/tex_…png`, `mod.json`, `preview.*`, `readme.txt`, `clone_art/ms_*.png`, `stage_art/(ms|vs)_*.png`. A file with any other name is silently dropped.

The patch only works for players whose game file matches the original you used (same game version, same SHA-1). With a different version, Apply skips the patch and says so in the log.
