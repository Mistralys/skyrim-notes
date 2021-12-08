# Skyrim notes

Collected notes for playing and modding Skyrim.

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


