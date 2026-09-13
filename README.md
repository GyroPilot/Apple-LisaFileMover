# LISAFile

A standalone file utility for the Apple Lisa Office System: a native LOS
desktop tool that lists, copies, renames and deletes "invisible" files
between volumes and floppies, built on the working-volume model from
LISACom 1.6. Later: moving whole tool file sets with their labels.

Tool number **419311** in the GyroPilot series (LISACom 419306, Atkinsonpoint
419307, LOS Installer 419310). Written in Lisa Pascal with the Workshop 3.0
toolchain for Lisa Office System 3.1, developed and verified on a Lisa 2/10.

## Status

REV A not started. This repository holds the project skeleton, the build
helpers, and the conventions carried over from LISACom and Atkinsonpoint.
See CHANGELOG.md once builds begin.

## Layout

    sources/LFU-MAIN.TEXT      the program (to come)
    sources/LFU-GLOBALS.TEXT   unit globals: menu constants, panes (to come)
    sources/LFU-ALERTS.TEXT    alerts + menus, Alert tool input (to come)
    sources/LFU-MAKE.TEXT      Workshop exec: compile, link, InstallTool (to come)
    sources/fmt_text.py        REQUIRED for building: converts each source to the
                               Workshop paged .TEXT format (1024-byte header page,
                               no line straddling a 1024 boundary, bare CR line
                               endings). Raw text files will not compile.
    sources/fix_dc42.py        recomputes a DiskCopy 4.2 image's header checksums
    SOURCES.txt                index of what is here and how to build it

## Conventions (from LISACom 1.7 and Atkinsonpoint 1.1)

- Source file names are 8-character identifiers on the Lisa; the LFU- prefix
  keeps this tool's files apart from LMX- (LISACom), SLD- (Atkinsonpoint) and
  INS- (LOS Installer) on a shared Workshop volume.
- Menus are matched to the mi* constants in GLOBALS by position, so MAIN,
  GLOBALS and ALERTS always ship together.
- The linker caps global data at 32K; keep an eye on it from REV A.
- Every source carries a REV header; page-formatted copies sent to the Lisa
  are named with the revision letter (for example LFUMAINA.TEXT).
- Tool icons are a Lisa FONT (chars 0..2, 48x32); a malformed icon file causes
  Level 7 bus errors when the Filer copies the tool. Build icons with
  lisaicon.py from the LISACom kit.
- Floppy masters are written on the 2/10, not the LisaFPGA, and named with
  underscores and one period (for example LISAFILE_1_0.dc42).
