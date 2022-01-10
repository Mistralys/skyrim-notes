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
  
## Managing mods with Vortex

### Profiles

Profiles are an awesome tool: they can completely separate mods, savegames and the like, to be able to switch between playthroughs that use different sets of mods. Also a great way to test if mods work together: Duplicate a profile to a new one, deploy with the mods, run the game to try them out. The original profile can stay unchanged.

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
* `[WorldEdits]` - Contains world edits (changing locations, adding things).
* `[Craftable]` and `[NonCraftable]` - For armors and weapons.
* `[F]`, `[M]` and `[F/M]` - For armors, sets which sexes are supported by the armor.
* `[QuestRequired]` - For items that require a quest to be completed.
* `[Skyforge]` - For items that can only be crafted at the Skyforge.
* `[Console]`- Requires console commands to be run to use.
* `[Hearthfire]` - Adds/chages things related to the Hearthfire system.

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
   
### Light plugins, ESPFE, ESL and co

Skyrim has a hardwired limit of 256 plugins (the `.esp` or `.esm` files). However, smaller plugins which only do a limited number of edits in the game world can be flagged as "Light" plugins. In this case, they do not take up a space towards the plugin limit. Many of the plugins on Nexusmods are already flagged as light.

To check how many plugins are in the load order that are not flagged as light, do the following:

1. Go to the plugins list.
2. Select all plugins (CTRL+A).
3. Note how many plugins there are in total (bottom right).
4. In the Flags column, filter by "Light".
5. Subtract the amount of light plugins from the total.
   
As long as this number stays below 256, all is good. Beyond this, manual adjustments are needed: Converting plugins that could be light to light plugins in xEdit, or even merge mods. This needs separate tutorials however.
   
### Exporting the Vortex mods list

This can only be done with a Vortex extension. At the time of writing (december 2021), there is only one extension that does this: [ModlistBackup][].

To install it, do the following:

1. Open Vortex 
2. Go to "Extensions"
3. Click "Find more" 
4. Search for "Modlist"
5. Install the mod from the list
6. Restart Vortex
7. Go to "Mods"
8. Click on the "Modlist" button
9. Choose "Modlist backup only this game"

This creates a JSON file with a list of all mods. However, this list only contains the original mod names - not the ones renamed and tagged in Vortex.

To add the custom name to the JSON, a small hack is needed:

1. Close Vortex
2. Open the folder `%AppData%\Vortex\plugins`
3. Find the extension folder, e.g. `Vortex Extension Update - Modlist Backup v0.3.2`
4. Open the file `index.js` in a text editor
5. Search for `transformModFormat`
6. Insert the following line after `name: mod.attributes.modName,`:
7. `displayName: (typeof(mod.attributes.customFileName) !== undefined ? mod.attributes.customFileName : ''),`
8. Start Vortex again, export the list.

To get even more data per mod, this can be used:

```javascript
const transformModFormat = (mod) => ({
    name: mod.attributes.modName,
    displayName: getSafe_1.default(mod.attributes, ['customFileName'], ''),
    version: mod.attributes.version,
    modVersion: getSafe_1.default(mod.attributes, ['modVersion'], ''),
    installTime: getSafe_1.default(mod.attributes, ['installTime'], ''),
    category: getSafe_1.default(mod.attributes, ['category'], ''),
    pictureURL: getSafe_1.default(mod.attributes, ['pictureUrl'], ''),
    fileType: getSafe_1.default(mod.attributes, ['fileType'], ''),
    game: mod.attributes.downloadGame,
    modId: mod.attributes.modId,
    fileId: mod.attributes.fileId,
    source: mod.attributes.source,
});
```
   
## ENB handling

Download for Skyrim: [ENB][].
 
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

## Editing textures

### Lexicon

- **DDS**: Specialized texture file that also contains Mipmaps.
- **Normal map**: Relief, topography or bump map. A separate texture file that contains the elevation information, as companion to the visual texture file.
- **Mipmaps**: Different sized versions of a texture used depending on the player's distance from the textured object. Since an object far away does not need the full sized texture, a smaller version is used. Mipmaps are typcially generated automatically an directly integrated into the DDS file.
- **Alpha channel**: Also called *specular* layer. This does not actually give the texture transparency, it determines how glossy it is. The more opaque the layer is (=no transparency), the glossier the result is. Not using an alpha layer will cause the texture to have the maximum glossiness.

### DDS Files

Required tool to open and save DDS files in Photoshop (requires an Nvidia Graphics Card, and Nvidia account):

https://developer.nvidia.com/nvidia-texture-tools-exporter

Structure of a texture:

- `TextureName.dds` - The base texture file
- `TextureName_n.dds` - The normal map

> Warning: Since DDS files are not lossless, opening and saving it reduces the quality each time. It is best to use the original files if available.

### Generating normal maps from textures

- Use a flattened, grayscale image of the source texture
- In Photoshop, go to Filters > 3D > Generate normal map
- Choose "Cube" as view for a good preview

### Specular layer

In Photoshop, the firstmost layer is used as alpha channel for the texture's specular aspect (its glossyness). It can stay invisible, it just needs to be there.


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
[ENB]:http://enbdev.com/download_mod_tesskyrimse.htm
[ModlistBackup]:https://github.com/Garethp/Vortex-Modlist-Backup
