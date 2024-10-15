http://10.50.22.129:8000/
https://os.cybbh.io/public

###Powershell Day 1:
##Commands and Arguments
Get-Content -Path "C:\Test Files\content.txt"                                         # Displays the contents of the file
Get-Variable                                                                          # Displays current Variables
Get-Verb                                                                              # List the PowerShell verbs
Get-Command                                                                           # List the PowerShell cmdlets
Get-Command -Type Cmdlet | Sort-Object -Property Noun | Format-Table -GroupBy Noun    # Get cmdlets and display them in order
Get-Command -Module Microsoft.PowerShell.Security, Microsoft.PowerShell.Utility       # Get commands in a module

##Using the Methods of Objects
Get-Process | Get-Member | Where-Object {$_.Membertype -match "Method"}

