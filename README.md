# romcard
A periferal card for Apple][

The ROMcard2 is intended to work with EPROM 27C040 and compatible.
The ROM is organized in 256 banks of 2kB each, numbered #00 to #FF
Banks are selected by writing a byte (#00 - #FF) into $C0Nx, where N = 8 + [slot number]
When writing to $C0Nx at the same time the ROM chip is also enabled
When a bank is selected, its content are seen in the address space $C800-$CFFF
To de-enable the ROM chip a write must be performed to address $CFFF or reset executed
If a user program is accessing the card, it is important that at the end a write is performed to $CFFF so that the card is deactivated and does not conflict with other hardware, which is using the same address space.
The bootloader is programmed in the lowest 256 bytes of the ROM chip
The boot loader is always available at addresses $CM00-$CMFF, where M = [slot number]
The bootloader can also be seen at addresses $C800-$C8FF of bank #00
Each program must be recorded in the ROM as follows:
4 markers – #AA #D5 #55 #2A, always starting at an address $xxx00 – multiple of #100 
16 bytes with the name of the program
2 bytes indicating the start address of the program
2 bytes with the length of the program
The actual binary code of the program
Recommended installation is on Slot 7.
The boot loader has functionality that it captures the boot sequence of the computer and executes the first program recorded onto the ROM – usually DOS.
If ”\” is pressed while performing a cold reset – the boot sequence will override the ROMcard2 boot so floppy disk can boot.
Programs are called with “&” followed by the number of the program
&2 calls the program which returns a list of programs recorded onto ROMcard2

 


	
