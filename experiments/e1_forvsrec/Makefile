#Run after running make in the 6502 dir.
BUILDDIR=../../datasources/6502/apps/cc/apps
#Compiler
CC65BINDIR = ../../datasources/6502/ext/install/bin

START?=0
MAX?=10

IMGDIR?='images'

CC = $(CC65BINDIR)/cc65
AS = $(CC65BINDIR)/ca65
LD = $(CC65BINDIR)/ld65
AR = $(CC65BINDIR)/ar65

BU6502LIB = $(BUILDDIR)/bu6502.lib 
BU6502CFG = $(BUILDDIR)/bu6502.cfg 

SRCS=$(wildcard *.c)
IMGS=$(SRCS:.c=.img)

all: $(IMGS)

#Is this right? This .exe stuff? Add it so I could have a matching target.
#Is this too tearse?

%.img: %.exe
	[ -d 'backup' ] || mkdir backup
	mv *.lst *.map *.s backup
	[ -d ${IMGDIR} ] || mkdir ${IMGDIR}
	mv $* ${START}_${MAX}$@
	mv *.img ${IMGDIR}

%.exe: %.o 
	$(LD) -o $* -C ${BU6502CFG} $< ${BU6502LIB}  -m $*.map

%.o: %.s
	$(AS) --cpu 6502 $< -l $*.lst

#%.s: %.c ?
forCount.s: forCount.c
	$(CC) -D START=${START} -D MAX=${MAX} -D__6502__ -t none -O -Oi --cpu 6502 $<

recCount.s: recCount.c
	$(CC) -D START=${START} -D MAX=${MAX} -D__6502__ -t none -O -Oi --cpu 6502 $< 

clean:
	-rm -rf *~ *.o *.map *.img *.lst *.out memcpy.s memcpy backup ${IMGDIR} *.s traces tmp