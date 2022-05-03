# Mod Definition

The mod definition file, well, *defines* the mod. It provides SuperBLT or BeardLib with the information it needs to properly load the mod you have created.

This portion of the guide covers creating defintion files for SuperBLT, also known as the `mod.txt` file. For BeardLib's `mod.xml`, see [BeardLib](../beardlib/index.md)

## Barebones mod.txt

The `mod.txt` should be in the root of your mod folder for SuperBLT to find it.

It is in `json` formatting and will not load if incorrectly formatted

Here is an example of a very minimal `mod.txt` file:

```js
{
        'blt_version' : 2,
        'name' : 'Disable Halloween Flashlights',
        'author' : 'theokrueger',
        'description' : 'Disables the annoying green halloween flashlight on all levels.',
        'version' : '1.2',
        'hooks' : [
                {
                        'hook_id' : 'lib/units/weapons/weaponflashlight',
                        'script_path' : 'hooks/disable_hwn_flashlights.lua'
                }
        ]
}
```

**Parameters**

`blt_version`: not necessary in modern PAYDAY modding, but should be there anyways.

`name`: the name of the mod you wish to show up in your in-game mod list.

`author`: your name or username

`description`: a short description of what your mod does

`version`: the current version of the mod

`hooks`: a list containing every 'hook' you wish SuperBLT to perform. Each 'hook' is a table containing the *source code file* you are changing (`hook_id`) and the path to *your code* (`script_path`).

## Advanced Parameters

`updates`: see [automatic updates](./automatic_updates.md)

`contact`: email, website, or social media for mod users to contact you on

`priority`: see [priority](./priority.md)

`dependencies`: see [dependencies](./dependencies.md)

`image`: path (relative to your mod's folder) to a square image to show as the icon in the SuperBLT mod list

`disable_safe_mode`: TODO

`undisableable`: prevent users from disabling the mod in the SuperBLT mod list

`is_library`: TODO

For the complete functionality of everything listed, browse the [SuperBLT basemod source code](https://gitlab.com/znixian/payday2-superblt-lua)
