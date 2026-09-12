I'm writing this post mostly to keep track of the mechanics behind dual booting. I've done this so many times before, by just blindly following instructions, but this time I wanted to ensure I understood each step and document it. PS: this isn't a complete breakdown of eveyrthing but just enough for someone like me (who doesn't have a background in CS) to actually understand dual booting.

So the first step is to decide what os you want on the dual boot, most people have windows pre-installed and choose another os to boot alongside it. As a robotics students ROS is very critical for my applications so i naturally went with ubuntu (24.04) to install the recommended ROS2 Jazzy on it.

So now you know what os to install, I want linux distributed as Ubuntu versioned at 24.04.5 named Noble Numbat. Then we have to decide how muc space on disk to allocate to this installation. Start by checking the free space disk and create a new partition that is unallocated which we will later allocate to linux during installation. For this go to Disk Management. You'll see some basic partitions like EFI system, recovery windows C: and any other disk partitions you might have.

On the bar here you can see the capacity of the disk, then the disk on the far right that has the most amount of free space will be unallocated. Decide how much free space you want to be retained in windows and unallocate accordingly. 

so now you have the os, and the space set up. lets go get the iso image to be installed. Then go ahead and install the latest version of rufus. Get an empty usb drive or one you dont mind being wiped.

basically, windows automatically starts bootmgr as the bootloader, which is responsible for windows startup, but to dual boot you want to override this and have a custom boot menu where you have windows and linux as options. So selecting windows will load bootmgr and startup windows as usual with its own disk partitions, whereas selecting ubuntu will load ubuntu with its own disk partitions that we are yet to allot.

so to override booting from bootmgr, we need to start the system with a bootable drive, which is our usb drive which is made bootable through running rufus and selecting the usb drive as the target and flashing it with the iso image you downloaded so that the bootloader called grub that the booted pendrive installs can then load the iso image and install ubuntu.

once you get here, your installation basically needs you to know what partitions are needed for a linux installation. PS: while flashing the drive with the iso image, make sure you are selecting GPT as the partitioning system, because the newer disks come with uefi partitioning systems and so using gpt to do the linux partitions is compatible with uefi. Also selct DD for disk write in rufus options, this is faster and doesnt loose data (you will be asked if it is ok to wipe the drive out while flashing, say yes and backup any data) while writing the iso into the drive.

PS: in newer systems, bitlocker is automatically enabled. Simply speaking this is way that windows ensures the contents of your drive are safe. And booting from grub (say you have installed ubuntu all went well but now want to get back into windows) into windows, might flag to bitlocker as unauthorized entry and without the encryption key, you will loose acces to your disk. So make sure you have this key and password safely stored to enter if asked. (this is normally attached to the microsoft account you use on windows).

