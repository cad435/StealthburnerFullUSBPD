# StealthburnerFullUSBPD
Two PCB's to connect a Voron Stealthburner Toolhead via USB-PD providing both power and data.

This is aimed at people which are either having some kind of toolchanging system (like me) or are for whatever reason are changing their toolheads often. Upsides of this project compared to CAN: One cable does it all. Plug it in, it'll work. Well and of course its for people who think USB-C PowerDelivery is cool...


![Konzept_V1 1](https://github.com/cad435/StealthburnerFullUSBPD/assets/16453385/a327e2c8-aeb2-4a48-b4ca-d89504ecc0b9)




Out of my latest Project (Voron 2.4 with toolchanger) I felt the need to simplify connecting Stealthburner-Toolheads to the printer. USB-C PowerDelivery seems suitable. Although it'll only provide 20V to the Toolhead instead of the 24V, it should be good enough.

I asked around at the Voron-Discord (May 2023), only to find out that there was an attempt by Mellow, but it was taken out of the market. So I sat down and created my own.

The Project consists of 2 Boards:
 - The "Feeder" PCB which basically integrates a 4-Port USB 2.0 Hub, some step-Down converter and USB-PD source frontend IC's
   -> The USB2.0 Hub was removed in later revisions, as it was to unreliable.
 - The "Toolhead" PCB which consists of an MCU and the neccessary hardware to run fans, heaters, thermistors and the like. 


Note that I designed it to be used with 12V Fans (partly because I have loads of 12V Fans laying around). As you need all available airflow you can get, using 12V Fans with 12V seems a better Idea to me that using 24V fans with only 20V as this would mean loosing some power. If the interest is great enough I might add a stepup circuitry to provide 24V for the fans. I don't think its a good idea to step up heater-cartridge voltages as well, as this would mean I need to supply about 3A of current with a step up which generally will generate a considerable amout of heat (same goes for stepping down 20V to 12V). 

Right now I'm planning on using standard "non e-marked" USB-C cables which will result up to 60W of power which can be used in the toolhead (Feeder PCB can already provide 100W!). I'm not sure if the used PD-Source and Sink frondends are capable of using the 100W e-marked cables. Thats something which I have to try out.


Using 24V/40W heater cartridges with 20V will decrease power consumption to about 30W wich (I guess) should be enough for the standard Voron user (not enough though for High-Speed/High-Flow printing etc). That leaves 30W for the stepper-motors, fans etc. (should be plenty enough)


anyways, it's worth a try, this is ongoing, I'll push updates whenever I have time :)


Licensed under Open Source Hardware Association license https://www.oshwa.org/definition/

___

**Update 2023-06-08:** It seems like nothing is watching if you are limiting yourself to 60W (e.g. 3A@20V) which means you can use up to 100W power over a "standard" non-marked Cable. Might add a 5A fuse in the future. **USE PROPER CABLES** for now.

**Update 2023-07-19:** The IP2701 I'm using in the Power-Feeder board will not work. Unfortunately I missinterpreted the datasheet: this chip talks a bunch of protocols at the USB2.0 D+/D- datalines (for example QC2.0/3.0) as well as USB Type-C Power-Protocol over the USB-C CC-Lines which is 5V@3A. Unfortunately it will NOT talk USB-PD over the CC-lines. We do **NOT** want to use a protocoll like  QC2.0/3.0 as it'll use the USB 2.0 D+/D- lines, wich we need for communication. I already ordered some new chips (TPS25740BRGET) but that means I need to redo the PCB (Also that TPS25740 is already NRND albeit in active production which bothers me a bit). 

Alternatives are rare, as I try to find IC's which are not overly complicated and requires loads of loads of external components. I suspect more IC's of manufacturers like INJOINIC or WCH to slowly get those "one in a package" IC's for PD.


Possible Candidates:
+ IP5389 which essentially combines the Buck converter and PD-source into one IC (but those chips are only available on taobao, seems like INJOINIC - for some unknown reason - successfully prevented them to reach European & USA market)
+ IP2716.


**Update 2023-09-22:**
After a lot of debugging, one is working completely - The toolhead itself. The Gerbers I have are usable on first try. However some improvements were made for the next version.

The feeder presents itself pretty challenging. The FE1.1 used as a USB-Hub on that board is turning itself off when current for heating is drawn - I have no Idea why, but I suspect an EMI-Problem. Also, I recently learned, that with my setup, the store-bought USB-Hub (which also utilizes a FE1.1) have its trouble with klipper. For everything else it works fine. 
Therefore I made the decision to completely omit the on-board USB-Hub and make a single "Power-Infuser" board. It will take a single USB-Signal as well as 24V Power in and will provide USB2.0 Data and PD on the other side. No integrated hub. The Diagram is updated. In that version I'll try my best to integrate proper EMI-Shielding to the downstream USB-Hub.
