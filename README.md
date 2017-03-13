# mkshares
PowerShell script for creating base set of directories on a file server.

Allows you to easily create folder structure for fileshares (including but not limited to Users,
Profiles, Public, RemoteInstall), program installation and database directories on a drive other
than C:\.

Requirements:
* Run from an elevated PowerShell.
* PowerShell ActiveDirectory Module.
* PowerShell SmbShare Module.
* PowerShell SmbWitness Module. 
* PowerShell Version 3 or later.

WARNING: If any of the folders specfied already exist backup any custom ACE settings because they will be removed.
    
For more help, examples and syntax run `PS C:\Get-Help .\mkshares.ps1` or browse the code.
