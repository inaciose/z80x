# ROM2RAM

Copy the 16KB ROM contents to the first 16KB of RAM (while ROM still paged in).  

In minicom:  
sudo minicom -c on --device /dev/ttyUSB0  

Copy rom2ram.z80.hex contents and past it to SCM prompt  

Wait for:  
*Ready  

*  
then type:  
G 8000  

ROM contents copied to RAM. Now we can toogle ROM (PAGE) in/out by writing to 0x38 or reset PAGE (PAGE=0) by writing to 0x30.  

74LS393:Q0 = PAGE  

PAGE = 0: ROM in, RAMLL out;  
PAGE = 1: ROM out, RAMLL in;  

Toggle PAGE  
o 38 0  

Reset PAGE  
o 30 0  

# Assembler
Assembly for the asm80, the z80 assembler online.  
https://www.asm80.com/  
