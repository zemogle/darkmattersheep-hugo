+++
date = "2015-10-25T19:43:34+01:00"
draft = true
title = "Raspberry Sky: All sky Raspberry Pi camera"

+++

I've had a long running project to install an All Sky camera in [Brecon Beacons National Park](http://www.breconbeacons.org/about-brecon-beacons-dark-sky-reserve) has been awarded Dark Sky Reserve status. The camera is running nicely up there now, as [I've blogged out already](http://darkmattersheep.uk/blog/brecon-allsky/). I have to say the nice people at the Brecon Beacons National Park have been terrifically helpful (they were even kind enough to provide tea and cake too). While I was installing the original camera in September 2014, it broke (i.e the electronics got funked up). I'm not entirely sure how, but my dad was helping me, so I'm going to blame him.

While I was trying while I was trying to collect enough funds to buy a new camera, I started making my own from spare parts.

## The Challenge
![SBIG all Sky Camera 340](http://static.darkmattersheep.uk/uploads/allsky3.jpg)
This SBIG 340 all sky camera costs $4000! I aim to build a replacement for about &pound;100. Here is the parts list:

- Raspberry Pi B - &pound;35
- Raspberry Pi camera module - &pound;25
- <a href="http://www.ebay.co.uk/itm/121426112537">M12 fisheye lens 151 &deg;</a> - &pound;13
- <a href="http://www.ebay.co.uk/itm/111304951108">M12 board lens mount</a> - &pound;4
- Edimax EW&ndash;7811UN USB nano wifi dongle - &pound;7
- SD card - &pound;7
- 5V power supply &pound;5
- Raspberry Pi case &pound;5

#### Total: &pound;101

![The Raspberry Sky](http://static.darkmattersheep.uk/uploads/allsky4.jpg)
## Problems
1. Camera Module comes with a lens attached.
1. Short exposures:
  1. RPi camera module&rsquo;s firmware will only allow for a 6s maximum exposure time. Things in space are faint, you want to expose for as long as possible.
  1. M12 lens is small, only 21mm in diameter. Things in space are faint. You want as big a lens as possible to collect more light, but big lenses are expensive.
1. Camera Module claims it has a maximum ISO of 1600 but its really 800.
1. RPi detector is very small. The M12 lens is designed for CCTV cameras where the detector is larger, so the image it projects is bigger than the camera can see. That means we lose half the image. We want to see from horizon to horizon. Fisheye lens is not 180 &deg; and we&rsquo;re not seeing the whole image.

## Solutions

### 1. Remove the lens

The camera module lens is a very small pinhole lens and doesn't let me much light in. You want to get rid of that otherwise we won't be able to focus when we have our fisheye lens. You'll need tweezers to gentle turn the lens. Its glued in so be bold.
![](http://static.darkmattersheep.uk/uploads/allsky5.jpg)

### 2.1 Take mulitple exposures
There is a command line utility which can control the RPi camera. So we set shutter speed to 6s (6 million &micro;s), ISO of 800 and give us a grey image (thats the <code>cfx</code> setting).

{{< highlight bash >}}
raspistill &mdash;ss 6000000 -ISO 800 -cfx 128:128 -n -o allsky.jpg
{{< /highlight >}}

A single image is not long enough to see stars, so I wrote a bit of python to take 10 images and combine them.

### 2.2 Image Sequence
The read-out time on the camera module is quite long so the stars were in different positions in-between frames. I got around this by taking an image sequence. The Pi Camera module takes some time to start up and shut down if you take a single image, as well as read out. All of that amounted to about 20-30s. With an image sequence, it only does the camera start up at the very beginning of the sequence, and similarly it only does the shut down procedure once, right at the end of the sequence.

### 3. ISO 800
ISO is the 'speed' of the detect. In other words, how efficiently the light gets converted to an electrical signal. We're looking at really faint things, so we want this process to be as efficient as possible. The Raspberry Pi camera module advertises being able to get an ISO of 1600. I can't get more than 800 out of, so maybe it isn't available to the API.

## The Results


*You can find all my code in my [Raspberry Sky GitHub repository](https://github.com/zemogle/raspberrysky).*
