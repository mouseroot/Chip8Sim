Chip8, Well sorta

The Chip8 simulator here is a bit of a variation of the tradational chip8 system
this has no video,audio or keyboard support but instead has sockets,http,filesystem and file i/o
and has another Index register used for Strings called S

based on alot of the code from this article http://www.multigesture.net/articles/how-to-write-an-emulator-chip-8-interpreter/
Another epic reference is http://devernay.free.fr/hacks/chip8/C8TECH10.HTM

MSB (Most Significant Byte) - Big Endian System [1] 0 0 0 0 0 0 0

System Memory map

0x000 - 0x1FF - Empty space reserved for temp data and ram
0x200 - 0xFFF - program code loaded in from file or memory
 
Supported Opcodes
[X] 00EE - Returns from subroutine
[X] 1NNN - Jumps to address NNN
[X] 2NNN - Calls subroutine at NNN
[X] 3XNN - Skips next if VX == NN
[X] 4XNN - Skips next if VX != NN
[X] 5XY0 - Skips next if VX == VY
[X] 6XNN - Sets VX to NN
[X] 7XNN - Adds NN to VX
[X] 8XY0 - Sets VX to VY
[X] 8XY1 - Sets VX to (VX | VY)
[X] 8XY2 - Sets VX to (VX & VY)
[X] 8XY3 - Sets VX to (VX ^ VY)
[X] 8XY4 - Adds VY to VX. VF set to 1 when carry, 0 otherwise
[X] 8XY5 - VY is subtracted from VX. VF set to 0 when borrow, 1 otherwise
[X] 8XY6 - Shifts VX right by one. VF is set to the value lsb of VX before the shift
[X] 8XY7 - Sets VX to VY minus VX. VF is set to 0 when borrow, and 1 otherwise
[X] 8XYE - Shifts VX left by one. VF is set to the value of the msb of VX before the shift
[X] 9XY0 - Skips next if VX != VY
[X] ANNN - Sets I to NNN
[X] BNNN - Jumps to address NNN + V0
[X] CXNN - Sets VX to random number + V0
[X] D0NN - Calls OS functions

           Client Sockets
[ ]        D010 - Connect to Address I,VE success
[ ]        D011 - Send Data at Address I Size V0
[ ]        D012 - Recv Data Size V0 at Address I

           String Functions
[ ]        D020 - String Compare Memory[I] == Memory[S]
[ ]        D021 - String Compare Memory[I] != Memory[S]
[ ]        D022 - String Memory[I] Contains Memory[S]
[ ]        D023 - String Memory[I] Append Memory[S]
[ ]        D034 - Set N to String Length

           Stack Functions
[X]        D0A0 - Push I
[X]        D0A1 - Push S
[X]        D0A2 - Pop I
[X]        D0A3 - Pop S
[X]        D0A4 - Clear Stack

           Directory Functions
[X]        D0D0 - Create Directory at Address I
[X]        D0D1 - Set VE if Directory Exists at Address I
[ ]        D0D2 - Delete Directory at Address I

           File Functions
[ ]        D0F0 - Create File
[ ]        D0F1 - Set VE if File Exists at Memory[I]
[X]        D0F3 - Read Text File into Memory[I] starting at Memory[S]
[X]        D0F4 - Read Binary File into Memory[I] starting at Memory[S]
[ ]        D0F5 - Write Text Memory[I] Size V0 to Memory[S] File
[ ]        D0F6 - Write Binary Memory[I] Size V0 to Memory[S] File
[ ]        ENNN - Sets S to NNN

[X] FX1E - Adds VX to I

[ ] FX33 - Stores the Binary-coded decimal representation of VX
[X] FX55 - Stores V0 to VX in memory starting at address I
[X] FX65 - Fills V0 to VX with values from memory starting at address I
[X]        FFFD - Load Memory at I into execution memory starting at V0 size VF  (Load Memory[I] to Memory[512 (0x200) + V0)])
[X] FFFE - End Program
[X] FFFF - Reset