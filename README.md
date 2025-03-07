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

Highly suggest Z offset is set with Z0 having a small paper gap and baby stepping used to get a proper first layer.

### Connect to printer
Connect to printers web interface, or use front pannel.

### Set babysteps to 0 
"Job" > "Status" > "Z Babystepping" 



## How to load filament

## How to send a print

## How to starting a print

## Troubleshooting

 

This is intented to be a how to guid on using the large format Tractus T3500SE at the HIL.
