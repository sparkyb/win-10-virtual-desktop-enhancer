Windows 10 Virtual Desktop Enhancer
===

This application enhances the Windows 10 virtual desktops feature. It makes available the following new features:

- Extra customizable keyboard shortcuts to switch or move a window to a different desktop.
- Customizable keyboard shortcuts to pin a window/all windows for an app to all desktops.
- Custom wallpaper per virtual desktop (either a picture or a solid color).
- Current desktop indicator in the tray area.
- Custom desktop names.
- Tooltips showing the desktop name when switching desktops.

Go to the ["Releases" page to download](https://github.com/sdias/win-10-virtual-desktop-enhancer/releases).

## Installation

This app does not need to be installed, simply extract it into a folder in your computer.

To run this app, just run the "virtual-desktop-enhancer.exe" program.

Alternatively you can install AutoHotkey and run the "virtual-desktop-enhancer.ahk" script file.

This application only works on Windows 10 x64.

### Prerequisites

For this app to work, you first might need to install "Visual C++ Redistributable for Visual Studio 2015".
It should be available [here](https://www.microsoft.com/en-us/download/details.aspx?id=48145).

If you want to run version 0.7.0 or above of this app, you need to have the "Windows 10 Anniversary" update installed.

## Troubleshooting

For version 0.6.2 and below, there is an optional patch you can install that will enable you to use the app in case you don't have the update mentioned above.

## Usage

### Custom Wallpapers Per Desktop

To configure the wallpapers, edit the "settings.ini" file.
For each desktop, you can either set the wallpaper to be an image file or a fixed color.
To use images, set the path of the image, either absolute or relative (ex: "1=C:\wallpapers\1.jpg", "2=./wallpapers/2.jpg").
To use fixed colors, set the color in hexadecimal (ex: "3=0xff0000" for red, "4=0xff00" or "4=0x00ff00" for green).
If you set the config of that desktop to empty (ex: "5=") the wallpaper won't change when you switch to that desktop.
Also note that any number of desktops are supported, just add a line for each new one, like for example:

<pre>
[Wallpapers]
1=C:\Wallpapers\Default.jpg
2=
3=
4=
5=
6=
7=
8=
9=
10=
11=C:\Wallpapers\Work.jpg
12=C:\Wallpapers\Email.jpg
20=
50=
999=C:\Wallpapers\End of the world.jpg
</pre>

### Desktop Names

In a similar manner to wallpapers, you can also set a custom name for each desktop.

<pre>
[DesktopNames]
1=Work
2=Games
3=Movies
4=Presentations
5=
6=
7=
8=
9=
10=
15=No idea
</pre>

Note that the desktop's name will be visible in the tooltip of the tray icon and also in the larger tooltip that appears momentarily when you switch desktops.
If a desktop's name is not set, "Desktop <number>" will be displayed.
Again, like wallpapers, any number of desktops are supported by this feature.

### Tooltips

If you enable tooltips, every time you switch desktops a tooltip will appear letting you know the name of the desktop you switched to.

You can customize the appearance of this tooltip:

| Setting         | Description                                                                               | Valid Values                                   |
| --------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Enabled         | If tooltips should be shown.                                                              | 1 (Yes), 0 (No).                               |
| Centered        | If the tooltips should appear at the center of the screen, or in the bottom right corner. | 1 (center), 0 (corner).                        |
| FontSize        | The size of the font.                                                                     | Any reasonable number.                         |
| FontColor       | The color of the font.                                                                    | Any hexadecimal number (from 0x0 to 0xFFFFFF). |
| FontInBold      | If the font should be in bold.                                                            | 1 (Yes), 0 (No).                               |
| BackgroundColor | The color of the background.                                                              | Any hexadecimal number (from 0x0 to 0xFFFFFF). |
| Lifespan        | The time in milliseconds for which each tooltip will be displayed.                        | Any reasonable number.                         |

As an example, you have the default configuration:

<pre>
[Tooltips]
Enabled=1
Centered=1
FontSize=11
FontColor=0xFFFFFF
FontInBold=1
BackgroundColor=0x1F1F1F
Lifespan=750
</pre>

It draws tooltips at the center of the screen, in a white, bold and small font, with a dark background, and they are displayed for 750 milliseconds.

### Keyboard Shortcuts

There are several actions available that can be bound to keyboard shortcuts. These are:
* Switching to another desktop
* Moving the current window to another desktop
* Moving the current window to another desktop and then switch to that desktop
* Affect the next 10 desktops instead, for any of the actions above

For each of these actions, you can set modifier keys (a combination of one or more keys, out of the `Ctrl`, `Shift`, `Alt` and `Win` keys) and identifier keys (keys to identify the context of the action).
For example: if you want to set up a keyboard shortcut to be able to switch to the next desktop, you need to set up the modifier keys for "switch to another desktop" (for example, `Ctrl + Win`), and also set up the identifier key for "next desktop" (for example, `Right Arrow`).

These are the available keyboard shortcut settings:

| Section                      | Name                         | Description |
| -                            | -                            | - |
| KeyboardShortcutsModifiers   | SwitchDesktop                | Switch to a desktop.                        |
| KeyboardShortcutsModifiers   | MoveWindowToDesktop          | Move the current window to another desktop. |
| KeyboardShortcutsModifiers   | MoveWindowAndSwitchToDesktop | Move the current window to another desktop, and switch to it. |
| KeyboardShortcutsModifiers   | NextTenDesktops              | If doing any of the actions above and targetting a specific desktop (ex: Switch to desktop no. 3) it instead targets the desktop that comes 10 desktops after that one (ex: Switch to desktop no. 13 instead of no. 3). Note that this modifier is works together with the modifiers above. |
| KeyboardShortcutsIdentifiers | PreviousDesktop              | Do the action for the previous desktop. |
| KeyboardShortcutsIdentifiers | NextDesktop                  | Do the action for the next desktop. |

In addition to the configurable identifier keys, the number keys above the letters on your keyboard also act as identifier keys, and each targets a specific desktop (from Desktop 1 to 10, unless the "NextTenDesktops" modifier is pressed, which will make them target Desktop 11 to 20 instead).

Each modifier keys' setting can be a combination of the `Ctrl`, `Shift`, `Alt`, `Win` keys, separated by commas. For each key, you can use the left or right variant of the keys specifically, by adding `L` or `R` before the name of the key (ex: `LCtrl`), otherwise both can be used. See below for examples.

Each identifier keys' setting can be single key of your keyboard. [They can be set to any value in this page (except modifiers)](https://www.autohotkey.com/docs/KeyList.htm). See below for examples.

Also note that if the setting is set to empty or not set at all, the feature will be disabled.

Here are some examples with different configs:

#### Behavior with default config

With this config:
<pre>
[KeyboardShortcutsModifiers]
SwitchDesktop=LAlt
MoveWindowToDesktop=LAlt, Shift, Ctrl
MoveWindowAndSwitchToDesktop=LAlt, Shift
NextTenDesktops=

[KeyboardShortcutsIdentifiers]
PreviousDesktop=Left
NextDesktop=Right
WindowActions=LAlt, Shift, Ctrl
PinWindow=
UnpinWindow=
ToggleWindow=Q
AppActions=LAlt, Shift, Ctrl
PinApp=
UnpinApp=
ToggleApp=A
</pre>

The following shortcuts are available:

| Description                                                                    | Keyboard Shortcut                            |
| ------------------------------------------------------------------------------ | -------------------------------------------- |
| Switch to desktop by number                                                    | Left Alt + (0-9)                             |
| Switch to next/previous desktop                                                | Left Alt + (Left/Right Arrow)                |
| Move the current window to desktop by number                                   | Left Alt + Shift + Ctrl + (0-9)              |
| Move the current window to next/previous desktop                               | Left Alt + Shift + Ctrl + (Left/Right Arrow) |
| Move the current window to desktop by number and switch to it                  | Left Alt + Shift + (0-9)                     |
| Move the current window to next/previous desktop and switch to it              | Left Alt + Shift + (Left/Right Arrow)        |
| Open Desktop Manager                                                           | Left Alt + (key under Esc)                   |
| Switch to desktop by number (desktops 11-20)                                   | Disabled                                     |
| Move the current window to desktop by number (desktops 11-20)                  | Disabled                                     |
| Move the current window to desktop by number and switch to it (desktops 11-20) | Disabled                                     |
| Pin current *window* to all desktops                                           | Disabled                                     |
| Unpin current window from all desktops                                         | Disabled                                     |
| Pin/unpin (toggle) current window                                              | Left Alt + Shift + Ctrl + Q                  |
| Pin current *app* to all desktops                                              | Disabled                                     |
| Unpin current app from all desktops                                            | Disabled                                     |
| Pin/unpin (toggle) current app                                                 | Left Alt + Shift + Ctrl + A                  |

#### Behavior with custom config

With this config:
<pre>
[KeyboardShortcutsModifiers]
SwitchDesktop=LWin
MoveWindowToDesktop=
MoveWindowAndSwitchToDesktop=LWin, Alt
NextTenDesktops=LShift

[KeyboardShortcutsIdentifiers]
PreviousDesktop=PgUp
NextDesktop=PgDn
</pre>

The following shortcuts are available:

| Description                                                                    | Keyboard Shortcut                    |
| ------------------------------------------------------------------------------ | ------------------------------------ |
| Switch to desktop by number                                                    | Left Win + (0-9)                     |
| Switch to next/previous desktop                                                | Left Win + (Page Up/Page Down)       |
| Move the current window to desktop by number                                   | Disabled                             |
| Move the current window to next/previous desktop                               | Disabled                             |
| Move the current window to desktop by number and switch to it                  | Left Win + Alt + (0-9)               |
| Move the current window to next/previous desktop and switch to it              | Left Win + Alt + (Page Up/Page Down) |
| Open Desktop Manager                                                           | Left Win + (key under Esc)           |
| Switch to desktop by number (desktops 11-20)                                   | Left Win + Left Shift + (0-9)        |
| Move the current window to desktop by number (desktops 11-20)                  | Disabled                             |
| Move the current window to desktop by number and switch to it (desktops 11-20) | Left Win + Alt + Left Shift + (0-9)  |

### Mouse Shortcuts

You switch between desktops by scrolling over the taskbar, if that setting is enabled.

### Tray Icon

A new tray icon will be available. It indicates the number of the current desktop (1-10).
If you click on it the desktop management screen is displayed.

#### Icon Packs

By default the white text on black background icon pack is set, but more packs are available.

To change between them, go into the "icons" folder and extract the ZIP file for the theme you want to use, and replace any existing files if prompted.

To create custom packs, simply create one icon per desktop and name them appropriately ([desktop number goes here].ico, ex: 1.ico, 5.ico, 99.ico). If the current desktop does not have an icon for it, the "+.ico" icon is shown instead, so make sure you create that as well for your pack.

### Additional Configuration

You can set what is the default desktop using the "[General] DefaultDesktop" setting.
You can set if you want to be able to switch desktops by scrolling over the taskbar using the "[General] TaskbarScrollSwitching" setting (1 for yes, 0 for no).

### Settings Migration Guide

Between version 0.9.1 and the current one, the name and location of some settings changed. The table and examples below should explain what was changed.

| Old location                      | New Location                                              |
| -                                 | -                                                         |
| [KeyboardShortcuts] Switch        | [KeyboardShortcutsModifiers] SwitchDesktop                |
| [KeyboardShortcuts] Move          | [KeyboardShortcutsModifiers] MoveWindowToDesktop          |
| [KeyboardShortcuts] MoveAndSwitch | [KeyboardShortcutsModifiers] MoveWindowAndSwitchToDesktop |
| [KeyboardShortcuts] PlusTen       | [KeyboardShortcutsModifiers] NextTenDesktops              |
| [KeyboardShortcuts] Previous      | [KeyboardShortcutsIdentifiers] PreviousDesktop            |
| [KeyboardShortcuts] Next          | [KeyboardShortcutsIdentifiers] NextDesktop                |

Example (old):
<pre>
[KeyboardShortcuts]
Switch=LAlt
Move=LAlt, Shift, Ctrl
MoveAndSwitch=LAlt, Shift
PlusTen=
Previous=Left
Next=Right
</pre>

Example (new):
<pre>
[KeyboardShortcutsModifiers]
SwitchDesktop=LAlt
MoveWindowToDesktop=LAlt, Shift, Ctrl
MoveWindowAndSwitchToDesktop=LAlt, Shift
NextTenDesktops=

[KeyboardShortcutsIdentifiers]
PreviousDesktop=Left
NextDesktop=Right
</pre>

## Credits

Thanks to Ciantic (Jari Pennanen) for his library and sample AHK script, which can be found [here](https://github.com/Ciantic/VirtualDesktopAccessor).

Thanks to engunneer for his AHK library, which can be found [here](http://www.autohotkey.com/board/topic/21510-toaster-popups/#entry140824).

Thanks to the creator of the ReadINI AHK library, found [here](https://autohotkey.com/board/topic/33506-read-ini-file-in-one-go/).

Thanks to the artists that created the packed wallpapers, whom I lost track of. Sorry.

Thanks to rob3110 on reddit for the extra white icon theme.

Thanks to several people on reddit.com/r/windows10 and in the project's github page for their suggestions.