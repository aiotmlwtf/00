---
title: ae-notes
description: 
published: 1
date: 2020-03-01T19:02:47.011Z
tags: 
---

# sd-cards
1. old
2. original working inference and opencv
3. idem

Jetson.GPIO works version 2.0.4

## Clone sd-card

Run <kbd>diskutil list</kbd>, and find the disk corresponding to your Raspberry Pi's SD card:

$ <kbd>diskutil list</kbd>
/dev/disk0
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI                         209.7 MB   disk0s1
   2:                  Apple_HFS Macintosh HD            499.2 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
/dev/disk1
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *7.9 GB     disk1
   1:             Windows_FAT_32                         58.7 MB    disk1s1
   2:                      Linux                         7.9 GB     disk1s2

Clearly <kbd>/dev/disk1</kbd> is my 8GB SD card, the Linux partition name is also a bit of a clue.

However, instead of using <kbd>/dev/disk1</kbd> with <kbd>dd</kbd>, you should use <kbd>/dev/rdisk1</kbd>, like so:

<kbd>sudo dd if=/dev/rdisk1 of=/path/to/backup.img bs=1m</kbd>

And to restore it, just swap the if (input file), and of (output file) parameters:

But unmount first:
<kbd>diskutil unmountDisk /dev/diskX</kbd>
<kbd>sudo dd if=/path/to/backup.img of=/dev/rdisk1 bs=1m conv=sync</kbd> 

Or, with gzip, to save a substantial amount of space:

<kbd>sudo dd if=/dev/rdisk1 bs=1m | gzip > /path/to/backup.gz</kbd>

And, to copy the image back onto the SD:

<kbd>gzip -dc /path/to/backup.gz | sudo dd of=/dev/rdisk1 bs=1m</kbd>

Note
This takes long, use Ctrl-T to see progress.