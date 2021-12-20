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

> NOTE: I have taken the habit of also adding the date I enabled a mod. This way it's 
> easy to find a save game that was made prior to enabling the mod, if needed.

#### General tags

* `[NoSKSE]` and `[SKSE]` - Whether [SKSE][] (Skyrim Script Extender) is required.
* `[NewGame]` - Requires a new game, cannot be enabled mid-save.
* `[BodySlide]` - Includes BodySlide files.
* `[ReadNotes]` - Important info available in the Vortex mod notes.
* `[EnvX]` - Where `X` is a number: Environment mod sets.
* `[Options]` - Mod has options that can be set in the FOMOD installer.
* `[Dependencies]` - Mod has dependencies with other mods.
* `[ENBDependent]` - Mod is tied to specific ENB presets, or requires [ENB][].
* `[Craftable]` and `[NonCraftable]` - For armors and weapons.
* `[F]`, `[M]` and `[F/M]` - For armors, sets which sexes are supported by the armor.
* `[QuestRequired]` - For items, means that a quest has to be completed to get them.

#### Specific mod dependency tags

* `[RaceMenu]`- Requires the [Race Menu][] mod.
* `[SkyUI]` - Requires or uses the [SkyUI][] mod.
* `[AddressLib]` - Mod requires the [Address Library][] mod.
* `[CBBE]` - Requires the [CBBE][] (Calient's Beautiful Bodies Enhancer) mod.
* `[USSEP]` - Requires the [USSEP][] (Unoffical Skyrim Special Edition Patch) mod.
* `[WACCF]` - Requires the [WACCF][] (Weapons Armor Clothing and Clutter Fixes) mod.
* `[CLLF]` - Requires the [CLLF][] (Containers and Leveled Lists Fixes) mod.
* `[ACE]` -  Requires the [ACE][] (Armor and Clothing Extension) mod.

#### SKSE/Non SKSE mods

These tags make it very easy to create a mods profile that does not use SKSE, simply by enabling all mods tagged `[NoSKSE]` in Vortex. All SKSE-dependent mods can inversely easily be listed by searching for the `[SKSE]` tag.

#### Environment sets

An environment set refers to a collection of mods that are used together for adjusting the environment, from the weather to the flora. Since they are typically mutually exclusive, this makes it handy to keep track of which mods must/should be used together. Mods that can be used with several get multiple environment tags.

For example, `[Env1]` for Obsidian Weathers and `[Env2]` for Cathedral Weathers. Searching for either tag directly shows which mods need to be enabled for it.

Example in my mods list:

* `Blended Roads [Env1] [Env2]`
* `Nordic Snow [Env1]`
* `Obsidian Weathers [Env1]`
* `Cathedral - Weathers [Env2]`
* `Cathedral - Landscapes [Env2]`
   
## Mod notes

### Race Menu

#### Mid-save script cleanup

I had to disable Race Menu mid-game at some point, because of the Anniversary Edition update. While the game still loaded correctly, saving caused an instant CTD. This was caused by leftover Race Menu scripts in the save game. I managed to solve this issue by using ReSaver from [FallrimTools][]. I searched for `RaceMenu` in the tool, and simply removed everything from the search results. Using this cleaned save, I was able to continue playing.
   
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
[Race Menu]:https://www.nexusmods.com/skyrimspecialedition/mods/19080
[SkyUI]:https://www.nexusmods.com/skyrimspecialedition/mods/12604
[FallrimTools]:https://www.nexusmods.com/skyrimspecialedition/mods/5031
[CLLF]:https://www.nexusmods.com/skyrimspecialedition/mods/26575
[ACE]:https://www.nexusmods.com/skyrimspecialedition/mods/19002
[CBBE]:https://www.nexusmods.com/skyrimspecialedition/mods/198
[SKSE]:https://skse.silverlock.org/
[ENB]:http://enbdev.com/
