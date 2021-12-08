# Skyrim notes

Collected notes for playing and modding Skyrim.

## Creation Kit

### Configuration

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

