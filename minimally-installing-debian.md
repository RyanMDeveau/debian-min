### Recommended Release

This has been created with the intent to use on a [netinst testing release of Debian](https://www.debian.org/devel/debian-installer/)

### Manual Partitioning

Basic instructions for installation of debian with two partitions, a small boot partition that should/can be installed onto a USB, and an encrypted partition on another mass storage device

1. **Creat Boot Partition**  
create a **512MB /boot** partition on a USB drive  
let it be a primary partition  
let it be created at the beginning of the storage space  
set the mount point to /boot  
change the bootable flag to on  

1. **Create Encrypted Partition**  
create a new partition the size you would like your encrypted drive to be  
let it be a logical partition  
let it be created at the beginning of the storage space  
change the use to "physical volume for encryption"  

1. **Configuring Encrypted Volume**  
auto configure the encrypted volume - encryption password should be at least 20ch  
change the use of the encrypted volume to "physical volume for LVM"  
create a LVM volume group called "vg" on the encrypted drive  
create a **minimum 20GB** logical volume called "root"  
create a *remaining space/optional* logical volume called "home"  
set the file system of "root" logical volume to use Ext4  
set mount point of "root" to /  
set the file system of "home" logical volume to use Ext4  
set mount point of "home" to /home  
change the reserved blocks to 1%  
install grub onto USB drive

1. **Creating Swap File**  
sudo fallocate -l 2G /swapfile  
sudo chmod 600 /swapfile  
sudo mkswap /swapfile  
sudo swapon /swapfile  
sudo nano /etc/fstab  
/swapfile none swap sw 0 0
