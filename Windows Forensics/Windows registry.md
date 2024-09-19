# Windows registry:

## About

The Windows Registry is a collection of databases that contains the system's configuration data.

The registry on any Windows system contains the following five root keys:

1. HKEY_CURRENT_USER (logged on user config)
2. HKEY_USERS (All actively loaded user profiles - subkey of HKEY_CURRENT_USER)
3. HKEY_LOCAL_MACHINE (Config info for the computer (any user))
4. HKEY_CLASSES_ROOT (ensures the correct program opens when file opened by Windows explorer - sub key of HKEY_LOCAL_MACHINE)
5. HKEY_CURRENT_CONFIG ( info about hardware profiles used by the local computer at system startup)

These keys can be viewed from **regedit.exe**  if accessing a live system. If accessing a disk image most are located in **C:\Windows\System32\Config** 

1. **DEFAULT** (mounted on **`HKEY_USERS\DEFAULT`**)
2. **SAM** (mounted on **`HKEY_LOCAL_MACHINE\SAM`**)
3. **SECURITY** (mounted on **`HKEY_LOCAL_MACHINE\Security`**)
4. **SOFTWARE** (mounted on **`HKEY_LOCAL_MACHINE\Software`**)
5. **SYSTEM** (mounted on **`HKEY_LOCAL_MACHINE\System`**)

**Other user info hives:**

1. **NTUSER.DAT** (mounted on HKEY_CURRENT_USER when a user logs in) - **C:\Users\{username}**
2. **USRCLASS.DAT** (mounted on HKEY_CURRENT_USER\Software\CLASSES) - **C:\Users\<username>\AppData\Local\Microsoft\Windows**

**The Amcache Hive:**

Windows creates this hive to save information on programs that were recently run on the system.

**C:\Windows\AppCompat\Programs\Amcache.hve**

**Transaction Logs and Backups**

**Transaction logs:** Considered as the journal of the changelog of the registry hive. Can often have the latest changes in the registry that haven't made their way to the registry hives themselves. Stored as a .LOG file in the same directory as the hive itself and with the same name

**Registry Backups:**  These are the backups of the registry hives located in the **`C:\Windows\System32\Config`** directory. These hives are copied to the **`C:\Windows\System32\Config\RegBack`** directory every ten days. It might be an excellent place to look if you suspect that some registry keys might have been deleted/modified recently.

## Data Acquisition

In forensics we will generally encounter a live system or an image taken of a system. It is best practice to take an image or extract the required data before forensics. 

tools for acquisition:

- KAPE - live data - command line and GUI
- Autopsy - live system or disk image - GUI
- FTK Imager - live system or disk image - GUI

## Analysis

**tools:**

- Registry Viewer - Only one hive at a time and can’t take transaction logs.
- Registry Explorer - Eric Zimmerman
- RegRipper - Takes hives as inputs and outputs a report of forensically important keys and values. No transaction logs.

**System info:**

OS - **`SOFTWARE\Microsoft\Windows NT\CurrentVersion`**

Computer name - **`SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`**

Time Zone info - **`SYSTEM\CurrentControlSet\Control\TimeZoneInformation`**

Network interface/Past nets - **`SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`**

**Current control set**

configuration data used for controlling system startup are called Control Sets. 

**`SYSTEM\ControlSet001`  -**  point to the control set the system booted with

**`SYSTEM\ControlSet002`  -** last known good config

**`HKLM\SYSTEM\CurrentControlSet`** - volatile control set - most accurate system info

**Autostart/Autorun**

Programs/commands when a user logs on:

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`**

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`**

**`SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`**

**`SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`**

**`SOFTWARE\Microsoft\Windows\CurrentVersion\Run`**

Services: 

**`SYSTEM\CurrentControlSet\Services`**

**SAM hive and user info**

includes RID, number of times logged in, last login, last failed login, last password change…

**`SAM\Domains\Account\Users`**

## Files and Folders

Recent files

Explorer:

Recent user files - last used at top

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`**

Can get recent files by extension

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.pdf`**

Office

Office 2013:

**`NTUSER.DAT\Software\Microsoft\Office\VERSION`**

Office 365 - tied to the users live ID

**`NTUSER.DAT\Software\Microsoft\Office\VERSION\UserMRU\LiveID_####\FileMRU`**

ShellBags - Different folder layout for each user - can identify most recently used files. Not much info from Registry Explorer - Eric Zimmerman ShellBag Explore has GUI. 

**`USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags`**

**`USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU`**

**`NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU`**

**`NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags`**Open/Save and LastVisited Dialog MRU - Dialog box when we open or save a file. 

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU`**

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU`**

Explorer address/search bar -  Can identify users recent activity

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`**

**`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`**

## Evidence of Execution

UserAssist

Info about programs launched, time and number of times executed. Programs run via command line not here. 

**`NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count`**

ShimCache

Tacks all applications launched on OS for compatibility reasons.  AKA AppCompatCache. Need to use tool like Eric Zimmerman AppCompatCache Parser to read in human readable format. 

**`SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`**

Running this command will allow the output to be viewed in EZviewer (Eric Zimmerman)

**`AppCompatCacheParser.exe --csv <path to save output> -f <path to SYSTEM hive for data parsing> -c <control set to parse>`**

AmCache

Similar to ShimCache, additional data including execution path, installation, executio/deletion times and Sha1 of executed programs.

**`C:\Windows\appcompat\Programs\Amcache.hve`**

Info about the last executed program

**`Amcache.hve\Root\File\{Volume GUID}\`**

BAM/DAM

Background Activity Monitor (BAM) - activity of background applications

Desktop Activity Moderator (DAM) - Optimises the power consumption of the device.

Contains info about last run programs, full paths and last exe time. 

**`SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`**

**`SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`**

## External Devices/USB

Identification:

Record of USB keys (vendor_id, product_id, version, time plugged in)

**`SYSTEM\CurrentControlSet\Enum\USBSTOR`**

**`SYSTEM\CurrentControlSet\Enum\USB`**

First/last time device was connected

**`SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####`**

Device volume name

**`SOFTWARE\Microsoft\Windows Portable Devices\Devices`**