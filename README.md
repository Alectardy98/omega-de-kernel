###### FORKED FROM https://github.com/ez-flash/omega-de-kernel

# SimpleLight Fork - Overclocking Edition for EZ Flash Omega Definitive Edition.... No support is planned for the other EZ Flash Products.
###### *If you're looking for SimpleLight lite as it was originally created, check here: [https://github.com/Sterophonick/SimpleLight](https://gbatemp.net/threads/new-theme-for-ez-flash-omega.520665/)*

Hello all!

WHAT IS THIS...
This fork is intended to allow full compatibility for a crystal oscillator-modified GBA systems to function in a stable manner when saving and loading from an EZ Flash DE. Having this custom firmware is only one step. As you will need to perform the hardware modification to allow for the overclock, as well as a modified ROM file with a WAITCNT Patch.  

This is a fork of the Simple Kernal, which itself is a fork of the original EZ-Flash Omega Kernal. I do not have any affiliation with either team, though I greatly appreciate the work done by both of them.

I have had a few EZ flash DE flashcards, and I have found that the various revisions use diferent quality components, that may or may not be very stable with overclocking. Primarily the issue that I was running into had to do with save file loading into SRAM, and moving back into the SD card while overclocking. As you can see from the code modified here, I added a much more robust error correction method for saving and loading games to and from the SD card. Now there is error correction and a byte byte-by-byte copy method. I have tested this with a handful of different games while overclocking a full 2x and have no issues. Even if you are not planning on overclocking, this way of saving and loading into SRAM may be an improvement if you are experiencing save file corruption or deletion.

Unlike the original Simple DE, you have no option between light mode and dark mode here, I have made a new custom Pinkish colorway, that may or may not be to your liking. I did it this way because that was what was most appealing to me. If you would rather use one of the OG colorways, you can revert that part of the code to reflect the original Simple DE fork.

I am also using a fork of the Newest JaGoomba Color, which I also had to modify in order to get working with save games under an overclock. The TLDR of the modifications made is that goomba color uses a compression algorithm to shrink the size of saved game files. This compression algorithm when overclocked would fail and cause save data to not read properly from SRAM. This compression algorithm has been removed, meaning that RAW save games are now being used. This has the unfortunate downside of greatly reducing or completely removing the save state function in games due to lack of space. If someone wants to add SRAM Bank switching into the goomba color source code, we could allow for the full SRAM size of the EZ flash... but as of right now, we are still limited to just one 64k bank. Here is the link to the fork if you wish to see the full source [https://github.com/Alectardy98/jagoombacolor/blob/master/README.md](https://github.com/Alectardy98/jagoombacolor)

Hope everyone likes it!

THE REST IS COPIED FROM THE ORIGINAL FORK

Official forum thread:
https://gbatemp.net/threads/new-theme-for-ez-flash-omega.520665/

## Installation instructions:

_**Be sure you're using the most recent version, and follow the installation instructions in the !!!!!!!!!IMPORTANT!!!!!!!!!!!.TXT file in the GBAtemp package before reporting issues.**_

_**ALSO YOU MUST USE THE OFFICIAL KERNEL TO UPDATE THE FIRMWARE; THIS DOES NOT APPLY TO THE BASE OMEGA :(**_

1. Copy the SYSTEM and BACKUP folder to the root of the SD Card.
2. Move your IMGS, SAVER, RTS, and PATCH folders to SYSTEM.
3. If you want the light theme, copy ezkernel-light.bin to the root of the SD Card. If you want the dark thing, do the same with ezkernel-dark.bin
4. Rename the new kernel file to ezkernel.bin
5. You're done!

## Registered file types:
### Game ROMs
    .gba - GBA ROM
    .bin - GBA ROM
    .mb - GBA Multiboot ROM
    .agb - GBA ROM
    .col - ColecoVision ROM (Requires Cologne) *
    .gb - Game Boy ROM (Jaga's Goomba Color)
    .gbc - Game Boy Color ROM (Jaga's Goomba Color)
    .gg - Game Gear ROM (SMSAdvance)
    .rom - MSX Cartridge ROM (MSXAdvance) **
    .ngp - Neo Geo Pocket ROM (NGPAdvance)
    .ngc - Neo Geo Pocket ROM (NGPAdvance)
    .ngpc - Neo Geo Pocket Color ROM (NGPAdvance)
    .nes  - NES ROM File (PocketNES)
    .pce - PC-Engine ROM File (PCEAdvance)
    .sms - Sega Master System ROM File (SMSAdvance)
    .sg - Sega SG-1000 ROM File (SMSAdvance)
    .sv - Watara Supervision ROM File (Wasabi)
    .ws - WonderSwan ROM File (SwanAdvance)
    .wsc - WonderSwan Color ROM File (SwanAdvance)
    .z80 - 48k ZX-Spectrum Z80 ROM (ZXAdvance)
    .c8 - Chip-8 ROM (Chip8Adv (My First Emulator! :D))
    .arc - 4kb Emerson Arcadia 2001 ROM File

### Media
    .jpg - JPEG Image
    .jpeg - JPEG Image
    .mod - ProTracker Module file
    .bmp - Bitmap Image
    .pcx - ZSoft Paintbrush PCX image
    .mid - MIDI sequence
    .nsf - NES Music file (Nintendo Sound File)
    .vgm - SMS/GG music file
    .vga - aPlib Compressed SMS/GG music file
    .vgl - LZ77 Compressed SMS/GG music file
    .txt - Text Document
    .wav - Wave Sound (formatted in GSM 6.10)
    .k3m - Krawall Advance Sound
    .sb - MaxMod sound bank
    .lz - LZ77 Compressed Image
    .raw - Uncompressed Mode 3 Bitmap
    .ap - aPlib compressed Mode 3 Bitmap
    .bgf - BoyScout module
    .mda - Sharp X68000 Music
    .cwz - CWZ Music (IDK what exactly it is, but it was included with PogoShell 1.2)

*\* For Cologne, you have to make the ROM yourself.*\
*\*\* MSXAdvance uses the C-BIOS, so I can redistribute the emulator.*

##### Cologne Emulator Guide:
1. Download the latest version of Cologne.
2. Open the EXE file.
3. Take a blank file, and also add the Official Colecovision BIOS.
4. Create col.gba in the PLUG folder.

### This ZIP file contains some tech demos/games:
* XBill (SG-1000)
* Sega Tween (SMS)
* WinGG (Game Gear)
* HuZERO (PC-Engine)
* 1968 (ZX-Spectrum)
* Adventures Of Gus and Rob (Neo Geo Pocket)
* Kaboom! (Homebrew) (ColecoVision)
* Motkonque (MSX)
* SwanDriving (WonderSwan)
* F8Z (Chip-8)

### How to build 
1. Install [devkitPro](https://devkitpro.org/)
2. Set the following environment variables to their correct directories: `DEVKITPRO, DEVKITARM, LIBGBA`
3. Comment or uncomment the `#define DARK` line in `draw.h`. If uncommented, a dark theme is generated.
4. Run the command `make`. If done successfully, this should give you an `ezkernel.bin` file.
5. Follow the installation instructions above.
4. Update your flashcart and enjoy! :)

### Special Greetz & Contributors:
Sasq\
Moonlight\
Kuwanger\
veikkos\
DarkFader\
CoolHJ\
Let's Emu!\
Izder456\
NuVanDibe\
SLKun\
Mintmoon\
hitsgamer\
Rocky5

### Credits
[EZ-FLASH](https://www.ezflash.cn/) - The original firmware & hardware creators\
Kuwanger - PogoShell plugin integration\
Sterophonick - SIMPLE theme for EZO & EZODE\
fluBBa - SMSAdvance, MSXAdvance, Cologne for GBA, Goomba for GBA (Original), PCEAdvance, PocketNES, SNESAdvance, Wasabi, NGPAdvance, SwanAdvance\
[Jaga](https://github.com/EvilJagaGenius) - [Jaga's Goomba Color fork](https://github.com/EvilJagaGenius/jagoombacolor)\
...and others!
