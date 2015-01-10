<!-- 
.. title: How-To: Install Arch Linux on an encrypted Btrfs partition
.. slug: how-to-install-arch-linux-on-an-encrypted-btrfs-partition
.. date: 2014-10-14T22:17:40+02:00
.. tags: archlinux, btrfs, encryption, luks
.. link: 
.. description: 
.. type: text
-->

These are the steps I followed to install Arch Linux on my SSD. There are two
partitions: `/dev/sda1` for `/boot` and `/dev/sda2` for the rest of the system.
The last one is encrypted with dm-crypt and formatted in Btrfs. The first one
stays unencrypted as it is needed by the BIOS to boot the system (although it
seems possible to have it encrypted too, but I didn't try).

Please use common sense and do not copy/paste commands without first trying to
understand what they do! And also remember to backup everything: I am not
responsible for any loss of data!

I consider that you just booted on your Arch Linux install medium (note that the
"SSD preparation" step can be done from an already installed system as it might
take some time).

# Keyboard layout
```console
# loadkeys be-latin1
```

# SSD preparation
We will fill up the SSD with random data.

Create a temporary encrypted container on `/dev/sda`:
```console
# cryptsetup open --type plain /dev/sda container
```

Check it exists:
```console
# fdisk -l
Disk /dev/mapper/container: 232.9 GiB, 250059350016 bytes, 488397168 sectors
```

Wipe it with pseudorandom encrypted data (use of `/dev/urandom` is not required
as the encryption cipher is used for randomness):
```console
# dd if=/dev/zero of=/dev/mapper/container
```
(Took me 1 hour on my 250 GB Samsung 840 EVO)

Close the container:
```console
# cryptsetup luksClose container
```

# Partitioning
Create two GPT partitions:
```console
# gdisk /dev/sda
```

* `/dev/sda1`: 128 MiB for `/boot`
* `/dev/sda2`: the remaining space for the system

Prepare boot partition:
```console
# mkfs.ext2 /dev/sda1
```

Prepare encrypted partition:
```console
# cryptsetup --cipher aes-xts-plain64 --hash sha512 --use-random --verify-passphrase luksFormat /dev/sda2
```

Open encrypted partition:
```console
# cryptsetup luksOpen /dev/sda2 root
```

Format encrypted partition in Btrfs:
```console
# mkfs.btrfs /dev/mapper/root
# mount -o noatime,discard,ssd,defaults /dev/mapper/root /mnt
```

Create Btrfs subvolumes:
```console
# cd /mnt
# btrfs subvolume create __active
# btrfs subvolume create __active/rootvol
# btrfs subvolume create __active/home
# btrfs subvolume create __active/var
# btrfs subvolume create __snapshots
```

# System configuration
Mount subvolumes in `/mnt`:
```console
# cd
# umount /mnt
# mount -o subvol=__active/rootvol /dev/mapper/root /mnt
# mkdir /mnt/{home,var}
# mount -o subvol=__active/home /dev/mapper/root /mnt/home
# mount -o subvol=__active/var /dev/mapper/root /mnt/var
```

Mount boot partition:
```console
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot
```

Install system
```console
# pacstrap /mnt base base-devel btrfs-progs
```

Generate fstab
```console
# genfstab -p /mnt >> /mnt/etc/fstab
```

Edit /mnt/etc/fstab and add the following options:
```console
/dev/mapper/root    /       btrfs   noatime,discard,ssd,autodefrag,compress=lzo,space_cache,subvol=__active/rootvol ...
/dev/mapper/root    /home   btrfs   noatime,discard,ssd,autodefrag,compress=lzo,space_cache,subvol=__active/home    ...
/dev/mapper/root    /var    btrfs   noatime,discard,ssd,autodefrag,compress=lzo,space_cache,subvol=__active/var     ...
/dev/sda1           /boot   ext2    ...
```

Chroot into the new system
```console
# arch-chroot /mnt
```

Configure hostname, timezone, locale, keymap, etc.

Add the `encrypt` hook in /etc/mkinitcpio.conf (before `filesystems`) so that it
looks something like this:
```console
HOOKS="base udev autodetect modconf block encrypt filesystems keyboard fsck"
```

Rebuild the boot images:
```console
# mkinitcpio -p linux
```

Set root password:
```console
# passwd
```

Configure SYSLINUX:
```console
# pacman -S syslinux gptfdisk
# syslinux-install_update -iam
```

Edit `/boot/syslinux/syslinux.cfg`:
```
LABEL arch
    ...
    APPEND root=/dev/mapper/root rootflags=subvol=__active/rootvol cryptdevice=/dev/sda2:root rw
    ...
```

Exit chroot.

Unmount everything:
```console
# umount /mnt/{home,var,boot}
# umount /mnt
```

Reboot:
```console
# reboot
```
