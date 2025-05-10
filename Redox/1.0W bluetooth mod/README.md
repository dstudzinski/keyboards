## Redox Wireless 1.0W: Modding from QMK Dongle to ZMK Bluetooth

### Background

I own a Redox 1.0W, originally purchased from FalbaTech.  
It's a really nice, well-made keyboard, but unfortunately, I can’t use it anymore due to interference issues on the
2.4GHz band.  
This board doesn't use Bluetooth; instead, it uses a custom dongle to communicate with the computer. The dongle connects
via USB and both halves of the keyboard talk to this dongle.

There is an old thread about these issues [here](https://github.com/mattdibi/redox-keyboard/issues/55)—unfortunately, I
found it only after buying the keyboard. If I’d known about these problems earlier, I might have chosen the wired
version, which can easily be converted to Bluetooth by replacing the Pro Micros with nice!nano controllers.

> **Note:** I didn’t experience any issues with this keyboard for several years until I moved to a different apartment
> in a more “crowded” building (in terms of wireless signals).

---

### My DIY Wireless Keyboard Journey

When the interference problems started, I built a Sweep (see notes in this repo), and I really enjoy features like "home
row modifiers." I don’t have to move my fingers as much, but I do miss full-height tactile switches.  
On such a small keyboard, entering special characters, shortcuts, etc., is sometimes harder because you have to switch
layers more often—meaning more key presses compared to a larger keyboard.

Recently, I started thinking about handwiring the Redox so it fits inside my existing case (the cases differ between
versions, so I can’t just swap out the PCB).  
I opened up one half and used the other side of the PCB as a template for my handwired version (the PCBs are reversible
in this build).

My first idea was to "not break anything," so I could always go back to the original wireless version. But I quickly
realized that the top plate has wider holes than the switches, meaning the switches can move left and right slightly. To
keep them steady, I’d have to glue them to the plate—and the build wouldn’t be as clean as I wanted.  
At that point, I decided I probably wouldn’t use the original wireless version again, so I began analyzing the PCB
layout and comparing it to the wired version (which is much easier to convert to Bluetooth).

The PCB of the wireless version has the exact same switch connections as the wired one (diodes, columns, rows, etc.).
The only differences are the controller connections (the controller is a different shape) and some added components: a
power switch, programming connector, and battery socket.

So, I decided to create a "partially handwired" build, reusing as much of the existing PCB as I could.

---

### The Build Process

I wasn’t able to unsolder the YJ-14015 controller because I don’t have a heat gun. As you’ll see in the photos, I had to
remove it quite forcefully.

- I used a regular soldering iron with copper wire to remove as much of the "solder" as possible.
- Then, I used a sharp knife, placed between the PCB and controller (from the edge of the PCB), and alternately heated
  solder points
  on the left and right, pushing the knife deeper as I worked.
- I also removed the battery socket in a similar fashion.
- I used a rotary tool (like a Dremel) to smooth off a small bump on the PCB for the negative terminal and covered it
  with a bit of **nail polish**.

Naturally, the PCB was damaged in the process, but there are no shorts, and I don’t plan to revert to the old wireless
design.

Using the board’s schematic, I found where the Pro Micro connects on the wired version and soldered jumper wires (cut in
half to keep female connectors on the other end).  
I did this for all rows and columns, making each PCB symmetrical in color by cutting and using each half for opposite
sides.

To connect to the nice!nano-compatible controllers, I used right-angle header pins (see the `controllers` directory in
the repo for details about alternatives), making the assembly as flat as possible.  
This way, I can easily connect and disconnect the controller—and so far, I haven’t had any connectivity problems.  
On one controller, the whole row of pins is soldered. On the other, I used individual pins (removed from the plastic
strip), soldering only the necessary connections.

For the reset button (a tiny one, like in my Sweep build), I soldered additional jumper wires and hot glued the button
in the space where the programming pins had been. This lets me easily reset the board by pressing the button **through a
hole in the case**.

I also purchased USB-C female and male connectors. I used these to create a very short USB-C cable:

- The male end connects to the controller.
- The female end is hot glued where the battery used to be—hidden, but still easy to access for charging.
- This USB socket should be glued slightly above the PCB, so the cable’s connector doesn’t push against the wooden case,
  making it hard to plug in (which could also put stress on the connector).

**NOTE:** I'm not sure why, but when I use a long USB-C to USB-C cable, the controller isn’t detected by my computer and
I can't copy new firmware to it. However, if I connect the long cable directly to the controller—bypassing my short,
homemade USB-C cable—everything works as expected.
This means that, due to my short USB-C extension inside the keyboard, I need to use shorter cables between the keyboard
and the computer whenever I want to upload new firmware.

---

### Fit, Assembly, and Power

My original wireless build uses Kailh hot-swaps, so there’s only about 3–3.5mm between the PCB (plus hot-swaps) and the
case.  
Other versions (without hot-swaps) likely have more room. In my case, the top plate screws pinch the wires/controllers a
bit, but that doesn’t seem to cause any problems.
The top plate is a little lower than the edge of the cover, so you can probably use some small distances between pcb and
cover to gain around 1mm.

For power, I bought small 3mm thick batteries. Using ZMK’s power profiler, I estimate about 1 month of battery life for
the “central” half and more than 7 months for the “peripheral” half.

The battery is handwired to the controller with jumper wires, and I retained the existing switch to turn the battery
power on and off.

---

### Bill of Materials (BOM)

| Item                         | Quantity | Details                                                                                                                                       | Link                                                                                                                                                   |
|------------------------------|:--------:|-----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Battery                      |    2     | Li-Pol Akyga 320mAh 1S 3.7V 40x30x3mm (you can see smaller 110mAh 301330 battery from Sweep design on some photos which was used for testing) | [Botland](https://botland.store/battery-li-pol-1s-37-v/12207-akyga-li-pol-battery-320mah-1s-37v-jst-bec-connector-socket-40x30x3mm-5904422318857.html) |
| Reset button                 |    2     | B3U-1000P 4x2.5mm (legs) or 3x2.5mm (no legs), 1.6mm height                                                                                   | [AliExpress](https://aliexpress.com/item/1005003045038291.html)                                                                                        |
| Jumper wires (Dupont cables) |    20    | 20cm female-to-female; per board: 12 half-length + 4 full-length (reset & battery), total of 20 for both boards                               | [AliExpress](https://aliexpress.com/item/1005007072081464.html)                                                                                        |
| Right-angle pin headers      |    4     | Four strips, each with 13 pins; covers both controllers on both sides. 16 pins are used per controller (32 total)                             | [AliExpress](https://aliexpress.com/item/1005003646655689.html)                                                                                        |
| USB-C F+M connectors pair    |    2     | Two pairs (four pieces): two female and two male connectors                                                                                   | [AliExpress](https://aliexpress.com/item/1005007458786256.html)                                                                                        |
| nice!nano V2 Controller      |    2     | I used clones                                                                                                                                 | [AliExpress](https://aliexpress.com/item/1005007426478606.html)                                                                                        |

---
