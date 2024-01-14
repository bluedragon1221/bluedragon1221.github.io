## Check for UEFI
Before doing this, make sure your system uses EFI. You can check by finding the `efivars` folder.
```sh
[[ -d /sys/firmware/efi/efivars ]] && echo "EFI" || echo "BIOS"
```
If it returns `BIOS`, don't use this guide.

## Find the Right Drive
Sometimes `/dev/sda` is not the drive you want to install to. On virtual machines it can be `/dev/vda`, and on newer systems it can be `/dev/nvme0n1`. To make sure you use the right drive, check with `lsblk`.

## Partitioning
Now we will make the actual partitions. If you are uncomfortable with using `parted`, you can use `cfdisk` in the same way.

Create a new GPT partition table (this will wipe your drive).
```sh
parted /dev/sda -- mklabel gpt
```

Add the root partition. This will fill the whole disk, besides the 512MB in front (for the boot partition).
```sh
parted /dev/sda -- mkpart primary 512MB 100%
```

Finally, the boot partition. It uses the reserved 512MB at the start of the disk.
```sh
parted /dev/sda -- mkpart ESP fat32 1MB 512MB
```
## Formatting
For creating boot partitions (`fat32`), use `mkfs.fat`. Assign a label to the boot partition with `-n`.
```sh
mkfs.fat -F 32 -n boot /dev/sda3
```

For creating btrfs partitions, use `mkfs.btrfs`. `-L` labels the partition.
```sh
mkfs.btrfs -L root /dev/sda1
```
### Subvolumes
For this install, we'll have the following subvolumes:
- @ – This is the main root subvolume /.
- @tmp – Contains certain temporory files and caches
- @var - More temporary files
- @home - This is the home directory. This consists of most of your data including Desktop and Downloads. (Note: Not necessary with [[Create User#Systemd-homed|systemd-homed]])
- @snapshots – Directory to store snapshots.

```sh
mount --mkdir /dev/disk/by-label/root /mnt/btrfs
cd /mnt/btrfs
btrfs subvolume create @
btrfs subvolume create @var
btrfs subvolume create @tmp
btrfs subvolume create @home # Optional
btrfs subvolume create @snapshots
```

## Mounting
We'll mount all of the subvolumes:
```sh
mount -o subvol=@ /dev/disk/by-label/root /mnt

mount --mkdir -o subvol=@var /dev/disk/by-label/root /mnt/var
mount --mkdir -o subvol=@tmp /dev/disk/by-label/root /mnt/tmp
mount --mkdir -o subvol=@home /dev/disk/by-label/root /mnt/home # If you created it
mount --mkdir -o subvol=@snapshots /dev/disk/by-label/root /mnt/.snapshots
```

Mount the EFI Boot partition to `/mnt/efi`.
```sh
mount --mkdir /dev/disk/by-label/boot /mnt/efi
```
## Swapfile
You'll notice that we didn't allocate any space for a swap partition. That's because we're using a swap file.
```sh
btrfs subvolume create @swap
mount --mkdir -o subvol=@swap /dev/disk/by-label/root /mnt/swap
btrfs filesystem mkswapfile --size 4g --uuid clear /mnt/swap/swapfile
```