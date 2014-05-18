Chip8, Well sorta

The Chip8 simulator here is a bit of a variation of the tradational chip8 system
this has no video,audio or keyboard support but instead has sockets,http,filesystem and file i/o

based on alot of the code from this article http://www.multigesture.net/articles/how-to-write-an-emulator-chip-8-interpreter/
Another epic reference is http://devernay.free.fr/hacks/chip8/C8TECH10.HTM

MSB (Most Significant Byte) - Big Endian System

System Memory map

0x000 - 0x1FF - Empty space reserved for temp data and ram
0x200 - 0xFFF - program code loaded in from file or memory
 
Supported Opcodes
[X] 00EE - Returns from subroutine
[X] 1NNN - Jumps to address NNN
[X] 2NNN - Calls subroutine at NNN
[X] 3XNN - Skips next instruction if VX == NN
[X] 4XNN - Skips next instruction if VX != NN
[X] 5XY0 - Skips next instruction if VX == VY
[X] 6XNN - Sets VX to NN
[X] 7XNN - Adds NN to VX
[X] 8XY0 - Sets VX to VY
[X] 8XY1 - Sets VX to (VX | VY)
[X] 8XY2 - Sets VX to (VX & VY)
[X] 8XY3 - Sets VX to (VX ^ VY)
[X] 8XY4 - Adds VY to VX. VF is set to 1 when there's a carry, and to 0 when there isn't 
[X] 8XY5 - VY is subtracted from VX. VF is set to 0 when there's a borrow, and 1 when there isn't.
[ ] 8XY6 - Shifts VX right by one. VF is set to the value of the least significant bit of VX before the shift
[X] 8XY7 - Sets VX to VY minus VX. VF is set to 0 when there's a borrow, and 1 when there isn't.
[ ] 8XYE - Shifts VX left by one. VF is set to the value of the most significant bit of VX before the shift
[X] 9XY0 - Skips the next instructure if VX != VY
[X] ANNN - Sets I to NNN
[X] BNNN - Jumps to address NNN + V0
[X] CXNN - Sets VX to random number + V0
[X] D0NN - Calls OS functions
[X] FXE1 - Adds VX to I
[ ] FX33 - Stores the Binary-coded decimal representation of VX
[X] FX55 - Stores V0 to VX in memory starting at address I
[X] FX65 - Fills V0 to VX with values from memory starting at address I
[ ] FFFD - Load Memory at I into execution memory starting at V0 size  (Load Memory[I] to Memory[512 (0x200) + V0)])
[X] FFFE - End Program
[X] FFFF - Reset