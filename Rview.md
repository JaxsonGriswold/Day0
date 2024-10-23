##Review Day 
Forms of Persistence 
#Linux
-Cron
    -/etc/crontab
    -/var/spool/cron
    -/etc/cron.d
-/etc/Init  ---- specfies run levels for sysv
-/etc/profile
-/etc/enironment
-/etc/inittab  ---- Sysv
-/etc/rc.d/rc0.d/           Run Levels

-SERVICES/PROCESSES
    -ps -elf
    -top or htop
    -systemctl status <pid>
    
-/lib/systemd/systemd
-usr/lib/systemd/system




#Windows
Forms of Persistence
-SCHTASKS
-POWERSHELL PROFILE
  -4 profiles
  Test-Path -Path $profile.currentUsercurrentHost
-REGISTRY LOCATIONS
-SERVICES/PROCESSES
    -GET-SERVICE
      Get-process -id <pid>
    -GET-CIMIMSTANCE     
      win32_service
Artifacts (Windows Auditing and Logging)
-BAM
-Prefetch
-Userassist

Ports: Repeating or Sequential
44444444
55555555
12345678
3389(RDP) dont look at
Obfuscation:
taking the name of something legit ex.GoogleUpdate
Abnormal for a Gov device ex.Spotify, Steam, Discord
Mispellings of words
C:\windows\system32
C:\users\public\downloads\(for ex.) svchost.exe        stuff running from the wrong area
Autoruns - use Jump to entry option


Linux-
Find Evil
Process Validity

Windows-
Process Validity

User things on Windows Boot process
/etc/environment
/etc/profile
