# Flashforge Guider IIs Cura Profile Setup
<sub>Tested on Cura version 5.2.2</sub>

1. Open Cura and go to Settings -> Printer -> Add Printer
2. Find Flashforge (under Non-Networked Printer), type your Printer name then click Add
3. Once added open Machine Settings, and enter the Printer Setting

![Machine Settings](https://content.invisioncic.com/ultimake/monthly_2022_08/1668565318_MachineSettings.thumb.jpg.7e7a41ccf21e338593a9b4c9c7cba2ab.jpg)

4. Add the [G-Code](./Cura-Guider_2s.gcode)

Start G-Code
```
M118 X10 Y10 Z10
M140 S{material_bed_temperature_layer_0}; set initial bed temp
M104 S{material_print_temperature_layer_0} T0;set initial extruder temp
M107; disable cooling fan
G90; set to absolute positioning
G28; home axes
M132 X Y A B; recall home offsets from EPROM
G1 Z50.0 F420; adjust Z
G161 X Y F3300;
M7 T0; wait for bed to stabilise
M6 T0; wait for extruder to stabilise
M651 S255; start case fan
G1 Z0.3 F3600 ; move down to purge
G92 E0 ; zero extruders
G1 X120 Y-125 E20 F2000 ; extrude a line of filament across the front edge of the bed
G1 X130 Y-125 F180 ; wait for ooze
G1 X140 Y-125 F5000 ; fast wipe
G1 Z1 F100 ; lift
G92 E0 ; zero extruders again
G1 E-1.0000 F1800
```

End G-code
```
M104 S0 T0; cool down extruder
M140 S0 T0; cool down bed
G162 Z F1800; 
G28 X Y; home axes
M132 X Y A B; recall home offsets from EPROM
M652; turn off rear fan
G91; set to relative positioning
M18; disable stepper motors
```

4. Then add the Post Processing 'Search and Replace' rules to Cura

Post Process Scripts

**Search and Replace**
```
Search	M104 S(.*)\.0
Replace	M104 S\1
Use RegEx	Yes
```

**Search and Replace**
```
Search	M140 S(.*)\.0
Replace	M140 S\1
Use RegEx	Yes
```

5. Import the Print Setting Profiles

* [Fine Quality](./12mm.curaprofile)
* [Normal Quality](./18mm.curaprofile)
* [Draft Quality](./30mm.curaprofile)

6. Sliced the file in CURA and Save to Disk 

     - Rename the file extension from filename.gcode to filename.g
     - Or install the [GXWriter](https://marketplace.ultimaker.com/app/cura/plugins/Ronoaldo/GXWriter) plugin and save the file in .gx format

`Unfortunately you can't connect the Guider IIs to Cura through USB`

## Reference Links
* [FlashForge Documentation](https://www.flashforge.com/download-center/53)
* [UltiMaker Community Forum](https://community.ultimaker.com/topic/41418-guider-2s/)
* [Reddit Post](https://www.reddit.com/r/FlashForge/comments/euyqt4/guider_ii_guider_iis_cura_profile/)


https://pxit.com.au

© 2023 PXIT. All rights reserved.