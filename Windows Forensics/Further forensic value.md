# Further forensic value

## File Allocation table (FAT)

Was previously the defualt file system for Microsoft OS. Creates a table that indexes the location of bits allocated to files. 

Supports Clusters (basic storage unit) and Directory (info about file id e.g. name, length)

| **Attribute** | **FAT12** | **FAT16** | **FAT32** |
| --- | --- | --- | --- |
| **Addressable bits** | 12 | 16 | 28 |
| **Max number of clusters** | 4,096 | 65,536 | 268,435,456 |
| **Supported size of clusters** | 512B - 8KB | 2KB - 32KB | 4KB - 32KB |
| **Maximum Volume size** | 32MB | 2GB | 2TB |

FAT12 is rare, FAT16/32 are still used in some USB, SD cards etc.

exFAT - now the default for SD cards over 32GB and has been adopted by most manufacturers. Max file and volume of 128PB. 

## New Technology File System (NTFS)

Resolves many issues in FAT and has more security, reliability and recovery. 

**Journaling**: Keeps a log of changes to the metadata in the volume. Stored in $LOGFILE of the volumes root. 

**Access Controls**: Can define owner and permissions for each user.

**Volume Shadow Copy:** Keeps track of changes made to a file using Shadow Copies. Can restore previous file versions for recovery.  

**Alternate Data Streams**: Allows files to have multiple streams of data stored in a single file. E.g. can identify files downloaded from internet. Malware observed to hide here. 

**Master File Table**

There is a master file table in NTFS that is more extensive than FAT. NTFS file sytem data organized here. Can use MFT Explorer on CMD or GUI Forensic value:

**$MFT**: First record in volume. Contains a directory of all the files present on the volume. 

**$LOGFILE**: Stores the transactional logging of the file system.

**$UsnJrnl**: Updated Sequence Number Journal. Contains info about all the files changed on the files system and the reason for their changes. 

## Deleted Files/Data Recovery

When a file is deleted, the file system deletes the entries that store the file location on the disk. The location is now shown as available or unallocated, but the actual contents are still on the disk as long as they are not overwritten by the file system e.g. by copying files or disk maintenance. 

**Disk Image:** A file that has a bit-by-bit copy of a disk drive including metadata. Can make multiple images for forensics and prevents the original evidence from being destroyed. 

Can use a tool like autopsy to image a disk and then restore deleted files. 

## Prefetch files

When a program runs on Windows, it stores info for future use e.g. to load the program quickly. Files have the extension .pf. The files have last run times and number of run times of apps. Also stores any file and device handles used by the file. 

**`C:\Windows\Prefetch`**

Can use PECmd.exe (Eric ZIMMERMAN) to parse. 

**`PECmd.exe -f <path-to-Prefetch-files> --csv <path-to-save-csv>`**

**`PECmd.exe -d <path-to-Prefetch-directory> --csv <path-to-save-csv>`**

## Windows 10 Timeline

In Windows 10, recently used apps and files are stored in an SQLite DDB called ‘Windows 10 Timeline’. Useful for info on last executed programs. 

**`C:\Users\<username>\AppData\Local\ConnectedDevicesPlatform\{randomfolder}\ActivitiesCache.db`**

WxTCmd

**`WxTCmd.exe -f <path-to-timeline-file> --csv <path-to-save-csv>`**

Windows Jump Lists

Jump Lists help users go directly to their recently used files from the taskbar. When right clicking on an apps icon, it will show recent files opened by that app. 

**`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations`**

JLECmd.exe

**`JLECmd.exe -f <path-to-Jumplist-file> --csv <path-to-save-csv>`**

## Shortcut Files

A shortcut file is created for each file opened locally or remotely. Contains info e.g. first and last open times and file paths. 

**`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\`**

**`C:\Users\<username>\AppData\Roaming\Microsoft\Office\Recent\`**

LECmd.exe

**`LECmd.exe -f <path-to-shortcut-files> --csv <path-to-save-csv>`**

## IE/Edge history

Internet Explorer and Edge history also includes data on files opened in the system and if theu were opened by the browser or not. Can view this through Autopsy.

**`C:\Users\<username>\AppData\Local\Microsoft\Windows\WebCache\WebCacheV*.dat`**

## USB/External Drives

When a new device is attached, info related to the setup is stored. It contains device serial number, first/last times it was connected. 

**`C:\Windows\inf\setupapi.dev.log`**