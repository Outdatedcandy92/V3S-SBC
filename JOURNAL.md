# 2 October, 2025 - Initial Planning & Schematics  

Did a lot of initial planning and research today about the Allwinner V3S. I researched about a lot of SoCs but the V3s was my top choice due it having embedded DRAM and its availability on JLCPCB.

My plan with this project is to make my own SBC in a Raspberry Pi Zero form factor to learn about embedded linux. 

In addition to reading the V3s datasheet I also worked on researching ICs for my video output (the V3s does not have a HDMI PHY so I'll need a RGB to HDMI bridge), and an IC for wifi.

I also started working on its schematics today. So far I've only labeled and setup my power rails for the V3s
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTM1LCJwdXIiOiJibG9iX2lkIn19--efa0e1e3f304121f3930118ea33e82b2dc16f962/image.png)
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTM2LCJwdXIiOiJibG9iX2lkIn19--3ad72e337529938395a419ed88e164ce82d9ca71/image.png)


## Time Spent: 3 Hours
  

# 6 October, 2025 - Power and Peripherals  

Added a Buck Boost and a LDO to create the 4 voltage rails required for the V3S. 1.2v for core, 1.8v for DRAM, 3.0v and 3.3v for peripherals. 
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Nzc4LCJwdXIiOiJibG9iX2lkIn19--afb2fb2ec08349c86cc16f217b65f1cff8f6c136/image.png)


Also added up the low power and rtc crystal for the V3S. It took a while to find out the correct part for the crystals. I also added a SD Card on the SDIO Interface for boot.
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Nzc3LCJwdXIiOiJibG9iX2lkIn19--eef0281da22a29318d696a07b5059cb560386791/image.png)
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6NzgyLCJwdXIiOiJibG9iX2lkIn19--014fce70a09cd9980faa2263d9ff8ecbd199bd4a/image.png)
  

## Time Spent: 2 Hours


# 11 October, 2025 - More Peripherls + Layout  

I added ESD protection diodes on the SDIO lines for the SD card.
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTcxMSwicHVyIjoiYmxvYl9pZCJ9fQ==--dfe0f2968a646a64d4ce8a3752620669b0965d7f/image.png)

And I also spent probably like 2 hours trying to find an IC that I could use to integrate wifi on my board and so far I've had no luck. 
Realtek had a lot of cheap chips but had shit documentation which was very to understand, the rest of the chips were either not in stock on JLC or just straight up too big to fit on the board. So I decided to skip over wifi for now and I'll maybe come back and consider Realtek later.

I did however add the MIPI CSI header for interfacing cameras, I copied the pinout of the headers from the Raspberry Pis and I used the 15 pin version. Its a 1mm pitch right angle lower contact FPC connector.
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTcxMiwicHVyIjoiYmxvYl9pZCJ9fQ==--c975db478ac0ab843cc92bcd228599b7b26a9398/image.png)

I also did a little bit of PCB Layout just to see how everything goes together and so far its looking pretty packed. I'm not even sure if I'd be able to fit everything in this tiny space.

![image.png](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTcxMywicHVyIjoiYmxvYl9pZCJ9fQ==--061313d87165a605248495c4c0d70dde9511cf59/image.png)



## Time Spent: 5 Hours
  

# 15 October, 2025 - Finished Schematics (Almost)  

I did a lott of work since the last devlogs.
Here's a list of updates to the schematics
- Added SII9022ACNU which is used to convert the parallel RGB output from the V3s to HDMI
- Added a HDMI port (duh)
- Changed my CSI connector from a 15pin 1mm pitch to a 22pin 0.5mm pitch to save space
- Wired up an Ethernet Receptacle
- Sorted up and organized my schematic, neatly and nicely!

This is what the final schematic looks like!
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MjQyMSwicHVyIjoiYmxvYl9pZCJ9fQ==--5acd79fee05bddf8ecbe8b920a0d990263460bc8/image.png)
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MjQyMiwicHVyIjoiYmxvYl9pZCJ9fQ==--626ce8971b8e18884b92a656faba170dc53cf6d6/image.png)
![image.png](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MjQyMywicHVyIjoiYmxvYl9pZCJ9fQ==--c957be3ee42e7252e181df08a9f6a70661b1e0cd/image.png)

   
## Time Spent: 8 Hours


# 10/25/2025 - Did some off camera mining  

Well uhh as the title says I might have done some off camera mining :D I was slightly busy these past weeks and my work was mostly done in small chunks, but I locked in yesterday and today and spent the entire day working on the PCB and I have my first essential routing completed! (just missing gpio)

This is what my glorious board look like!

*front side*
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU3MCwicHVyIjoiYmxvYl9pZCJ9fQ==--5242b89b2d86e503334ef289e2fe85b752b45940/image.png)
*back side*
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU3MSwicHVyIjoiYmxvYl9pZCJ9fQ==--318523d2ed9583f2de778f895f00a30af44ef655/image.png)

And this is what my PCB looks like
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU3MiwicHVyIjoiYmxvYl9pZCJ9fQ==--74590d5630f5b2e77dee82a7dc44f2c0c4d2708e/image.png)


Instead of going over everything I'll just give you a rundown of the important stuff.

Firstly I switched over from a 4 layer board to a 6 layer board. I initially went with 4 layers just for the challenge, but very quickly realized upgrading to a 6 layer is basically a no brainer as theres only a ~$20 difference plus I get free capped vias and ENIG. Going 6 layers also gave me an additional plane that I could dedicate just for power and another plane just for signals.
The Stackup I went with was-
- SIG
- GND
- PWR
- SIG
- GND
- SIG

The most time consuming part of my board was definitely the routing out the power plane as I had around 7 different power rails (9 if you include the USB and its inrush limited output). Routing out a plane with 9 different rails was certainly not easy but it  was kinda fun and the results in the end were also amazing imo.

![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU3NywicHVyIjoiYmxvYl9pZCJ9fQ==--9f0beacffb056828909fe3a8906ebb57ecc1615e/image.png)

Honestly this could have been done with 4 power rails but the `SII9022ACNU` recommended that I filter out the power rail for it.

On the topic of the RGB to HDMI IC,routing out the parallel RGB signals was very fun and I think the end results look very pretty!
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU3OSwicHVyIjoiYmxvYl9pZCJ9fQ==--eaa8476f5d3e0cfa502eca8864fe9a6abc85ce7b/image.png)


Going back to power, finding a small Inductor for my PMIC was kinda hard. I had to make compromise DCR in order to get a smaller footprint for the inductor so it could actually fit on my board
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU4MCwicHVyIjoiYmxvYl9pZCJ9fQ==--d33368bb54cc43352120b4944fa52702c7f89d59/image.png)
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU4MSwicHVyIjoiYmxvYl9pZCJ9fQ==--0dac8d413caaa58d6a34412ff763045a1da8c157/image.png)

That's basically everything major I did so far. I'll just add a few more screenshots for fun here!
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU4MiwicHVyIjoiYmxvYl9pZCJ9fQ==--0b0970dbf0b257090b70ba25fcca03cd62c1fa11/image.png)
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU4MywicHVyIjoiYmxvYl9pZCJ9fQ==--d6c3d52a081c20b0e7c36c6948e28c2a4ff9b4bf/image.png)
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NTU4NCwicHVyIjoiYmxvYl9pZCJ9fQ==--455591569f358ebf94686df90a46f3c04180841a/image.png)

I'll most likely share my PCB in r/printedcircuitboard for feedback as I'm very confident that there are a few mistakes in my board that I'm not smart enough to catch right now



## Time Spent: 14 Hours
  

# 2 November, 2025 - Routed GPIO  

Finally routed up the GPIO and my PCB is basically finished now! All I need to do now is to just make a post on reddit and ask for feedback or improvements.

Anyways this is how my PCB looks now!
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NzgzMCwicHVyIjoiYmxvYl9pZCJ9fQ==--5417b7f1fbabe5275fbf5b493dc4a288bda5a06b/image.png)
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NzgzMSwicHVyIjoiYmxvYl9pZCJ9fQ==--6d1e891e03d7c3a32879b9c2bdf7b1f944ea8d20/image.png)
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6NzgzMiwicHVyIjoiYmxvYl9pZCJ9fQ==--e032da460ee0947ff7f55aba848e6b5dac97017d/image.png)

The V3s unfortunately does not have a lot of GPIO pins so I had to route out and connect my CSI signals to the GPIO and basically share them with the V3s and the GPIO.


## Time Spent: 4 Hours


# 9 November, 2025 - Fixed the PCB + BOM  

Made a reddit post last week, did not get a lot of feedback :sob: but the main feedback was about my CSI differential pairs being too close to each other and not having pairs length matched relative to the clock pair. I fixed both those issues by moving a few vias around and rerouting the CSI data lines.

![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6OTkwMSwicHVyIjoiYmxvYl9pZCJ9fQ==--1b248eb24f7f3d5cd36fa90a0fa8c280f269357e/image.png)

I also probably spent about an hour just assigning parts (i hated it) but in the end all my components finally have a JLC part assigned to them. Also taking a look at JLC, the PCB currently costs around $150 for 2 PCBA which is honestly good and cheaper than what I expected  

## Time Spent: 4 Hours

# 28 November, 2025 - Board Arrived!!

I finally got my board delivered today! I was pretty excited to test them out but also nervous because what if they didn't work.

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F1e3f84d5_image.png)

Before plugging in power I took my multimeter and probed all the various test points on the back to check for continuity and to check if any of them were shorted together, luckily I designed it correctly so nothing was wrong.

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F96994fcf_image.jpeg)

I plugged it into my laptop and expected a USB device or something to show up but nothing happened. At this point I figured I might be a bit cooked. So I took out my test probe and attached to boards UART interface. I hooked the UART pins up to a USB to UART board I had and connected it to my computer and then reconnected the board, expecting to see something on putty, but again nothing happened. 

*Recreation (I was too locked in when this was happening and forgot to take pictures)*

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2Ff0fa8a07_image.jpeg)



At this point I was kinda sweating, so I whipped out my multimeter and tested all the voltage rails. But the problem was that my multimeter was actually tweaking and not display accurate values at all, everything was skewed and offset. It displayed 5.4v instead of 5v and 3.6v instead of 3.3v and so on. The multimeter couldn't really be trusted but the rough values kinda aligned with the power rails.

I though it might just be my USB to UART adapter as it only worked when it was set on 5v mode and my V3S was 3v3, so I went ahead and used my raspberry pi pico as a USB to UART adapter but still no success.

I was pretty confused at this point, so I took my oscilloscope and debugged the board. I probed the power rails for noise but it all seemed alright. I then probed the clock signals because I thought that this was all caused by a failed clock but upon measuring I see that both the clocks are oscillating perfectly. I was kinda stumped at this point so as a last resort I hooked up my scope to the UART pins in hopes that I could notice something, upon plugging the board I did notice some quick activity on the scope and thought maybe it was a problem with my UART adapters so I spent some more time making sure my raspberry pi was working properly and spent more time in putty trying to receive something from the board. 

Long story short the activity I saw on the scope was likely just noise which I took as activity because I was desperate. I wasted a few hours on this. At first I thought that maybe my test points didn't have secure enough connections with the pads and so I soldered on some headers, but again no success. 

*Troubleshooting the Board*

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2Fc7757c76_image.jpeg)

If I remember correctly I think the board sometimes did show up as a unrecognized USB device. And the V3S by default starts up in USB FEL mode if no boot media is detected so I though maybe I should try and see that. I tried installing sunxi-tools and testing USB FEL but it showed no FEL devices on windows, I tried it on Linux too but had no success, heck I even tried using WSL but it didn't work.

At this point I was pretty lost and disappointed, I tested out both my assembled boards, soldered headers onto it, probed them and everything but still couldn't find why the board wasn't working.

But then I was just probing the voltage rails again when I noticed something that completely slipped by me. I saw that the 3.0v analog rail was outputting 3.3v , and it was at this moment that I knew where I f*cked up.

So I forgot to mention this in my last journal entry but on my reddit post one commenter recommend I should switch to a better LDO.

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2Fb594cc42_image.png)


And so I did switch the LP5907 last minute but what I didn't care to realize was that I accidentally selected the 3.3v output variant and not 3.0v.

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2Faea52a2d_image.png)

And this little mistake cooked me and wasted so much of my time, I pretty much spent my entire day trying to figure out why it wasn't working and I somehow overlooked the main reason. I don't know how I didn't realize my analog rail was outputting the wrong voltage.

I cannot tell you how relieved I was when I finally found the reason for my board my not working. I decided to wrap up for the day and hopefully work on fixing the board tomorrow.

## Time Spent: 6 Hours



# 29 November, 2025 - Trying To Fix The Board

Since I now knew that the reason for my board not working was due to incorrect voltage on the PLL and analog rails, I could try to externally feed the correct voltage and see if the board works.

I first started off my cutting off the LDO's output pin.

![img](https://cdn.2008000.xyz/cdn/23-01-2026%2F9fc5a3cd_20260123_145731.jpg)


And then on the back I soldered a wire onto the 3.0V test pad to inject the correct voltage and test it. Now unfortunately I did not have a variable PSU and I was pretty tired and decided to derive 3.0V from a voltage divider, which was a dumb idea because a voltage divider is a poor voltage source as the output voltage changes depending on the load resistance. So obviously the board still did not boot.
I did try and use my raspberry pico as a makeshift multimeter by using its ADC pins to detect and report average voltage, and I used this to check the voltage and fine tune my resistor divider based on the load.


![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F30c40b3a_image.jpeg)

Looking at the datasheet for the V3S and scrolling all the way down to the Electrical Characteristic of the chip, you can see that the max voltage for the PLL and analog rail is 3.3V, which probably meant that our SoC most likely got destroyed when we fed it 3.3v.

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F9bf185e8_image.png)


I decided to not further botch the board and just order a new pair of V3S and the correct LDO and manually replace them myself later on.

## Time Spent: 3 Hours


# 20 January, 2025 - Board Working!!!


I know it's been a while but I was waiting to bundle up my V3S and correct LDO with other parts from LCSC to save on shipping.

*Blurry ahh picture*

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F709706b7_image.jpeg)


I took my board and put it on a hotplate and replaced the old V3S and LDO with new parts.


*Reenactment (I was too locked in to take pictures when I was doing it)*

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2Fcdcb7854_image.jpeg)


But I wasn't done just yet, I had to touch up the soldering and fix any bridges. I wore my magnifying glasses and inspected the V3s pins, and say a lot of bridges.

I took my pinecil, put on a knife tip on it, and put a shit ton flux on the V3S pins and went ahead and fixed the solder bridges. 
The tip to fixing solder bridges is to start off from one end and glide your tip to the other end, and then cleaning your tip to ensure there's no solder on it. Doing this a few tips eventually clears up any bridges.

After fixing the solder bridges I was left with a ton of flux residue on my board and oh boy, it was painful to clean off, in fact there's still a ton of residue left on my board as I kind of gave up cleaning it.


I crossed my fingers and plugged in my board to my laptop and I hear the USB device connected sound on windows. I was super relieved as this meant my board was enumerating properly and actually working. I open up device manager and I see an unrecognized USB device.

*Reenactment* 

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F7232c9e8_image.png)

I used usbipd to basically attach this USB to WSL, and inside WSL I has sunxi-tools installed and I used lsusb and I saw the Allwinner SoC descriptor.

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F36bd5991_image.png)

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F66e6808f_image.png)

I was pretty relieved and called it a day. I'll work on installing the kernel on it when I finish my exams

## Time Spent: 2.5 Hours

# 23 January, 2025 - Mini Heart Attack

I was retroactively writing the journals today, and I wanted to get screenshots of the USB device in device manager and usbipd, so I plugged in my board and tried to recreate it but nothing showed up, no usb device was detected.

This freaked me out because there was absolutely nothing I changed on my board, so there should be no reason for it to not work when it was working 3 days ago. I looked at the voltage rails using my scope and sure enough everything seemed fine and correct.

I took my magnifying glasses and visually inspected everything and sure enough it seemed fine to. I tired connected it on my other laptop running linux and I see absolutely nothing when I run lsusb.

I looked through my scope on the data lines and I see no activity at all. I was pretty confused why it was not showing up as a USB device in FEL mode. There was no boot media present, no flash or sd card so it had to boot in FEL mode but it didn't?!


I decided the best way to debug would be to check UART, but I didn't have my flashed pico right now, so I decided to hook it up to my scope and see if there's any activity. Before doing that I decided to clean up my board a bit more, I sprayed some IPA and cleaned the gunk off with a toothbrush and Q-tips. After cleaning the board I went ahead and hooked it up to the scope and plugged it to my computer and then boom, I hear the USB device connected sound on windows, I was super relieved.

It finally showed up as a USB device on windows device manager and showed up in FEL mode when I checked in WSL.


![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F15cf9c4c_image.png)

![image](https://cdn.2008000.xyz/cdn/23-01-2026%2F3e82065e_image.png)

My guess is that a small piece of solder shorted something and by cleaning the board I might have removed the problem? that's my most plausible theory on what happened and why it happened.

## Time Spent: 2 Hours