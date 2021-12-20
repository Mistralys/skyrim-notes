# Skyrim notes

Collected notes for playing and modding Skyrim.

## Taking Screenshots

* `tm` (Toggle Menu) will hide all the HUD components, including the console menu. Type the command again blindly afterwards to restore the UI.
* `tfc` (Toggle Free Camera) will let you move the camera anywhere. Key: Movement keys to move, left/right mouse buttons to move up and down. 
* `tfc 1` Pauses the game with the free camera.
* `sucsm <value>` (Set UFO Camera Speed Multiplier) Camera speed. 1=slow, higher values go faster.
* `fov <angle>` (Field of View) Default: 65. Lower values = zoom in, higher = zoom out.
* `csb` (Clear Screen Blood) Remove the blood on-screen effect.
* `set gamehour to <hour>` changes the time, with `<hour>` between 0 and 23.
* `fw <formid>` (Force Weather) temporarily changes the weather.

More here: https://steamcommunity.com/sharedfiles/filedetails/?id=134522361
  
## Vortex

### Tagging 

In my Vortex mods list, I rename mods to add custom tags. This makes it a lot easier to work with a large list of mods, and easily filter them by criteria.

* `[NoSKSE]` and `[SKSE]` - Whether SKSE is required.
* `[CBBE]` - Requires CBBE.
* `[BodySlide]` - Includes BodySlide files.
* `[ReadNotes]` - Important info available in the Vortex mod notes.
* `[EnvX]` - Where `X` is a number: Environment mod sets(1)
* `[Options]` - Mod has options that can be set in the FOMOD installer.
* `[Dependencies]` - Mod has dependencies with other mods.
* `[ENBDependent]` - Mod is tied to specific ENB presets, or requires ENB.
* `[AddressLib]` - Mod requires the [Address Library][] mod.
* `[Craftable]` and `[NonCraftable]` - For armors and weapons.
* `[F]`, `[M]` and `[F/M]` - For armors, sets which sexes are supported by the armor.
* `[USSEP]` - Requires the [USSEP][] (Unoffical Skyrim Special Edition Patch) mod.
* `[WACCF]` - Requires the [WACCF][] (Weapons Armor Clothing and Clutter Fixes) mod.

(1) Each number identifies a set of mods that are used together for adjusting the environment, from the weather to the flora. This way, searching for `[Env1]` for example, will display all mods required for that environment set (e.g. Obsidian weathers or Cathedral Landscapes).
   
## Creation Kit

### Installation

To get the creation kit for the Special Edition, log in to the [bethesda.net](https://bethesda.net) website, and download the launcher. The kit can only be installed from the launcher.

> Once installed, it can be launched from the `CreationKit.exe` in the game folder.

### Configuration

Go to the game folder, there should be a `CreationKit.ini` file there, along with the excecutable. Open this to make some necessary adjustments.

Add the following under `[GENERAL]`:

```
bAllowMultipleMasterFiles=1
bAllowMultipleMasterLoads=1
```

Add the following under `[Archive]`:

```
SInvalidationFile=ArchiveInvalidation.txt
iRetainFilenameOffsetTable=1
iRetainFilenameStringTable=1
iRetainDirectoryStringTable=1
bCheckRuntimeCollisions=0
```

Add the following under `[MESSAGES]`:

```
bBlockMessageBoxes=1
```

> Note: This will prevent the message popups on initialization. They can be safely ignored.

### Creating a new mod

To create a new mod, do not select an active file in the open dialog.

### Making changes to an existing mod

* Create a new mod
* Duplicate the item to modify (to keep the original intact)
* Do any necessary changes
* Save to a new mod
* Load the new mod after the original mod

### Making an item craftable

Use case: A mod adds items, but they are not craftable. They can be easily made craftable.

* Open the source mod without making it active
* Create a copy of the item, to leave the original intact
* In case of armor, also copy the matching Armor Addon item
* Remove any enchantments and scripts from the item
* Edit the item as necessary
* Save as a new mod file

> Drawback: If the original mod is updated and item stats change, for example, the changes must be made in the crafting mod as well.


[USSEP]:https://www.nexusmods.com/skyrimspecialedition/mods/266
[Address Library]:https://www.nexusmods.com/skyrimspecialedition/mods/32444
[WACCF]:https://www.nexusmods.com/skyrimspecialedition/mods/18994
