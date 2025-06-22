# Ymir changelog

## Version 0.1.5

### New features and improvements

- App: Added command-line option `-P` to force emulator to start paused.
- App: Added option to create internal backup RAM files per game. (#99)
- App: Added option to override UI scale. (#251)
- App: Added option to toggle fullscreen by double-clicking the display. (#197)
- App: Added recent games list to File menu. (#196)
- App: Automatically center Settings window when opening it. (#251)
- App: Close windows when pressing B or Circle on gamepads while nothing is focused. (#251)
- App: Enable gamepad navigation on GUI elements. (#251)
- App: Store relative paths in Ymir.toml. (#207)
- Backup RAM: Support interleaved backup image formats such as the ones produced by Yaba Sanshiro or the MiSTer core. (#87)
- Backup RAM: Support standard BUP backup files. (#87)
- VDP: Added option to deinterlace video. (#66)
- VDP: Added option to move VDP1 rendering to the emulator thread to improve compatibility with some games (e.g. Grandia). (#233)
- VDP1: Added option to replace meshes with 50% transparency.

### Fixes

- App: Fix rare crash when loading a backup memory image in the Backup Memory Manager.
- App: Prevent loading internal backup memory image as backup RAM cartridge image.
- CD Block: Start new playbacks from starting FAD when previous playback has ended. Fixes WipEout freeze after SEGA logo.
- Media: Fix pregap handling in single BIN images.
- SCSP: Apply DAC18B to output (thanks to @celeriyacon). Fixes quiet audio in many games. (#237)
- SCSP: Fix send level, panning and master volume calculations.
- SCSP: Fix slot output processing order (thanks to @celeriyacon).
- SCSP: Fix swapped DAC18B and MEM4MB bits (thanks to @celeriyacon).
- SCSP: Run one additional DSP step to fix FRC issues (thanks to @celeriyacon).
- SCU, SH-2, SMPC, SCSP, VDP: Numerous fixes to interrupt handling (thanks to @celeriyacon). Fixes intermittent Rayman inputs and some audio glitches.
- SCU: Various DSP accuracy fixes (thanks to @celeriyacon).
- SH2: More fixes to WDT and DIVU (thanks to @celeriyacon).
- SMPC: Cancel scheduled command processing event when resetting SMPC. Fixes a long hang after hard resetting in some cases.
- SMPC: Change fixed bits from 111 to 100 in TH/TR control mode responses for the first data byte of the Control Pad and 3D Control Pad peripherals. Fixes Golden Axe booting back to BIOS. (#231)
- SMPC: Eliminate spurious INTBACK interrupts.
- SMPC: Prevent COMREG writes when a command is in progress. Fixes some boot issues leading to the "Disc unsuitable for this system" message. (#219)
- SMPC: Prioritize INTBACK continue requests over break requests.
- System: Tighten synchronization between the two SH-2 CPUs and remove artificial timeslice limit. Improves performance and fixes Fighters Megamix and Sonic Jam intermittent boot issues. (#236, #242)
- VDP1: Lower command limit to work around problematic games that don't set up a terminator in the command table. (#213, #216)
- VDP1: Significantly slow down command execution when running the VDP1 renderer on the emulator thread. Fixes Dragon Ball Z - Shinbutouden freeze after SEGA logo. (#233)
- VDP2: Apply window effect to sprite layer. Fixes graphics going out of bounds in many games. (#173)
- VDP2: Check for invalid access patterns to determine if NBG characters should be delayed. Fixes background offsets in many games. (#169, #190, #226)
- VDP2: Disable NBG1-3 only if both RBG0 and RBG1 are enabled simultaneously.
- VDP2: Honor access cycles and VRAM bank allocations to restrict pattern name and character pattern accesses. Fixes garbage graphics in Panzer Dragoon Saga, Sonic 3D Blast and Street Fighter Alpha/Zero 2. (#203, #213)
- VDP2: Invert back screen color calculation ratio. Fixes black background on Sakura Taisen FMVs. (#241)
- VDP2: Move existing VCounter into VDP2 VCNT register. Fixes Assault Suit Leynos 2 freeze when going in-game and King of Fighters '95 not booting. (#75)
- VDP2: Synchronize background enable events with the renderer thread. Fixes FMV slicing issues on slow machines on Sakura Taisen.


## Version 0.1.4+1

### New features and improvements

- App: You can now drag and drop CCD, CHD, CUE, ISO or MDS files into the emulator window to load games.

### Fixes

- VDP2: Fix black screen on SSE2 builds.


## Version 0.1.4

### New features and improvements

- App: Added option to pause emulator when the window loses focus. (#181)
- App: Added shadow under playback indicators to make them visible on white backgrounds.
- App: Automatically adjust scaling when system-wide DPI is changed. (@Wunkolo)
- App: Changed background color around screen to black on windowed mode.
- CD Block: Implement Put Sector command, used by After Burner II. (#78)
- Core: Performance improvements, especially for ARM builds. (@Wunkolo)
- Debug: Simple CD Block commmand tracer window.
- Input: Implemented 3D Control Pad. (#28)
- Media: Preliminary support for CHD files. (#48)
- Media: Support multi-indexed audio tracks (BIN/CUE only). (#58)
- SMPC: Set SF=0 on unimplemented commands so that games can move forward.
- SH-2: Build infrastructure needed to honor memory access cycles for improved performance and accuracy.
- SH-2: Slow down accesses to on-chip registers to 4 cycles.
- VDP: Rewrite VDP2 frame composition code to use SIMD on x86 and ARM for improved performance. (@Wunkolo)

### Fixes

- App: Customized profile paths are now created at the specified location instead of the default. (#119, #126; @lvsweat)
- CD Block: Clear partitions and filters on soft resets triggered by Initialize CD System command. Fixes some game boot issues.
- CD Block: Clear the "paused due to buffer exhausted" flag when SeekDisc command pauses playback. Fixes Sakura Taisen 2 read errors after FMVs.
- CD Block: Don't clear the file system when opening the tray.
- CD Block: Fix audio track sector sizes. Fixes some CD audio track playback glitches with certain images (particularly MDF/MDS).
- CD Block: Fix Delete Sector end position when sector count is FFFF. Fixes some game boot issues.
- CD Block: Fix directory indexing. Fixes one of Assault Suit Leynos 2 crashes on startup. (#127)
- CD Block: Free last buffer from partition when ending a Get Then Delete Sector transfer when the last sector isn't fully read. Fixes some game boot issues.
- IPL: Automatically load IPL ROM when switching disc images. (#128)
- M68K: Soft reset CPU when executing the `RESET` instruction. Fixes OutRun getting stuck on its own SEGA logo.
- Media: Fix crash when parsing CUE sheets with non-contiguous tracks.
- SCSP: Don't mirror sound RAM on 5A8'0000-5AF'FFFF. Fixes After Burner II audio and M68K crashes.
- SCU: Rework interrupt handling. Fixes Rayman inputs. (#59)
- SCU: Set ALU = AC before running DSP operations. Fixes Quake crash on boot. (#156)
- SCU: Timer enable flag applies to both timers. Fixes background priority issues in Need for Speed.
- SH-2: Fix PC offsets for exceptions, interrupts, TRAPA and RTE. Fixes some game boot issues.
- SH-2: Fix PC offsets for `mova`, `mov.w` and `mov.l` with `@(disp,PC)` operand (thanks to @celeriyacon).
- SH-2: Fixes and accuracy improvements to DIVU (thanks to @celeriyacon).
- SH-2: Fixes and accuracy improvements to FRT (thanks to @celeriyacon). Fixes freezes in Daytona USA. (#7)
- SH-2: Fixes and accuracy improvements to WDT (thanks to @celeriyacon).
- SH-2: Lazily update WDT and FRT timers. Provides a 5-10% performance boost *and* improves accuracy!
- SMPC: Various INTBACK handling adjustments. Partially fixes Assault Suit Leynos 2 no-boot issues.
- System: Fix cycle counting on the main loop not taking into account the number of cycles taken by the CPUs, resulting in undercounting timers.
- VDP1/2: Fix handling of 16-bit sprite data from VDP1 when VDP2 uses 8-bit sprite types. Fixes sprites in I Love Mickey Mouse/Donald Duck.
- VDP2: Allow 8-bit reads and writes to VDP2 registers.
- VDP2: Apply transparency to mixed-format sprite data when rendering the special value 0x8000. Fixes Assault Suit Leynos 2 black screen after loading.
- VDP2: Don't increment vertical mosaic counter if mosaic is disabled. Fixes text boxes and character portraits in Grandia. (#91)
- VDP2: Fix bitmap base address for RBGs. Fixes several graphics glitches on menus and in-game in Need for Speed.
- VDP2: Fix line screen scroll in double-density interlace mode. Fixes stretched videos in Grandia. (#91)
- VDP2: Fix special color calculation bits. Fixes Sonic R water effects. (#150)
- VDP2: Fix vertical cell scroll effect on games that set up access patterns that don't match the NBG parameters. Fixes Sakura Taisen 2 FMVs.
- VDP2: RBG0 was always being processed/rendered even when disabled.
- ymdasm: Fix file length when using a non-zero initial offset with the default length.


## Version 0.1.3

### New features and improvements

- Cartridge: Added 16 Mbit ROM cartridge for Ultraman: Hikari no Kyojin Densetsu and The King of Fighters '95. (#71)
- Cartridge: Added option to automatically load cartridges required by some games. (#98)
- Input: Categorize some actions as "triggers" (one-shot actions, optionally repeatable) to differentiate them from "buttons" (a binary state). This allows frame step to be repeated by holding the keyboard key bound to it.
- Input: Added a "Turbo speed (hold)" input bind that toggles turbo on and off. (#103)
- System: Automatically switch to PAL or NTSC based on auto-selected region.
- Save states: Automatically load IPL ROM matching the one used in a save state.
- Debugger: Added VDP2 layer toggles to Debug menu and in a new window.
- App: Allow customizing all profile paths. (#74)
- App: Add IPL ROM list sorting. (#92) (@Wunkolo)
- App: Add full screen mode (default shortcut: `Alt+Enter`) and command-line override `-f`. (#47)
- App: Improve frame pacing for a smooth full screen experience. (#97)
- App: Mitigate input lag in every mode (#101)
- App: Display reverse, rewind, fast-forward and pause indicators on the top-right corner of the viewport. (#103)
- Build: Added macOS builds. (huge thanks to @Wunkolo!)
- Core: Several performance and stability improvements. (@Wunkolo)

### Fixes

- VDP1: Preserve EWDR, EWLR and EWRR on reset. Fixes some graphics glitches on Capcom games. (#67)
- VDP2: RBGs would render incorrectly when starting the emulator with threaded VDP rendering disabled. (#77)
- VDP2: Honor access cycle settings (CYCA0/A1/B0/B1 registers) to fix vertical cell scroll effect. (#76)
- VDP2: Disable NBGs 1 to 3 if NBG0 or NBG1 use high color formats. (#76)
- VDP2: Apply mid-frame scroll effects properly. (#72)
- VDP2: Use the MSB from the final color value instead of the raw sprite data MSB, which fixes background priority bugs on Dragon Ball Z - Shinbutouden (#69)
- SCSP: More accuracy improvements and bug fixes (thanks to @celeriyacon)
- SCU: Fix repeated indirect DMA transfers when the write address update flag is enabled. Fixes a crash when going in-game on Shinobi X. (#84)
- Input: Assigning keys to connected controllers will no longer unbind keys from disconnected controllers.
- Rewind: Fix rare crash due to a race condition when resetting the rewind buffer.
- App: Fix handling of UTF-8 paths. (#88)
- Backup memory manager: Fix crash when loading an image with less files than the current image while having selected files at positions past the new image's file count.


## Version 0.1.2

### New features and improvements

- Input: Improved support for gamepads. You can now configure triggers as buttons, map analog sticks to the D-Pad, adjust deadzones, and more. (#36, #37, #54)
- Input: Added one more slot for input binds

### Fixes

- Input: Keys no longer get stuck when focusing windows, menus, etc.
- Input: Keys bound to controller on port 2 (by default: arrow keys, numpad and navigation block) should no longer prevent keys bound to the controller on port 1 from working. (#50)
- Several stability improvements (@Wunkolo)


## Version 0.1.1

### New features and improvements

- App: New logo and icon (thanks to @windy3862 on Discord!)
- App: Added Welcome window with instructions for first-time users
- App: Set initial window size based on display resolution
- App: Scale GUI based on system DPI scaling (#45)

### Fixes

- VDP1: Truncate polygon coordinates to 13 bits, fixing a short freeze in Virtua Fighter 2
- SCSP: Various accuracy improvements and bug fixes (thanks to @celeriyacon)
- CD Block: Fix errors when loading homebrew discs containing a single file
- Input: Properly handle gamepad buttons when binding inputs
- ymdasm: Fix disassembly skipping the very last instruction in files


## Version 0.1.0

Initial release.
