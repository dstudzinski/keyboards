## Disclaimer

I'm not responsible for any damage if you follow these notes.  
This is my first DIY keyboard. I don't have much experience with soldering or electronics (before this project, I only
soldered a few things like 3.5mm audio jacks, and that's almost all).  
It's my first Sweep build, so I'm not sure if all my assumptions or my understanding of other builds and upgrades are
correct.

Please let me know if you spot any mistakes (you can create an Issue on GitHub—making a PR is even better 😉).

---

## Intro

These are just my personal notes from the preparation and building process.

At the beginning, I had trouble understanding the Sweep keyboard project. For example, I didn't know why I saw a
Bluetooth version with TRRS, or why there were different connectors in the photos. I started reading, watching videos,
and these are my notes from that!

I already own a Redox Wireless v1 with hot-swap (Kailh hot-swap) switches. I wanted to try a smaller wireless keyboard.
I
heard about 34-key keyboards (and the Ferris Sweep mod) from this
video: [34 keys is all you need: an ergonomic keyboard journey](https://www.youtube.com/watch?v=unMXQTSQEak).  
Then I watched [You Won’t Believe How Effective This Keyboard Layout Is](https://www.youtube.com/watch?v=8wZ8FRwOzhU)
and [A Tiny, Ultra-Affordable Keyboard You Can Build Yourself!](https://www.youtube.com/watch?v=JqpBKuEVinw) by Bell
Vallack, and started thinking about trying this type of layout.

Later, I
found [“The REAL Ergonomic Keyboard Endgame!” - How To Design & Make A Totally Custom Keyboard](https://www.youtube.com/watch?v=UKfeJrRIcxw) —
a video about designing custom keyboards. Maybe that will be my next keyboard if the small layout works for me. 😉

---

## About the Sweep Keyboard

[Sweep](https://github.com/davidphilipbarr/Sweep) keyboards are available in
different [types](https://github.com/davidphilipbarr/Sweep#what-are-the-different-types).

When I looked at different photos, I was confused about what parts I needed and why I saw things like different
connectors, wired and Bluetooth builds, cables, etc. Here’s what I learned:

### Main Points

- You can build both wired or wireless versions using Kailh Choc switches (and low-profile keycaps) or standard switches
  like MX (and sometimes Alps, with standard keycaps). You need to choose the right PCB for your switches.
- There are PCBs for Choc switches with smaller spacing — that's why some keyboards look different in photos.
- Some PCBs support a **“Reversible PCB”** design. You need 2 of the same PCB (not a separate left/right). Reversible
  PCBs are cheaper to order because you can order 5 PCBs (enough for 2.5 keyboards). With non-reversible designs, you
  need 2 different boards—so you have to order 10 PCBs for 5 keyboards. Reversible is less expensive, but it's easier to
  make a
  soldering mistake because solder points are on both sides. If you mark the sides and stay careful, it should be fine.
- The Hot Swap column on the Sweep GitHub tells you which versions support hot-swap for switches. All versions support
  Mill-Max sockets for the
  microcontroller ([Mill Max Microcontroller socket support](https://github.com/davidphilipbarr/Sweep/issues/59)).
- Bluetooth (wireless) versions with `nice!nano` controllers only work with [ZMK](https://zmk.dev/). Wired (Pro Micro)
  versions use [QMK](https://qmk.fm/).
- The **central half** (usually left, sometimes called **middle half**) is the one that communicates with the computer
  and the other half.
- The **peripheral half** (usually right) only talks to the “middle half”.
- You can estimate battery life with the [ZMK power profiler](https://zmk.dev/power-profiler).

---

### Wired vs Wireless Sweep

#### **Wired (TRRS) Sweep**

- Must be connected to the computer with a USB cable.
- Needs TRRS sockets and a TRRS cable to link both halves.
- TRRS cable lets the “middle half” get key presses from the “peripheral half”.
- Only the “middle half” needs USB to connect to the computer.
- No need for batteries or power switches.
- Uses Pro Micro (less expensive than nice!nano).

#### **Wireless (Bluetooth) Sweep**

- “peripheral half” use Bluetooth to connect to the computer.
- “middle half” connects to the computer by Bluetooth.
- “middle half” can by connected by USB-C to the computer (if you want to use it as a wired keyboard). Halves always '
  talk' wirelessly.
- you can switch between bluetooth and USB-C during use, you can also have multiple bleuetooth devices connected at the
  same time and switch profiles.
- Does **not** need TRRS sockets/cable.
- Each half needs a power switch to turn it off when not in use.
- Needs batteries (standard: 301230 size).
- Uses two `nice!nano` controllers, which are more expensive than Pro Micro.
- Batteries can be charged using the nice!nano’s built-in charger. You can use the keyboard while charging over USB.
- You can also run both halves with no batteries by just powering them from USB.
- you can power both halves from USB-C with power banks, but many power banks will switch off for peripheral half after
  a few minutes because of a small power draw.

#### **Mixes & Conversion**

- You can convert a wired build to wireless: swap Pro Micros for nice!nanos, add power switches to both halves, and
  add batteries.
- To add hot-swap for switches, you can use Kailh hot-swap or Mill-Max sockets (if the PCB supports them).
- You can use nice!nano in a wired build too (though there might be some limitations/features you lose or gain depending
  on firmware and hardware).
- You can use larger, external batteries, but only the small flat "301230" fits under the microcontroller on the board.

---

### Important Terms

- **Hot-Swap** sockets allow you to change switches without soldering.
- **Mill-Max** (for microcontroller): The board supports using “Mill-Max” sockets so you can easily remove/replace the
  controller (Pro Micro / nice!nano).
- **Reversible PCB**: The PCBs are identical on both sides; you don’t need a unique “left” and “right” board.

---

## My Build Plan

> _Note: I don't know if a 34-key, high-profile keyboard will be comfortable for me (I like high/tactile switches). My
idea is to build a full MX version first. If I like the layout but not the size/feel, I'll try building a low-profile
Choc version later._

- Wireless build (“Sweep Bling MX” PCB)
- 34 x MX Brown switches (already have these)
- 34 x MX keycaps (already have these)
- 0 TRRS connectors/cables
- 2 x nice!nano controllers
- 48 Mill-Max pins & 2 x sockets
- 2 x power switches
- 2 x reset buttons
- 2 x batteries (301230, under microcontroller)

With this setup, it should last about 1 week (central half) and 2 months (peripheral half) per charge, according to [ZMK
Power Profiler](https://zmk.dev/power-profiler)

Check nested directories for details about my builds.

---

## Soldering and Risk of damage because of EDC

**Important:** nice!nano docs warn against using high soldering temperatures:
> "When soldering the nice!nano, avoid using high iron temperatures, as you could damage the main nRF52840 chip. A
> temperature around 270°C-300°C should be hot enough. The higher the temperature, the more likely you are to damage the
> board."  
[Source](https://nicekeyboards.com/docs/nice-nano/getting-started/)

**Important:** The nice!nano v2 does not have ESD (Electrostatic Discharge) protection, so it's possible to damage it if
you touch the pins or components with static electricity (you are not grounded), or if you 'shock' controller when you
connect USB cable.
Controller after such shock may work but not properly (eg some keys may not work only from time to time or keys can be
repeated from time to time). It always good to ground yourself before touching controller and you should cover
controller to not touch it when you connect USB cable.
Such problems can be caused also by bad soldering so sometimes is hard to find the reason of the problem.
Keep in mind that you can always switch controllers with second half (and flash it accordingly) @to check if the problem
is with the controller or with the soldering.

---

## Building and Flashing ZMK

1. Visit [https://github.com/new](https://github.com/new)
2. Set repo name to `zmk-config` (make it public or private).
3. Don’t check any options to initialize README or files.
4. Click “Create repository”.

**Generate ZMK files:**  
In any directory (I push the repo myself, so I skip GitHub steps in the setup tool):

1. Run: `bash -c "$(curl -fsSL https://zmk.dev/setup.sh)"`
2. Pick your shield (Sweep/Cradio)—when I tried, it was option 15.
3. Pick your controller (`nice!nano 2.0`, which was 6 when I tried).
4. For "Copy in the stock keymap for customization?"—choose `y` (yes).
5. Leave "GitHub username" empty to skip repo creation.
6. When it asks "Continue?"—choose `y`.
7. After a few moments, there will be a new directory, `zmk-config`.
8. `cd zmk-config`
9. Link your repo: `git remote add origin git@github.com:YOUR_GH_NAME/zmk-config.git`
10. `git branch -M main`
11. `git push -u origin main`

**Build and Download Firmware:**

1. Open the “Actions” tab in your GitHub repo.
2. Wait for the “Initial User Config.” build to finish (pick the latest, at the top).
3. Open the finished build (green check). Find and download the "firmware" artifact.
4. Unzip `firmware.zip`.

**Flashing:**

1. Switch off the left half (move switch toward nice!nano).
2. Connect it to the computer by USB-C.
3. Press the reset button twice quickly (or short the jumpers twice if you don't have a button).
4. It mounts as a drive—copy the firmware file (`cradio_left-nice_nano_v2-zmk.uf2`) onto the drive.
5. It auto-unmounts (on Mac, ignore "keyboard setup assistant").
6. Disconnect USB.
7. Do the same for the right half (firmware: `cradio_right-nice_nano_v2-zmk.uf2`).

You **can** test the left half without flashing the right half:

- Turn it on after flashing and wait for it to disconnect from USB (or use a battery/power bank).
- Open Bluetooth settings on your device, and search for a new device. You should see “Cradio” after a moment—you can
  pair with it.

---

## Troubleshooting

- **Problems with pairing?**  
  [ZMK split keyboard halves: unable to pair](https://zmk.dev/docs/troubleshooting#split-keyboard-halves-unable-to-pair)

- **Want to power from USB?**  
  [Powering keyboard from USB](https://zmk.dev/docs/behaviors/outputs)

---

## Useful Links

### Videos about Sweep/34-key keyboards:

- [34 keys is all you need: an ergonomic keyboard journey](https://www.youtube.com/watch?v=unMXQTSQEak)
- [You Won’t Believe How Effective This Keyboard Layout Is](https://www.youtube.com/watch?v=8wZ8FRwOzhU)
- [A Tiny, Ultra-Affordable Keyboard You Can Build Yourself!](https://www.youtube.com/watch?v=JqpBKuEVinw)

### Sweep Project:

- [Sweep main page](https://github.com/davidphilipbarr/Sweep)
- [Sweep types](https://github.com/davidphilipbarr/Sweep#what-are-the-different-types)
- [Sweep Mill Max microcontroller socket support](https://github.com/davidphilipbarr/Sweep/issues/59)

### Key Software:

- [ZMK](https://zmk.dev/)
- [QMK](https://qmk.fm/)
- [ZMK power profiler](https://zmk.dev/power-profiler)

### Other:

- [“The REAL Ergonomic Keyboard Endgame!” - How To Design & Make A Totally Custom Keyboard](https://www.youtube.com/watch?v=UKfeJrRIcxw)
- [ZMK Power Profiler](https://zmk.dev/power-profiler)

My config for ZMK can be found here: https://github.com/dstudzinski/zmk-config

---

