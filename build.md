# Harite Build Guide

## Issues and Improvements

For any known issues and improvements please see the repo's [issues](https://github.com/dlip/harite/issues)

## BOM

- Harite PCB - order from your preferred PCB manufacturer using the gerber files in the [gerber_to_order](./gerber_to_order) folder
- 2 x RP2040-Zero controller with headers 2.5mm height
- 2 x Cirque 40mm Trackpads TM040040-2024-302 flat overlay (optional)
  - If you are able to test the no cirque case please let me know if it was successful
- 2 x HRO TYPE-C-31-M-12 USB C female ports
- 10 x SKRHADE010 5-way switches
- 50 x 1N4148 SOD-123 Diodes
- 1 x USB-C to USB-C cable to connect halves
- 1 x USB-C to USB-A/C cable to connect to pc
- 10 x M2 5mm flat head screws for base
- 20 x M2 4mm flat head screws for pcb and hot-swapable joysticks
- 30 x Knurled Insert Nuts M2 x 3mm Length x 3.5mm outer diameter (20 for the case and 10 for the hot-swapable joysticks)
- 6 x insulated wires 6cm approx. to connect cirque trackpad the the PCB. I used some ethernet cable which contiains 8 wires inside and stripped the ends with an Irwin vise-grip
- 3D printed Case and joystick parts - the STLs are in the [printables](./printables) folder. If you want to modify anything, this is the [Onshape Project](https://cad.onshape.com/documents/b93bd8dc5e080887b7a35bc8/w/2fa13694cc5562fc6be45ae5/e/0e302524d10cd22e841a2c15)
- 10 x rubber feet for case base
- Blu-tack or similar to stick down Cirque trackpad
- Super glue for joytick stems
- Soldering tools

## Print Settings

| Part          | Layer Height | Supports | Brim |
| ------------- | ------------ | -------- | ---- |
| Case - top    | 0.1mm        | yes      | no   |
| Case - bottom | 0.2mm        | no       | no   |
| Stem/Caps     | 0.1mm        | no       | yes  |

## Steps

### Firmware

It's a good idea to flash both RP2040-Zero to ensure they aren't dead

- Install [QMK CLI](https://github.com/qmk/qmk_cli)
- Git clone my [QMK Firmware](https://github.com/dlip/qmk_firmware/tree/dlip/keyboards/harite)

```
git clone https://github.com/dlip/qmk_firmware.git
cd qmk_firmware
```

- Hold the boot button while connecting the RP2040-Zero and a new drive should appear
- Flash the left

```
qmk flash -kb harite -km default -bl uf2-split-left
```

- Flash the right

```
qmk flash -kb harite -km default -bl uf2-split-right
```

### Soldering USB Port

![USB Port](images/usb-port.jpg)

- Since its quite challenging, solder on the usb ports on both sides. Watch this [YouTube video on drag soldering](https://www.youtube.com/watch?v=uguPxmkmaSg&t=163s&ab_channel=OffTheClack) for tips.
- Test the connections with a multimeter: set it to continuity mode and ensure you only hear a beep when connecting the following pairs by testing one of the pairs against every other pin.

![USB Pairs](images/usb-pairs.jpg)

### Soldering RP2040-Zero

![RP2040-Zero with headers](images/rp2040-headers.jpg)

- If the legs on the on the headers are longer than 3mm you will need to cut them shorter.

![Cut Headers](images/cut-headers.jpg)

- Insert into the top of the pcb and slide RP2040-Zero onto it to ensure the legs are straight. You can use sticky tape on the top to hold it in place.

![RP2040-Zero Taped](images/rp2040-tape.jpg)

- Flip the board to solder the bottom side, then remove the tape and solder the top side.

![RP2040-Zero Soldered](images/rp2040-soldered.jpg)

### Test Connection Between Halves

- IMPORTANT: You must never connect or disconnect the halves while they are connected to the computer since it may cause a power surge and fry some components.
- Run `qmk console`
- Connect halves via USB-C cable
- Connect either half's RP2040-Zero to the computer
- If you see "Target connected" in the console after a few retries you are good to continue

```
Ψ Console Connected: Dane Lipscombe harite (FEED:0000:1)
Dane Lipscombe:harite:1: Failed to execute slave_matrix
Dane Lipscombe:harite:1: Target disconnected, throttling connection attempts
Dane Lipscombe:harite:1: Failed to execute slave_matrix
Dane Lipscombe:harite:1: Target disconnected, throttling connection attempts
Dane Lipscombe:harite:1: Failed to execute slave_matrix
Dane Lipscombe:harite:1: Target disconnected, throttling connection attempts
Dane Lipscombe:harite:1: Target connected
```

### Soldering 5 Way Switches and Diodes

- Be careful with the switch orientation: the side with the 'v' shape cutout goes at the top, relative to the PCB's switch label (north east for the left side and north west for the right side)

![Switch Orientation](images/switch-orientation.jpg)

- Be careful with the diode orientation: the side with the line on the diode goes at the tip of the arrow on the PCB's label

![Diode Orientation](images/diode-orientation.jpg)

- Prepare each set of pads by soldering one of its pads

![Switches Solder Prep](images/switches-solder-prep.jpg)

- Solder the first pad of each component. Ensure they are all aligned to the other pads then solder the rest of them.

![Switches Complete](images/switches-complete.jpg)

- Test the 5 way switches are working by connecting this half to the PC via the RP2040-Zero with the USB cable and pressing each direction then its center switch. You should see these characters typed for each direction: 'u', 'd', 'l', 'r', 'c'

### Soldering Cirque Trackpad

- Note: in my photos I soldered the wires on the front side. I realised afterwards that it might have been easier to do it on the back, so I have added the labels there in the latest design. There should be enough room with the 3mm stand-offs to do it from the back but it would be great if someone could try this and let me know, I would like to make it the preferred method. Photos would be appreciated too!
- Prepare wires and strip one end of each to about 2mm and bending it 90 degrees. Keep the wires a bit longer than needed as we will cut it to length afterwards. It's good to use different coloured wires to help keep track of what goes where.
- Insert wires into the labeled cirque holes and solder on the opposite side

![Cirque Wires](images/cirque-wires.jpg)

- The Cirque orientation is different for each side, ensure the 2 cutouts point towards the RP2040-Zero

![Cirque Orientation](images/cirque-orientation.jpg)

- In order to ensure the wires are the correct length to allow enough slack to fit through the case in the end, I recommend taping it and the PCB to the case while soldering. I messed this part up many times, trust me its worth the effort.

![Cirque Taped](images/cirque-tape.jpg)

- Add solder to each of the 6 pads on the Cirque
- Cut each wire to length, ensuring plenty of slack by curving it down then up as in the image
- Strip each end and bend it 90 degrees

![Cirque Soldered](images/cirque-soldered.jpg)

- Connect to the computer and test you can move the cursor
- Remove the tape and carefully push the Cirque through the slit in the case. Try not to bend the the wires connecting to the Cirque, its better to bend at the PCB side since they have a stronger weld

### Case

- Melt knurled insert nuts into holes in the base and top. Heat soldering iron to about 180c temperature and melt while holding the nut down with tweezers to ensure its level

![melt-nuts.jpg](images/melt-nuts.jpg)

- Screw the PCB to the 3D printed base using the M2 4mm screws

![PCB Screwed](images/pcb-screwed.jpg)

- Put the 3D printed top over the top while carefully feeding the Cirque trackpad through the slit and into position, following the 2 notches to ensure it has the correct rotation

![Cirque Bend](images/cirque-bend.jpg)

- Add some Blu-tack or similar to keep it from coming out

![Cirque Blu-tack](images/cirque-blutak.jpg)

- Screw on base using M2 4mm flat head screws
- Add rubber feet

![Rubber feet](images/rubber-feet.jpg)

### Joysticks

In order to ensure the top of the case can still be removed, the joysticks have a stem that is separate to the cap which is glued on

![Joystick Parts](images/joystick-parts.jpg)

- Test if the 3D printed stem with the 2mm or 2.1mm hole fits comfortably on the switch stem without too much forcing. If neither are great, you can modify it in OnShape and then export it to stl
- Melt knurled insert nuts into holes in the top of the stem. Do your best to make it flat, and if some melt off to the side its better to discard it and make a new one since they are going to be permananty attached
- Squeeze a small amount of super glue out onto a disposable surface and roll the tip of a toothpick to lightly cover it

![Joystick glue](images/joystick-glue.jpg)

- Thinly coat the inside of the switch hole at the bottom of the stem with super glue

![Glue stem](images/glue-stem.jpg)

- Press firmly onto switch and allow to set

![Joystick stem glued](images/joystick-stem-glued.jpg)

- Screw on cap of choice using M2 4mm flat head screws

### Joystick Caps

There are a few different joystick caps in the printables folder

#### X-Ring

This is inspired by the CharaChorder 2 caps, and give the best balance of grip and tactical feedback. They are meant to have a rubber X-Ring of thickness 1.78mm and inner diameter 6.75mm fitted to them such as [these](https://www.aliexpress.com/item/1005004871516731.html) from Ali Express.

![Cap X-Ring](images/cap-xring.jpg)

They can be a little tricky to put on, but you can stretch the ring oven the cap with some needle nose pliers and hold it in place while using tweezers to pull it over the edges.

![Cap X-Ring Hold](images/cap-xring-hold.jpg)

#### Meta Quest Thumbstick

This has decent grip, but it does reduce some of the tactile feedback. I still like it for thumbs and with cheap silicone Meta Quest thumbcaps from Ali Express

![Cap Quest thumbstick](images/cap-quest-thumbstick.jpg)

#### Rubber Feet Pad

Simple if you already have some flat rubber feet lying around

![Rubber Feet Pad](images/cap-rubber-feet.jpg)

#### Rounded square / Seat

This was my first 2 designs, the rounded square isn't bad but I really need some rubber grip with my dry hands.

The seat is ok in the left/right directions, but down is a bit uncomfortable and up is hard to feel any feedback from the switch to know if you have pressed it or not.

![Joystick Caps](images/joystick-caps.jpg)

### Congratulations

- Try my [Stained layout](https://github.com/dlip/qmk_firmware/tree/dlip/keyboards/harite/keymaps/stained) or make your own
- Play [Eye of the tiger](https://www.youtube.com/watch?v=CiIkBT-HFOA&ab_channel=n1ckr1vers) and start your epic training montage!
