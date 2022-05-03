# Writing the Mod

Actually creating the code for the mod is a (mostly) straightforward three step process.

1. Find the code you want to modify
2. Plan the best way to modify said code
3. Execute the plan

Of course, it is never this simple. But following these steps is always a start.

Our example will be the writing of our `disable_hwn_flashlights.lua` previously mentioned

## Finding the Code

Open the [PAYDAY Lua Source code](https://github.com/steam-test1/Payday-2-LuaJIT-Complete) you have downloaded and begin to look for the function that could be linked to teammate flashlights.

**General directory overview**

**`core`**: Core functions to the game, not very useful to newer modders. Contains heavily abstracted interfaces to basic menus, utilities, and the editor.

**`lib`**: The majority of files you will be messing with will be inside here. Its subdirectories are as follows:

`gamemodes`: only contains a few files about basic states, nothing worth touching.

`input`: Handles special functions for controllers and VR. Again, little to mess around with.

`managers`: An incredibly broad folder that contains most code controlling menus, dlc, ai states, achievements, etc.

`modifiers`: Crimespree modifiers

`mutators`: Crime.net mutators

`network`: Networking functions for matchmaking and in-game sync

`player_actions`: Player actions and certain skill upgrades

`setups`: Game setup files

`states`: Different states the game can be in, like menu or ingame

`tweak_data`: Almost every number value is contained in this folder. Stuff like XP multipliers, enemy HP, weapon damage, attachment stats, loot value, everything.

`units`: Units such as players, npcs, drills, deployables, etc

`utils`: Utilities like Base64 encode/decode, telemetry, or other functions that are useful as a library instead of a class


Since what we are looking for, to disable the halloween flashlights, involves a flashlight (which is a Unit), we shold look in the `units` folder. Since its a weapon attachment, we should look in the `weapons` subfolder.

And there seems to be a relevant file! `/lib/units/weapons/weaponflashlight`. We browse this for a bit until we find a function that enables and disables halloween flashlights...

## Editing our code

And we've found the function in `/lib/units/weapons/weaponflashlight` titled `WeaponFlashLight:is_haunted()`

Its code is as follows:

```lua
function WeaponFlashLight:is_haunted()
	local job_id = managers.job and managers.job:current_job_id()
	local tweak = job_id and tweak_data.narrative.jobs[job_id]

	return tweak and tweak.is_halloween_level
end
```

So it looks like if the current `job_id` (taken from `managers.job:current_job_id()`) is part of the `tweak_data` table with every halloween level in it, then the green flashlight is on. If we override the function to always return false:

```lua
function WeaponFlashLight:is_haunted()
    return false
end
```

Then the green flashlight should never be on!

## Testing

Our final structure should look like this:

```
disable_halloween_flashlights
├── hooks
│   └── disable_hwn_flashlights.lua
└── mod.txt
```

And with the hooks properly defined in the mod definition file, we should be ready to test!

In order to see the SuperBLT log in case of any errors, we can create a file called `developer.txt` in the root of PAYDAY 2's `mods/` folder. This will open up a command prompt when you launch the game that the logs will be output to.

You can also see a recent history of all logs by opening the log file located in `PAYDAY 2/mods/logs`

Linux users can either:

1. Close Steam and run it through a terminal
2. run `tail -f` on the log file located in `PAYDAY 2/mods/logs`
3. (If running through Proton) Install the Windows Command Prompt through winetricks and use the `developer.txt` method


At this point our mod should be functional and no errors should be in the SuperBLT log. Congrats on creating your first Lua mod!
