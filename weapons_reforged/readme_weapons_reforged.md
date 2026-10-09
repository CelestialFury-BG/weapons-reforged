# Weapons Reforged

**Weapons Reforged** is a modular overhaul of weapon usability and proficiency rules
for Baldur's Gate: Enhanced Edition, Baldur's Gate II: Enhanced Edition, and EET.

It provides a clean, data-driven framework for:

- **Universal weapon access** — clear class restrictions at the item level.
- **Universal proficiency minimums** — raise every class to at least N pips.
- **Class-restricted proficiency minimums** — raise only the classes that can
  already use a weapon, preserving Monk and Kensai restrictions.
- **Fighting style cap removal** — unlock Two-Handed, Sword & Shield,
  Single-Weapon, and Two-Weapon styles.

Every component is self-contained, order-safe, and designed to coexist with the
larger mod ecosystem. Weapons Reforged does **not** alter item descriptions,
weapon stats, or kit definitions. It touches only usability flags and
proficiency tables.

Original concept inspired by **Ashes of Embers** by Ghreyfain.

**Author:** Celestial Fury (Reddit: `/u/celestialfury`)
**Contact:** Please reach out via Reddit chat for issues, feedback, or
translation corrections.

---

## License

This mod is licensed under the **Creative Commons Attribution 4.0 International
License (CC BY 4.0)**. You are free to use, modify, and redistribute this work
for any purpose, provided you give appropriate credit to the original author.

Full license text: <https://creativecommons.org/licenses/by/4.0/>

---

## Component Overview

Weapons Reforged ships twelve components across four sections. Only one option
from the Universal group and one option from the Class-Restricted group may be
installed at a time.

### Section 1 — Core Rules

#### 0. Remove All Class-based Restrictions on Weapons (Item Usability)

Clears class, race, and kit restrictions from every weapon item in the game
while preserving alignment restrictions. Uses category-based detection (weapon
type byte) so only real weapons are affected — armor, shields, and other
equippable items are left untouched.

Patches the usability bits (`0x1e`, `0x2d`) on categories 15–30, 44, 51, and 57.

#### 1. All Classes Can Use All Weapons (Monks Excluded)

Patches `clasweap.2da` so that every class except **Monks** has full access to
all weapon categories. Monk is preserved so that their unique unarmed and
special-weapon progression remains intact.

Requires `clasweap.2da` to be present in the game.

---

### Section 2 — Universal Proficiency Minimums

These components raise **every class's** proficiency in every weapon category
to at least N pips. Monks and Kensai are excluded because their proficiency
tables are intentionally restricted — their zero entries are preserved.

**Only one may be installed.**

| Component | Effect |
|-----------|--------|
| **2. Minimum 1 Pip (Proficient)** | Every class gets at least 1 pip in every weapon. |
| **3. Minimum 2 Pips (Specialized)** | Every class gets at least 2 pips. |
| **4. Minimum 3 Pips (Mastery)** | Every class gets at least 3 pips. |
| **5. Minimum 4 Pips (High Mastery)** | Every class gets at least 4 pips. |
| **6. Minimum 5 Pips (Grand Mastery)** | Every class gets 5 pips in every weapon. |

**How it works:**

- Auto-detects the MONK and KENSAI columns in `weapprof.2da`.
- Raises any non-zero pip value below the target up to the target.
- Preserves Monks' and Kensai's zero entries.
- Zeroes the obsolete `LARGE_SWORD` through `MISSILE` rows (legacy rows no
  longer used by the EE engine).

---

### Section 3 — Class-Restricted Proficiency Minimums

These components raise proficiency only for classes that **can already use**
a given weapon. Weapons a class is forbidden from using stay forbidden — the
restriction is preserved, but the class gets a proper minimum for anything it
can wield.

This is the conservative option: it fills out the proficiency tables without
bypassing class design.

**Only one may be installed.**

| Component | Effect |
|-----------|--------|
| **7. Minimum 2 Pips (Specialized)** | Allowed weapons raised to at least 2 pips. |
| **8. Minimum 3 Pips (Mastery)** | Allowed weapons raised to at least 3 pips. |
| **9. Minimum 4 Pips (High Mastery)** | Allowed weapons raised to at least 4 pips. |
| **10. Minimum 5 Pips (Grand Mastery)** | Allowed weapons raised to 5 pips. |

**How it works:**

- Reads the pip value at each cell. If it is already zero, that class cannot
  use that weapon — the zero is preserved.
- If the value is greater than zero and below the target, it is raised.
- Monks and Kensai are excluded entirely (same rule as Section 2).

> **Note on naming**: An earlier draft of this readme labeled these components
> "Maximum N Pips." The code actually raises pip values, so the correct
> description is "Minimum." The component labels here reflect the code's
> behavior.

---

### Section 4 — Fighting Style Caps Removed

#### 11. Fighting Style Proficiency Caps Removed

Removes the vanilla style caps (2/2/2/3) for every class except Monks and
Kensai, and applies clean, auto-detected caps to:

- Two-Handed Weapon Style → **2**
- Sword and Shield Style → **2**
- Single-Weapon Style → **2**
- Two-Weapon Style → **3**

Monk and Kensai style caps are left untouched, since those kits have
deliberately restricted style progression.

---

## Compatibility

**Requires:**

- Baldur's Gate: Enhanced Edition, Baldur's Gate II: Enhanced Edition, or EET.
- `clasweap.2da` for the universal weapon access component.

**Works well with:**

- Most item overhaul mods (installed **before** Weapons Reforged so that new
  weapons are also covered by the usability cleanup).
- Most kit and class mods.
- Most proficiency and combat-rule mods, provided install order is respected.

**Not recommended with:**

- Mods that rewrite `weapprof.2da` **after** Weapons Reforged — they will
  override its pip changes.
- Mods that hard-patch item usability **after** Weapons Reforged — their
  changes will overwrite the usability cleanup.

**Install order guidance:**

Install Weapons Reforged **before** Sword Coast Stratagems, Tweaks Anthology,
and EET_End. If you also use a mod that adds new weapons (item packs, weapon
additions), install those first so the usability cleanup catches them.

---

## Installation

1. Extract the `weapons_reforged` folder into your game directory.
2. Run `setup-weapons_reforged.exe`.
3. Select the components you want.
4. **Only one Universal Proficiency option** may be installed (2–6).
5. **Only one Class-Restricted Proficiency option** may be installed (7–10).
6. Sections 1 and 4 are optional and can be combined freely.

Uninstall or reinstall using the same executable.

---

## Translation Support

Weapons Reforged ships with translations for:

- American English
- Français
- Deutsch
- Italiano
- Polski
- Português
- Español
- Українська

All languages include full component names and error messages. If a translation
is awkward or incorrect, please send a corrected version and it will be included
in the next release.

---

## Technical Notes

Weapons Reforged is built on a modular WeiDU architecture, with each component
isolated in its own `.tpa` file:

| File | Purpose |
|------|---------|
| `all_weapons.tpa` | Patches `clasweap.2da` to allow all classes (except Monk) to use all weapons. |
| `class_restrictions_weapons.tpa` | Clears item-level class/race/kit restrictions on all weapons. |
| `universal_profs_core.tpa` | Raises all-class proficiency minimums in `weapprof.2da`. |
| `class_restrictions_pips.tpa` | Raises class-appropriate proficiency minimums only where allowed. |
| `style_profs_apply_caps.tpa` | Applies clean style caps, preserving Monk/Kensai restrictions. |
| `zero_out_old_profs.tpa` | Zeroes obsolete `LARGE_SWORD` → `MISSILE` rows in `weapprof.2da`. |

**Safety features:**

- `REQUIRE_PREDICATE` guards against installing conflicting sub-components.
- `SUBCOMPONENT` grouping provides clean mutex UI for the proficiency options.
- `BUT_ONLY_IF_IT_CHANGES` avoids unnecessary file writes.
- `PRETTY_PRINT_2DA` keeps the resulting 2DA output readable.

A `/dev` folder in the source repository contains internal mapping resources
used during development. These files are not required for gameplay.

---

## Credits

**Author:** Celestial Fury
**Concept inspiration:** Ashes of Embers by Ghreyfain
**Best contact:** Reddit chat (`/u/celestialfury`)

Thanks to the modding community for documentation, testing, and tool support.

---

## Version History

**v1.0.1**
- Initial public release with full modular architecture.
- Universal proficiency system.
- Class-restricted proficiency system.
- Weapon usability cleanup.
- Fighting style cap removal.

**v1.0.0**
- Initial development build.
