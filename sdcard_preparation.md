---
layout: page
title: SD Card Preparation
permalink: /sdcard_preparation
parent: Tools and resources
nav_order: 1
---

# SD Card Preparation for xDOS Devices

To ensure optimal performance and compatibility with xDOS devices (AIRDOS, SPACEDOS, and GEODOS), it is necessary to format the SD card by overwriting all sectors with zeros. This step guarantees that no residual data remains on the card, which could interfere with the system's operation or possible data recovery attempts.

You can use the provided script to properly format the SD card: [Format SD Script](https://raw.githubusercontent.com/UniversalScientificTechnologies/SPACEDOS03/refs/heads/SPACEDOS03A/scripts/formatsd.sh).

The script overwrites the **entire device** three times with `badblocks` (`0xff`, `0x00`, `0xff`) and then creates a fresh FAT32 filesystem with `mkfs.vfat`. This is fully destructive and **cannot be undone**, so it is critical to point it at the SD card and not at any other disk.

## 1. Identify the SD card device

Plug in the card and list the block devices:

```bash
lsblk -d -o NAME,SIZE,TRAN,RM,HOTPLUG,MODEL
```

The SD card is the device that:

- has a size matching the card (e.g. ~908M for a "1GB" card),
- is connected over `usb` (a card reader / "Card Bridge") or `mmc`,
- is marked removable and hotplug (`RM` and `HOTPLUG` both `1`).

Your internal system disk (typically `/dev/sda`, several hundred GB, `sata`, `RM`/`HOTPLUG` `0`) must **never** be selected. Overwriting it destroys your operating system.

In the rest of this guide the card is referred to as `/dev/sdX` — replace it with the device name you found above (for example `/dev/sdb`).

## 2. Unmount any mounted partitions

After insertion the card is usually auto-mounted as a partition (e.g. `/dev/sdX1`), not as the whole device. The script's `umount` only acts on the argument you pass it, so unmount the partition(s) yourself first:

```bash
umount /dev/sdX1
```

Check that nothing from the card is still mounted:

```bash
lsblk /dev/sdX
```

The `MOUNTPOINT` column should be empty for every partition.

## 3. Run the script

Run it against the **whole device** (`/dev/sdX`, without a partition number). The script needs `sudo` for `badblocks` and `mkfs.vfat`:

```bash
./formatsd.sh /dev/sdX
```

## 4. Final safety check

Immediately before confirming, verify once more that the target is really the card:

```bash
lsblk -o NAME,SIZE,TRAN,MODEL /dev/sdX
```

If the size or model looks like your system disk (e.g. hundreds of GB, or your SSD model name), **stop** — the device letters may have shifted after re-plugging.

Running it on a 1GB card takes only a few minutes; larger cards take proportionally longer because every sector is written three times.
