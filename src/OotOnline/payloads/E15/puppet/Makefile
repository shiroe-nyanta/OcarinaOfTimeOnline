PROGRAM = link_no_pvp
OVLOUT = ../link_no_pvp.ovl
ADDRESS = 0x80800000
PARTS = $(PROGRAM).o

CC      = mips64-gcc
LD      = mips64-ld
OBJDUMP = mips64-objdump
NOVL    = novl

CFLAGS = -G 0 -O1 -fno-reorder-blocks -std=gnu99 -mtune=vr4300 -march=vr4300 -mabi=32 -c -mips3 -mno-explicit-relocs -mno-memcpy -mno-check-zero-division
LDFLAGS = -T /opt/n64/mips64/include/z64ovl/z64ovl.ld --emit-relocs
NOVLFLAGS = -v -c -A $(ADDRESS) -o $(OVLOUT)

default: $(PROGRAM).ovl init_vars

$(PROGRAM).ovl: $(PARTS)
	$(LD) -o $(PROGRAM).elf $(PARTS) $(LDFLAGS)
	$(NOVL) $(NOVLFLAGS) $(PROGRAM).elf

init_vars:
	@echo -n "init_vars   0x" > init_vars.txt
	@$(OBJDUMP) -t $(PROGRAM).elf | grep init_vars | head -c 8 >> init_vars.txt

clean:
	rm -fv $(PROGRAM).elf $(OVLOUT) $(PARTS)
