*genpngs.sh extracts bmp traces, & converts them to pngs
*Data for nets to work on.
*dataSrc/ contains the source that was compiled and run on our 6502 microprocessor simulator. 
*Full state traces were generated that are 2^16 + 8 bytes wide. I sliced just the register state of of this large trace and converted them to bmp images. A pixel is black if it is asserted at that position and point in time. For each byte, most significant bits are on the right. 

To DO: looks like 7 bytes of regs, think I cut an extra 8th byte out.For now take care of in pre processing. Should update. 

*Counting experiment, recursion vs looping:
The following directories each contain 100 raw register state traces.They are both from simple programs that start at an input value passen into the preprocessor, then count from that value up to that value + 10. forcountbmps accomplishes this by using a for loop, recCount uses recursion. I confirmed this is true after compilation by inspecting the .s files (jsr vs jmp) which are available in dataSrc/.

To Do: make sure that's not off by 1. 

forcountbmps:
Count from START to START+9 in a for loop.
559x64 bmp

recCountbmps:
Count from START to START+9 using recursion.
569x64 bmp

*Note these traces are slightly different lengths.

*Note that the compile line included definitions for START and MAX, eg.:
../../../../ext/install/bin/cc65 -D START=$K -D MAX=$[K+10] -D__6502__ -t none --cpu 6502 forCount.c -o intermed/forCount_${K}.s

#!/bin/bash                                                                                                                                                                                                                 

for i in $(ls);
do
    k=$(echo $i | sed 's/0_inc/_inc/')


    g=$(echo $i | cut -d '_' -f 4)

    mv $i $g$k
done