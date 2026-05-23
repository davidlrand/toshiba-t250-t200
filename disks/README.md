# Sample disk images

Bootable CP/M 2.2 disk images for both machines.

## Formats

- **`.imd`** — ImageDisk format. Standard for archiving early floppy media. **Read-only in MAME** (no save support).
- **`.mfi`** — MAME Floppy Image. MAME's native flux-level format. **Read AND write** — suitable for working with the disk inside the emulator (FORMAT, file creation, etc.).

## Conversion

To convert an IMD image to writable MFI:

```sh
# Using MAME's floptool
floptool flopconvert imd mfi source.imd output.mfi
```

To capture a fresh disk image from real hardware, use [Greaseweazle](https://github.com/keirf/greaseweazle):

```sh
# T-250 (8" DSDD)
gw read --drive=A --tracks=c=0-76:h=0-1 --format=ibm.scan disk.scp
gw convert disk.scp disk.imd

# T-200 (5.25" DSDD)  
gw read --drive=A --tracks=c=0-34:h=0-1 --format=ibm.scan disk.scp
gw convert disk.scp disk.imd
```

## Disk format reference

See [`../docs/disk-formats.md`](../docs/disk-formats.md) for the complete list of all 16 supported disk formats with cpmtools / libdsk / FlashFloppy definitions.

> **Note**: sample disk images to be added in a follow-up commit. Planned: at minimum one bootable T-250 image (CP/M 2.20 or 2.32) and one bootable T-200 image, plus an unformatted blank in each common format.
