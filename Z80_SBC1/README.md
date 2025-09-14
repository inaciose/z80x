# Z80_SBC1

3.6864Mz, 16KB ROM, 32K RAM and serial MC68B50 (0x80) 57600bps 8N1 (115200 c/ o dobro do relógio)  

ROM 9B000000.BIN with (RC2014 versions):  
- 0000-1FFF: SCM-Small Computer Monitor  
- 2000-3FFF: MS-BASIC  

Press reset after power on (the reset circuit must be revised)

Help (commands): help  
MS-BASIC: G 2000  
Exit MS-BASIC: monitor  

# Equations  
MEMRD = MREQ_ + RD_  
MEMWR = MREQ_ + WR_  

ROM_CE = A14 + A15  
ROM_OE = MEMRD  

RAM_CE = not(A15)  
RAM_OE = MEMRD  
RAM_WE = MEMWR  

ACIA = A7 x not(A6) (10XX XXXX, 0x80 com replicas, RC2014 MC68B50 serial module)  

# Notes
Based on Searle Grants Minimal Z80 with 8KB ROM, 32K RAM and serial MC68B50.  
http://searle.x10host.com/z80/SimpleZ80_32K.html  

