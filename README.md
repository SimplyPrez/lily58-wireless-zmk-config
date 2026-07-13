# zmk-config — Lily58 (nice!nano v2)

Colemak-DH coding keymap tuned for Vim / Python / C. Six layers:
`BASE · SYM · NUM · NAV · MEDIA · FUN`, home-row mods, and combos for
`-> == != :: :=`.

## Repo layout
```
config/
  lily58.keymap   # layers, home-row mods, combos, macros
  lily58.conf     # Kconfig (BLE power, sleep, optional display)
  west.yml        # pulls in ZMK
build.yaml        # GitHub Actions build matrix (one .uf2 per half)
```

## First-time setup
1. Create a new **empty GitHub repo** and drop these files in at the paths shown.
   (Or start from `zmkfirmware/unified-zmk-config-template` and replace its
   `config/` + `build.yaml` with these.)
2. Push. The included GitHub Actions workflow from the template builds on every
   commit; grab `lily58_left.uf2` and `lily58_right.uf2` from the run artifacts.
   - If you started from a bare repo, also copy `.github/workflows/build.yml`
     from the template so Actions runs.
3. Flash each half: double-tap reset on the nice!nano, then drag the matching
   `.uf2` onto the `NICENANO` USB drive.

## Tuning notes
- Mod misfires while typing fast → raise `require-prior-idle-ms` in the `hm`
  behavior (150 → 200) before anything else.
- Accidental taps on the thumb layer keys → switch those `&lt` to a
  `hold-preferred` variant.
- Verify the combo `key-positions` render where you expect with
  [keymap-drawer](https://github.com/caksoylar/keymap-drawer):
  `keymap parse -z config/lily58.keymap | keymap draw - > keymap.svg`.

## Porting to Corne / Totem
Same six layers. Add each board's own `config/<board>.keymap` with the number
row / outer column / 4th thumb dropped, recompute combo positions (the totals
differ), and uncomment the board in `build.yaml`.
