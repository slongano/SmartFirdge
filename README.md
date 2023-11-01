# SmartFridge
Software for a smart fridge based on ESP32 boards and ESPHOME software.

To "describe" a fridge there are "fridge templates" describing their physical components, like doors, compressors, sensors, and lights, in an abstract way.

The code will be written in modules corresponding to different fridge templates.

## Templates
Templates are used to describe how a fridge is physically made.

The model is that a fridge has doors, as you see them from left to right, with a / to separate door groups from top to bottom.

Each door closes a "cellar".

Templates are made by starting with the upper left door, followed by the list of its cellar components enclosed in [].

For

### Doors

A fridge door is indicated with an uppercase D, and a freezer door with a lowercase d.

If the letter is enclosed in parenthesis, it indicates that the door is behind the previous door. This happens with freezer compartments in small fridges.
A lowercase i after the letter indicates an ice dispenser.

### Sensors, lights, cameras and actuators

A fridge can have sensors, lights, cameras, and actuators serving each cellar.

Sensors can be:
- temperature (Symbol T, data type degrees in C or F)
- humidity (Symbol H, data type RH in %)
- door (Symbol D, binary state: open, close)
- dispenser (Symbol d, binary state: idle, dispensing)

There can be more than one temperature or humidity sensor in each cellar, but only one door sensor and one dispenser.

Each cellar can have zero or more lights. If present they are indicated with L1 to Ln. (on, off)

Each cellar can have zero or more cameras. If present they are indicated with C1 to Cn. (inside view, door view)

Each cellar can have one actuator to start the cooling in the cellar. Each actuator has an associated compressor and sometimes an air valve. 

At least one cooling actuator **must** be present. Fridges with a freezer compartment might not have a cooling actuator specific to the freezer. They are designed and built so that inside the freezer compartment the temperature is below zero (C) even when the rest of the fridge is at the upper limit of the temperature regulation (no more than 8°C). Some small fridges, especially under counter models or those for camper vans and trailers, are realized in this way.

The actuator is on or off, and it turns on the associated compressor and, if present, the air valve. This setup works with systems with one compressor for the fridge and one for the freezer (combined compressor) and with separate compressors for each function.

It is indicated with an A.

Each cellar can have an actuator for a fan. It is indicated with an F.

## HMI
The fridge can have an interface. It can be used to simply display status or to set operating parameters.

For this project we will consider five interfaces.

- Simple RGB LED.
- Matrix display
  - with buttons
- LED display
  - with buttons
- LED touch screen

