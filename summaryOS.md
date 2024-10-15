DAY 1

Powershell
https://ss64.com/    #Reference guide containing syntax and examples for the most prevalent computing commands
https://ss64.com/ps/  # Helpful Powershell Command References

https://training.13cubed.com/downloads #  cheat sheets, reference guides, study notes, and code 

https://www.tutorialspoint.com/powershell/index.htm

Powershell cmdlets
Get-Process | Get-Member | Where-Object {$_.Membertype -match "Method"}     
    # Displays all objects with Method in their name from the results from Get-Member of the Get-Process cmdlet #

Get-Process | Select-Object Name, ID, path | Where-object {$_.ID -lt '1000'} 
           # List all the processes with a PID lower than 1000 #

(Get-Process | Select-Object Name, ID, path | Where-object {$_.ID -lt '1000'}).count 
               # List all the processes with a PID lower than 1000

Get-Service | Where-Object {$_.Status -eq "Running"}
 #Get-Service gets all the services on the computer and sends the objects down the pipeline. The Where-Object cmdlet selects only the services with a Status property that equals Running.
Status is only one property of service objects. To see all of the properties, type Get-Service | Get-Member.#

Get-Service "s*" | Sort-Object status
# This example shows that when you sort services in ascending order by the value of their Status property, stopped services appear before running services. This happens because the value of Status is an enumeration, in which Stopped has a value of 1, and Running has a value of 4. For more information, see ServiceControllerStatus.

To list running services first, use the Descending parameter of the Sort-Object cmdlet #
PowerShell Profiles
PowerShell profiles are a convenient way to store PowerShell configuration information as well as personalized aliases and functions to persistent use in every PowerShell session.

Profiles are just scripts that have configurations set.
PowerShell profiles were intended to assist PowerShell users with mundane repeatable tasks, such as loading PowerShell modules daily, or configuring.

By default the profiles are not built, the paths are checked whenever PowerShell is opened.

PowerShell supports several profile files and host programs, like Windows, support their own specific profiles. The profiles below are listed in order of precedence with the first profile having the highest precedence.
Description
Path
All Users, All Hosts
$PsHome\Profile.ps1
All Users, Current Host
$PsHome\Microsoft.PowerShell_profile.ps1
Current User, All Hosts
$Home\[My]Documents\Profile.ps1
Current User, Current Host
$Home\[My ]Documents\WindowsPowerShell\Profile.ps1





To determines whether individual profiles have been created on the local computer:
Test-Path -Path $profile.currentUsercurrentHost
Test-Path -Path $profile.currentUserAllHosts
Test-Path -Path $profile.AllUsersAllHosts
Test-Path -Path $profile.AllUserscurrentHost

DAY 2

Understand the registry
When adversaries gain initial access to a system, they try to maintain their foothold to achieve persistence on the system.
Persistence allows an attacker to remain on the compromised system without having to re-infect it, after initial access, most especially at startup.

Run Keys in the Registry and Startup Folder in Users directory are “old but gold” locations that are utilized by attackers for persistence. Adding an entry to the Run Keys, or creating a shortcut in Startup Folder is enough to execute malicious code when a user logs in. Our research has found that Registry Run Keys / Startup Folder is the eighth most prevalent ATT&CK technique used by adversaries in their malware.

Introduction

Adversaries use built-in Windows features to execute their malicious executables to run at system startup or when a user logs in. For example, they schedule execution of their codes with Windows Task Scheduler as explained in our previous blog post, MITRE ATT&CK T1053 Scheduled Task. Other most common methods are utilizing Run Keys in the Registry and Startup Folder, which were included as a technique in the MITRE ATT&CK Framework, T1060 Registry Run Keys / Startup Folder. In the new sub-technique version of MITRE ATT&CK, it became a sub-technique of the T1547 Boot or Logon Autostart Execution, as T1547.001. 
In this article, we review:

registry keys used for persistence
startup folders utilized by adversaries
its use cases by threat actors and malware
red and blue team exercises for this technique

Registry Run Keys
Let’s start with important definitions:

Registry: It is a hierarchical database used by Windows to store information, settings and configuration options for the OS, programs and hardware. 
Key: A key is a container object similar to folders that may contain subkeys and values. 
Value: A value is a name/data pair stored within keys.
Root Key: A root key is a key at the root level of the hierarchical database.

HKEY_LOCAL_MACHINE (HKLM): It is a root key that includes settings for the local computer that applies to all users. HKLM includes four subkeys, SAM, SECURITY, SYSTEM and SOFTWARE. The "HKLM\SOFTWARE" subkey contains settings of software and OS.

HKEY_CURRENT_USER (HKCU): It is a root key that includes preferences and settings that are specific to the currently logged-in user. HKCU is loaded on login of the user, while HKLM is loaded at boot time.

Registry Run Keys: These keys contain settings to auto-launch applications on system startup.

Adversaries utilize the following registry keys to load malware on system startup to achieve persistence:

“Run” and “RunOnce” Registry Keys:
These keys enable programs to run each time a user logs in [1]. As a recent example, Saigon banking Trojan creates a new entry in the HKCU\Software\Microsoft\Windows\CurrentVersion\Run key to run with every startup for maintaining persistence [2].

The following registry keys are created by default: 

HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

The following key is not created by default, but you can create and use it:

HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnceEx

RunServices” and “RunServicesOnce” Registry Keys:

These keys include entries for services running in the background and control automatic startup of services. Attackers add new entries to add their malicious executables as background services.

HKLM\Software\Microsoft\Windows\CurrentVersion\RunServices
HKCU\Software\Microsoft\Windows\CurrentVersion\RunServices
HKLM\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce
HKCU\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce

Policies “Run” Registry Keys:

Policy settings can be used to specify startup programs:

HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run

HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
Winlogon Registry Keys:

The following keys control actions that occur when a user logs-in.

HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit : It usually points to userinit.exe. However, an adversary can alter userinit.exe with the malware executable, or add new entries that points to the malware executable. The malware executable will launch at system startup.

HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell :  This key points to just one entry, explorer.exe.

HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify : This subkey is used to notify event handles when Secure Attention Sequence (SAS) (Ctrl+Alt+Del) happens and loads a DLL. Adversaries alter this DLL to load their malware.

BootExecute Registry Key:

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager: The BootExecute value in this key is launched during boot. Although its default value is “autocheck autochk *”, adversaries can add other commands, scripts or programs to this value.

“Shell Folders” and “User Shell Folders” Registry Keys:

These keys are also referred to as “startup keys” since they are used by adversaries to set the location of the startup folder.

HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
Reference
https://www.picussecurity.com/resource/blog/picus-10-critical-mitre-attck-techniques-t1060-registry-run-keys-startup-folder


SOME CTFs

What registry subkey runs every time the machine reboots? The flag is the full path, using PowerShell.   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run

What registry subkey runs every time a user logs on? The flag is the full path, using PowerShell.
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run

What registry subkey runs a single time, then deletes its value once the machine reboots? The flag is the full path, using PowerShell.
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce

What registry subkey runs a single time, then deletes its value when a user logs on? The flag is the full path, using PowerShell.
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce

COMMAND-LINE + POWERSHELL COMMANDS EXAMPLES

Reg query HKLM\SYSTEM\CURRENTCONTROLSET\Enum\USBstor
                       ####gives value name for a plugged in usb ####

 Reg query “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList”
        ########gives a list of user profiles connected to a machine ########

Get-localuser | select name,sid
 ### gives name and sid for accounts#####

 Reg query “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList”
                         #####gives the hive and attached SID#####








The default file path for the init program is " /usr/sbin/init " but it can be changed by the kernel boot parameter as " init=/path/to/init_program ". " /usr/sbin/init " is symlinked to " /lib/systemd/systemd " after Debian 8 Jessie

https://os.cybbh.io/public/os/latest/002_powershell/pwsh_fg.html
###############student guide##################

Why is the registry important?

Anyone can hide all sorts of data including passwords, malicious code, and executable/binary files in the Registry.
They can effectively hide data in registry keys’ value entries.
By using different encoding techniques, they could obfuscate or hide data from forensic examiners.
It is important to know what right looks like and the places that are most likely to be compromised by a malicious actor.


View/manipulate the registry via CMDLINE
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
           ##Reg query - Reads keys from specific registry locations##
                  
Registry Manipulation with PowerShell
Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    <##returns nothing because it is listing the sub keys of \Run. Run has no sub keys,  only values.
                   Get-ChildItem - Reads sub keys from the input value##>

Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\
                              ##Returns sub keys of \CurrentVersion##

Get-item HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
                 ##Get-Item - Reads the value of the inputted object##

NOTE
Minimum commands to know
Query
Get-ChildItem cmdlet gets the items in one or more specified locations.
Get-ItemProperty cmdlet gets the items in one or more specified locations.
Get-Item cmdlet gets the item at the specified location. It doesn’t get the contents of the item at the location unless you use a wildcard character (*) to request all the contents of the item.
Modify
Set-ItemProperty cmdlet changes the value of the property of the specified item. example, changing setting to :true or :false.
Remove-ItemProperty cmdlet to delete registry values and the data that they store.
Create
New-Item cmdlet creates a new item and sets its value. In the registry, New-Item creates registry keys and entries.
New-Itemproperty cmdlet creates a new property for a specified item and sets its value. Typically, this cmdlet is used to create new registry values, because registry values are properties of a registry key item.


Forensically Relevant Keys

These are keys that hold any type of information that can be used to gather intelligence or track events.
These are some but not all of the keys that can be considered relevant to you or your mission set.
SANS Registry Cheat Sheet
Why do we care?
We are looking for keys that can be used for Persistence
Persistence consists of techniques that adversaries use to keep access to systems across restarts, changed credentials, and other interruptions that could cut off their access
As well as Privilege Escalation.
Privilege Escalation consists of techniques that adversaries use to gain higher-level permissions on a system or network.

Microsoft Edge Internet URL history and Browser Artifacts and Forensics
HKEY_CLASSES_ROOT\Local Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Storage\microsoft.microsoftedge_8wekyb3d8bbwe\Children\001\Internet Explorer\DOMStorage
USB history / USB Forensics
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB
This registry key contains information about all USB devices that have been connected to the system at some point, regardless of whether they are currently connected or not. It includes information about the USB controllers, hubs, and individual devices. Each device is typically identified by a unique identifier (like a device instance path or hardware ID).
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR
This registry key specifically deals with USB storage devices, such as USB flash drives, external hard drives, etc. It contains information about connected USB storage devices, including details like device instance paths, hardware IDs, and other configuration information.
Recent MRU history / MRU in forensics
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU
MRU is the abbreviation for most-recently-used.
This key maintains a list of recently opened or saved files via typical Windows Explorer-style common dialog boxes (i.e. Open dialog box and Save dialog box).
For instance, files (e.g. .txt, .pdf, htm, .jpg) that are recently opened or saved files from within a web browser (including IE and Firefox) are maintained.
Recent Files with LNK files
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
Windows User Profiles User Account Forensics
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
Saved Network Profiles and How to decode Network history
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles
Windows Virtual Memory and why it is important
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
This key maintains Windows virtual memory (paging file) configuration.
The paging file (usually C:\pagefile.sys) may contain evidence/important information that could be removed once the suspect computer is shutdown.
Recent search terms using Windows default search and Cortana
HKEY_CURRENT_USER\Software\Microsoft\Windows Search\ProcessedSearchRoots
Index of Search results by SID
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Search
Recent files searched




Registry locations that can be utilized for persistence

Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder - MITRE

<##
Adversaries may achieve persistence by adding a program to a startup folder or referencing it with a Registry run key. Adding an entry to the "run keys" in the Registry or startup folder will cause the program referenced to be executed when a user logs in.[1] These programs will be executed under the context of the user and will have the account's associated permissions level.
The following run keys are created by default on Windows systems:
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce
Run keys may exist under multiple hives.[2][3] The HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnceEx is also available but is not created by default on Windows Vista and newer. Registry run key entries can reference programs directly or list them as a dependency.[1] For example, it is possible to load a DLL at logon using a "Depend" key with RunOnceEx: reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx\0001\Depend /v 1 /d "C:\temp\evil[.]dll" [4]
Placing a program within a startup folder will also cause that program to execute when a user logs in. There is a startup folder location for individual user accounts as well as a system-wide startup folder that will be checked regardless of which user account logs in. The startup folder path for the current user is C:\Users\[Username]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup. The startup folder path for all users is C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp.
The following Registry keys can be used to set startup folder items for persistence:
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
The following Registry keys can control automatic startup of services during boot:
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices
Using policy settings to specify startup programs creates corresponding values in either of two Registry keys:
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
Programs listed in the load value of the registry key HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows run automatically for the currently logged-on user.
By default, the multistring BootExecute value of the registry key HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager is set to autocheck autochk *. This value causes Windows, at startup, to check the file-system integrity of the hard disks if the system has been shut down abnormally. Adversaries can add other programs or processes to this registry value which will automatically launch at boot.
Adversaries can use these configuration locations to execute malware, such as remote access tools, to maintain persistence through system reboots. Adversaries may also use Masquerading to make the Registry entries look as if they are associated with legitimate programs. ##>
     System-wide and per-user autoruns
HKLM\Software\Microsoft\Windows\CurrentVersion\Run

HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\Run

HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKLM\SYSTEM\CurrentControlSet\services

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders

HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon

























DAY 3

LINUX ESSENTIALS
Netstat command

https://phoenixnap.com/kb/netstat-command

NOTE: THE MOST IMPORTANT WEBSITE OF ALL
                                ##  https://cheat.sh/  ##
                                   https://ss64.com/

SITUATION AWARENESS
After first obtaining access to a system an operator must gather as much information about their environment as possible, this is referred to as situational awareness. pwd is just one command of many on Linux which can provide us some insight.

other commands to help gain situational awareness:
hostname or uname -a displays the name of the host you are currently on.
whoami shows the user you are currently logged in as (useful after gaining access through service exploitation).
w or who shows who else is logged in.
ip addr or ifconfig displays network interfaces and configured IP addresses.
ip neigh or arp displays MAC addresses of devices observed on the network.
ip route or route shows where packets will be routed for a particular destination address.
ss or netstat will show network connections or listening ports
nft list tables or iptables -L to view firewall rules.
sudo -l displays commands the user may run with elevated permissions.

C:\Windows> tasklist /svc


DAY 4
SysV
SysV initialization is a legacy system initialization method, but it is still used today in many older systems Linux systems or Unix machines like Oracle’s Solaris. It starts with the kernel executing the first process on the machine, or the Initialization daemon. In SysV machines it is the /etc/init program. Then, init reads /etc/inittab to start creating processes in groups called Run Levels. The processes that each Run Level starts are defined in /etc/rc*.d
SysV Init Daemon
The program /etc/init is the first process to start in SysV Linux machines. The kernel spawns /sbin/init. Its role is to initialize the system to a target run level specified in /etc/inittab.
The file /etc/inittab is a text file that contains Run Level entries as variables read by /etc/init. Entries numbered 0-6 specify a directory with scripts to start at the specified Run Level. By default the system will try to start the initdefault run level. If that fails to start, the machine will display an error, then execute the scripts in the 0(halt) run level.

Systemd
Systemd is the modern initialization method. Its starts with the kernel spawning /sbin/init which is symbolically linked to /lib/systemd/system. systemd interacts with flat configuration files called units. There are many types, but the target and service units determine system initialization.
​
   Systemd Init target.units
The kernel spawns /usr/lib/systemd/system as the first process on the system. It then executes configurations starting at mounting the local file system to bringing the system to a desired state specified in the default target unit. Targets in systemd are like runlevels in SysV. The name of the default target is default.target and located in /lib/systemd/system.

 

This means that the default.target is actually graphical.target
The graphical.target unit wants to start:
display-manager.service
udisks2.service
accounts-daemon.service
systemd-update-utmp-runlevel.service
But, the graphical.target requires the multi-user.target to execute.

student@linux-opstation-kspt:/$ ls -l /etc/systemd/system/ | grep graphical

The /etc/profile file
/etc/profile is a script that executes whenever a user logs into an interactive shell on Linux. its functionality depends entirely on the version of Linux being used. Ubuntu Linux uses it to set the BASH shell prompt by executing /etc/bash.bashrc and execute any script named *.sh in /etc/profile.d.
Unlike /etc/environment it executes every time a user logs in interactively; therefore, when the file is modified logging out then in again will apply the changes.

the .bash_profile and .bashrc files
Unique to BASH(Bourne Again Shell) are .bash_profile and .bashrc. They execute on a per user basis for interactive logins only. Both files are located every user’s /home directory. They are user specific configurations and freely editable by the owning user or root.
.bash_profile is a bash script that executes when a user invokes an interactive login shell on the system. Interactive login shells only occur when prompted for a password while logging in like when using ssh or telnet to access a system. .bash_profile is also called .profile on many systems as well.
.bashrc on the other hand, executes when an interactive non-login shell is invoked. Non-Login interactive shells occur when not prompted for credentials.






REVIEW  2024 04 16 
FG
NOTES
SYSINTERNALS ( net use) from the directory

WINDOWS PERSISTENCE MECHANISM\LAUNCH MECHANISM
          #RUN/RUN ONCE KEYS IN THE REGISTRY
          #SCHEDULED TASKS
          #POWERSHELL PROFILES
                   #test-path -path $profile.alluserallhost

LINUX PERSISTENCE
            #BASH PROFILES(ETC/PROFILE)
            #CRON -ETC/CRON    AND VAR/SPOOL/CRON ( SUDO -L SHOWS SUDO PRIVILEGES
            #INIT ( MAKE SURE I KNOW THE SYSTEM I HAVE, V OR D
           #DAEMON
           #RUNLEVEL

 METHODOLOGY

1.SUSPICIOUS PORT ( SUCCESSIVE NUMBERS >> “NETSTAT -ANOB” FOR WINDOWS
TO GET PORTS AND PIDS ####SUDO NETSTAT -LTUP for linux
2. FOUND THE PROCESS AND FIND OUT WHO STARTED THE PROCESS
3. MECHANISM FOR PERSISTENCE
4. LOOK FOR A FILE OR A PATH

LINUX PROCESS TREE((( PS -ELF - - FOREST))))

WINDOWS WE USE SYSINTERNALS

AUTORUNS


IF A HAVE A PORT OR A PID I CAN USE
      #####GET-PROCESS <PID> | SELECT NAME, ID, PATH
WINDOWS ARTIFACTS 
THINGS LEFT BEHIND
RECYBLE BIN, BAM, PREFETC, RECENT, JUMP LIST , BROWSER
USER ASSIST  ROT 13(NEEDS TO DECODE IT)

BAM -PRETTY EASY, SUS PATHS NOT SYS32, MAYBE PUBLIC/DOWNLOADS



PS C:\windows\system32> net use * http://live.sysinternals.com


LORDHAVEmercy$$

23456 port
Pid 


7632

## open powershell, run as admin **POWERSHELL COMMANDS**

    **commands:**
    **pwsh** - gets you powershell version
    **history** - shows commands you've used
    **get-member** - shows properties, methods and definitions for command
    **get-process** - shows running processes.
     **example of using get process**  get-process | select name,id,starttime
    **get-content** - to read a file
    **get-alias** - shows aliases of cmdlets
    **get-help** - gives you a help page. ex: get-help get-process
    **get-location / pwd** - shows current working directory
    **whoami** - shows who you're logged in as on box
    **dot notation:**
    get-process | select name
    (get-process).name
    **start processes** - notepad.exe (opens notepad)
    start-process notepad
    stop-process -name notepad
    or
    start-process chrome
    (get-process chrome*).kill()
    
    get-process | get-member | where-object {$_.membertype -match "method"}
    only pulling method's from the output of get-member

    get-process | select name, id, path | where {$_.id -lt '1000'}
    shows processes with an id less than 1000

    get-host - shows version of powershell you're using

    measure-object - counting lines in a file, summing, averaging
    select-string - search for text patterns in a string

    get-alias -definition Get-childitem (shows all aliases for get childitem)

     Get-CimInstance win32_service | ?{$_.Name -like 'LegoLand'} | select Description ((shows description of service))

      Compare-object (get-content new.txt) (get-content old.txt) ((compares difference between two text file))

     (get-content words.txt | Select-String -pattern "a","z").length ((counts number of times a or z appears in a word in the text file

     attached drives cli - fsutil fsinfo drives
     
 ## transcripts

    start-transcript
     ** enter commands here **
     stop-transcript
     ** then navigate to location and view/rename transcript **


 ## CIM Classes
    use this command when dealing with things like bios, or other physical things on machine.
    get-cimclass *
     shows all of your cim classes
    get-ciminstance -class win32_bios
     shows all of your bios information

 ## adding and removing items

    new-item does_not_exist.txt (-erroraction SilentlyContinue)
    remove-item does_not_exist.txt (-verbose)
## variables
    get-variable - shows variables
    $processes = get-processes
 
    $today = (get-date).datetime
    $today
    Tuesday, April 2, 2024 1:04:08 PM
    remove-variable -name today
    or clear variable by using
    clear-variable -name today

## wildcards
    if using wildcards * before or after, use -match(matches or when using regex) or -like(looking for   something similar)

## execution policy
    get-executionpolicy
    set-executionpolicy -executionpolicy unrestricted -scope currentuser
    get-executionpolicy
    unrestricted

## windows persistence mechanisms
    powershell profiles - 
     highest order of presidence = all users, all hosts - if this profile setting is set, it'll apply to all users, all hosts.
     all users, current host - if this is set, the profile will be set to all users on current machine
     current user, all hosts - if this is set, it applies to a current user on all machines
     current user, current host - applies to one user on one host.

     how to check = test-path -path $profile.currentusercurrenthost

     if it comes back true, 'cat' the command as seen above.

     $profile - tells us where the current profile is stored at
     
## linux persistence mechanisms

    /etc/init, /etc/inittab and /etc/rd0.d
    Are all places to look for persistence in Linux
    /etc/environment
    Holds all environmental variables and can contain persistence
    /etc/profile 
    Holds script 
          -	Bash_profile and .bashrc
          -    scheduled tasks
          -    zombie or orphaned processes/damaen
          -    crontab
          /etc/profile
    /etc/profile.d/* (various scripts in /etc/profile.d/)
    /home/<username>/.bash_profile (this fails, I have no such file)
    /home/<username>/.bash_login (this fails, I have no such file)
    /home/<username>/.profile
    /home/<username>/.bashrc
    /home/<username>/.bash_history (hi


## Windows Registry

    HKLM - HKEY_LOCAL_MACHINE
      HARDWARE - contains a database of installed devices along with their drivers
      SAM - Security Account Manager stores user and group accounts along with NTLM hashes of passwords
      Security - Local Security policy accessed by lsass.exe used to determine rights and permissions for users on the machine
      System - Contains keys pertaining to system startup such as programs started on boot or driver load order.
      
    HKU - HKEY_USERS
     contains user profiles on system. one key per user, each key is named after the SID of the user
     
    HKCU - HKEY_CURRENT_USERS
      is the copy of the logged in user’s registry key based on thier SID from HKEY_USERS.
    HKCC - HKEY_CURRENT_CONFIG
    
    HKCR - HKEY_CLASSES_ROOT

    All hives in HKLM are stored in %SYSTEMROOT%\System32\config\ (%SYSTEMROOT% usually refers to C:\WINDOWS).

    view/manipulate registry - regedit.exe
## manipulating registry in cmd

    ex: opening registry in command line
    reg query HKLM\software\microsoft\windows\currentversion\run
    reg add HKLM\SOFTWARE\microsoft\windows\currentversion\run /v testme /t REG_SZ /d C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
    reg delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v testme

## manipulating registry in powershell

    Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run ((reads sub keys from input value))
    Get-item HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run ((reads value of inputted object))
    New-Item "HKLM:\Software\Microsoft\Office\14.0\Security\Trusted Documents\TrustRecords" -Force ((creates new sub key associated with hive))
    
    New-ItemProperty "HKLM:\Software\Microsoft\Office\14.0\Security\Trusted Documents\TrustRecords" -Name "%USERPROFILE%Downloads/test-document.doc" -PropertyType Binary -Value ([byte[]](0x30,0x31,0xFF)) 

     New-ItemProperty HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run -Name Test -PropertyType String -Value C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe 

      Get-LocalUser | select Name, sid ((to see local users & sids in powershell))

## PSDrives

    Get-PSDrive ((find current PSDrives))
    New-PSDrive -PSProvider Registry -name HKU -Root HKEY_USERS ((add a drive))
    https://os.cybbh.io/public/os/latest/004_windows_registry/reg_fg.html

## Alternate Data Streams 

    https://os.cybbh.io/public/os/latest/005_windows_ads/ads_fg.html
    echo Always try your best > reminder.txt
    echo social security numbers > reminder.txt:secret.info ((adds social security numbers to reminder .txt in ADS))
    more < reminder.txt:secret.info ((to view hidden ADS))
    or
    notepad reminder.txt:secret.info

    To determine if there is an ADS do:
    dir /R

  ## Linux Essentials
  
     https://os.cybbh.io/public/os/latest/003_linux_essentials/bash_fg.html
     netstat -ano         to look at connections / ports
     pivot from port opening an executable - netstat -ano ((sudo netstat -ltup))
     ~ home directory
     / root directory
     file permissions       user,group,owner
     help information ls -- help
     or 
     man ls
     variables in linux:     a="100"       directories=$(ls /)
                             echo $a       echo $directories
                             100
     
     redirection -           echo $directories 1> thisisanewfile
     0 - standard input      cat thisisanewfile ((opens up your ls output from above))
     1 - standard output
     2 - standard error      ls bacon 2>/dev/null ((bacon doesnt exist, sends error message to the void))

     piping -                ls -Rlisa /etc | grep syslog ((R means recursive, grep is to search for a string)) 

     looping -                objects=$(ls -d /etc/*)
                              echo $objects
                              for item in $objects; do echo $item; done
                              or 
                              for object in $objects; do if [ -d $object ]; then echo "$object is a directory"; else echo "$object is a file" ; fi ; done

## Linux File Systems

    /bin directory - contains system binaries (commands like ls and echo)
    /home - contains directories for non root users
    /etc - contains configuration files, network configs, system services, firewall stuff etc
    /var - contains variable data, system logs etc.

    id - command that shows user id, group id etc. 
    cat /etc/passwd - also shows user information (might have to sudo it)
    ex: sudo cat /etc/passwd | grep garviel

    ex: man -k "digest"            searches man pages for something containing digest

    find ip's in a file:            cat numbers.txt | grep -Po '^\d{1,3}\.\d{1,3}\.\d{1,3}.\d{1,3}$' | wc -l


 ## Windows Boot Process

    https://os.cybbh.io/public/os/latest/006_windows_boot_process/winboot_fg.html
    
    lsass.exe - the Local Security Authority Subsystem (LSASS) provides user authentication services, manages the local security policy, and generates access tokens.

    services.exe the Services Control Manager (SCM) loads AutoStart services, using LSASS to authenticate if they run as something other than System.

    Ways to check services - 
     reg query hkey_local_machine\system\currentcontrolset\services\Spooler
     tasklist /svc

     bcdedit
     bcdedit /set {current} description "this is a description" ((to change something in bcd)
     
     To add stuff to bcd --
     bcdedit /create {ntldr} /d "win XP" -> bcdedit /set {ntldr} device partition=C: -> bcdedit /set {ntldr} path \downloads -> bcdedit /displayorder {ntldr} /addfirst

     to delete stuff from bcd --
     bcdedit /delete {ntldr} /f

     to restore backup -- 
     bcdedit /import C:\bcd.bk

 ## Linux Boot Process

    https://os.cybbh.io/public/os/latest/007_linux_boot_process/linboot_fg.html
    MBR - first 512 bytes of the HDD
    lsblk - list block devices, shows disk spaces 
    ex:
    sudo xxd -l 512 -g 1 /dev/vda
    shows:
    Execute xxd to hexdump 512 bytes in separated by 1 byte from /dev/vda to the screen
    The start of the hard drive shown by the code eb 63. File signature for an MBR.
    The first partition of the hard drive in 0x01be shown as 80
    The second partition entry is blank!

    ex:
    dd if=/dev/vda of=MBRcopy bs=512 count=1
    shows:
    Execute dd which copies 512 bytes once from /dev/vda to a file in my current directory called MBR
    Notice, dd failed to run
    !! represents the previous command. Run it with sudo permissions.
    Execute file to read the file signature from the MBR file
    ((dd is a bit for bit copy))

    ex:
    cat /boot/grub/grub.cfg
    shows:
    look through kernel to see what config you're going to load
    
     ex:
     ltrace -S cat /etc/passwd
     shows:
     shows system calls in linux

     ex:
     /etc/rc3.d$ ls -l /etc/rc3.d/
     List the contents of the /etc/rc3.d/ directory
    
     ex:
     systemctl list-dependencies graphical.target
     list unit dependencies in tree-form

     ex:
     systemctl show -p Wants graphical.target
     show wants to individual units

     ex:
     systemctl list-unit-files
     list every individual unit file

     The /etc/environment file sets Global Variables. Global Variables are accessible by every user or process on the system. It is read once when the machine completes Init. Any changes to the file require a system restart for them to apply. ((persistence))
     ex: cat /etc/environment
     
    /etc/profile is a script that executes whenever a user logs into an interactive shell on Linux. its functionality depends entirely on the version of Linux being used. Ubuntu Linux uses it to set the BASH shell prompt by executing /etc/bash.bashrc and execute any script named *.sh in /etc/profile.d ((persistence))
    ex: cat /etc/profile 

     Unique to BASH(Bourne Again Shell) are .bash_profile and .bashrc. They execute on a per user basis for interactive logins only. Both files are located every user’s /home directory. They are user specific configurations and freely editable by the owning user or root. ((persistence))

     linux persistence: etc/environment | inittab | /etc/profile | .bashprofile | runlevels
  

     How many wants dependencies does SystemD actually recognize for the default.target
     systemctl show -p Wants default.target | wc
 


 ### Windows process validity

     https://os.cybbh.io/public/os/latest/008_windows_process_validity/winproc_fg.html

 ## Windows Auditing and Logging
    https://os.cybbh.io/public/os/latest/011_windows_auditing_&_logging/artifacts_fg.html
    UserAssist
    Windows Background Activity Moderator (BAM)
    Recycle Bin
    Prefetch
    Jump Lists
    Recent Files
    Browser Artifacts
     
     Many artifacts will require the use of a Security Identifer (SID) to dig into the user specific registry locations for the artifact information.
     powershell - 
     Get-LocalUser | select Name,SID
     Get-WmiObject win32_useraccount | select name,sid

     CMD -
     wmic UserAccount get name,sid 

     The UserAssist registry key tracks the GUI-based programs that were ran by a particular user
     They are located in HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count\ * they are encoded in ROT13
     CEBFF5CD-ACE2-4F4F-9178-9926F41749EA A list of applications, files, links, and other objects that have been accessed
     F4E57C4B-2036-45F0-A9AB-443BCFE33D9F Lists the Shortcut Links used to start programs
     Get-ItemProperty "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count"
     *** for all users ***
     Get-ItemProperty "Registry::Hkey_Users\*\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count"

     Windows Background Activity Moderator (BAM) BAM is a Windows service that Controls activity of background applications (shows full path of an executable / last execution date/time.)
     HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings
     HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\UserSettings

     BAM entries for every user on the system
     Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\bam\state\UserSettings\*

     single user on the system
     wmic useraccount  get caption,sid | more -> then
     Get-Itemproperty 'HKLM:\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings\S-1-5-21-1584283910-3275287195-1754958050-1005'

     Recycle Bin
     SID - determines which user deleted it
     Timestamp - When it was deleted
     $RXXXXXX - content of deleted files
     $IXXXXXX - original PATH and name

     C:\$Recycle.bin

     Find the Contents of the Recycle Bin
     Get-Childitem 'C:\$RECYCLE.BIN' -Recurse -Verbose -Force | select FullName

     Match SID to USER:
     wmic useraccount where 'sid="S-1-5-21-1584283910-3275287195-1754958050-1005"' get name

     To find Recycle Bin artifacts for a specific user, match the SID, then append it to the previous command:
      Get-Content 'C:\$Recycle.Bin\S-1-5-21-1584283910-3275287195-1754958050-1005\$R8QZ1U8.txt'

      Prefetch
      Prefetch files are created by the windows operating system when an application is run from a specific location for the first time.
      location -> C:\Windows\Prefetch

      ex: Get-Childitem -Path 'C:\Windows\Prefetch' -ErrorAction Continue | select -First 8

      Jump Lists:
      location -> C:\%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations
      demo:
      Get-Childitem -Recurse C:\Users\*\AppData\Roaming\Microsoft\Windows\Recent -ErrorAction Continue | select FullName, LastAccessTime

      Recent Files -
      HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
      HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt

      Demo: Query the Hex Value Stored in the Key
      Get-Item 'Registry::\HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.*'

      Browser Artifacts - 
      %USERPROFILE%\AppData\Local\Google\Chrome\User Data\Default\history
      C:\Users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\

      #frequency : Z:\strings.exe 'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\History' -accepteula

      #most visited: Z:\strings.exe 'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\Top Sites'

      #user names: Z:\strings.exe  'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\Login Data'

      Get history - 
    $History = (Get-Content 'C:\users\student\AppData\Local\Google\Chrome\User Data\Default\History') -replace "[^a-zA-Z0-9\.\:\/]",""
     then
     $History| Select-String -Pattern "(https|http):\/\/[a-zA-Z_0-9]+\.\w+[\.]?\w+" -AllMatches|foreach {$_.Matches.Groups[0].Value}| ft

     Command Prompt: Checking System Wide Auditing Policy for all objects
     auditpol /get /category:*

     *Viewing Logs in Powershell*
     Get-EventLog -LogName System -Newest 10
     Get-EventLog -LogName System -Newest 3 | Format-Table -Wrap
     or
     Get-Eventlog -LogName Security | ft -wrap 
     Get-Eventlog -LogName Security | ft -wrap | findstr /i StR1nG 

     find log type to query
     Get-WinEvent -Listlog *
     Get-WinEvent -Listlog * | findstr /i "Security"

     Check if a user logged in:
     Get-Winevent -FilterHashtable @{logname='Security';id='4624'} | ft -Wrap
     
     powershell history location
     C:\Users\username\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
     
     Which sysinternals tool is used to parse logs? - psloglist

     What Sysinternals tool will allow you to read the SQLite3 database containing the web history
     of chrome? - strings

     Enter the full path of the program that was run on this computer from an abnormal location.
     Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\state\UserSettings\*
      
## Linux Auditing and Logging

     https://os.cybbh.io/public/os/latest/012_linux_auditing_&_logging/linlog_fg.html
     logging is controlled by syslog or journald
     Syslog stores its logs as human-readable text documents within /var/log. It is configured using files in /etc/rsyslog/
     
     view syslog configuration -> cat /etc/rsyslog.d/50-default.conf
     
      Filtering Syslog Output With Grep
      grep timesyncd /var/log/syslog

      Any logs having to do with logins and authentication attempts. . /var/log/auth.log - Authentication related events . /var/run/utmp - Users currently logged in .. Not in human readable format. Must use last command . /var/log/wtmp - History file for utmp .. Not in human readable format. Must use last command . */var/log/btmp - Failed login attempts

      Any logs having to do with programs. . Apache - Webserver (dir) . apt - Package Manager (dir) . /var/log/mysql.log

      SYSTEM - 
      /var/log/messages - Legacy Catch all

    /var/log/syslog - Ubuntu/Debian Catch all
    
    dmesg = Device Messenger (queires /proc/kmsg)
    
    Kernel Ring Buffer - Never fills
    
    First logs generated by the system

    Journald logs - 

    Journald or systemd-journald.service is the logging daemon for systemd init Linux systems. It logs everything in regards to *.units from unit startup status to logs generated by each individual unit. Journald stores its logs in binary form. journalctl is the open command that reads them.

     journalctl in its base form shows all the logs currently saved by journald. Warning, journald is verbose so it saves a lot of logs.

     ex:
     journalctl --list-boots
     journalctl -b b3076f6774b841e08c19236bf327f529
     journalctl -u ssh.service
     journalctl -u ssh.service --since "2 days ago"

     Select all of the IP addresses and ports using a single XPATH Union Statement
     xpath -q -e '//address/@addr | //ports/port/@portid' output.xml | md5sum

     This file is a conn.log made in Zeek (Bro) with data about TCP/IP connections.

    Use jq to locate and count the unique originating endpoint IP addresses in the file. Enter the number of unique originating IP addresses as the flag.
    jq -r '.["id.orig_h"]' conn.log | sort | uniq -c | wc -l


    This file is a conn.log made in Zeek (Bro) with data about TCP/IP connections.

    Use jq to locate and count connections where the destination IP sent more than 40 bytes to the source IP.
    jq -r 'select(.resp_ip_bytes > 40)' conn.log | sort | uniq -c

    Select every IP address with open (in use) ports using XPATH queries and XPATH axes.
    xpath -q -e '//ports/port/state[@state="open"]/../../../address/@addr | //ports/port[state/@state="open"]/@portid' output.xml | md5sum


 ## Memory Analysis

    Order of Volatility From Most to Least

    CPU registers, cache
    
    Routing table, ARP cache, process table, kernel stats, memory
    
    Temporary file systems
    
    Disk
    
    Remote logging and monitoring data
    
    Physical configuration, network topology
    
    Archival media - backups

    ex:
    What profile do you use in conjunction with this memory image?

    Use the following file (memory image) to answer the rest of the Memory Analysis challenges.
    
    0zapftis.vmem
     
     .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" imageinfo

     ex: to view history

     What command did the attacker type to check the status of the malware?

     .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" --profile=WinXPSP2x86 cmdscan
     
     ex:
     What are the last 7 digits of the memory offset for the driver used by the malware?
     .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" --profile=WinXPSP2x86 driverscan

     ex:
     The process running under PID 544 seems malicious. What is the md5hash of the executable?
      .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" --profile=WinXPSP2x86 procdump -p 544 -D .
      then
      Set-MpPreference -ExclusionPath 'C:\Users\andy.dwyer\Desktop\Memory_Analysis\'
      then
      Get-FileHash .\executable.544.exe -algorithm md5 ((run mppreference before everything maybe))

      ex:
       What remote IP and port did the system connect to?
      .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" --profile=WinXPSP2x86 connscan


  ## Active Directory

    https://os.cybbh.io/public/os/latest/014_windows_active_directory_enumeration/active_fg.html
    Examples of suspicious accounts include:

    Administrator accounts that aren’t known to the network owners
    
    Accounts that have been active outside of normal work hours
    
    Accounts that are nested in multiple administrative groups
    
    Service accounts logging into workstations
    
    Accounts that have logged in directly to the Domain Controller that are not normally authorized to do so
    
    This information can be collected through PowerShell and Windows Event Logs on the Domain Controller. Windows Logs are the best way to identify security issues.*

    *** use event viewer to check windows event logs ***

    Find the unprofessional email addresses. List the email's domain.
    Get-ADUser -Filter {EmailAddress -like '*'} -Properties EmailAddress | Select Name, EmailAddress

     
     ex:
     Find the accounts that contain unprofessional information in the description.
       Get-ADUser -Filter * -properties description | Select-Object Description,name

       ex:
       How many total users are members of the Domain Admins group?
        Get-ADGroupMember -Identity 'Domain Admins' -recursive | select name


   ## Test Review

      pull over sysinternals tools suite using net use
      https://os.cybbh.io/public/os/latest/015_windows_sysinternals/sysint_fg.html
      PS C:\windows\system32> New-PSDrive -Name "SysInt" -PSProvider FileSystem -Root "\\live.sysinternals.com\Tools"
      PS C:\Users\andy.dwyer\Desktop> $wc = new-object System.Net.WebClient
      PS C:\Users\andy.dwyer\Desktop> $wc.DownloadFile("https://download.sysinternals.com/files/SysinternalsSuite.zip","$pwd\SysinternalsSuite.zip")
      PS C:\Users\andy.dwyer\Desktop> Expand-Archive SysinternalsSuite.zip

      Windows persistence / launch mechanisms
         - run/run once keys
         - scheduled tasks 
         - Powershell profiles: testpath -path $profile allusersallhosts -> if true, cat what you just tested (test-path -path $profile.allusersallhosts)

     Linux Persistence:
         - bash profiles (etc/profile)
         - Cron (etc/cron or /var/spool/cron) ** if ya see something there, cat it, if permission denied try sudo *** sudo -l
         - init 
         - daemons
         - runlevels

     methodology - 

          - suspicious ports (repeating / sequential numbers)
             in linux - get ports and pids using (sudo netstat -ltup)
             netstat -ano/b

             find the process -> what started the process? -> find where the process was launched from, persistence mechanism, maybe multiple. 

     linux process tree - 

         ps -elf --forest

     windows process tree - 

        use sysinternals for process tree (procmon/procexp) don't forget autoruns for other things (scheduled tasks, runkeys etc)

          PORT/PID
           get-process <pid> | select name, id, path

           Windows Artifacts:
           https://os.cybbh.io/public/os/latest/011_windows_auditing_&_logging/artifacts_fg.html
             recycle bin
           1** BAM - Pretty easy, just pulling registry location (suspicious paths, not sys32, maybe public/downloads)
           2** prefetch - alot of stuff to parse through
               jump list
               recent
           3** userassist - ROT13 
               browser

        EXTRA USEFUL SHIT - 

        Get-LocalUser | select Name,SID (find usernames and SIDS)
        Get SIDS in command prompt -> wmic UserAccount get name,sid

        SysV or SystemD
        /lib/systemd/system ** for SystemD
        /sbin/init ** for SysV

        FraG=P3rS1st_@Ll_DaY!
        more $profile.allusersallhosts
