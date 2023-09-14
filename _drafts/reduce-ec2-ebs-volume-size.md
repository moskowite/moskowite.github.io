---
layout: post
title: "Reduce EC2 EBS Volume Size"
date: 2023-09-08 08:08:08 -0800
last_modified_at: 2023-09-09 09:09:09 -0800
category: Documentation
tags:
    - aws
    - ec2
    - ebs
    - ubuntu
---



```console
lsblk
```

```console
blkid
```

```console
sudo rsync -axv / /mnt/small/
```

```console
sudo umount /mnt/small
```

```console
sudo grub-install --root-directory=/mnt/small/ --force /dev/nvme1n1
```

```console
sudo mount /dev/nvme1n1p3 /mnt/small
```



```console
sudo e2label /dev/nvme1n1p3 cloudimg-rootfs
```

```console
sudo tune2fs -U cd72a83d-aff1-4c36-b01f-a89a2f03d063 /dev/nvme1n1p3
```

```console
sudo e2fsck -f /dev/nvme1n1p3
```


```console
sudo mkfs.ext4 /dev/nvme1n1p3
```

```console
sudo mkfs.vfat -F 32 /dev/nvme1n1p2
```

## Getting Started

SSH into the EC2 instance and run the following commands to get started.

```console
sudo parted
```
From the parted command prompt, run the following commands to print the partition table. You will want to seek out the unrecognized disk label. In this example, the unrecognized disk label is `/dev/nvme1n1`.

Quit the parted command prompt when finished reviewing the partition table.

```console
(parted) print all
Model: Amazon Elastic Block Store (nvme)
Disk /dev/nvme0n1: 268GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name  Flags
14      1049kB  5243kB  4194kB                     bios_grub
15      5243kB  116MB   111MB   fat32              boot, esp
 1      116MB   268GB   268GB   ext4


Error: /dev/nvme1n1: unrecognised disk label
Model: Amazon Elastic Block Store (nvme)
Disk /dev/nvme1n1: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: unknown
Disk Flags:

(parted) quit
```

```console
sudo parted /dev/nvme1n1
```


```console
(parted) mklabel gpt
(parted) print
Model: Amazon Elastic Block Store (nvme)
Disk /dev/nvme1n1: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start  End  Size  File system  Name  Flags

(parted)
```


```console
(parted) mkpart bios_grub 1MB 5MB
(parted) mkpart 'boot, esp' fat32 5MB 116MB
(parted) mkpart ext4 116MB 100%
(parted) set 1 bios_grub on
(parted) set 2 boot on
(parted) set 2 esp on
```



```console
ubuntu@ip-172-40-19-82:~$ sudo mkfs.ext4 /dev/nvme1n1p3
mke2fs 1.46.5 (30-Dec-2021)
Creating filesystem with 13078528 4k blocks and 3270400 inodes
Filesystem UUID: bfc16f8a-2d7b-44ba-889c-3496da59a49d
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624, 11239424

Allocating group tables: done
Writing inode tables: done
Creating journal (65536 blocks): done
Writing superblocks and filesystem accounting information: done
```

```console
ubuntu@ip-172-40-19-82:~$ sudo mkfs.vfat -F 32 /dev/nvme1n1p2
mkfs.fat 4.2 (2021-01-31)

```




```console
ubuntu@ip-172-40-19-82:~$ sudo mount /dev/nvme1n1p2 /mnt/boot
ubuntu@ip-172-40-19-82:~$ sudo mount /dev/nvme1n1p3 /mnt/small
```