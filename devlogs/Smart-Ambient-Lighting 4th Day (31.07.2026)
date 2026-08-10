Today's research will be the remaining component research. After doing these, if I have enough time, I will also do the necessary analyses, and I want to write a very detailed and complete report about the analyses, so I will get help from AI. Afterward, I will write a test code for an initial demo structure and to speed up the process—just a code running at max usage that will turn the PWM on and off as much as its power allows per second. Then, using a simulation (first I need to find the right simulation), I will do thermal tests and similar tests to see if there is a heating problem, a short circuit, or a problem in the program or on the PCB. After passing the circuit test, I can finally start the real project. I don't know how long this process will take, but after finishing the research phase, I will write and program the code on an online ESP sim. After that, I will design the PCB and put them all into a program where I can simulate them together. Once the tests there are also successful, I will then design a case on Fusion 360 and move on to the assembly phase.

Alright, plans changed. Learning thermal test sims would take months; I found this out in a brief research. So the plan will be like this:
Component research -> Doing necessary analyses (SWOT-PEST, etc.) -> ESP code writing -> Breadboard test once necessary parts arrive -> Thermal tests -> PCB design -> Case design ->
AI recommendation, things not to forget:
- 1000µF (35V or higher) Electrolytic Capacitor
- 330 Ohm Resistor
- 10K Ohm Resistor
- TO-220 Aluminum Mosfet Heatsink
- 2-Pin and 3-Pin Screw Terminals
- Female Header Sockets
- 18 AWG Thick Copper Wire
- Jumper Wires
- Perfboard (For the initial test board)
**Things to Remember (Cyprus / Closed Box Conditions):**

- PLA will definitely not be used in the 3D printing of the box (PETG or ABS will be used).
- Ventilation grilles will be opened on the top and bottom surfaces of the box for passive airflow (chimney effect).
- The Mosfet will definitely not be used without a heatsink (naked).

Right now I'm looking for a converter for 24V 5A. Since running it at full power could be an issue, I will buy a 24V 10A adapter. As for the case type, AI recommends SMPS, but if the cost difference is huge, I don't think getting a normal plastic case would be a problem. Important datasheet values = SCP (short circuit protection), OTP (over-temperature protection: cuts power instead of burning), OVP (over-voltage protection).
As for the brand, it recommends Mean Well, but I don't know, if it's too expensive I can't buy it anyway. The brand I found is Mervesan Power 10A 24V 250W Metal Case Indoor Ac/Dc Smps Adapter MRW-250-24-S. I didn't quite understand this, couldn't find a datasheet either, but I learned this: that 10W excess is because it has a screw inside to increase V, and it says we can increase it up to 25V. Next is the 24-5V regulator. For the regulator, the first important thing is the architecture part. There are 2 different types: 1st is linear, 2nd is called DC-DC converter/Step-Down.

A linear one acts like a smart resistor, converts 24V to 5V, but 19V comes out as heat.
A DC-DC, on the other hand, opens and closes the current thousands of times a second like a PWM signal, keeping it stable at 5V. There is very little heating in between, and according to the information I got (AI), it has up to 90% efficiency. In this case, we use DC/DC. The other important value is the input voltage. The 24V adapter might give more V due to fluctuations, so the max input voltage must be at least 28-29V so it doesn't burn.
The other important thing is the output voltage. Here two options come up: either 5V fixed or adjustable. Since I don't want to take risks, I'll choose Fixed (but to be able to do tests for future projects, buying an adjustable one also seems logical, I'll think about it). The 3rd value is the output current. The ESP32 server + I2C will draw a certain current, so it should be min 1 amp, but just in case, I think we can find 1.5 or 2 amps. The one I found is "https://www.direnc.net/lm2596s-usb-voltaj-dusurucu-6-40-giris-5v-3a-cikis"
its info:

LM2596S Usb Voltage Step-Down

---
- Input voltage: DC 6v-40v
- Output voltage: DC 5v
- Output Current: 3A (Maximum)
- Type: LM2596S usb voltage step-down
- Conversion Efficiency: 92% (Highest)
- Switching Frequency: 150KHz
- Weight: 17gr
- Operating temperature: -40°C - +85°C
- Size: 50mm X 35mm X 12mm

Next is fuse selection. There are critical points here. First is where it will be connected. It needs to be connected right after the power supply; it will be connected right at the output of the +24V. Next is the correct fuse selection. There are 2 types: 1st is glass, 2nd is blade fuse. A glass fuse is light and fragile, but it's easy to tell when it burns—the thin wire inside leaves soot anyway when it burns. However, there is a risk of breaking, and if too much load passes, it can explode suddenly, and I could break it while plugging/unplugging. The other one, the blade type, is very sturdy and has international color codes; plugging/unplugging is very easy and it doesn't break. But it's a bit hard to tell when it burns; you have to look through the tiny hole inside to understand. But if the lights suddenly go out, I know where to look. Therefore, I will choose a blade fuse. And again, I will add a 20% tolerance, because if it burns at 5A, since we are already using 5A, it will burn immediately as soon as we plug it in, which we don't want. Also, to be able to plug the fuse in properly, I need a socket/holder. I didn't feel the need to put the link for it, but a 7.5V fuse will do the job for me.
That's all for now.
