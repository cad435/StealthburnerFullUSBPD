Update 2024-10-05: I accidentlly left R7 and R8 as 100R series resistance for the USB-Lines. This seemes to be working good for my main Printer <br>
For another setup however, I encountered problems. After a while I found 100R to be too much resistance. Therefore I replaced it with 0R default. <br>
If you find yourself to have random disconnects I advice you to increase those values (20R should be enough!) <br>
However I believe that the 2.2kR@100Mhz Common-Mode chocke (FL1) should be more than enough. <br> <br>


I found it working with all the Ferrite beads (L1/L4/L5) beeing only ~300R@100Mhz, as well as the common-mode choke beeing just ~600R@100Mhz. <br> <br>

Use two M2 brass inserts on the 2 holes beside the USB-C Connector. <br> <br>

![2024-05-16-00-29-13-719](https://github.com/cad435/StealthburnerFullUSBPD/assets/16453385/809f11b5-40af-4fe9-a6dc-24aade0a903b)

The holes where the "unknurled" shoulder is fitted is 3.1mm in diameter 
Brass inserts I used are sold as "OD=3.5mm, Lenght=3mm". The critical measurement is denoted as "dk" in the picture below.

![image](https://github.com/cad435/StealthburnerFullUSBPD/assets/16453385/aa13ce6a-dc5a-4a47-8c9e-2a4b785ed0c6)

