# Weapons Reforged

**A modular overhaul of weapon usability and proficiency rules for Baldur's Gate: Enhanced Edition, Baldur's Gate II: Enhanced Edition, and EET.**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Platform: Windows](https://img.shields.io/badge/platform-Windows-blue)](https://github.com/CelestialFury-BG/weapons-reforged/releases)
[![Games: BGEE | BG2EE | EET](https://img.shields.io/badge/games-BGEE%20%7C%20BG2EE%20%7C%20EET-red)](https://github.com/CelestialFury-BG/weapons-reforged/releases)
[![Latest Release](https://img.shields.io/github/v/release/CelestialFury-BG/weapons-reforged?color=gold)](https://github.com/CelestialFury-BG/weapons-reforged/releases/latest)

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
- WeiDU 24600+ recommended.

### Steps

1. **Extract** the `weapons_reforged` folder into your game directory.
2. **Run** `setup-weapons_reforged.exe`.
3. **Select** the components you want.
4. **Only one Universal Proficiency** option (2–6) may be installed.
5. **Only one Class-Restricted Proficiency** option (7–10) may be installed.
6. Sections 1 and 4 are optional and combine freely with the pip options.

Uninstall or reinstall using the same executable.

### Recommended Install Order

Weapons Reforged should be installed **after** item/content mods but **before**:

- **Sword Coast Stratagems** (`stratagems`)
- **Tweaks Anthology** (`cdtweaks`)
- **EET_End** (`eet_end`)

If you use item-pack mods (weapon additions, item overhauls) that add new weapons to the game, install those **first** so the usability cleanup catches the new items.
