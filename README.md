# Setting-Up-Ubuntu-18.04-and-Windows-10-dual-boot-XPS-15-9570
I had lots of trouble trying to find a working step by step guide for this. So after spending a weekend to get my system to work without any problems taking bits from every guide out there, I wanted to fill that gap.
# Disclaimer
I am just sharing what has worked for me. You might experience different results or a damage to your system or OS that might require you to reset your laptop. Please back up everything and have a windows recovery USB ready before continuing! Also make sure to register your laptop with Windows. I have read that some people were asked for their bitlocker key after changing from "Raid On" to "AHCI" and you need your recovery key from microsoft for that.
## Specs of the XPS 15 I used while making this guide
  * nVIDIA 1050Ti GPU
  * Intel 8th Gen i7-8750H CPU
  * 1TB M.2 2280 PCIe Solid State Drive
  * 32GB of DDR4-2666MHz RAM
## This guide assumes:
You have installed Windows 10 when you first got your laptop.
That's it!
## Before doing anything
* You need to update your BIOS and nVDIA drivers.
    1. Go to https://www.dell.com/support/ and detect your PC.
    2. Select Drivers & downloads
    3. Download and update the BIOS and nVIDIA drivers.
* You need to turn off fast startup because of Windows hibernation.
    1. Search for "Power & Sleep Settings" in your search box.
    2. Click "Additional power settings" ->  "Choose what the power buttons do" -> "Change settings that are currently unavailable"
    3. Check off fast startup and save changes.
## Setting up a live boot USB
  1. Go to https://www.ubuntu.com/download/desktop and download the ISO.
  2. Go to http://rufus.akeo.ie/ and download Rufus to be able to create the bootable USB.
  3. Open Rufus after downloading.
  5. From Device select your USB.
  4. From boot selection select Disk or ISO image and click "SELECT".
  5. Find and select your Ubuntu ISO.
  6. You need to set the Partition Scheme to GPT as we need to boot in UEFI and not legacy.
  7. Make sure that the file system selected is FAT32 or it won't work.
  8. Click "START"
  9. Select write in DD image mode.(I had trouble booting up from the USB when I selected ISO Image mode.)
## Changing from RAID to AHCI
  1. Boot in to Windows
  2. Type 'Change advanced Startup Options' to your search box.
  3. Click 'Restart Now'.
  4. You wil boot to a blue screen with options.
  5. Click Troublehoot -> Startup Settings-> Restart
  6. Press F2 repeatedly while booting up to go into BIOS setup
  7. Once in the menu go to System Configuration -> SATA operation and change it from "Raid On' to "AHCI"
  8. Apply and exit
  * If you are asked for your bitlocker key(I was not)
    9. Go to https://account.microsoft.com/devices/recoverykey to get your key
  10. Choose option 4.Enable Safe Mode
  11. Search for 'Device Manager' in your search box.
  12. Check that your "ATA/ATAPI Controller" is a SATA AHCI Controller.
## Managing partitons your Windows partition
  1. Search for "Create and format hard disk partitions" in your search box.
  2. Find "(C:)" in your partitions
  3. Right click and "Shrink Volume"
  4. Enter the amount you want to seperate for your Ubuntu installation and click "Shrink"
## BIOS Changes
  1. Reboot your computer and repeatedly press F2 until you get in to the BIOS Setup
  2. Go to "Secure Boot" -> "Secure Boot Enable" and un-check the box for "Secure Boot Enable"
  3. Go to "General" -> "Advanced Boot Options" and check "Enable Legacy Options ROMs"
  4. Connect your USB.
  5. Apply and exit.
## Installing Ubuntu
  1. Press F12 repeatedly while booting to acces the boot menu.
  2. Look under the "UEFI Boot" to find your USB and select that option.
  3. This will take you to GRUB.
  4. Choose Install Ubuntu.
  5. Choose your language settings and connect to your WiFi.
  6. On the "Updates and Other Software" un-check "Download updates while installing Ubuntu".
  7. On the "Installation Type" screen select "Something Else".
  8. On the partition screen find the space you allocated for Ubuntu Installation from Windows. It Should say free next to it, select it and click "+" each time to add the partitons below.
  9. Allocate space for "/" (Root) partiton. (I allocated something like 20 GB for this. >10GB)
  10. Allocate space for "Swap" partition. (2x your RAM size is recommended.)
  11. Allocate space for "/boot" partition. (500MB-1GB. I allocated 1 GB.)
  12. Allocate space for "/home" partition. (This is the filesystem for your user's files: documents, images, music and videos.I allocaed the rest of the free space to this partition.)
  13. Just follow the installation as the rest of it is trivial.
  14. When you reboot after the installation you should be greeted by GRUB if everything went the way it should!
 
  
