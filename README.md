# Ambilight-project
I created an ambilight system for my TV to improve experience when gaming. Feel free to use as you please.

## What is ambilight?
Ambilight is a feature that's been around for quite a while that will give your TV a backlight that corresponds to the colors shown on the TV - a blue skye will give a blue backlight. The cool thing is that it changes with the picture. Philips has recently tried to bring it back, but those things are expensive AF and doesn't work any better than something homemode.
If you try to start an ambilight project from scratch you will quickly find a billion guides that all have their own take on things. 

So there are two main ways of doing this. I have seen some projects that uses a Webcamera to record whats on the screen, but this seemed to me to be a shitty solution that cannot possible be giving an acceptable result. So this setup **DOES NOT USE WEBCAM**, instead it uses Hyperbian and USB capture mode. This is done through a dongle that is able to convert the signal for us. All this will be better explained down the guide don't worry.

This overall setup is straightforward and will work 100% on HDMI input sources. Depending on your splitter, and it's abaility to split and strip images of protection you may or may not be able to use newer HDCP for example, I have not had this problem. Considering this requires an external source, this means you won't get ambilight effects on anything seen through a Smart TV's OS as this is not an HDMI input source. The Netflix app on your TV won't work, in other words.

I use it for two things: 
1. My Xbox
2. My Chromecast

Using a Chromecast is great because it lets you turn literally any streaming app on your phone into a HDMI input source, meaning we can watch netflix with ambilight as long as it's running through the chromecast.

Oh, and this thing hooked up to the Xbox is lit AF. It looks really good and you're gonna be in awe the first time you get it working :-)


# WIP - Tutorial for building

I will update this more soon once i've been able to take some pictures etc.

## Powering the WS8212B

Powering this strip will vary depending on the number of LEDs you have. Each LED on the WS2812B uses anywhere from 20-60ma. It’s a good idea to assume maximum brightness when calculating amperage even if you don’t plan to keep them at maximum brightness. Although it’s safer to use USB power for the Raspberry Pi you can power it from the power supply so If you plan on doing this then you should factor in another 2.4A for the Pi. 

A 10A or 15A power supply should be fine for the average TV (less than 200 LEDs). Most “wall wart” power supplies (the black power bricks you’re used to seeing) don’t usually come any bigger than 15A so if you need more than 15A then you’ll likely end up with a metal power supply that needs to be placed inside of a box. If you absolutely need to, you can save some amperage by lowering the brightness of the LEDs. 


You can calculate the required power supply amperage for you LEDs using the simple calculation below: 

    0.06 x numberofleds = maximum amperage
    (Ex. 0.06 x 300 = 18A)

There are 3 wires on the WS2812B. The two wires on the outside are used to power the strip and the wire in the middle is used for data. 

![bilde](https://user-images.githubusercontent.com/42509703/115116270-05bcbd00-9f99-11eb-8be8-e47aace62241.png)

Connect the power wires to your power supply ensuring that you have the correct polarity (+/-). I recommend adding a 1000uf capacitor as close as you can get it to the first LED in the strip. As long as the capicitor is at least 6.3v or higher it  will work just fine for this. Most 1000uf capacitors are electrolytic so they are polarized. It’s important that you take note of the markings on the capacitor to determine which lead is the negative side and connect that side to the white or negative wire. You don’t wanna find out what happens if you get this wrong.

## Connecting the Data pins

Take note of the tiny arrows on the LED strip. The arrows should be pointing away from the wires. This indicates the beginning of the strip where you should connect the data wire. Use a jumper wire and the 470 ohm resister to connect the data wire from the LED strip to Pin 6 on the Arduino Uno (Pin 50 on Arduino Mega 2560). You can technically use any pin you want.

## HDMI and HDCP

Lot’s of fun with HDMI and HDCP

Since we need to feed a video signal to the Raspberry Pi we have to use an HDMI Splitter to split the signal from your media player to the TV and the Raspberry Pi. It’s no doubt that this is one of the most challenging parts of this project if you plan to watch 4K HDR content. This isn’t a problem if you only watch 1080p content but HDCP (High-Bandwidth Digital Content Protection) encrypts the video signal to make it difficult to copy/split a 4K HDR signal in an effort to prevent piracy. 

If you attempt to split a 4K HDR signal using the average 1x2 HDMI splitter the best you will get is 4K SDR @ 30hz since it downgrades to a non-HDR signal. This means that with most HDMI splitters you will never see 4K HDR on your TV. 

Thankfully there are a few HDMI Splitter options out there that can decode the HDMI EDID signal and send 4K HDR to your TV and SDR to the Raspberry Pi. The first option I found was the gofanco Prophecy Intelligent 1x4 HDMI Splitter.

# Finished Setup Schematics

![bilde](https://user-images.githubusercontent.com/42509703/115116350-5502ed80-9f99-11eb-8383-b421ac0546f0.png)


## HyperBian Dashboard & Setup

![bilde](https://user-images.githubusercontent.com/42509703/115116184-a199f900-9f98-11eb-8229-ee2fc31a66c5.png)

![bilde](https://user-images.githubusercontent.com/42509703/115116200-b8d8e680-9f98-11eb-8641-7bdadbbd3095.png)
