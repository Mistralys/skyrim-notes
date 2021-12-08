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

