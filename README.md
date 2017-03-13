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

If you want to change the permissions for Limited add the user/group and set the permissions
in Explorer. Use PS C:\> Get-ACL -path "[Path\To\File/Directory]" | select -expand access | Format-List
to see the new permissions. Add or Remove the ones you want to these entries in the "Limited" section
appropriate line either 343, 345 or 346. If an entry says None use ::None.

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!   WARNING: If any of the folders specfied already exist any custom ACE settings will be removed.   !!!!! 
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    
Parameter -Root_Drv "<DriveLetter>"
        MANDATORY The root drive letter for the folders to be created. Use only the drive letter (E not E:\).

Parameter -Share_DIR "SharedFolderName
        OPTIONAL Changes the name of the root shared folder from "Shares". Only used to modify -AD_DIR and/or
               -WDS_DIR.

Parameter -Share
      OPTIONAL Creates fileshares for the folders created in "$Root_Drv:\Shares" and grants "Everyone"
               FullAccess. Use NTFS premissions to granulary control access to the shares. Only used to modify
               -AD_DIR and/or -WDS_DIR.

Parameter -AD_DIR
      OPTIONAL Creates a base set of directories to be shared and their ACLs.
               See AD_DIR section to modify the directories.

Parameter -DB_DIR
      OPTIONAL Create $Root_Drv`:\Databases directory and ACLs. If -Share is specified the folder will be created
               in $Root_Drv`:\$Share_DIR and shared.

Parameter -IIS
      OPTIONAL Use flag to see link to move IIS cleanly. 

Parameter -Prog_DIR
      OPTIONAL Creates $Root_Drv:\Program Files for application installation. If the system is 64Bit
               creates $Root_Drv:\Program Files (x86) also.

Parameter WDS_DIR
      OPTIONAL Creates $Root_Drv:\RemoteInstall directory and ACLs for Windows Deployment Services.
      
Example
      PS C:\> mkshares.ps1 -Root_Drv "E" -AD_DIR -WDS_DIR
      Creates a base set of folders to be shared and a RemoteInstall folder.

Example
      PS C:\> mkshares.ps1 -Root_Drv "E" -AD_DIR -WDS_DIR -Share
      Creates a base set of folders to be shared, a RemoteInstall folder and shares them.

Example
      PS C:\> mkshares.ps1 -Root_Drv "E" -Share_DIR "Put Shares Here" -AD_DIR -DB_DIR
      Creates a base set of folders to be shared, changes the shared folder name to "Put Shares Here"
      and creates a Database folder.

Example
      PS C:\> mkshares.ps1 -Root_Drv "D" -Prog_DIR
      Creates program installation directories on a drive other than C:\.
