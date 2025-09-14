# Z80_SBC2

3.6864Mz, 16KB (0KB paged) ROM, 48KB (64KB paged) RAM and serial MC68B50 (0x80) 57600bps 8N1  
Pageable ROM/RAML16K (0x38 toggle page, 0x30 reset page)  

Same ROM as Z80_SBC1: 9B000000.BIN; (or the one with CP/M 2.2 bootloader ?)  

Press reset after power on (the reset circuit must be revised)
Help (commands): help  
MS-BASIC: G 2000  
Exit MS-BASIC: monitor  

# Page ROM

Copy ROM to RAM  
Load rom2ram.z80.hex file contents    
G 8000  

Toogle PAGE  
o 38 HH  

Reset PAGE  
o 30 HH  


# Equations  
MEMRD = MREQ_ + RD_  
MEMWR = MREQ_ + WR_  

PAGE = Q0 of 74LS393 counter with COUNTER_CLK via port 0x38, and COUNTER_RESET via port 0x30 or RESET  

ROM_CE = A14 + A15  
ROM_OE = PAGE + MEMRD  

RAML_CE = A15  
RAML_OE = A15 + (not(A14) x not(PAGE)) + MEMRD  
RAMH_WE = MEMWR  

RAMH_CE = not(A15)  
RAMH_OE = MEMRD  
RAMH_WE = MEMWR  

# Truth table for RAML_OE  
MR = MEMRD  

M A A P Y  
R 1 1 A  
  5 4 G  
      E  
0 0 0 0 1  
0 0 0 1 0 > MR + A15 + A14 + not(PAGE)  
0 0 1 0 0 > MR + A15 + not(A14) + PAGE  
0 0 1 1 0 > MR + A15 + not(A14) + not(PAGE)  
0 1 0 0 1  
0 1 0 1 1  
0 1 1 0 1  
0 1 1 1 1  
0 0 0 0 1  
0 0 0 1 1  
0 0 1 0 1  
0 0 1 1 1  
0 1 0 0 1  
0 1 0 1 1  
0 1 1 0 1  
0 1 1 1 1  

RAML_OE = (MR + A15 + A14 + not(PAGE)) x (MR + A15 + not(A14) + PAGE) x (MR + A15 + not(A14) + not(PAGE))  

Simplificado, fica: RAML_OE = A15 + (not(A14) x not(PAGE)) + MEMRD  

Com ROM 8K ???:  
ROM_CE = A13 + A14 + A15 (no IC: A15-GND, A14-GND, A13-GND)  
RAML_OE = A15 + (not(A13) x not(PAGE)) + MEMRD  

# Notes
Based on Z80_SBC1, and part of the RC2014 Pageable ROM (74LS138, 74LS393 and its input logic) with some more required logic.  
https://rc2014.co.uk/modules/pageable-rom/  

