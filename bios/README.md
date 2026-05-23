# CP/M 2.2 BIOS source

The replacement CP/M 2.2 BIOS source, written by Dave L. Rand in 1981-83. Assembled with Microsoft MACRO-80 (`M80`) or Digital Research RMAC.

## Files

| File | Purpose |
|------|---------|
| `bios64.asm` | Main BIOS source. Selects T-200 or T-250 build via `T250 equ 1` macro flag. |
| `equate.lib` | Port and constant definitions. |
| `handler.lib` | Non-disk I/O handlers (console, keyboard, printer, comm). |
| `diskdef.lib` | DPH/DPB definitions for all 16 disk formats (8 per machine). |

## Build flags

The single source builds for either machine and either hard-disk configuration via these conditional flags at the top of `bios64.asm`:

| Flag | Values | Meaning |
|------|--------|---------|
| `T250` | 0 / 1 | 1 = T-250 (8" floppy), 0 = T-200 (5.25" floppy) |
| `T200` | NOT T250 | (computed) |
| `M64` | 0 / 1 | 1 = 64K RAM, 0 = 68K (banked) RAM model |
| `M68` | NOT M64 | (computed) |
| `hard` | 0 / 1 | 1 = include SASI hard-disk support, 0 = floppy-only |
| `inch5` | 0 / 1 | 1 = 5.25" floppy media, 0 = 8" media |
| `m32` | 0 / 1 | 1 = 32 MB hard disk type variant (T-250 only) |

A typical T-250 build:
```
T250  equ 1
M64   equ 1
hard  equ 0   ; or 1 if SASI controller is wired
inch5 equ 0
m32   equ 0
```

A typical T-200 build:
```
T250  equ 0
M64   equ 1
hard  equ 0
inch5 equ 1
m32   equ 0
```

## Provenance

These files were recovered from period-original floppies of Dave Rand's source archive. The directory of best provenance (lowest corruption, fully-defined macros, all 8 disk formats and SASI support enabled) is the `b1/5` set. Other directories (`b2`, `b3`, `bios1`, `tm3`) contain alternate copies with varying levels of recovery quality — see commit history for the authoritative source path.

> **Note**: BIOS source to be added in a follow-up commit.
