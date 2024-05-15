
## Before you download:
There are new Versions with better EMI protection regarding the USB Data lines on the way. Also, on the feeder I connected the free-wheeling diode wrong. It'll also be fixed.

The current versions however are working. <br>

 - Update 2024-05-16: I implemented the new and EMI-improved toolhead-boards and my errors went away. However, new feeders are untested right now. As it is working, I'll only upload the EMI-improved toolhead for now. While manufacturing the new toolheads I also discovered that some of the STM32F072 MCUs I used, are lacking pin 1 markers. It looked to me as if they where sanded down and re-marked (yes I bought them from Aliexpress). I'm not sure if the new EMI-improving did the trick or if some of the MCU's where just faulty. However I do like the new EMI-protection features, so it definately was not a bad investment. 


# StealthburnerFullUSBPD
Two PCB's to connect a Voron Stealthburner Toolhead via USB-PD providing both power and data.

**This has compliant USB-C PD communication, this is not a "hacky" solution where I just shove 20V over the Power-Lines!** <br/>


You can actually charge your Phone, Power your USB-Soldering Iron or whatever you like with it :) <br/>
You can also just use the Feeder Board for whatever non-3D-Printer related USB-PD circuitry you like <br/>

This is aimed at people which are either having some kind of toolchanging system (like me) or are - for whatever reason - changing their toolheads often. Upsides of this project compared to CAN: One cable does it all. Plug it in, it'll work. Well and of course its for people who think USB-C PowerDelivery is cool...<br/><br/>


![Konzept_V1 1](https://github.com/cad435/StealthburnerFullUSBPD/assets/16453385/a327e2c8-aeb2-4a48-b4ca-d89504ecc0b9)




Out of my latest Project (Voron 2.4 with toolchanger) I felt the need to simplify connecting Stealthburner-Toolheads to the printer. USB-C PowerDelivery seems suitable. Although it'll only provide 20V to the Toolhead instead of the 24V, it should be good enough.<br/>

I asked around at the Voron-Discord (May 2023), only to find out that there was an attempt by Mellow, but it was taken out of the market. So I sat down and created my own.<br/>

The Project consists of 2 Boards:
 - The "Feeder" PCB which basically integrates some step-Down converter and a USB-PD source IC's
 - The "Toolhead" PCB which consists of an MCU and the neccessary hardware to run fans, heaters, thermistors and the like. <br/><br/>

<p align="center">
 <img src="https://github.com/cad435/StealthburnerFullUSBPD/assets/16453385/4bae19de-991d-4e09-b4a6-d78c65856573" alt="drawing" width="400"/>
</p>
<br/><br/>
--> If you use a 4-port USB-Hub, use a half-decent one. I had bad experiences with the 3€ ultra-cheap hubs from Aliexpress, I'm running on a (cheap) Anker-Hub smoothly now. <br/>
<br/>

**Note** that I designed it to be used with 12V Fans (partly because I have loads of 12V Fans laying around). As you need all available airflow you can get, using 12V Fans with 12V seems a better Idea to me that using 24V fans with only 20V as this would mean loosing some power. If the interest is great enough I might add a stepup circuitry to provide 24V for the fans. I don't think its a good idea to step up heater-cartridge voltages as well, as this would mean I need to supply about 3A of current with a step up which generally will generate a considerable amout of heat (same goes for stepping down 20V to 12V). <br/>
<br/>

As of now, the PD power provider IC claim to use e-mark detection for the cables. <br/>
<br/>

Using 24V/40W heater cartridges with 20V will decrease power consumption to about 30W wich (I guess) should be enough for the standard Voron user (not enough though for High-Speed/High-Flow printing etc). That leaves 30W for the stepper-motors, fans etc. (should be plenty enough). Also there are higher power cartridges out there which'll increase power. <br/>
<br/>

**Comment on the Relay switching 5V AUX into the Powerpath:**<br/>
This is actually one of the biggest features of the board - another level of protection for avoiding damage to the printer and possibly other things.
If the heater switching-FET fails and shorts out (zero resistance, actually not uncommon on FET's), the cartridge would heat up indefinately until it fails, ignites or whatever it'll happen. Klipper can't do anything against it, because it will have no hardware controll over the FET and the Heater anymore.<br/>

UNLESS you have another switch to cut off the power - which comes in form of the FET Q1. It'll get switched off from klipper, as Klipper is able to disable the PD-Chip, therefore cutting power completely. However, we don't want to cut power completely, otherwise we can't talk to our MCU anymore an therefore would not be able to restart klipper. So the relay also switches, redirecting the powerpath around the PD-Chip from the "default" Stepdown (5V) to the toolhead. So we just "switch" power to another safe Level (5V). With 5V the heater doesn't have enough power to get seriously hot (I tested, it merely gets 50C hot).



Licensed under Open Source Hardware Association license https://www.oshwa.org/definition/
