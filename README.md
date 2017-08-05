# til
Repository of things I've learned from the various things I do.

### Atmega32u4
Atmega32u4 has the GSCLK on D5 instead of D3, MOSI is on B1 and SCLK is on B2. (Ref. [datasheet](http://www.atmel.com/Images/Atmel-7766-8-bit-AVR-ATmega16U4-32U4_Datasheet.pdf) p79)


### Connecting Atmega32u4 to TLC5940
```
      ---u----
OUT1 |1     28| OUT channel 0
OUT2 |2     27|-> GND (VPRG)
OUT3 |3     26|-> SIN (B2)
OUT4 |4     25|-> SCLK (B1)
  .  |5     24|-> XLAT (B5)
  .  |6     23|-> BLANK (B6)
  .  |7     22|-> GND
  .  |8     21|-> VCC (+5V)
  .  |9     20|-> 2K Resistor -> GND
  .  |10    19|-> +5V (DCPRG)
  .  |11    18|-> GSCLK (C6)
  .  |12    17|-> SOUT
  .  |13    16|-> XERR
OUT14|14    15| OUT channel 15
      --------
```

##### Atmega32u4 Breakout TLC5940 pinout file (modified from the teensy one)
```cpp
#ifndef TLC_Arduino_Leonardo_h
#define TLC_Arduino_Leonardo_h

#if DATA_TRANSFER_MODE == TLC_BITBANG
#error "If you want bitbang mode, insert pin defs here"
#endif

// MOSI (Leo outter center ICSP pin) -> SIN (TLC pin 26)
#define TLC_MOSI_PIN   2
#define TLC_MOSI_PORT   PORTB
#define TLC_MOSI_DDR   DDRB

// SCK (Leo inner center ICSP pin) -> SCLK (TLC pin 25)
#define TLC_SCK_PIN   1
#define TLC_SCK_PORT   PORTB
#define TLC_SCK_DDR   DDRB

// SS (Leo RX LED)
#define TLC_SS_PIN   0
#define TLC_SS_DDR   DDRB

// OC1A (Leo pin 9) -> XLAT (TLC pin 24)
#define XLAT_PIN   5
#define XLAT_PORT   PORTB
#define XLAT_DDR   DDRB

// OC1B (Leo pin 10) -> BLANK (TLC pin 23)
#define BLANK_PIN   6
#define BLANK_PORT   PORTB
#define BLANK_DDR   DDRB

// OC3A (Leo pin 5) -> GSCLK (TLC pin 18)
#define GSCLK_PIN   6
#define GSCLK_PORT   PORTC
#define GSCLK_DDR   DDRC
#define TLC_TIMER3_GSCLK 1

#endif
```
