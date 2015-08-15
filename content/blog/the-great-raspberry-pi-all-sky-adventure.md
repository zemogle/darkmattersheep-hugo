+++
date = "2015-06-13T19:43:34+01:00"
draft = false
title = "The Great Raspberry Pi all sky adventure"

+++

<p>I&rsquo;m building an all sky camera. Cardiff University was donated an <a href="https://www.sbig.com/products/cameras/specialty/the-allsky-340-camera/">SBIG 340 all sky</a> camera by <a href="http://lcogt.net">LCOGT</a>. After a lot of installation, commissioning, and software rewriting we eventually had it working on the roof of the <a href="http://www.astro.cf.ac.uk">School of Physics and Astronomy</a>. The image below is what resulted.</p>
<p><img src="/media/uploads/cardiff_allsky.png" height="300" width="400" /></p>
<p>This is a perfectly clear night with a 4 minute exposure at 3am. The light pollution from the city is so bad you can&rsquo;t see any stars, and can only barely see the moon.</p>
<p>Fortunately, <a href="http://www.breconbeacons.org/about-brecon-beacons-dark-sky-reserve">Brecon Beacons National Park has been awarded Dark Sky Reserve status</a>, and the nice people up there were keen on hosting the all sky camera (they were even kind enough to provide tea and cake too).</p>
<p>While I was installing it in September 2014, it broke. We&rsquo;re not entirely sure how but my dad was helping me, so I&rsquo;m going to blame him.</p>
<p><img src="/media/uploads/allsky3.jpg" height="400" width="600" /></p>
<p>An SBIG all sky camera costs $4000! I aim to build a replacement for about &pound;100. Here is the parts list:</p>
<ul>
<li>Raspberry Pi B - &pound;35</li>
<li>Raspberry Pi camera module - &pound;25</li>
<li><a href="http://www.ebay.co.uk/itm/121426112537">M12 fisheye lens 151 &deg;</a> - &pound;13</li>
<li><a href="http://www.ebay.co.uk/itm/111304951108">M12 board lens mount</a> - &pound;4</li>
<li>Edimax EW&ndash;7811UN USB nano wifi dongle - &pound;7</li>
<li>SD card - &pound;7</li>
<li>5V power supply &pound;5</li>
<li>Raspberry Pi case &pound;5</li>
</ul>
<h4>Total: &pound;101</h4>
<p><img src="/media/uploads/allsky4.jpg" height="400" width="600" /></p>
<h2>Problems</h2>
<ol>
<li>RPi camera module&rsquo;s firmware will only allow for a 6s maximum exposure time. Things in space are faint, you want to expose for as long as possible.</li>
<li>RPi detector is very small. The M12 lens is designed for CCTV cameras where the detector is larger, so the image it projects is bigger than the camera can see. That means we lose half the image.</li>
<li>M12 lens is small, only 21mm in diameter. Things in space are faint. You want as big a lens as possible to collect more light, but big lenses are expensive.</li>
<li>We want to see from horizon to horizon. Fisheye lens is not 180 &deg; and we&rsquo;re not seeing the whole image.</li>
<li>Camera Module claims it has a maximum ISO of 1600 but its really 800.</li>
<li>Camera Module comes with a lens attached.</li>
</ol>
<h2>Solutions</h2>
<h3>Remove the lens</h3>
<p>The camera module lens is a very small pinhole lens and doesn't let me much light in. You want to get rid of that otherwise we won't be able to focus when we have our fisheye lens. You'll need tweezers to gentle turn the lens. Its glued in so be bold.</p>
<p><img src="/media/uploads/allsky5.jpg" height="400" width="600" /></p>
<h3>Take mulitple exposures</h3>
<p>There is a command line utility which can control the RPi camera. So we set shutter speed to 6s (6 million &micro;s), ISO of 800 and give us a grey image (thats the <code>cfx</code> setting).</p>
<pre><code class="&ldquo;bash&rdquo;"> raspistill &mdash;ss 6000000 -ISO 800 -cfx 128:128 -n -o allsky.jpg </code></pre>
<p>A single image is not long enough to see stars, so I wrote a bit of python to take 10 images and combine them.&nbsp;</p>
<h3>Image Sequence</h3>
<p>The read-out time on the camera module is quite long</p>
<p>You can find all my code in <a href="https://github.com/zemogle/raspberrysky/blob/master/allsky.py">my GitHub repository</a>.</p>