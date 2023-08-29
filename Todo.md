On the Footprint of the FE1.1S D+ and D- are switched (wrong symbol). Patch-wires fiexed the problem

Replace the IP2701 with TPS25740

PowerFeeder: Not somewehere: when R16 is placed, feeder will only function when connected to USB, not standalone. R16 not placed will enable standalone. Consider this when designing with TPS25740.

PowerFeeder: Integrate 6A Fuse into all path. Preferably swappable ones

PowerFeeder: Increase C4 to a 1uF Capacitor

PowerFeeder: what if the Hotend-FET fails into short circuit? We want a way to separate power if needed.
--> Second input for 5V and 24V will be switched on when in "production"? Does this interfere with the PD-Delivery?

--> Powerfeeder needs new Gerber Version

___


PD-Toolhead: Remove R13 & R15 as it interferes with USB-PD

PD-Toolhead: populate R11 Resistor. Without it, CH224K won't have power

-> PD-Toolhead, Power over USB-PD and Datatransfer confirmed working. No gerber-changes needed, only assembly-options for now
