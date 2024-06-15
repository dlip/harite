# Harite Keyboard (WIP)

Harite is 5-way switch keyboard with dual trackpads. The word Harite is the Sumo Slap attack in Japanese, I thought it was appropriate since it looks like a grabbing hand with the 5 joysticks for each finger and the trackpad as the palm.

## BOM

- Harite PCB - order from your preferred PCB manufacturer using the gerber files in the [gerber_to_order](./gerber_to_order) folder
- 2 x RP2040-Zero MCU with headers 2.5mm height
- 2 x Cirque 40mm Trackpads TM040040-2024-302 flat overlay
- 2 x HRO TYPE-C-31-M-12 USB C female ports
- 10 x SKRHADE010 5-way switches
- 50 x 1N4148 SOD-123 Diodes
- 1 x USB-C to USB-C cable to connect halves
- 1 x USB-C to USB-A/C cable to connect to pc
- 10 x M2 6mm flat head screws for base
- 10 x M2 4mm flat head screws for pcb
- 20 x Knurled Insert Nuts M2 x 3mm Length x 3.5mm outer diameter
- 6 x insulated wires 6cm approx. to connect cirque trackpad the the PCB. I used some ethernet cable which contiains 8 wires inside and stripped the ends with an Irwin vise-grip
- 3D printed Case and joystick caps - the STLs are in the [printables](./printables) folder. If you want to modify anything, this is the [Onshape Project](https://cad.onshape.com/documents/b93bd8dc5e080887b7a35bc8/w/2fa13694cc5562fc6be45ae5/e/f3942d0fbdb4c55aacbbd3d2)
- Soldering tools

## Steps

- Git clone my [QMK Firmware](https://github.com/dlip/qmk_firmware/tree/dlip/keyboards/harite) and flash to both RP2040-Zero to ensure they aren't dead
- Since its quite challenging, solder on the usb port. Watch this [YouTube video on drag soldering](https://www.youtube.com/watch?v=uguPxmkmaSg&t=163s&ab_channel=OffTheClack) for tips
- Solder RP2040-Zero with headers - if the legs on the on the headers are longer than 3mm you will need to cut them shorter. Insert into the top of the pcb and slide RP2040-Zero onto it to ensure the legs are straight. You can use sticky tape on the top to hold it in place while soldering the bottom side, then remove the tape and complete the top side.
- Solder 5 way switches - the side with the 'v' shape cutout goes at the top, relative to the PCB's switch label (north east for the left side and north west for the right side)
- Solder diodes - the side with the line on the diode goes at the tip of the arrow on the PCB's label
- Test the 5 way switches are working by connecting this half to the PC via the RP2040-Zero with the USB cable and pressing each direction then its center switch
- Solder Cirque trackpad to the PCB, matching the labels on them. You can give this a test on the computer afterwards too
- Melt knurled insert nuts into holes in the base and top. Heat soldering iron to about 170c temperature and melt while holding the nut down with tweezers to ensure its level.

![melt-nuts.jpg](images/melt-nuts.jpg)

- Screw the PCB to the 3D printed base using the M2 4mm screws
- Put the 3D printed top over the top while feeding the Cirque trackpad through the slit and into position, following the 2 notches to ensure it has the correct rotation.
- Repeat the process for the other half
- IMPORTANT: Disconnect both halves from the computer before connecting them together with the USB port on the side. You must never connect or disconnect the halves while they are connected to the computer since it may cause a power surge and fry some components.
- Connect one half to the computer and test
- Flash my QMK engram layout to the RP2040-Zero or make your own
- Play [Eye of the tiger](https://www.youtube.com/watch?v=CiIkBT-HFOA&ab_channel=n1ckr1vers) and start your training. Good luck!
