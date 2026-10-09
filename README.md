# Weapons Reforged

**A modular overhaul of weapon usability and proficiency rules for Baldur's Gate: Enhanced Edition, Baldur's Gate II: Enhanced Edition, and EET.**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Platform: Windows | macOS | Linux](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-blue)](#installation)
[![Games: BGEE | BG2EE | EET](https://img.shields.io/badge/games-BGEE%20%7C%20BG2EE%20%7C%20EET-red)](#requirements)
[![Latest Release](https://img.shields.io/github/v/release/CelestialFury-BG/weapons-reforged?color=gold)](https://github.com/CelestialFury-BG/weapons-reforged/releases/latest)
[![Components: 12](https://img.shields.io/badge/components-12-brightgreen)](#component-reference)

---

## What It Does

Weapons Reforged provides a clean, data-driven framework for modifying how weapons and proficiencies work in the Enhanced Edition games:

- **Universal weapon access** — clear class, race, and kit restrictions at the item level.
- **Universal proficiency minimums** — raise every class to at least N pips in every weapon category.
- **Class-restricted proficiency minimums** — raise only the pips a class is already allowed to use, preserving restrictions.
- **Fighting style cap removal** — unlock Two-Handed, Sword & Shield, Single-Weapon, and Two-Weapon styles beyond the vanilla caps.

Every component is self-contained and safe for large mod stacks. Weapons Reforged does **not** alter item descriptions, weapon stats, or kit definitions. It only touches usability flags and the `weapprof.2da` / `clasweap.2da` tables.

> **Concept inspiration**: Ashes of Embers by Ghreyfain.

---

## Component Reference

Weapons Reforged ships **12 components** across **4 sections**. Only one option from the Universal group and one option from the Class-Restricted group may be installed at a time.

### Section 1 — Core Rules

| # | Component | Effect |
|---|-----------|--------|
| **0** | Remove All Class-based Restrictions on Weapons (Item Usability) | Clears class/race/kit restrictions from every weapon item. Preserves alignment restrictions. Category-based detection so only real weapons are affected. |
| **1** | All Classes Can Use All Weapons (Monks Excluded) | Patches `clasweap.2da` so every class except Monks has full weapon access. |

### Section 2 — Universal Proficiency Minimums

Raises **every class's** proficiency to at least N pips. Monks and Kensai excluded — their zero entries are preserved.

**Only one may be installed.**

| # | Component | Effect |
|---|-----------|--------|
| **2** | Minimum 1 Pip (Proficient) | Every class gets at least 1 pip in every weapon. |
| **3** | Minimum 2 Pips (Specialized) | Every class gets at least 2 pips. |
| **4** | Minimum 3 Pips (Mastery) | Every class gets at least 3 pips. |
| **5** | Minimum 4 Pips (High Mastery) | Every class gets at least 4 pips. |
| **6** | Minimum 5 Pips (Grand Mastery) | Every class gets 5 pips in every weapon. |

### Section 3 — Class-Restricted Proficiency Minimums

Raises proficiency **only for classes that can already use** a given weapon. Class restrictions are preserved — a class that was forbidden from a weapon stays forbidden.

**Only one may be installed.**

| # | Component | Effect |
|---|-----------|--------|
| **7** | Minimum 2 Pips (Specialized) | Allowed weapons raised to at least 2 pips. |
| **8** | Minimum 3 Pips (Mastery) | Allowed weapons raised to at least 3 pips. |
| **9** | Minimum 4 Pips (High Mastery) | Allowed weapons raised to at least 4 pips. |
| **10** | Minimum 5 Pips (Grand Mastery) | Allowed weapons raised to 5 pips. |

### Section 4 — Fighting Style Caps Removed

| # | Component | Effect |
|---|-----------|--------|
| **11** | Fighting Style Proficiency Caps Removed | Removes vanilla caps (2/2/2/3) for all classes except Monks/Kensai. Applies clean, auto-detected caps to Two-Handed (2), Sword & Shield (2), Single-Weapon (2), and Two-Weapon (3) styles. |

---

## Installation

### Requirements

- **BGEE**, **BG2EE**, or **EET** (Enhanced Edition games only — not compatible with classic BG/BG2).
- `clasweap.2da` must be present (standard in all EE installs).
- WeiDU 24600 or higher (bundled with the mod).

### Windows

1. Download the latest release from the [Releases page](../../releases/latest).
2. Extract the archive into your game directory (the folder containing `Baldur.exe`).
3. Run `setup-weapons_reforged.exe` and follow the installer prompts.

If `setup-weapons_reforged.exe` is not included in the archive, copy `weidu.exe` from your game folder and rename the copy to `setup-weapons_reforged.exe`, then run it.

### macOS / Linux

1. Extract the mod folder into your game directory.
2. Open a terminal in that directory and run:

       weidu --install weapons_reforged.tp2

### Project Infinity

Import the `.iemod` file directly, or point PI at the extracted mod folder. The mod ships with `weapons_reforged.ini` metadata so PI will detect the components automatically.

---

## Recommended Install Order

Weapons Reforged patches three different tables, and install position affects each one differently. There is **no single correct position** — the right choice depends on what you want the mod to do.

### What Each Patch Is Sensitive To

| Patch | Table | Install-position sensitivity |
|-------|-------|------------------------------|
| Item usability cleanup | `.*\.itm` | Patches only items that exist at install time |
| Class weapon access | `clasweap.2da` | Patches only class rows that exist at install time |
| Proficiency minimums | `weapprof.2da` | Determines which proficiency system wins per cell |

The first two favor **late installation**. The third is a philosophy choice — it depends on whether you want Weapons Reforged's pip changes or another proficiency mod's changes to be authoritative.

### Two Valid Approaches

**Approach A — Install late (recommended for most users)**

Install Weapons Reforged near the end of your install order, after item, weapon, and kit mods but before EET_End.

This approach ensures:

- **Every weapon is caught.** Weapons Reforged's item usability cleanup runs over the final `override/`, so it clears class/race/kit restrictions from every weapon that every mod has added — not just vanilla ones.
- **Every kit is caught.** Its `clasweap.2da` patch runs over the final class list, so kits added by other mods also receive universal weapon access.
- **Weapons Reforged's pip minimums are the final word.** Any earlier mod's changes to `weapprof.2da` are still present, but Weapons Reforged raises pip values on top of them. The result is the union of both changes.

Use this approach if you want Weapons Reforged to be the authoritative voice on weapon access and pip minimums.

**Approach B — Install early (for users who want another proficiency mod to win)**

Install Weapons Reforged after item mods but before Sword Coast Stratagems and Tweaks Anthology.

This approach is appropriate when:

- You plan to use **Tweaks Anthology's proficiency components** (`#2160`, `#2200`, `#2280`) and want TA's system to be authoritative.
- You plan to use **SCS's IWD-proficiencies component** and want SCS's system to win.
- You plan to use **Combat Skills & Proficiencies**, **Might & Guile**, or **Skills and Proficiencies** and want their proficiency design to override Weapons Reforged's.

The tradeoff: because Weapons Reforged installs earlier, any items or kits added by mods installed *after* it will not receive its usability cleanup or its `clasweap.2da` patch. For most users, that's a meaningful loss for a marginal proficiency-system preference.

### Comparison

| Position | Item usability catches all weapons? | `clasweap.2da` catches all kits? | `weapprof.2da` final word goes to |
|----------|-------------------------------------|----------------------------------|-----------------------------------|
| **Late (Approach A)** | Yes | Yes | Weapons Reforged |
| **Early (Approach B)** | No — only items present at install time | No — only kits present at install time | Whatever proficiency mod installs after it |

### Recommended Sequences

Here are both recommended sequences, output cleanly.

---

**Approach A — Install late (recommended for most users):**

```
1. Item and content mods
2. Sword Coast Stratagems
3. Tweaks Anthology
4. Proficiency-adjacent tweaks
5. Weapons Reforged          <-- install here
6. EET_End
```

**Approach B — Install early (only if you want another proficiency mod to win):**

```
1. Item and content mods
2. Weapons Reforged          <-- install here
3. Sword Coast Stratagems
4. Tweaks Anthology
5. Proficiency-adjacent tweaks
6. EET_End
```

---

If you want a version without the inline comment (some markdown renderers treat `<--` as HTML), use this instead:

**Approach A — Install late (recommended for most users):**

```
1. Item and content mods
2. Sword Coast Stratagems
3. Tweaks Anthology
4. Proficiency-adjacent tweaks
5. Weapons Reforged (install here)
6. EET_End
```

**Approach B — Install early (only if you want another proficiency mod to win):**

```
1. Item and content mods
2. Weapons Reforged (install here)
3. Sword Coast Stratagems
4. Tweaks Anthology
5. Proficiency-adjacent tweaks
6. EET_End
```

The second version is safer for GitHub's markdown renderer, which will pass `<--` through unmodified but could be confused by it in some contexts. Use whichever you prefer — both convey the same install position.





### One Rule That Never Changes

**EET_End is always installed last.** No exceptions. It finalizes the merged EET install, and any mod installed after it will not be seen by the merge process.

### Interaction Notes

| Mod | Interaction |
|-----|-------------|
| **Tweaks Anthology** (`cdtweaks`) | Proficiency components `#2160`, `#2200`, `#2280` patch `weapprof.2da`. Whichever mod installs later wins per cell. |
| **Sword Coast Stratagems** (`stratagems`) | Core AI reads proficiency tables at runtime, so install order is neutral. Only the IWD-proficiencies component patches the table — that one behaves like cdtweaks. |
| **Combat Skills & Proficiencies** | Restructures the proficiency system. Same cell-by-cell tradeoff. |
| **Might & Guile** | Overhauls proficiencies via its own system. Same tradeoff. |
| **Skills and Proficiencies** | Modifies `weapprof.2da`. Same tradeoff. |

---

## Technical Architecture

Weapons Reforged is built on a modular WeiDU architecture. Each component is isolated in its own `.tpa` file:

| File | Purpose |
|------|---------|
| `components/all_weapons.tpa` | `clasweap.2da` patch for universal weapon access |
| `components/class_restrictions_weapons.tpa` | Item-level usability cleanup (categories 15–30, 44, 51, 57) |
| `components/universal_profs_core.tpa` | All-class proficiency minimums with auto-detected MONK/KENSAI columns |
| `components/class_restrictions_pips.tpa` | Class-appropriate proficiency minimums (preserves zeros) |
| `components/style_profs_apply_caps.tpa` | Clean style caps with Monk/Kensai restrictions preserved |
| `components/zero_out_old_profs.tpa` | Zeroes obsolete `LARGE_SWORD` → `MISSILE` rows |

**Safety features baked in:**

- `REQUIRE_PREDICATE` guards against conflicting sub-component installs.
- `SUBCOMPONENT` grouping provides clean mutex UI for proficiency options.
- `BUT_ONLY_IF_IT_CHANGES` prevents unnecessary file writes.
- `PRETTY_PRINT_2DA` keeps resulting 2DA output human-readable.
- Full EET compatibility — safe to install on the BG1 side or BG2 side of an EET merge.

---

## Translations

Weapons Reforged ships with full translations for:

English · Français · Deutsch · Italiano · Polski · Português · Español · Українська

All languages include complete component names and error messages. If you find an awkward or incorrect translation, please open an issue with the corrected `.tra` file — community corrections are welcome and will be included in the next release.

---

## Credits

**Author:** Celestial Fury
**Concept inspiration:** Ashes of Embers by Ghreyfain
**Contact:** Reddit chat — [`/u/celestialfury`](https://www.reddit.com/user/celestialfury)

Thanks to the modding community for documentation, testing, and tool support — Gibberlings3, Spellhold Studios, Beamdog forums, and the wider WeiDU ecosystem.

---

## Links

- [Report a bug or request a feature](../../issues)
- [Contact the author](https://www.reddit.com/user/celestialfury)

---

## Version History

### v1.0.1 — Initial public release

- Full modular WeiDU architecture with isolated component files.
- Universal proficiency system (Min 1–5 Pips).
- Class-restricted proficiency system (Min 2–5 Pips).
- Weapon usability cleanup for all weapon categories.
- Fighting style cap removal.
- Translations for 8 languages.

### v1.0.0 — Internal development build

- Concept validation and initial component structure.

---

## License

Weapons Reforged is licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

You are free to share, remix, and redistribute this mod for any purpose — even commercially — provided you give appropriate credit.

Full license text: <https://creativecommons.org/licenses/by/4.0/>
