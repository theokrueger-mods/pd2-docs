# QuickMenu

[QuickMenu](https://gitlab.com/znixian/payday2-superblt-lua/-/blob/master/req/utils/QuickMenu.lua) is a class included in the SuperBLT basemod that allows easy creation and display of small menus or popups.

EXAMPLE IMAGE HERE

----

## Create the QuickMenu

#### `QuickMenu:new(title, message[, options][, show_immediately])`
xs
Creates a QuickMenu using the provided `title`, `message`, and `options` and returns it as a class variable. Will display the menu immediately if `show_immediately` is set to `true`.

**Parameters**

`title`: The display title of the menu. This string is not automatically localised.

`message`: The message to be displayed in the menu. This can be a multiline string. This string is not automatically localised.

`options`: An array of options containing data to use for the options of the menu. Specifying a nil value or an empty array will create a localised default 'OK' button.

`show_immediately` If this QuickMenu should pop-up immediately without requiring the menu to be stored and have `show()` expressly called on it.

`returns` A QuickMenu object.

**Options data**

The `options` array should be a 2D array containing arrays of options. The values that can be specified are as follows:

`text` The text to display on this button. This string is not automatically localised.

`callback` The callback function to run if this button is pressed by the user.

`is_cancel_button` If this button should do nothing other than close the menu.


**Example QuickMenu**

```lua
local menu_title = 'Mod or Menu Title'
local menu_message = 'This text shows what the menu does'
local menu_options = {
        [1] = {
                text = 'Open the SuperBLT mod updater',
                callback = LuaModUpdates.OpenUpdateManagerNode,
        },
        [2] = {
                text = 'Close the menu',
                is_cancel_button = true,
        }
}
-- creates a new QuickMenu object and shows it immediately, but does not store it as a variable.
QuickMenu:new(menu_title, menu_message, menu_options, true)
```

If your mod uses localisation/internalisation, you can use `managers.localization:text('my_string_id')` to use the correct language. See [localisation](./localisation.md] for more information.

### Change visibility of the QuickMenu

#### `QuickMenu:show()`

For older mod compatibility, this can also be called with `QuickMenu:Show()`

Displays the specified QuickMenu to the user.

```lua
local mymenu = QuickMenu:new(
        'My Menu Title',
        'A test message',
        -- empty or nil options array means the menu has a default 'OK' button
        {}
)
mymenu:Show()
```

#### `QuickMenu:hide()`

For older mod compatibility, this can also be called with `QuickMenu:Hide()`

Hides the specified QuickMenu without removing it, so that it can be shown to the user again.  

	local menu = QuickMenu:new( "My Title", "A test message.", {}, true )
	menu:Hide()

# Functional Example

**[DOWNLOAD COMPLETE EXAMPLE]()**

This demonstration will open a QuickMenu upon entering the main menu of PAYDAY 2.

```lua
-- hook to '
Hooks:PostHook(
        -- class we hook to
        MenuMainState,
        -- function in that class
        'at_enter',
        -- id / custom name for our addition
        'TEST_mainmenustate_at_enter',
        -- inserted function
        function(...)
                local menu_title = 'QuickMenu example'
                local menu_message = '
                local menu_options = {
                        [1] = {
                                text = 'Open the SuperBLT mod updater',
                                callback = LuaModUpdates.OpenUpdateManagerNode
                        },
                        [2] = {
                                text = 'Close the menu',
                                is_cancel_button = true,
                        }
                }
                local menu = QuickMenu:new(menu_title, menu_message, menu_options)
                menu:Show()
        end
)
```
