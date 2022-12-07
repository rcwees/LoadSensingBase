# Overview
This is a modification/revision/update to the Jflyer F-16 Grip on thingiverse. in thise design i took his model and changed it and modified it to fit onto a 2020 extrusion. i then used The open Viper Hotas V2 By Bacon8tor on thingiverse, which took the original Jflyer81 model and added pcb support so you dont have to wire every wire to each button, and rather just use 5 Pos Navigation Switches From ada fruit. i created my own base that uses loadcells to measure your force applied vs ange of motion. this is realistic to the actual jet as that f-16 has a force sensing stick rather than that of a F-15 which measure where your stick is using hall effect sensors. below i will list the things i used, the code produced during this project, the issues, the versions, and everything i have used to get started.
# Parts made
## The Grip
To make the grip i used the Open Viper Hotas V2 By Bacon8tor. this is a remix of the original grip by Jflyer81 but this one has support for pcb such that you use Adafruits 5 way Thru Hole navigational switch. this means there is less soldering, 3D Printing, And effort in making this. everything went smoothely for me, but it depends on your printer. the pcbs were the tricky part, you have to order them from PCB Way or Any company that can manufactur pcbs. they take about 2 weeks to get here, and come fully assembled. they costed $20 and you get two sets of them depending on where you order them from. After all this it should go together realy well. links to all products are in the description.
## The Base
the base was probably the most tricky part. it went through many iterations, some worked some failed, but i learned from them all. the first design used traditionaly wheatstone bridge loadcells, like these seen here




<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRwDXsmqYrnBvKlI4qTI3hgRt6SoX7Hc7H-qO6vfch9yXgBGuoxTyWAQO0D7l3JEMmTnhs:https://www.phidgets.com/productfiles/3135/3135_0/Images/3150x-/0/3135_0.jpg&amp;usqp=CAU" alt="Micro Load Cell (0-50kg) - 3135_0 at Phidgets"/>
these worked well, but they had their issues, like mounting them to a metal plate, you had to buy extra brass standoffs, you needed 2020 extrusion 90 Degree corner mounts etc. it was just innefficient and it ended up being very flimsy and now sturdy. that where these loadcells came in:
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTb2MgdJkO08hu76myKwEDyZmaogyTvwIoWKg:cdn.shopify.com/s/files/1/0559/1970/6265/products/1_f1b14fe3-3905-4217-b2a7-2311fb62a2b5.jpg%3Fv%3D1669816302&amp;usqp=CAU" alt="Buy 50 kg Load cell Online in India | Robocraze"/>
which work much much better, as the force is being distrubuted down intot he metal plate, rather than these brass standoffs. then i used HX711 Loadcell Amplifiers that were distributed by Sparkfun. these work great adn were really easy to use. 

# Other Details

## Buying Guide
1) [Loadcells](https://www.amazon.com/Weighing-Resistance-Half-Bridge-Amplifier-Arduino/dp/B097T3SX6W/ref=sr_1_4?keywords=load+sensors&qid=1670266200&sr=8-4) $12.99
    - those come with HX711s which might work for you but they arent able to be put into 80 Hz Mode so they might appear slow to some people. they come extra at no cost so its no problem.
2) [HX711](https://www.sparkfun.com/products/13879) you need 2 (My Choice) $10.95
3) [M4 Bolts](https://www.amazon.com/HELIFOUNER-Pieces-Button-Washers-Stainless/dp/B09GRHHXT5/ref=sr_1_3?keywords=m4+bolts&qid=1670266352&sr=8-3) (if you dont already have them)$11.99
4) [Hose O-Ring](https://www.amazon.com/PAGOW-Rings-Pressure-Connect-Coupler/dp/B07RZBHSNG/ref=sr_1_8?crid=1SM57JTUYDIQQ&keywords=hose+O+ring&qid=1670266422&sprefix=hose+o+rin%2Caps%2C160&sr=8-8) (random but used to creat movement in the stick. without it, you cant feel the sticks position at all) $6.99
5) [Teensy Board 4.0](https://www.pjrc.com/store/teensy40.html) (Controller of it all) $23.8
    - the alternative to this is the arduino pro micro as they are much much easier to get, and to distribute. they are cheaper and look better for most people but what i found is the faster teensy 4.0 performs better as it can update the inputs faster. meaning the stick doesnt have a delay. arduinos can be bought [here](https://www.amazon.com/OSOYOO-ATmega32U4-arduino-Leonardo-ATmega328/dp/B012FOV17O) if needed.
# Code
- the code will be placed in the top of the Repo, i will attatch multiple files. look here to refrence what code you need
    - HX711_Basic_Example: this is used to test if your loadcells are registering. i used this to test my wiring before i permanently attatched everything. all you need for this sketch is to change the pins for what you attatched your hx711 to. if your HX711 Data is to pin 2 and CLK is to pin 3 then set those variables in the sketch. after this you can load it onto the teensy board, and see in the serial print the numbers. their gonna be in the thousands, its just a raw number so dont worry about the values. this is just to test that the numbers show up or move. if the serial moniter shows "HX711 Not Found" then you have a wiring issue. make sure the hx711 VCC and VDD are bridged on the hx711 and that the hx711 is getting 5v not 3v.
    - HX711_Joystick_Example: this is to test that your stick is registering as a joystick. make sure your teensy board is set to "Keyboard Mouse Serial Joystick" in the tools menu, and upload the sketch, making sure the pins are corresponding to each Data And CLK on the HX711s. then in the bottom of your computer search in the search bar "joy.cpl" from there you should be able to see the "keyboard Mouse Serial Joystick" in that menu. click on it, and select properties. then Calibrate. follow that manu and you should be able to see the joysticks registering.
    - Grip_Mux_Example: this sketch is to test the multiplexors, and that their working. wire the multiplexors up to the board, and change the values in the sketch so that they are correctly corresponding. then upload the sketch and you should see in the serial moniter a ton of Zeros. when you press one of the button, a 1 will switch into the place of the Zeros. test that this happens for every switch. once this is done, your stick is fully functional. you just have to peice it together
    - Joy_Final: this is the final sketch combining all of the Multiplexors and the HX711s. 
## Sources
- Real Cool Visualization of what im [doing](https://www.youtube.com/watch?v=0AL7oeH1EnU)
- Very First Design i Based off [of](https://forum.dcs.world/topic/289020-force-sense-stickdiy/)
- Open V2 3D Print [Thingiverse](
