# Mod Structure

Good organisation is inhherent to any well made mod. It is important to set up your mods in an orderly way to save yourself and others great pain.

## Mod Definition

Every lua mod needs what is called a 'mod definition file' in order to be loaded, and thus to work. This is covered in-depth in the [Mod Definition](./moddefinition.md) section.

This file will point to all the Lua scripts you have written, and where they need to be inserted into PAYDAY's own Lua.

It is either named `mod.txt` if hooking using SuperBLT, or `mod.xml` if hooking using BeardLib.

## Hooks

These are the files which contain the code you are 'injecting' into PAYDAY. It is important to either have descriptive names that show what the script does, such as `disable_hwn_flashlights.lua`.

Alternatively, for multi-function mods which hook into many files, naming files what they hook into, such as `blackmarkettweakdata.lua` should suffice.

## Assets

Some mods will add things like models or textures into the game, alongside Lua scripts. These should be separate from other files for (hopefully) obvious reasons.

## Examples

For a mod that disables halloween flashlights:
```
disable_halloween_flashlights
├── hooks
│   └── disable_hwn_flashlights.lua
└── mod.txt
```

For a mod that adds a new flashlight attachment to weapons:
```
new_flashlight_attachment
├── assets
│   └── units
│       └── mods
│           └── weapons
│               └── wpn_fps_upg_fl_new
│                   ├── wpn_fps_upg_fl_new.cooked_physics
│                   ├── wpn_fps_upg_fl_new.model
│                   ├── wpn_fps_upg_fl_new.object
│                   └── wpn_fps_upg_fl_new.unit
├── hooks
│   └── weaponfactorytweakdata.lua
├── scripts
│   └── add_assets.lua
└── mod.txt
```
