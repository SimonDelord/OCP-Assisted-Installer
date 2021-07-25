# OCP-Assisted-Installer
These are my experiments with the OCP Assisted Installer


Here's the process that I have followed to deploy an OCP Cluster on 3 NUCs (4 vCPUs, 16 GB for 2 of them and 8 vCPUs and 16 GB of RAM for the 3rd one).

## 1st step: log into cloud.redhat.com/openshift/assisted-installer/clusters
## 2nd step: follow the menu until you download the ISO file.
## 3rd step: I did not use PKE, for this one I used a bootable USB device (using my Mac).
I followed the steps in https://www.lewan.com/blog/2012/02/10/making-a-bootable-usb-stick-on-an-apple-mac-os-x-from-an-iso

    - first step: convert the .iso into a .img by using hdiutil convert -format UDRW -o /path/to/target.img /path/to/source.iso

    - second step: convert the .img.dmg file into a .img (OS X does that not sure why). mv /path/to/target.img.dmg /path/to/target.img
    
    - third step: run diskutil list to get the current list of devices
    
    - fourth step: insert your flash media and run diskutil list again to determine the device node assigned to the flash media (typically /dev/disk2 or /dev/disk3)
    
    - fith step: Execute sudo dd if=/path/to/downloaded.img of=/dev/rdiskN bs=1m (replace /path/to/downloaded.img with the path where the image file is located; for example, ./ubuntu.img or ./ubuntu.dmg).

Note: Using /dev/rdisk instead of /dev/disk may be faster.
Note: If you see the error dd: Invalid number '1m', you are using GNU dd. Use the same command but replace bs=1m with bs=1M.
Note: If you see the error dd: /dev/diskN: Resource busy, make sure the disk is not in use. Start the 'Disk Utility.app' and unmount (don't eject) the drive.
   - six step: run diskutil eject /dev/disk2 (or disk3) and remove the USB stick.


## 4th step: repeat the operation above until you have 3 USB sticks with the bootable ISO (e.g the .img file) on each one of them. 
Please note that I used the Disk Utility facility from MAC to erase them first (as MS-DOS (FAT)) for each USB stick.

## 5th step: plug each USB stick onto each of the NUCs
You may have to change the boot order, but as part of the setup, each NUC needs to have Internet access and simply boot from the USB.

## 6th step: just watch the OCM console 
after a few minutes, the NUCs should come online and you will be able to change their names

## 7th step: click on the proceed button at the bottom of the screen

## 8th step: wait for the installation to finish (around 30-40 minutes).

## 9th step: connect to the cluster
you may have to change your DNS settings on your laptop or on your DNS server to reach the OCP cluster.
