# Klipper Configuration

Inside the provided Klipper_Toolhead.cfg there are only the lines written down which are tied to the hardware. <br>
Anything else (PID values, min temp, max temp for example) is setup specific. See https://www.klipper3d.org/Config_Reference.html for aditional information<br>

For the compile config, consider setting PB9 in GPIO pins (see Image below). <br>
This will spin up the fan connected to the bottom fan-connector (usually the fan for the Heatsink!) <br>
If anything happens during the print and the printer changes into error-mode, then your hotend (more specific the coldend/heatsink) will not overheat.

![2024-05-16-00-29-13-719](https://github.com/cad435/StealthburnerFullUSBPD/blob/main/PD-Toolhead/Klipper%20Configuration/Compile_Config.png)

---

## Flashing with KIAUH v6:
KIAUH v6 has the ability to save compile configs.
 - download pd-hotend-stm32f072.config
 - place it inside /home/usr/klipper-kconfigs/ folder<br>
    (replace usr with your klipper user. On a standard installation this would be "pi" --> /home/pi/klipper-kconfigs/)
 - restart KIAUH v6 and navigate to the "Advanced"-Menu to get the firmware flashing Menu
 - when try to build or build+flash KIAUH should present you the option to load the config.

You also don't have to place the board in bootloader mode anymore. When flashing with KIAUH just select "connected via USB". The flash utility of KIAUH will place the board into bootloader-mode on its own. <br>
I'm not exactly sure since when this is possible. My setup runs with KIAUH v6 and Klipper v0.12.0. <br><br>

Be aware, that KIAUH may state a failed flash although flashing actually succeeds.<br>
Inside your command-Line you are looking for the lines:
```
[...]

Download        [=========================] 100%        36988 bytes
Download done.
File downloaded successfully
Submitting leave request...

[...]

```

See this post for additional reference:
https://github.com/dw-0/kiauh/issues/545#issuecomment-2395065270

---

## "Legacy" Flashing:

Hold down the "BOOT" button (see Pin Description PDF), than press the RESET Button. The Toolhead will be accessible via ST's USB-Hardware Bootloader in DFU. Use "USB (DFU mode)" option in KIAUH.

