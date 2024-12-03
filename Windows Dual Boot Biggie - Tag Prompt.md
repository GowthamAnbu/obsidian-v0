Okay I was dual booting fedora 38 with windows 11 (upgraded from windows by disabling boot security and tpm - since my machine is very old) in my LENOVO-G50-45 laptop 1 TB, 16 GB, AMD A8, 2GB graphics card.
now I wanted to get rid of fedora 38 completely and only boot with windows 11

so I followed a youtube video title "How to Remove Ubuntu(Linux) From Dual Boot In Windows 11/10" (https://www.youtube.com/watch?v=mQyxtWrUNlE).It basically removed linux and boot directories inside the efi directory from a partition say eg.A and he deleted a healthy partition which has no letter assigned (i realise this just now. I thought he deleted the partition A, not sure why he added this deletion part this is very random and should not be in the video in the first place).

so simply removed the boot,fedora directories from partition say B (don't know the letter assigned exactly). Note I did the same he did in the youtube where he assigned some letter first and then removed the boot,fedora directories.after this I rebooted the machine and instead of the usual grub reboot window it simply notified not able to boot linux entry and I cliked ok. windows 11 booted normally)

now the part where I screwed up. I was trying to delete the partition (with boot,fedora, windows entries) from disk management utility but it only showed the help option when right clicked(i think this is the safety net by OS). I thought it is not helping and installed the easy us parition assistant and deleted the volume which had the boot,fedora,windows entries(boot and fedora directories are already removed previously form first step). Easy US app notified that restart is required. and then bang It didn't boot up...

help me boot windows 11 normally now.
now I have been again trying to solve it using the command prompt.

bootrec /fixmbr,
bootrec /fixboot,
bootrec /rebuildbcd

but the third rebuild command failed with "The requested system device can not be found".
I also fixed it by following the "https://www.partitionwizard.com/partitionmagic/the-requested-system-device-cannot-be-found.html" titled "3 Solutions to Fix the Requested System Device Cannot Be Found - MiniTool Partition Wizard"

START OF BLOG
Step 2. Input diskpart and press Enter to list all partitions and for you to identify EFI partition. Please note that EFI partition is formatted as FAT32 type (if the EFI partition is missing, click here to follow the instruction to create one).
Step 3. Input select volume 3 and press Enter (here volume 3 is the volume number of the EFI partition).
Step 4. Input assign letter=m to assign a letter to the EFI partition and press Enter. You may replace m with a letter of your choice.
Step 5. Input exit and press Enter to exit diskpart
Step 6. Then type the following commands in Command Prompt and press Enter after every command.
cd into EFI\Microsoft\Boot
bootrec /fixboot
Step 7. Input ren BCD BCD.bak and press Enter to change the name of BDC file from BCD to BCD.bak file.
Step 8. Input bcdboot c:Windows /l en-us /s m: /f ALL and press Enter to recreate BCD. If the letter you’ve assigned for the EFI partition earlier is not m, then change it in this command accordingly.
Step 9. Input exit to close Command Prompt and restart your computer.
END OF BLOG


but the problem still exists.

again after googling found out from reddit post "https://www.reddit.com/r/WindowsHelp/comments/wjtyhf/bootrec_rebuildbcd_the_requested_system_device/" titled "bootrec /rebuildbcd “The requested system device cannot be identified” : WindowsHelp" that there are multiple boot entires I mean there are multiple partitions with Boot,Microsoft,Fedora entries in it.

so now help me fix this. also I prefer commnand prompt and DON"T want to REINSTALL WINDOWS


okay I found this reddit post where it is clear

Reddit Start
DISKPART> list partition
Partition HHH Type Size Offset
Partition 4 System 499 MB 1024 KB
Partition 2 Reserved 128 MB 500 MB
Partition 3 Primary 464 GB 628 MB
Partition 4 System See mB 464 GB
Partition S Recovery s28 MB 46S GB
OK, by the look of partition's on "Disk 1" you have 2 EFI boot partitions; this may be confusing UEFI firmware, it's probably trying to boot from EFI boot partition with index 1 instead of EFI boot partition with index 4.

I have seen this issue happen when disk was converted from MBR to GPT with Microsoft's mbr2gpt tool, it creates new EFI partition by shrinking Windows partition (in your case partition with index 3) and creating new EFI boot partition (in your case EFI boot partition with index 4) and leaving original EFI boot partition (in your case EFI boot partition with index 1).



First, I would try to enter CMOS setting (BIOS / UEFI firmware settings) and specify to boot from "Disk 1 / Partition 4" instead of "Windows Boot Loader" entry that it detected.

If that does not work I would delete partition 4 from "Disk 1" and try to fix the the EFI boot partition under index 1.

Steps in DiskPart:
select disk 1
sel part 3
assign letter c
select part 4
del part override
sel part 1
format fs=fat32 quick label=Boot
assign letter s
exit

In command prompt now re-create EFI boot partition contents using BCDBOOT command like this:

bcdboot c:\windows /s S: /f UEFI

In order for this to work properly you need to make sure that windows partition (where Windows folder is located) is mounted with letter "C" as in "C:\Windows" and that EFI boot partition is mounted with letter "S" as in "S:\EFI".

After this you should be able to boot into your Windows system but the recovery tools will be busted...

To fix Windows Recovery Environment follow one of the methods in this video: https://www.youtube.com/watch?v=94QInTcTWt4
You will need to fiddle around with BCDBOOT.EXE to get the GUID of your "Windows Boot Loader" entry and REAGENTC.EXE from Command Prompt.
***Reddit End***



now I have partitions like 

Partition 1 - vol 5 - C - winre_drv - NTFS -> bcdbackup, EFI, Recovery.txt
Partition 2 - vol 6 - D - lrs_esp - FAT32 -> bootmgr.efi, Version.txt., EFI OneKey
Partition 4 - vol 7 - NO Letter - NO Label - NTFS -> No file
Partition 10 - vol 10 - K - PBR_DRV - NTFS -> OKRBackup, onekey, Recovery.txt


now I assume I can del part partitions 2,4,10 and only have part 1 format to fat32 and use bcdboot to configure it

D letter lrs_esp label - 709 files
+ Boot
	+ fonts
	+ bg-BG
	+ en-Us
	+ etc…(all languages)
	+ Resources
+ EFI
	+ Boot
		+ no files
	+ Microsoft
		+ Boot
			+ cs-cz
			+ en-us
			+ etc,…(all languages)
			+ Resources
			+ CIPolicies
		+ Recovery
			+ BCD file
+ OneKey
	+ winpe
		boot.sdi
		LRS.wim
	+ Main
		+ DRIVER
		+ IMAGE
		+ LANGUAGE
		+ MUITRANSFER
	+ OKR
		+ DRIVER
		+ IMAGE
		+ LANGUAGE
		+ MUITRANSFER
	+ OsImage
		+ CopySparse.exe
		+ Microsoft.VC80.CRT.manifest
		+ Microsoft.VC80.MFC.manifest
		+ msvcp80.dll
		+ msvcr80.dll
		+ OSImage.exe
		+ OSImage.ini
		+ OSImageDll.dll
		+ QuotaTools.exe
Bootmgr.efi
version.txt




C letter winre_drv label - 139 file 
+ Boot
	+ fonts
	+ bg-BG
	+ en-Us
	+ etc…(all languages)
	+ Resources
+ EFI
	+ Boot
		+ no files
	+ Microsoft
		+ Boot
			+ cs-cz
			+ en-us
			+ etc,…(all languages)
			+ Resources
			+ CIPolicies
		+ Recovery
			+ BCD file
+ Recovery 
	+ Logs
		BootUX(1).sqml
		BootUX(2).sqml
		Reload.xml
bcdbackup
Recovery.txt


given this  info I assume partition C is better partition to assume for configuring using 

bcdboot C:\Windows /l en-us /s C: /f ALL


or i should use partition D it has more files but it doesn't have recovery directories instead has a one key directory (this is not in C partition)