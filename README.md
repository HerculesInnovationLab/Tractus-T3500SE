# Using the Tractus-T3500SE

## Overview
The Tractus printer we have here at the HIL was purchased from the company Tractus in early 2023.
This is a very large format printer, it prints aproxomatly 1 meter diameter by 2 meter tall.
It is a Delta style printer, and comes with 2 interchangable heads and an attachable bed probe.

The system is a Reprap Logicboard tightly integrated with a raspberry pi (displayed on the large screen).
The Raspberry Pi is on the HIL Staff wifi, and is assisable at 192.168.1.44
The password will not be posted here, but is with HIL staff.

### ${\textsf{\color{red}WARNING!}}$ Operating the Tractus printer with the door open is not advised.
The head can move quite quickly at times, and is some what unpradictable.
It is advised to keep the door shut as much as possible.
During 1st layer calibration care will have to be taken to not be in the path of the print head.

### ${\textsf{\color{yellow}CAUTION!}}$ The print bed is ...**glass**... DO NOT PLACE UNDUE WEIGHT ON IT.
Doing so could missalign the bed, requireing a new mesh compensation.
EXTEME care should be taken when moveing Z to 0. 
Any impact with the print head COULD damage the glass bed.

## Homing procedure explained

The Printer Homes iteself in a somewhat unique way.
When you hit "Home All" or run a G28, the printer raise up to ~3 meter, until the endstops are hit.
It then drops 5mm, and raises again slower until the endstops are hit again.
It then lowers 5mm.

The printer is now at its maximum height.

As you see the printer has never probed the bed, it pulls from memory its maximum height.
It only knows what Z0 (glass beds location) based on this hieght memory.

The line of code from config.g that sets the Height is line 5. 

````gcode
M665 L1060.000:1060.000:1060.000 R495.543 H2201.50 B500.0 
````
Due to the fact that the belts can change with tempature, this number may need adjusted at times.

## How to do Z calibration

Highly suggest Z offset is set with Z0 having a small paper gap using baby stepping to get a proper first layer.

### Connect to printer

- Connect to the printers web interface from Orca slicer "device page"
- Connect to the printers web interface from web browser via IP
- Use front pannel at printer

### Set babysteps to 0 

Press "Job" > "Status" > "Z Babystepping" 

### Home all

Press "Control" > "Dashboard" > "Home All"
The print head should now be at the top of the printer.

### Command print head to bed

Press "Control" > "Dashboard" > "Z-500" 
This will drop the print head in 500mm steps
Do this 3 times should get the print head to around Z500
This is shown under "Status" > "Tool Position" > "Z"

Press "Control" > "Dashboard" > "Z-100"
This will drop the print head in 100mm steps
Do this 4 times should get the print head to around Z100

Press "Control" > "Dashboard" > "Z-10"
This will drop the Print head by 10mm steps
Do this 9 times, this should get the print head to around Z10

Use the smaller Z-1 and Z-0.5 steps until the print head is doing 1 of 2 things.
1. Nozzle is touching glass bed
2. Status shows Z at Z0, but still has a large gap

**IF 1:** make note of Z height in status. We will subtract this number from the saved height value.
**IF 2:** make note of the gap, and take a rough guess of that distance. this will be the amount added to the saved height.

### Adjust saved height value
Press "Files" > "System" > "config.g"
Edit the H value for the M665 command on Line 5
The larger the H value, the further down the print head will be a Z0
The smaller the H value, the higher up the print head will be at Z0
This is in mm. currently for the 0.4mm nozzle it is H2201.50

Press "Save" > "Restart Mainboard"

### Repeat process 
You will need to repeat this until Z0 allows a piece of paper to slide between nozzle and bed, while slightly dragging.

### Adjust babysteps to prevent bed crash

Press "Job" > "Status" > "Z Babystepping" > "+0.05mm"
Raise the bed to between 0.5mm - 1mm

## How to load filament

** macros have been made to load and unload filament **

## How to send a print

### Pre-Heat the bed
Due to the bed taking so long to heat up, it is advised that you preheat the bed to the type of plastic using.
60C is standard for PLA.

### Verify The following items
1. Fillament loaded:
You want to double check that the fillament is loaded properly, and there is enough for the print you are about to attempt.
2. Baby steps: are at least + 0.5 to 1 mm from bed. This prevents head crashes during print start.
3. Bed is clean: With time dust will collect on the bed. Use clean water and paper towels to clean the bed. once clean apply a thin layer for 3dLac.

### Open/use Orca Slicer
The two desktops in the lobby have Orca slicer setup. if you would like to use on a different machine, the Orca configs are in this repo.
You use Orca Slicer exactly like you would Prusa slicer, with the only exception that "send to printer" does not work.

** Note: ** You want to ensure skirt is enabled with at least 4 loops. This lets you get your Z offset correct before the print starts.

Once you have sliced the object, select "Save Gcode".

You can then click the device tab for the web gui, select jobs, and "upload gcode" or "upload and start".

## How to starting a print

The printer should now be homing itself, and waiting for the hotend/bed to heatup.
You will then grab the tablet (easier) or use the front screen to adjust baby steps while it is printing the skirt.
You are trying to get the correct "squish" for the first layer.
Once your first layer seems to have the right baby step settings... Pray that your 8 day print works. 

## Troubleshooting

If you are running into any issues you can reach out to Ramroth on Global.
 



** This is intented to be a how to guid on using the large format Tractus T3500SE at the HIL. **
It is not finished to the perfect amount, but inttended to get someone up and using it.
