# Preserving Previous Functionality

Say we are trying to modify a tiny portion of a much larger function. It could work to entirely copy the function and just change the lines we want to, but if another mod ever touches that function, or if the game updates and that function is changed, issues will arise.

When changing the function, we have three options to change what it does:

1. Completely overwrite it
2. Prepend or append code
3. Use a SuperBLT Hook function

They function as follows:

## Overriding a Function

This is generally bad practise when writing mods for PAYDAY. It completely overwrites the function with your own

If we wanted to increase the number of infamy ranks, we would have to modify the function

```lua
function InfamyTweakData:init()
         -- lots of original code
         (...)

         -- our change
         self.ranks = 501
end
```

In `lib/tweak_data/infamynewtweakdata.lua`. Open this file yourself, and you would see that to override this function completely just to change one value (number of infamy ranks), we would have to paste *over 1300* lines of code.

We could just paste the whole thing and change our one line `self.ranks` to `501` or whatever. This is completely suboptimal because if this function is ever modified by the developers or any other modder, it will probably cause issues.

Instead, we can use a Lua technique called 'oldinit'

## The oldinit

Lua has many fun tricks you can pull off due to its immense flexibility. One such thing is saving an entire function to a variable, then changing the function

In our infamy example, the code would look like this:

```lua
-- store old function as a variable
local old_infamytweakdata_init = InfamyTweakData.init

-- overwrite the function
function InfamyTweakData:init()
         -- execute old, stored function
         old_infamytweakdata_init(self)

         -- our change
         self.ranks = 501
end
```

This version is much more resistant to tampering from other mods or developer updates. But there is an even better way still.

## SuperBLT Hooks

It should work fine if you have a ton of these oldinit functions stacked on top of eachother, but so many nested functions and duplicated variables can cause performance or loadtime issues.

SuperBLT has built-in functions to help prevent this:

`Hooks:PostHook(...)` allows you to execute a block of code *before* the original function

`Hooks:PostHook(...)` allows you to execute a block of code *after* the original function

Here is our infamy example as a `PostHook`

```lua
Hooks:PostHook(
         -- class we hook to
         InfamyTweakData,
         -- function in that class
         'init',
         -- id / custom name for our function
         'add_infamy_ranks',
         -- inserted function
         function(self)
                  -- put our code here
                  self.ranks = 501
         end
)
```

This has the main disadvantage of **not being able to change the return value**. If you need to change the return value, try to use an 'oldinit'

Read the [vanilla BLT's documentation](https://payday-2-blt-docs.readthedocs.io/en/latest/lua/hooks/) to learn more.
