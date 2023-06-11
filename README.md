# StealthburnerFullUSBPD
Two PCB's to connect a Voron Stealthburner Toolhead via USB-PD providing both power and data.

This is aimed at people which are either having some kind of toolchanging system (like me) or are for whatever reason are changing their toolheads often. Upsides of this project compared to CAN: One cable does it all. Plug it in, it'll work. Well and of course people who think USB-C is cool...

![Konzept](https://github.com/cad435/StealthburnerFullUSBPD/assets/16453385/6de83345-7aa8-42fd-a45c-025c5a4657a1)

Out of my latest Project (Voron 2.4 with toolchanger) I felt the need to simplify connecting Stealthburner-Toolheads to the printer. USB-C PowerDelivery seems suitable. Although it'll only provide 20V to the Toolhead instead of the 24V, it should be good enough.

I asked around at the Voron-Discord (May 2023), only to find out that there was an attempt by Mellow, but it was taken out of the market. So I sat down and created my own.

The Project consists of 2 Boards:
 - The "Feeder" PCB which basically integrates a 4-Port USB 2.0 Hub, some step-Down converter and USB-PD source frontend IC's
 - The "Toolhead" PCB which consists of an MCU and the neccessary hardware to run fans, heaters, thermistors and the like. 


Note that I designed it to be used with 12V Fans (partly because I have loads of 12V Fans laying around). As you need all available airflow you can get, using 12V Fans with 12V seems a better Idea to me that using 24V fans with only 20V as this would mean loosing some power. If the interest is great enough I might add a stepup circuitry to provide 24V for the fans. I don't think its a good idea to step up heater-cartridge voltages as well, as this would mean I need to supply about 3A of current with a step up which generally will generate a considerable amout of heat (same goes for stepping down 20V to 12V). 

Right now I'm planning on using standard "non e-marked" USB-C cables which will result up to 60W of power which can be used in the toolhead (Feeder PCB can already provide 100W!). I'm not sure if the used PD-Source and Sink frondends are capable of using the 100W e-marked cables. Thats something which I have to try out.

**Update:** It seems like nothing is watching if you are limiting yourself to 60W (e.g. 3A@20V) which means you can use up to 100W power over a "standard" non-marked Cable. Might add a 5A fuse in the future. **USE PROPER CABLES** for now.

Using 24V/40W heater cartridges with 20V will decrease power consumption to about 30W wich (I guess) should be enough for the standard Voron user (not enough though for High-Speed/High-Flow printing etc). That leaves 30W for the stepper-motors, fans etc. (should be plenty enough)


anyways, it's worth a try, this is ongoing, I'll push updates whenever I have time :)


Licensed under Open Source Hardware Association license https://www.oshwa.org/definition/
