# Tlaser

Tlaser is a laser engraver designed as proof of concept of a new motion system, coreXY cantilever. It's called Tlaser because this motion system, and thus this machine, is shaped like a T.  
  
<img align="right" height="240" src="https://github.com/FiCacador/Tlaser/raw/master/images/Tlaser%20logo.png" />

### Main features:

- **CoreXY cantilever**
- **5500mW blue laser**
- **315mm x 205mm engraving area**
- **Linear guide rails**
- **Adjustable height at each corner**
- **3D printed**  
  
## [Video of Tlaser in action!](https://youtu.be/NjZCqPt6v3c)

<p float="center">
  <img width="430" src="https://github.com/FiCacador/Tlaser/raw/master/images/Tlaser FreeCAD.jpg" />
  <img width="430" src="https://github.com/FiCacador/Tlaser/raw/master/images/Tlaser_0.JPG" />
</p>

## CoreXY cantilever

Tlaser was developed to validate and demonstrate a new motion system, which the author named  *CoreXY cantilever*.  
CoreXY cantilever has the same kinematics as [CoreXY](https://corexy.com/theory.html), so it is easy to configure in existing firmware like Grbl or Marlin. If the motors rotate to the same directions, the head travels along the X axis. If the motors rotate to opposite directions, the head travels along the Y axis.  
This mechanism has two belts, one over another, each on a circuit shaped like a T. Both circuits have pulleys at the middle on both sides and at the end of the cantilever.  
The upper belt is driven by the motor at the right end, has a pulley on the left end and is locked to the left side of the carrier. The lower is symmetric, motor on the left, pulley on the right, locked to the right side of the carrier.

<p float="center">
  <img width="430" src="https://github.com/FiCacador/Tlaser/raw/master/images/coreXY%20cantilever%20X.png" />
  <img width="430" src="https://github.com/FiCacador/Tlaser/raw/master/images/coreXY%20cantilever%20Y.png" />
</p>

## Hardware

The following parts are required for building this machine:

- [5.5W 445NM blue laser module w/ power supply](http://s.click.aliexpress.com/e/bAbwR1Wg)
- [MGN12H 300mm and MGN15H 400mm Blocks and Rails](http://s.click.aliexpress.com/e/bKj8dYfI)
- [2 Nema 17 stepper motors](http://s.click.aliexpress.com/e/cpg92iXI)
- [Arduino Uno R3 /w CNC shield v3 and A4988 stepper drivers](http://s.click.aliexpress.com/e/b7E6Xk5a)
- [2 mechanical endstops](http://s.click.aliexpress.com/e/CIG3mQk)
- [Timing belt GT2 6mm 5m](http://s.click.aliexpress.com/e/belvtmGu)
- [2 Belt drive Pulleys GT2 16 teeth bore 5mm](https://s.click.aliexpress.com/e/_d7v8uTQ)
- [GT2 pulleys, 4 w/ 16 teeth and 4 w/ no teeth](https://s.click.aliexpress.com/e/_dZuRE9S)
- [M3x6 and M3x30 round head hex bolts](http://s.click.aliexpress.com/e/cScWFTX6)
- [M3x8 socket head hex bolts](http://s.click.aliexpress.com/e/b72TH5Nm)
- [M3x12 self tapping bolts](http://s.click.aliexpress.com/e/bZMmlnQu)
- [M3x50 socket head bolts](http://s.click.aliexpress.com/e/t3QLC2k)
- [M3 hex nuts](http://s.click.aliexpress.com/e/nRG0NIC)

The list above contains affiliate links.  
The total cost should be below €150 / $165 USD, 3D printed parts not included.
For a more detailed table with quantities check the [Bill of Materials](https://github.com/FiCacador/Tlaser/raw/master/BOM.ods).

## 3D Printed parts

All parts are already correctly oriented for ease of printing and available in [STL files](https://github.com/FiCacador/Tlaser/tree/master/STLs) and [AMF files](https://github.com/FiCacador/Tlaser/tree/master/AMFs).  
Dimensional accuracy is very important. This is an assembly of mechanical parts designed to fit tight, the slightest overextrusion will make for a hard time during the assembly.  
Due to proximity to the stepper motors and laser module, [Laser Mount](https://github.com/FiCacador/Tlaser/blob/master/STLs/Laser%20Mount.stl), [Motor Mount Left](https://github.com/FiCacador/Tlaser/blob/master/STLs/Motor%20Mount%20Left.stl) and [Motor Mount Right](https://github.com/FiCacador/Tlaser/blob/master/STLs/Motor%20Mount%20Right.stl) should be printed with a more heat resistant material, like ABS or PETG.  
Recommended settings: 0.5 mm line width, 0.2 mm layer height, 2 mm wall thickness, over 15% infill. Some parts require support. [Base Left](https://github.com/FiCacador/Tlaser/blob/master/STLs/Base%20Left.stl) and [Base Right](https://github.com/FiCacador/Tlaser/blob/master/STLs/Base%20Right.stl) are prone to warping, requiring good bed adhesion.  
Total printing time around 38h. Total filament used approximately 600g.

## Assembly

### [Video of Tlaser Exploded Assembly on FreeCAD](https://youtu.be/6Z7JV-q1IXA)

An [Exploded Assembly CAD file](https://github.com/FiCacador/Tlaser/raw/master/CAD/Tlaser%20Exploded%20Assembly.FCStd) for [FreeCAD](https://www.freecadweb.org/) with the [Exploded Assembly workbench](https://github.com/JMG1/ExplodedAssembly) added is available to guide the assembly process.  
Required tools are a set of hex key wrenches, a philips screwdriver, a small flat head screwdriver, a rubber mallet and a wire cutter.  
The controller wiring is pretty straight forward, the exceptions being the laser TTL connects to the Z+ endstop pins and the red wire is left out when connecting the X and Y endstops. The power supply and 12V laser PCB cables need to be cut so both can be connected to the same respective + and - on the CNC shield.

<p float="center">
  <img width="430" src="https://github.com/FiCacador/Tlaser/raw/master/images/Tlaser%20Exploded%20Assembly.jpg" />
  <img width="430" src="https://github.com/FiCacador/Tlaser/raw/master/images/Controller%20Assembly%205%20Shield.JPG" />
</p>

## Firmware

An Arduino running [Grbl](https://github.com/gnea/grbl) is used to control Tlaser. It uses Grbl version 1.1g with a modified [config.h file](https://github.com/FiCacador/Tlaser/blob/master/Firmware/grbl-v1.1/grbl/config.h) with the configuration and default values that better suit this machine.  
You can find an hex file and the source code of Grbl for Tlaser [here](https://github.com/FiCacador/Tlaser/tree/master/Firmware).  
Instructions on how to [flash Grbl to an Arduino](https://github.com/gnea/grbl/wiki/Flashing-Grbl-to-an-Arduino) or alternatively [compile and upload Grbl](https://github.com/gnea/grbl/wiki/Compiling-Grbl) can be found on the [Grbl Wiki](https://github.com/gnea/grbl/wiki).  
Grbl is distributed under the GPLv3 license and is developed by Sungeun K. Jeon Ph.D.

## CAM Software

[LaserWeb4](https://github.com/LaserWeb/LaserWeb4/wiki) is simple yet powerful, graphically pleasing open source laser CAM software available for Windows, Mac and Linux.  
A [file containing Tlaser profile](https://github.com/FiCacador/Tlaser/blob/master/CAM%20profiles/laserweb-profiles-tlaser.json) for LaserWeb4 v4.0.996 is available.  
There are many valid laser CAM software options, use whatever one you like the most.

## Design

This project was designed using [FreeCAD](https://www.freecadweb.org/). There are more powerful and certainly more user friendly options, but none is actually free (of charge, of licensing, of login) and available for Windows, Mac and Linux.  
Designed with FreeCAD version 0.18.3 with the added workbenches [Fasteners](https://github.com/shaise/FreeCAD_FastenersWB), [A2plus](https://github.com/kbwbe/A2plus) and [Exploded Assembly](https://github.com/JMG1/ExplodedAssembly).  
You can find the CAD files for the individual parts and the assembly [here](https://github.com/FiCacador/Tlaser/tree/master/CAD).  
All the features and sketches of the 3D Printed parts are named, for ease of understanding and editing

---

Tlaser is developed by Filipe Caçador.

## License

Tlaser is published under the Creative Commons [Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/) Public License.  
Under this license, anyone can share, copy, redistribute, edit, remix and develop this work, for any purpose, as long as credit is attributed to the original author and any further developments are distributed under the same license.  
No warranty of any kind is provided and the author is not liable for any losses, damages or injuries in any way related to this work.
