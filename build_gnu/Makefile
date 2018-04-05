FTL	= faster
PREFIX 	= arm-none-eabi-
CC 	= $(PREFIX)gcc
AS 	= $(PREFIX)as
LD 	= $(PREFIX)ld
OBJCOPY	= $(PREFIX)objcopy
RM	= rm

INCLUDE = -I../include -I../ftl_$(FTL) -I../sata -I../target_spw
CFLAGS 	= -mcpu=arm7tdmi-s -mthumb-interwork -ffreestanding -nostdlib -std=c99 -O2 -g -DPROGRAM_MAIN_FW -Wall
ASFLAGS	= -R -mcpu=arm7tdmi-s
LDFLAGS	= -static -nostartfiles -ffreestanding -T ld_script -Wl,-O1,-Map=list.txt
LIBS	= -lgcc
VPATH	= ../ftl_$(FTL);../sata;..;../target_spw

SRCS 	= ftl.c sata_identify.c sata_cmd.c sata_isr.c sata_main.c sata_table.c initialize.c mem_util.c flash.c flash_wrapper.c misc.c uart.c shashtbl.c
INITSRC	= ../target_spw/init_gnu.s
OBJS	= ftl.o sata_identify.o sata_cmd.o sata_isr.o sata_main.o sata_table.o initialize.o mem_util.o flash.o flash_wrapper.o misc.o uart.o shashtbl.o init.o
DEPS	= ftl.d sata_identify.d sata_cmd.d sata_isr.d sata_main.d sata_table.d initialize.d mem_util.d flash.d flash_wrapper.d misc.d uart.d shashtbl.d
TARGET 	= firmware
TARGETELF = $(TARGET).elf
TARGETBIN = $(TARGET).bin

$(TARGETBIN): $(TARGETELF)
	$(OBJCOPY) -O binary --strip-all --strip-debug $< $@

$(TARGETELF): $(OBJS)
	$(CC) $(LDFLAGS) $^ -o $@ $(LIBS)

ftl.o:	../ftl_$(FTL)/ftl.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

sata_identify.o:	../sata/sata_identify.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

sata_cmd.o:	../sata/sata_cmd.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

sata_isr.o:	../sata/sata_isr.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

sata_main.o:	../sata/sata_main.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

sata_table.o:	../sata/sata_table.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

initialize.o: ../target_spw/initialize.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

mem_util.o:	../target_spw/mem_util.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

flash.o:	../target_spw/flash.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

flash_wrapper.o:	../target_spw/flash_wrapper.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

misc.o:	../target_spw/misc.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

uart.o:	../target_spw/uart.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

shashtbl.o:	../target_spw/shashtbl.c
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

init.o: $(INITSRC)
	$(AS) $(ASFLAGS) $< -o $@



ftl.d:	../ftl_$(FTL)/ftl.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

sata_identify.d:	../sata/sata_identify.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

sata_cmd.d:	../sata/sata_cmd.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

sata_isr.d:	../sata/sata_isr.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

sata_main.d:	../sata/sata_main.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

sata_table.d:	../sata/sata_table.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

initialize.d: ../target_spw/initialize.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

mem_util.d:	../target_spw/mem_util.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

flash.d:	../target_spw/flash.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

flash_wrapper.d:	../target_spw/flash_wrapper.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

misc.d:	../target_spw/misc.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

uart.d:	../target_spw/uart.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

shashtbl.d:	../target_spw/shashtbl.c
	$(CC) $(CFLAGS) -M $(INCLUDE) -c $< -o $@

clean:
	$(RM) $(OBJS) $(DEPS) $(TARGETELF) $(TARGETBIN)


include $(DEPS)
