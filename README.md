## Installing Debian 10 (Buster) on Dell XPS 13 9300

I recently managed to install Debian 10 on my new Dell XPS 13 9300 along side of Windows 10 (pre-installed). This installation process was complicated enough I thought I should write out how I managed to do this.

 System Specs
 * Dell XPS 13 9300- 13" UHD Touch
 * Intel i7-1065G7
 * 16GB RAM - 512GB SSD
 * Win 10 Home

### Warning
It really is possible to lose files in this process. Do back up anything important and be (at least mentally) prepared to reinstall Windows if necessary.

### Installation
* In Windows open the Disk Management partition.
 * Shrink the partition labelled "C:" by about 235 GB, or however much space you want to allocate to Debian
* Download the iso from [here](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/10.4.0-live+nonfree/amd64/iso-hybrid/)
  * I used one which included a desktop environment (KDE) since my machine does not have an ethernet connection.
* Create bootable usb with that iso
  * On another machine where linux already installed I could use this command with lsblk to check the location for the "of="
    *  sudo dd bs=4M if=path/to/input.iso of=/dev/sd<?> conv=fdatasync  status=progress
* Follow Choice #2 in [this answer](https://askubuntu.com/questions/1041305/ubuntu-16-04-cant-see-my-ssd-partitions-when-installing-alongside-windows-10/1041384#1041384)
    * Use F2 to enter Bios Setup directly (or F12)
    * The option to change to AHCI is under System Configuration on the left
    * I also tried Choice #1 but then Windows wouldn’t boot and I needed to fix that before moving on…
    * Check Windows still boots
* Plug in your bootable USB
* Restart and return to Bios Setup
    * In Bios Setup enable USB Boot Support and External USB Ports as well as Thunderbold Technology and Boot Support to allow booting from your USB.
    * Apply changes and exit tapping F12 to enter the One-Time Boot Menu.
* From the boot menu which you got to from using F12 on reboot
 * Select the option to boot from your USB
* Follow graphical installer prompts to install
  * I found that [this video](https://www.youtube.com/watch?v=kN5GYyTRG94&t=203s) and [this video](https://www.youtube.com/watch?v=3lRkjWTUuhc&t=1255s) were helpful
  * I chose manual partition and split the space allocated to Debian 10 into a 32 GB swap and the rest as Ext4 journaling file system
    * For more on swap see [here](https://itsfoss.com/swap-size/)
    * For the Ext4 partition choose
      * Yes to format
      * / as mount point
      * The other defaults are fine.
    * Finish and write changes to disk.
  * Choose 'no' to network mirror

And after all that the GUI doesn't load. I just get a console when Debian boots. To be continued...
