# 2 October, 2025 - Initial Planning & Schematics  

Did a lot of initial planning and research today about the Allwinner V3S. I researched about a lot of SoCs but the V3s was my top choice due it having embedded DRAM and its availability on JLCPCB.

My plan with this project is to make my own SBC in a Raspberry Pi Zero form factor to learn about embedded linux. 

In addition to reading the V3s datasheet I also worked on researching ICs for my video output (the V3s does not have a HDMI PHY so I'll need a RGB to HDMI bridge), and an IC for wifi.

I also started working on its schematics today. So far I've only labeled and setup my power rails for the V3s
![image.png](../attachments/image-1774026500469-0rt1n09p0.png)
![image.png](../attachments/image-1774026500486-3v2ubhjdj.png)


## Time Spent: 3 Hours
  

# 6 October, 2025 - Power and Peripherals  

Added a Buck Boost and a LDO to create the 4 voltage rails required for the V3S. 1.2v for core, 1.8v for DRAM, 3.0v and 3.3v for peripherals. 
![image.png](../attachments/image-1774026500498-3g9ql54fq.png)


Also added up the low power and rtc crystal for the V3S. It took a while to find out the correct part for the crystals. I also added a SD Card on the SDIO Interface for boot.
![image.png](../attachments/image-1774026500521-r7t4j63sp.png)
![image.png](../attachments/image-1774026500532-7kjvfelmv.png)
  

## Time Spent: 2 Hours


# 11 October, 2025 - More Peripherls + Layout  

I added ESD protection diodes on the SDIO lines for the SD card.
![image.png](../attachments/image-1774026500549-jqxvsb0fl.png)

And I also spent probably like 2 hours trying to find an IC that I could use to integrate wifi on my board and so far I've had no luck. 
Realtek had a lot of cheap chips but had shit documentation which was very to understand, the rest of the chips were either not in stock on JLC or just straight up too big to fit on the board. So I decided to skip over wifi for now and I'll maybe come back and consider Realtek later.

I did however add the MIPI CSI header for interfacing cameras, I copied the pinout of the headers from the Raspberry Pis and I used the 15 pin version. Its a 1mm pitch right angle lower contact FPC connector.
![image.png](../attachments/image-1774026500561-mmpswanhy.png)

I also did a little bit of PCB Layout just to see how everything goes together and so far its looking pretty packed. I'm not even sure if I'd be able to fit everything in this tiny space.

![image.png](../attachments/image-1774026501081-64xxkup71.png)



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
![image.png](../attachments/image-1774026501634-8g70xw068.png)
![image.png](../attachments/image-1774026502156-5kwmfedcn.png)
![image.png](../attachments/image-1774026502650-apjlscat3.png)

   
## Time Spent: 8 Hours


# 10/25/2025 - Did some off camera mining  

Well uhh as the title says I might have done some off camera mining :D I was slightly busy these past weeks and my work was mostly done in small chunks, but I locked in yesterday and today and spent the entire day working on the PCB and I have my first essential routing completed! (just missing gpio)

This is what my glorious board look like!

*front side*
![image](../attachments/image-1774026503281-4baiu9c8f.png)
*back side*
![image](../attachments/image-1774026504051-rs25kps7s.png)

And this is what my PCB looks like
![image](../attachments/image-1774026504591-v19p9r2q7.png)


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

![image](../attachments/image-1774026505051-nqxc4214q.png)

Honestly this could have been done with 4 power rails but the `SII9022ACNU` recommended that I filter out the power rail for it.

On the topic of the RGB to HDMI IC,routing out the parallel RGB signals was very fun and I think the end results look very pretty!
![image](../attachments/image-1774026505545-voi4zy943.png)


Going back to power, finding a small Inductor for my PMIC was kinda hard. I had to make compromise DCR in order to get a smaller footprint for the inductor so it could actually fit on my board
![image](../attachments/image-1774026506240-5dis1nz5d.png)
![image](../attachments/image-1774026506756-5d04udzwk.png)

That's basically everything major I did so far. I'll just add a few more screenshots for fun here!
![image](../attachments/image-1774026507172-ij95lrf6r.png)
![image](../attachments/image-1774026507727-290jzkkno.png)
![image](../attachments/image-1774026508410-5zkzmgwfe.png)

I'll most likely share my PCB in r/printedcircuitboard for feedback as I'm very confident that there are a few mistakes in my board that I'm not smart enough to catch right now



## Time Spent: 14 Hours
  

# 2 November, 2025 - Routed GPIO  

Finally routed up the GPIO and my PCB is basically finished now! All I need to do now is to just make a post on reddit and ask for feedback or improvements.

Anyways this is how my PCB looks now!
![image](../attachments/image-1774026508981-s6c759an3.png)
![image](../attachments/image-1774026509544-nhj8ccf52.png)
![image](../attachments/image-1774026510096-n4awb6d1o.png)

The V3s unfortunately does not have a lot of GPIO pins so I had to route out and connect my CSI signals to the GPIO and basically share them with the V3s and the GPIO.


## Time Spent: 4 Hours


# 9 November, 2025 - Fixed the PCB + BOM  

Made a reddit post last week, did not get a lot of feedback :sob: but the main feedback was about my CSI differential pairs being too close to each other and not having pairs length matched relative to the clock pair. I fixed both those issues by moving a few vias around and rerouting the CSI data lines.

![image](../attachments/image-1774026510604-5qrkpcqj7.png)

I also probably spent about an hour just assigning parts (i hated it) but in the end all my components finally have a JLC part assigned to them. Also taking a look at JLC, the PCB currently costs around $150 for 2 PCBA which is honestly good and cheaper than what I expected  

## Time Spent: 4 Hours

# 28 November, 2025 - Board Arrived!!

I finally got my board delivered today! I was pretty excited to test them out but also nervous because what if they didn't work.

![image](../attachments/image-1774026510930-y1lrbw981.png)

Before plugging in power I took my multimeter and probed all the various test points on the back to check for continuity and to check if any of them were shorted together, luckily I designed it correctly so nothing was wrong.

![image](../attachments/image-1774026511013-8npt5yo5a.jpeg)

I plugged it into my laptop and expected a USB device or something to show up but nothing happened. At this point I figured I might be a bit cooked. So I took out my test probe and attached to boards UART interface. I hooked the UART pins up to a USB to UART board I had and connected it to my computer and then reconnected the board, expecting to see something on putty, but again nothing happened. 

*Recreation (I was too locked in when this was happening and forgot to take pictures)*

![image](../attachments/image-1774026511097-pvc69t2nd.jpeg)



At this point I was kinda sweating, so I whipped out my multimeter and tested all the voltage rails. But the problem was that my multimeter was actually tweaking and not display accurate values at all, everything was skewed and offset. It displayed 5.4v instead of 5v and 3.6v instead of 3.3v and so on. The multimeter couldn't really be trusted but the rough values kinda aligned with the power rails.

I though it might just be my USB to UART adapter as it only worked when it was set on 5v mode and my V3S was 3v3, so I went ahead and used my raspberry pi pico as a USB to UART adapter but still no success.

I was pretty confused at this point, so I took my oscilloscope and debugged the board. I probed the power rails for noise but it all seemed alright. I then probed the clock signals because I thought that this was all caused by a failed clock but upon measuring I see that both the clocks are oscillating perfectly. I was kinda stumped at this point so as a last resort I hooked up my scope to the UART pins in hopes that I could notice something, upon plugging the board I did notice some quick activity on the scope and thought maybe it was a problem with my UART adapters so I spent some more time making sure my raspberry pi was working properly and spent more time in putty trying to receive something from the board. 

Long story short the activity I saw on the scope was likely just noise which I took as activity because I was desperate. I wasted a few hours on this. At first I thought that maybe my test points didn't have secure enough connections with the pads and so I soldered on some headers, but again no success. 

*Troubleshooting the Board*

![image](../attachments/image-1774026511182-35yimvutw.jpeg)

If I remember correctly I think the board sometimes did show up as a unrecognized USB device. And the V3S by default starts up in USB FEL mode if no boot media is detected so I though maybe I should try and see that. I tried installing sunxi-tools and testing USB FEL but it showed no FEL devices on windows, I tried it on Linux too but had no success, heck I even tried using WSL but it didn't work.

At this point I was pretty lost and disappointed, I tested out both my assembled boards, soldered headers onto it, probed them and everything but still couldn't find why the board wasn't working.

But then I was just probing the voltage rails again when I noticed something that completely slipped by me. I saw that the 3.0v analog rail was outputting 3.3v , and it was at this moment that I knew where I f*cked up.

So I forgot to mention this in my last journal entry but on my reddit post one commenter recommend I should switch to a better LDO.

![image](../attachments/image-1774026511230-mldkbckjv.png)


And so I did switch the LP5907 last minute but what I didn't care to realize was that I accidentally selected the 3.3v output variant and not 3.0v.

![image](../attachments/image-1774026511272-6j1bd629g.png)

And this little mistake cooked me and wasted so much of my time, I pretty much spent my entire day trying to figure out why it wasn't working and I somehow overlooked the main reason. I don't know how I didn't realize my analog rail was outputting the wrong voltage.

I cannot tell you how relieved I was when I finally found the reason for my board my not working. I decided to wrap up for the day and hopefully work on fixing the board tomorrow.

## Time Spent: 6 Hours



# 29 November, 2025 - Trying To Fix The Board

Since I now knew that the reason for my board not working was due to incorrect voltage on the PLL and analog rails, I could try to externally feed the correct voltage and see if the board works.

I first started off my cutting off the LDO's output pin.

![img](../attachments/image-1774026511369-uybyaq3ka.jpg)


And then on the back I soldered a wire onto the 3.0V test pad to inject the correct voltage and test it. Now unfortunately I did not have a variable PSU and I was pretty tired and decided to derive 3.0V from a voltage divider, which was a dumb idea because a voltage divider is a poor voltage source as the output voltage changes depending on the load resistance. So obviously the board still did not boot.
I did try and use my raspberry pico as a makeshift multimeter by using its ADC pins to detect and report average voltage, and I used this to check the voltage and fine tune my resistor divider based on the load.


![image](../attachments/image-1774026511470-mhd85gvur.jpeg)

Looking at the datasheet for the V3S and scrolling all the way down to the Electrical Characteristic of the chip, you can see that the max voltage for the PLL and analog rail is 3.3V, which probably meant that our SoC most likely got destroyed when we fed it 3.3v.

![image](../attachments/image-1774026511513-rp4kp2gtn.png)


I decided to not further botch the board and just order a new pair of V3S and the correct LDO and manually replace them myself later on.

## Time Spent: 3 Hours


# 20 January, 2026 - Board Working!!!


I know it's been a while but I was waiting to bundle up my V3S and correct LDO with other parts from LCSC to save on shipping.

*Blurry ahh picture*

![image](../attachments/image-1774026511603-vtuf9co9x.jpeg)


I took my board and put it on a hotplate and replaced the old V3S and LDO with new parts.


*Reenactment (I was too locked in to take pictures when I was doing it)*

![image](../attachments/image-1774026511684-nzzhutqh9.jpeg)


But I wasn't done just yet, I had to touch up the soldering and fix any bridges. I wore my magnifying glasses and inspected the V3s pins, and say a lot of bridges.

I took my pinecil, put on a knife tip on it, and put a shit ton flux on the V3S pins and went ahead and fixed the solder bridges. 
The tip to fixing solder bridges is to start off from one end and glide your tip to the other end, and then cleaning your tip to ensure there's no solder on it. Doing this a few tips eventually clears up any bridges.

After fixing the solder bridges I was left with a ton of flux residue on my board and oh boy, it was painful to clean off, in fact there's still a ton of residue left on my board as I kind of gave up cleaning it.


I crossed my fingers and plugged in my board to my laptop and I hear the USB device connected sound on windows. I was super relieved as this meant my board was enumerating properly and actually working. I open up device manager and I see an unrecognized USB device.

*Reenactment* 

![image](../attachments/image-1774026511733-fwumn00ui.png)

I used usbipd to basically attach this USB to WSL, and inside WSL I has sunxi-tools installed and I used lsusb and I saw the Allwinner SoC descriptor.

![image](../attachments/image-1774026511791-sbjejyyv0.png)

![image](../attachments/image-1774026511832-idxgylylg.png)

I was pretty relieved and called it a day. I'll work on installing the kernel on it when I finish my exams

## Time Spent: 2.5 Hours

# 23 January, 2026 - Mini Heart Attack

I was retroactively writing the journals today, and I wanted to get screenshots of the USB device in device manager and usbipd, so I plugged in my board and tried to recreate it but nothing showed up, no usb device was detected.

This freaked me out because there was absolutely nothing I changed on my board, so there should be no reason for it to not work when it was working 3 days ago. I looked at the voltage rails using my scope and sure enough everything seemed fine and correct.

I took my magnifying glasses and visually inspected everything and sure enough it seemed fine to. I tired connected it on my other laptop running linux and I see absolutely nothing when I run lsusb.

I looked through my scope on the data lines and I see no activity at all. I was pretty confused why it was not showing up as a USB device in FEL mode. There was no boot media present, no flash or sd card so it had to boot in FEL mode but it didn't?!


I decided the best way to debug would be to check UART, but I didn't have my flashed pico right now, so I decided to hook it up to my scope and see if there's any activity. Before doing that I decided to clean up my board a bit more, I sprayed some IPA and cleaned the gunk off with a toothbrush and Q-tips. After cleaning the board I went ahead and hooked it up to the scope and plugged it to my computer and then boom, I hear the USB device connected sound on windows, I was super relieved.

It finally showed up as a USB device on windows device manager and showed up in FEL mode when I checked in WSL.


![image](../attachments/image-1774026511873-j3yzvc8ck.png)

![image](../attachments/image-1774026511919-k94maa5fq.png)

My guess is that a small piece of solder shorted something and by cleaning the board I might have removed the problem? that's my most plausible theory on what happened and why it happened.

## Time Spent: 2 Hours

# 28 January, 2026 - U-Boot

I have zero prior experience in embedded linux bringup so this was pretty tough for me. I was basically lost and had no idea where to start from. But luckily I few people made blog posts on how they bringup their V3s boards and so I referred to them and google for general help.

Here are some helpful articles/blogs I used.

- [Lichee Zero u-boot Getting Started!](https://hackaday.io/project/171402-lichee-zero-u-boot-getting-started)
- [Bringup V3s in 3 hours](https://blog.yuuta.moe/2024/10/30/v3s-in-3hrs/)
- [Lichee Pi Zero](https://licheepizero.us/)

The Lichee Pi Zero is a very popular SBC that uses the V3S SoC, so it was relatively easy to get setup and start with building a u-boot file. I followed the [Lichee Zero u-boot Getting Started!](https://hackaday.io/project/171402-lichee-zero-u-boot-getting-started) guide for most of this.


![image](../attachments/image-1774026512002-53oopv7qb.jpeg)



I did run into a brick wall when trying to build the image as I kept getting this error

![image](../attachments/image-1774026512049-z82squkiv.png)

This was pretty frustrating as I couldn't really find why this was going on and why armv5 was the target when it was specified as armv7 everywhere, after a bit of back and forth with perplexity. It just suggested I use `sed -i 's/-march=armv5/-march=armv7-a/g' ./arch/arm/Makefile` to search and replace the bad armv5 flag and it worked. However there was now another error where `binman` couldn't be found and it turns out it was because it depended on python 2 which was an easy fix.

After a few more errors and debugging sessions with perplexity I finally successfully complied the u-boot file and used sunxi-fel to load the SPL into RAM using FEL with the following command:

`sunxi-fel -v uboot u-boot-sunxi-with-spl.bin`

This worked out nicely and I could see the u-boot logs on my serial port!!

![image](../attachments/image-1774026512090-xakx5pfql.png)

I tried to start the USB inside uboot but it threw a No controllers found. But that was okay as I can just work on fixing that later.

![image](../attachments/image-1774026512130-y9095war2.png)


A little side note here, my board was genuinely tweaking out the entire time. It would show up as a USB device but then after some time like 30 or 40 minutes it would disappear and would not show up till I spray the board with IPA and brush it off. I have no idea why this keeps happening and no idea why this fixes it but If I were to make a guess it'd be that the board probably absorbs moisture and stops working!?


After successfully getting uboot to work by flashing it to RAM, it was now time for me to make it a bit more permanent and use and SD card. I connected an SD card but passing it to WSL was pretty problematic and I was tired, so I hopped on my other debian laptop, and tried building the uboot spl again but got a shit ton of errors so I just ended up using the one I already built on WSL.
After flashing the SD card with the uboot spl, I plugged it in and nothing happened. There were no UART logs or anything which was a bad sign, it meant that it was definitely not in uboot. I tried flashing to the RAM and it worked again but as soon as I plug the SD card in the UART just stops. Which again I have no idea why that's happening, and I was pretty tired so I decided to wrap it up for the day and continue with this some other day.


## Time Spent: 5 Hours

# 13 February, 2026 - Troubleshooting SD Card

I finally got the chance to work on this again, I started off by just trying to get uboot in RAM again, but it turns out I somehow lost the old uboot file that was on WSL, I think I accidentally rm -rf'd the whole folder, and so I had to rebuild it over again.

Now It's been a while since I last worked on this so I basically forget everything, and I ran into the same errors I faced last time - the march target and binman error. But luckily I documented these errors last time, so I just referred back to this journal and solved them.

After rebuilding the spl with uboot I went ahead and flashed it on the board, and as usual I saw the uboot log in the uart console. Oh also a sidenote, I mentioned about spraying IPA on the board to get it working, well that's still true and now I have to do it more frequently, probably like every 15-20 minutes. The board just straight up disconnects and wont show up in FEL unless you spray it with IPA. I have absolutely no clue why this is the case, but it is what it is.

Anyways, after getting uboot on RAM successfully, I tried to reflash a smaller 32GB SD card I found and then try to use it, but I had no luck with that. I seem to get no uart logs if I try to boot with the SD card. I even tried just flashing it to RAM and then inserting SD card to maybe see if I could do a a `mmc list` to see it. But as soon as I insert the SD card, uboot just stops and my uart connection dies, I can't type anything in the console, just like last time. 

I tried to reflash and try different methods of inserting the card and power cycling but nothing seemed to work. After a while, I was just going back and forth with chatgpt about why this is happening and it you know as usual spit out some weird stuff about "oh yes, this is a common glitch and all that" when its not, but it did say something useful and that was about huge inrush current spike. I realized that I had actually skipped decoupling capacitors on the SD card interface and was actually wondering now if that was the reason why it didn't work.

To test out my theory I pulled out my scope and and hooked it up to the 3V3 rail and then put a high time division of around 500ms to 2s and just looked at the voltage rail (which was a mistake), I couldn't see much drops, the rail seemed a bit noisy but everything seemed fine. The rail would occasionally have a tiny drop sometimes if I plugged in the card but not always. 

![image](../attachments/image-1774026512200-jzmjmffvy.jpg)

The reason for this inconsistent behavior was my mistake of using such a big time division, at the time of measuring it I went with a large time div just because it gave me more time to see the rail and any major events but what I didn't realize was the at such a huge time division I wouldn't be able to see the voltage spike when the SD card gets inserted because its a very tiny dip. A better choice would have been a 1ms/div or 500us/div.


Anyways I suspected the problem was definitely with my SD card or its circuitry, I suspected it might be due to a voltage dip because I didn't including any decoupling capacitors on my 3V3 pin for the SD card. I decided to wrap it up for the day, and decided that I'll try to boot linux directly from RAM and just skip the SD card for now.

## Time Spent: 3 Hours

## 14 February - Fixed SD Card

I wasn't fully sure why my board crashed everytime I inserted an SD card, but my best guess was a voltage drop due to huge inrush current. And as it turns out I forgot to put any decoupling capacitors on the SD card IO.

But luckily enough I was smart enough to put test points that expose all the pins of the SD interface, and I used the test points to sort of add botched decoupling. I soldered on a 100nF + 1uF capacitor across 3V3 and GND test point of the SD interface.

![image](../attachments/image-1774026512294-ecb1b2ao3.jpg)

Soldering 0402s here by hand was a bit challenging but it only took me about 10 or so minutes to get right. After soldering I made sure to inspect it visually with a magnifying glass to confirm that nothing is shorted. It did look like 3v3 and clock were bridged so I pulled out some flux and fixed it.

After doing this the board no longer crashed as soon as I inserted an SD card!
Though I still had no success getting uboot running off SD card. So I had to still flash it to RAM first. But while in uboot I could now run MMC info and see my SD card show up.

![image](../attachments/image-1774026512340-c9cjbjsa2.png)


However when trying to read the MMC it crashed the board again, I'm assuming this might be due to the fact that its a high capacity card?! I might try with a smaller 1 or 2 gb once I get them. 

Anyways at this point I was ready to give up on getting SD card to work properly and just straight up boot linux from RAM, but right as I went to do it ubutu on WSL straight up died.

![image](../attachments/image-1774026512384-hiuypckum.png)

I have no idea how or why but wsl literally just killed itself.

And yea so that was pretty much when I decided to wrap it up for the day and hopefully work on it another day in the future.

### Time Spent: 2.5 Hours