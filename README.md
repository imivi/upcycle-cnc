![UpCycle CNC](https://raw.githubusercontent.com/imivi/upcycle-cnc/refs/heads/main/docs/image_s.jpg)

# UpCycle CNC

UpCycle CNC is an open source DIY CNC design that reuses parts from the popular 3018 CNC.

It features a 30x18 cm cutting area with around 9 cm of Z travel.

The full part list (bill of materials) is included in `cnc_bom.csv`.

Requires the 3D printed parts found in the `printed-parts` directory. Freecad, STEP and STL files are included.

The endstop brackets are available here:

* [Sculpfun S10 Limit Switch Mount](https://www.printables.com/model/898865-sculpfun-s10-limit-switch-mount/files)

## How to install GRBL onto an Arduino Uno

1. Download the GRBL firmware (as zip file): https://github.com/gnea/grbl
2. Unzip and then zip the **grbl** subdirectory
3. In the Arduino IDE, Sketch > include library... > add .zip library
4. Select the zipped grbl subdirectory
5. File > examples > grblUpload
6. Upload the sketch

## Wiring the relay module to toggle the spindle

![Relay module](https://raw.githubusercontent.com/imivi/upcycle-cnc/refs/heads/main/docs/relay.jpg)

In order to use the relay to toggle the spindle, we must customize the GRBL configuration.

We have to modify the grbl configuration file (config.h) and reupload GRBL:

* **Windows:**`C:\Users\[YourName]\Documents\Arduino\libraries\grbl\config.h`

* **Linux:**`~/Arduino/libraries/grbl/config.h`

1. open `config.h`
2. comment "#define VARIABLE_SPINDLE" to disable spindle PWM control (only on/off)
3. uncomment "INVERT_SPINDLE_ENABLE_PIN" so that the enable pin is HIGH by default, which turns OFF the relay (which has an inverted behavior)
4. reupload GRBL