# Weapons Reforged

**Weapons Reforged** is a modular overhaul of weapon usability and proficiency rules for the Enhanced Editions and EET.  
It provides a clean, data‑driven framework for universal weapon access, proficiency minimums, class‑restricted proficiency caps, and optional removal of fighting style limits. All components are designed to be interoperable, predictable, and safe for long‑term mod stacks.

This mod does not alter item descriptions, weapon stats, or kit definitions. It focuses exclusively on usability flags and proficiency tables.

Author is /user/celestialfury from Reddit.com. Please contact me for any issues, concerns, questions, improvements, and if the translations are goofy, please let me know with the updated version and I'll correct them.

---

## License

This mod is licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.  
You are free to use, modify, and redistribute this work for any purpose, provided that you give appropriate credit to the original author.

Full license text: https://creativecommons.org/licenses/by/4.0/

## Features Overview

### Core Options
These components modify weapon usability at the item level.

**Remove All Class‑based Restrictions on Weapons (Item Usability)**  
Clears class, race, and kit restrictions from all weapon items while preserving alignment restrictions.  
Uses category‑based detection to ensure only real weapons are affected.

**All Classes Can Use All Weapons (Monks Excluded)**  
Patches `clasweap.2da` so every class except Monks has full access to all weapon categories.

---

## Universal Weapon Options  
(No class restrictions; Monks and Kensai remain restricted)

These components enforce a minimum proficiency level across all weapon categories.  
Only one option may be installed.

- Minimum 1 Pip (Proficient)  
- Minimum 2 Pips (Specialized)  
- Minimum 3 Pips (Mastery)  
- Minimum 4 Pips (High Mastery)  
- Minimum 5 Pips (Grand Mastery)

Each option:
- Auto‑detects MONK and KENSAI columns  
- Applies minimum pips to all classes except those two  
- Zeroes out obsolete proficiency rows (LARGE_SWORD → MISSILE)  
- Preserves zero values for MONK and KENSAI where appropriate

---

## Enhanced Weapon Options  
(Standard class restrictions preserved)

These components apply minimum proficiency levels while respecting class‑based restrictions.  
Only one option may be installed.

- Maximum 2 Pips (Specialized)  
- Maximum 3 Pips (Mastery)  
- Maximum 4 Pips (High Mastery)  
- Maximum 5 Pips (Grand Mastery)

Each option:
- Detects MONK and KENSAI columns  
- Applies minimum pips only where allowed  
- Preserves class‑restricted zeros  
- Zeroes obsolete proficiency rows for consistency

---

## Fighting Style Proficiency Caps Removed

Removes the default style caps (2/2/2/3) for all classes except Monks and Kensai.  
Applies clean, auto‑detected caps to:

- Two‑Handed Weapon Style  
- Sword and Shield Style  
- Single‑Weapon Style  
- Two‑Weapon Style

---

## Technical Architecture

Weapons Reforged is built on a modular WeiDU architecture:

### Item‑Level Patching
- Category‑based weapon detection  
- Alignment‑preserving usability cleanup  
- Kit usability bytes cleared safely  
- No reliance on item type offsets or regex functions

### Proficiency Table Patching
- Auto‑detection of MONK and KENSAI columns  
- Auto‑detection of weapon row ranges  
- Zeroing of obsolete proficiency rows  
- PRETTY_PRINT_2DA for clean output  
- Fully compatible with EE and EET

### Component Isolation
Each component is self‑contained and uses:
- `REQUIRE_PREDICATE` to prevent conflicting installs  
- `SUBCOMPONENT` grouping for clean UI  
- `BUT_ONLY_IF_IT_CHANGES` for safe patching

---

## Compatibility

**Requires:**  
- BGEE, BG2EE, or EET  
- `clasweap.2da` for universal weapon access components

**Compatible with:**  
- Most item overhauls  
- Most kit/class mods  
- Most proficiency or combat rule mods (load order dependent)

**Not recommended with:**  
- Mods that rewrite `weapprof.2da` after installation  
- Mods that hard‑patch item usability after this mod

---

## Installation

1. Extract the mod folder into your game directory.  
2. Run `setup-weapons_reforged.exe`.  
3. Select the components you want.  
4. Only one Universal Proficiency option may be installed.  
5. Only one Enhanced Weapon Option may be installed.

Uninstall or reinstall through the same executable.

---

## Translation Support

Weapons Reforged includes translations for:

- English  
- French  
- German  
- Italian  
- Polish  
- Portuguese  
- Spanish  
- Ukrainian  

All languages include full component names and error messages.

---

## Development Notes

The mod includes a `/dev` folder with internal mapping resources used during development.  
These files are not required for gameplay and are provided for transparency and future modders.

---

## Credits

**Author:** Celestial Fury  
Best contact: Reddit chat

Thanks to the modding community for documentation, testing, and tool support.

---

## Version History

**v1.0.1**  
Initial release with full modular architecture, universal proficiency system, class‑restricted proficiency system, weapon usability cleanup, and style cap removal.

