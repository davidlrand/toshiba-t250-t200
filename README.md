# Toshiba T-250 / T-200

Preservation archive for the **Toshiba T-250** and **Toshiba T-200** CP/M business computers (circa 1981), including the replacement boot ROM and CP/M 2.2 BIOS authored by Dave Rand, sample bootable disk images, and documentation for using the surviving machines in emulation.

## What these machines were

The T-200 (5.25" DSDD floppies) and T-250 (8" DSDD floppies) were Toshiba's early-1980s 8085-based desktop business computers. Both share the same main board, peripheral set, and replacement CP/M BIOS — only the floppy subsystem differs.

| | T-200 | T-250 |
|---|---|---|
| Released | 1981 | 1981 |
| CPU | Intel 8085A @ 5.333 MHz | Intel 8085A @ 5.333 MHz |
| RAM | 64 KB | 64 KB |
| Display | 80 × 24 character, hardware inverse | 80 × 24 character, hardware inverse |
| Keyboard | 8279 matrix + 8-key keypad | 8279 matrix + 8-key keypad |
| Floppy | 5.25" DSDD, 35 tracks, 300 RPM | 8" DSDD, 77 tracks, 360 RPM |
| Serial | 8251 USART (CCM board) | 8251 USART (CCM board) |
| Printer | Centronics parallel | Centronics parallel |
| Hard disk (optional) | SASI via 8155 host adapter | SASI via 8155 host adapter |

## About this BIOS

The boot ROM and CP/M 2.2 BIOS in this repo are **not** Toshiba's stock firmware. Dave L. Rand was a reseller of these machines in 1981-83, and wrote a replacement boot ROM and full CP/M BIOS from scratch because the supplied Toshiba firmware was inadequate for resold-system customers. The firmware in this archive shipped with the systems Dave sold.

## What's in this repo

| Path | Content |
|------|---------|
| [`rom/`](rom/) | Boot ROM binaries (`t250boot.bin`, `t200boot.bin`, `t250cg.bin` chargen) |
| [`bios/`](bios/) | CP/M 2.2 BIOS assembly source (`bios64.asm` + library files), recovered from period-original floppies |
| [`disks/T-250/`](disks/T-250/) | Two bootable T-250 CP/M 2.2 disk images (`Toshiba-original-v2.20`, `boot-2.14g`), each in both MFI and HFE formats, gzipped |
| [`docs/disk-formats.md`](docs/disk-formats.md) | Reference document for all 16 disk formats (8 per machine) — cpmtools `diskdef`, libdsk format definitions, FlashFloppy/GOTEK guidance, BIOS-extracted skew tables |
| [`docs/mame-usage.md`](docs/mame-usage.md) | Quick-start guide for using these ROMs and disks with MAME (driver at `src/mame/toshiba/t250.cpp` in upstream MAME) |

> **Note**: this repository is being populated incrementally. T-200 (5.25") bootable disks and BIOS assembly source are still to come — check back for new content.

## Quick start

```sh
# Get MAME 0.290 or later (driver landed 2026)
# Drop boot ROMs into MAME's ROM path:
mkdir -p roms/t250 roms/t200
cp rom/t250boot.bin roms/t250/
cp rom/t200boot.bin roms/t200/

# Uncompress one of the T-250 boot disks and run:
gunzip -k disks/T-250/Toshiba-original-v2.20.mfi.gz
mame t250 -window -flop1 disks/T-250/Toshiba-original-v2.20.mfi
```

For more options (serial port, hard disk, real-hardware replay via GOTEK), see [`docs/mame-usage.md`](docs/mame-usage.md).

## MAME emulation

These machines are emulated in upstream MAME by the `t200` and `t250` drivers in `src/mame/toshiba/t250.cpp` — same author as the BIOS. See [`docs/mame-usage.md`](docs/mame-usage.md) for the command-line invocations and a quick-start tutorial.

## License

- **Code, BIOS source, ROMs**: MIT License (see [`LICENSE`](LICENSE))
- **Documentation**: MIT License

## Credits

- **Hardware**: Toshiba Corporation, 1981
- **Replacement boot ROM and CP/M 2.2 BIOS**: Dave L. Rand, 1981-83
- **MAME driver**: Dave L. Rand, 2026 — derived from the original BIOS source and verified against working physical hardware
- **MAME `t250.cpp` source assistance**: collaboration with Claude (Anthropic), 2026

## Contact

GitHub: [@davidlrand](https://github.com/davidlrand)
