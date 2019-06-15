
ARMGNU?=arm-none-eabi

COPS = -Wall  -Os -nostdlib -nostartfiles -ffreestanding -save-temps
AOPS = --warn --fatal-warnings

.PHONY: all
all: clean mecrisp-stellaris-stm32f103rb.bin

mecrisp-stellaris-stm32f103rb.o: mecrisp-stellaris-stm32f103rb.s
	$(ARMGNU)-as mecrisp-stellaris-stm32f103rb.s -o mecrisp-stellaris-stm32f103rb.o

mecrisp-stellaris-stm32f103rb.bin: memmap mecrisp-stellaris-stm32f103rb.o
	$(ARMGNU)-ld -o mecrisp-stellaris-stm32f103rb.elf -T memmap mecrisp-stellaris-stm32f103rb.o
	$(ARMGNU)-objdump -D mecrisp-stellaris-stm32f103rb.elf > mecrisp-stellaris-stm32f103rb.list
	$(ARMGNU)-objcopy mecrisp-stellaris-stm32f103rb.elf mecrisp-stellaris-stm32f103rb.bin -O binary

.PHONY: clean
clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list

.PHONY: flash
flash:
	st-flash erase && st-flash --reset write mecrisp-stellaris-stm32f103rb.bin 0x8000000

.PHONY: console
console:
	picocom -f n -p n -b 115200 --imap lfcrlf /dev/ttyACM_stlink
