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
xfreerdp /u:student /v:10.50.36.208 /dynamic-resolution +glyph-cache +clipboard
     ########COMMAND TO GET IN THE WINDOWS SHELL#########

http://10.50.22.197:8000/register#####ip that gets me to the challenges####
      ####username : BRKA-M-502######
      ####password : MSFVENOM$$lauramu080897#######


https://vta.cybbh.space/project/instances/#####gets me to instances#####
#######username: bruno.kavutse58#######
#######password: MSFVENOM$$lauramu080897#######


xfreerdp /u:student /v:10.50.24.183 /dynamic-resolution +glyph-cache +clipboard
     ########RDP command to get to me to the_ADMIN_STATION#########
     #############Stack number = 1###################################
     ################IP ADDRESS = 10.50.24.183#####################


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


10.50.22.130  >>>>Windows

10.50.27.127 >>>>>linux

Stack 1


PS C:\windows\system32> net use * http://live.sysinternals.com


LORDHAVEmercy$$

23456 port
Pid 


7632
