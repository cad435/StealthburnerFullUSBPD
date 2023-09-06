On the Footprint of the FE1.1S D+ and D- are switched (wrong symbol). Patch-wires fiexed the problem

Replace the IP2701 with TPS25740

PowerFeeder: Not somewehere: when R16 is placed, feeder will only function when connected to USB, not standalone. R16 not placed will enable standalone. Consider this when designing with TPS25740.

PowerFeeder: Integrate 6A Fuse into all path. Preferably swappable ones

PowerFeeder: Increase C4 to a 1uF Capacitor

PowerFeeder: USB-Port Indicator LED's for Upstream Port 1 and 4 are switched

PowerFeeder: what if the Hotend-FET fails into short circuit? We want a way to separate power if needed.
--> Second input for 5V and 24V will be switched on when in "production"? Does this interfere with the PD-Delivery?

--> Powerfeeder needs new Gerber Version

___


Done - PD-Toolhead: Remove R13 & R15 as it interferes with USB-PD

Done - PD-Toolhead: populate R11 Resistor. Without it, CH224K won't have power

Done - PD-Toolhead: FAN0/1 Doku is wrong. Top Fan is PB8, Bottom Fan is PB9
Done - PD-Toolhead: RX on TMC driver servers as CS pin for SPI drivers

Done - PD-Toolhead: C18 & C22 are rated for 16V need 25V --> Increase Value if possible
Done - PD-Toolhead: change R22 to 680k, change R24 to 100nF
