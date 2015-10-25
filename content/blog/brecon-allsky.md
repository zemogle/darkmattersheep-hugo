+++
date = "2015-10-24T14:22:47-07:00"
draft = false
title = "Brecon Beacons Allsky Project"

+++

# Version 1
Back in 2012 I was sent an AllSky camera by [LCOGT](http://lcogt.net) (the observatory I work for). I was incredibly excited at the prospect of being  able to see stars above my house or even above Cardiff University. Cardiff has the worst light pollution in Wales. It is pretty shocking that for a nation which can boast 90% dark skies, in the capitol stargazing is virtually impossible.

I hired a summer intern (through the Cardiff University Research Opportunities scheme) to write controller software for the camera ([SBIG 340](https://www.sbig.com/products/cameras/specialty/the-allsky-340-camera/) - which only comes with Windows software) so we could control it with a Raspberry Pi (find his code for [SBIG 340 cameras is on GitHub](https://github.com/badders/pyallsky)). In the summer of 2013 we installed it next to the Cardiff University observatory.

![Cardiff city centre at 4am with horrific light pollution](http://static.darkmattersheep.uk/uploads/cardiff_allsky.png)
The image above is the result - the light pollution is so bad, you cannot identify any stars. Increasing the exposure time just makes the whole sky brighter. You can just about see the Moon at the bottom, left of centre. It looks like street light!

## Brecon Beacons Dark Sky Reserve
This was clearly unworkable so I approached the friendly people at Brecon Beacons National Park to install the camera there. In 2012 Brecon Beacons also [became a Dark Sky reserve](http://www.breconbeacons.org/about-brecon-beacons-dark-sky-reserve) meaning the dark skies over this national park are protected. At the time they were building an observatory and this camera would be the perfect accompaniment.

That was the plan... It didn't work out because the SBIG 340 Allsky camera was terribly unreliable. LCOGT have about a dozen of them deployed at remote astronomical sites all over the world and they have lots of problems. Ours went back to California to SBIG because it broke. When it came back it worked for a year, until the day I was installing it in Brecon, and broke again.

# Version 2
I thought this project was dead and all the free coffee and cake the nice people at Brecon Beacons Mountain Centre had given me would have been in vane. Forutnately, Cardiff University Public Engagement team really liked the idea and give me a small grant to buy a new camera. This time I was not going to buy the SBIG (which incidentally, costs ~$4000) but there were very few options. Eventually I found the [Oculus from Starlight Xpress](http://www.sxccd.com/oculus-all-sky-camera), but sadly I couldn't use my intern's code to control it on Linux.

The day was saved by the [INDI (Instrument Neutral Distributed Interface) project](http://indilib.org/) which provides an interface to the camera. I found a way to talk to it through Python and wrote some code to take pictures during the night only, and make nicely scaled images. Its on [GitHub, so please fork me](https://github.com/zemogle/pyOculus)!

# All Sky view over Wales
![Image from Brecon Beacons All Sky Camera on 25 Oct 2015 at 0340 UTC](http://www.zemogle.uk/allsky/20151025-0440.png)
It is currently up and running [in a field outside Brecon](https://www.google.com/maps/place/Brecon+Beacons+National+Park+Visitor+Centre/@51.923633,-3.4894071,17z/data=!4m5!1m2!2m1!1sbrecon+beacons+mountain+centre!3m1!1s0x0000000000000000:0xd94a023376c3d6e5), connected to a Raspberry Pi.

This Oculus camera gives beautiful images, is really reliable and quite a reasonable price. I can't wait to see more images from it looking out over the dark skies of South Wales (between the clouds).

You can find the latest images from the camera on [my Brecon Beacons All Sky page](http://www.zemogle.uk/allsky/).

*Big thanks to all the friendly and helpful staff at the Brecon Beacons National Park for being supportive of this project and Cardiff University Engagement team for seed funding for the replacement camera.*
