# Sample disk images

Bootable CP/M 2.2 disk images.  Files are gzip-compressed for repo size; uncompress before use.

## Contents

### T-250 (8" DSDD)

| File | Description |
|------|-------------|
| [`T-250/Toshiba-original-v2.20.mfi.gz`](T-250/Toshiba-original-v2.20.mfi.gz) / [`.hfe.gz`](T-250/Toshiba-original-v2.20.hfe.gz) | Original Toshiba-shipped CP/M 2.20 boot disk |
| [`T-250/boot-2.14g.mfi.gz`](T-250/boot-2.14g.mfi.gz) / [`.hfe.gz`](T-250/boot-2.14g.hfe.gz) | Earlier BIOS revision 2.14g, with a substantial collection of CP/M utility programs |

Two formats per disk:
- **`.mfi`** — MAME Floppy Image.  Read AND write inside MAME; suitable for adding files, formatting, etc.
- **`.hfe`** — HxC Floppy Emulator flux-level format.  Use with GOTEK/FlashFloppy hardware or the HxC Floppy Emulator software.  Read AND write.

## Quick start

Uncompress and launch in MAME:

```sh
gunzip -k T-250/Toshiba-original-v2.20.mfi.gz
mame t250 -window -flop1 T-250/Toshiba-original-v2.20.mfi
```

(`gunzip -k` keeps the `.gz` alongside the uncompressed file.)

For real hardware via GOTEK/FlashFloppy, copy the uncompressed `.hfe` to the USB stick.

## Format coverage

The MAME driver accepts a number of standard floppy formats: `.imd` (read-only), `.mfi` (read/write), and various MFM containers.  The HxC `.hfe` format is the most portable for both emulation and real-hardware replay via GOTEK.

`.imd` (Dave Dunfield's ImageDisk format) is widely supported by vintage CP/M tools.  MAME's `floptool` cannot write IMD; if you need it, convert via [Greaseweazle](https://github.com/keirf/greaseweazle):

```sh
gunzip -k T-250/Toshiba-original-v2.20.hfe.gz
gw convert T-250/Toshiba-original-v2.20.hfe T-250/Toshiba-original-v2.20.imd
```

Or via the HxC Floppy Emulator GUI's export function.

## Capturing fresh disks from real hardware

Use [Greaseweazle](https://github.com/keirf/greaseweazle):

```sh
# T-250 (8" DSDD)
gw read --drive=A --tracks=c=0-76:h=0-1 --format=ibm.scan disk.scp
gw convert disk.scp disk.imd
# or
gw convert disk.scp disk.hfe

# T-200 (5.25" DSDD)
gw read --drive=A --tracks=c=0-34:h=0-1 --format=ibm.scan disk.scp
gw convert disk.scp disk.imd
```

## Disk format reference

See [`../docs/disk-formats.md`](../docs/disk-formats.md) for the complete list of all 16 supported disk formats (8 per machine) with cpmtools / libdsk / FlashFloppy definitions.

## What's missing

- T-200 (5.25" DSDD) bootable disks — to be added.
- Source-disk images for the BIOS, debugger, language tools.
- Hard-disk CHD samples — covered separately in the MAME usage guide; not bundled here.
