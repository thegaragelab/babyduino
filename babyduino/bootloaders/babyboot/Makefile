# Makefile for ATmegaBOOT
# E.Lins, 2004-10-14

# program name should not be changed...
PROGRAM    = ATmegaBOOT

OBJ        = $(PROGRAM).o
OPTIMIZE   = -Os
#OPTIMIZE   = -Os -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums -ffunction-sections -fdata-sections -fno-split-wide-types -Wl,--relax -fno-inline-small-functions -mcall-prologues
#OPTIMIZE   = -Os -fdata-sections -fpack-struct -Wl,--relax  -mcall-prologues

CC         = avr-gcc


# Override is only needed by avr-lib build system.
override CFLAGS        = -g -Wall $(OPTIMIZE) -mmcu=$(MCU_TARGET) -D$(MCU)
override LDFLAGS       = -Wl,-Map,$(TARGET).map,$(LDSECTION)

OBJCOPY        = avr-objcopy
OBJDUMP        = avr-objdump
SIZE           = avr-size

all: babyduino8_nc babyduino88_nc

clean:
	rm -rf *.s
	rm -rf *.o *.elf
	rm -rf *.lst *.map

# Babyduino - ATmega8/Internal clock @8MHz
#
babyduino8_nc: TARGET = babyduino8_nc
babyduino8_nc: MCU = atmega8
babyduino8_nc: MCU_TARGET = atmega8
babyduino8_nc: CFLAGS += -DF_CPU=8000000 -DBAUD_RATE=38400
babyduino8_nc: LDSECTION  = --section-start=.text=0x1c00
babyduino8_nc: babyduino8_nc.elf
babyduino8_nc: babyduino8_nc.hex

# Babyduino - ATmega88/Internal clock @8MHz
#
babyduino88_nc: TARGET = babyduino88_nc
babyduino88_nc: MCU = atmega88
babyduino88_nc: MCU_TARGET = atmega88
babyduino88_nc: CFLAGS += -DF_CPU=8000000 -DBAUD_RATE=38400
babyduino88_nc: LDSECTION  = --section-start=.text=0x1c00
babyduino88_nc: babyduino88_nc.elf
babyduino88_nc: babyduino88_nc.hex

# Babyduino - ATmega168/Internal clock @8MHz
#
babyduino168_nc: TARGET = babyduino168_nc
babyduino168_nc: MCU = atmega168
babyduino168_nc: MCU_TARGET = atmega168
babyduino168_nc: CFLAGS += -DF_CPU=8000000 -DBAUD_RATE=38400
babyduino168_nc: LDSECTION  = --section-start=.text=0x3c00
babyduino168_nc: babyduino168_nc.elf
babyduino168_nc: babyduino168_nc.hex

# Common rules
#
%.hex: %.elf
	$(OBJCOPY) -j .text -j .data -O ihex $< $@
	$(SIZE) $@

%.srec: %.elf
	$(OBJCOPY) -j .text -j .data -O srec $< $@

%.bin: %.elf
	$(OBJCOPY) -j .text -j .data -O binary $< $@

%.elf: $(OBJ)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $^ $(LIBS)

