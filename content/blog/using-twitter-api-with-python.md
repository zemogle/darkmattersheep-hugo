+++
date = "2013-09-15T20:59:23+01:00"
draft = false
title = "Using Twitter API with Python"

+++

<p>My brain never rests. One of the ways I relax is finding solutions to problems. Sometimes thats with crosswords or old episodes of Poirot on ITV3, sometimes thats with writing code. I particularly like using Python.</p>
<p>I use <a href="http://twitter.com">Twitter</a> all the time, for finding out all the latest news and political gossip in astronomy. So, I thought I'd have a bash at using Twitter through python. You used to be able to access Twitter just by using your account username and password, with their basic auth in Twitter API v.1.0. Not any longer. Version 1.0 is now defunct and to do interesting things with Twitter API you have to use version 1.1 which requires OAuth.</p>
<p>This can be a whole world of pain, so I'm writing my findings here to help anyone experiencing similar discomfort.</p>
<h2>1. Find a Twitter library</h2>
<p><br />Various people have written libraries to access twitter (I tried writing my own and it was a thankless task). <span style="text-decoration: line-through;">I would recommend using the simply named <a href="https://pypi.python.org/pypi/twitter">twitter</a> package. You'll also need a python way of logging in via OAuth, so I would recommend using <a href="https://github.com/simplegeo/python-oauth2">OAuth2</a>.</span></p>
<p>I've changed my mind on which library to use. I'm now using <a href="https://github.com/geduldig/TwitterAPI">TwitterAPI</a>, which seems more flexible for my needs, has good documentation, examples and regular updates.</p>
<p>It is on <a href="https://pypi.python.org/pypi">PyPi</a> so you should be able use:</p>
<pre class="lang:sh theme:son-of-obsidian">pip install twitterapi</pre>
<h2>2. Get developer credentials</h2>
<p><br />You'll need a Twitter account to go much further with this tutorial. Once you have that:</p>
<p></p>
<ol>
<li>Log into the <a href="https://dev.twitter.com/">Twitter developer site</a>,</li>
<li>Create a new app by clicking on your icon in the top left</li>
<li>Click "My applications" in the menu,</li>
<li>Click the button "Create a new application"</li>
<li>Fill out all the details, sign your life away and click "Create you Twitter application"</li>
</ol>
<p>You should now be redirected to a page with all the information about your new app, including "OAuth settings". This page has the 4 horsemen of the OAuth apocalypse:</p>
<ul>
<li>Consumer Key,</li>
<li>Consumer secret,</li>
<li>Access token (often called "OAuth token")</li>
<li>Access secret (or "OAuth token secret") - these last 2 in the lower section</li>
</ul>
<h2>3. Put it together</h2>
<p><br />You are now ready to have a play with Twitter from python. Open up a python shell:</p>
<pre class="lang:sh theme:son-of-obsidian">&#10140;  ~ ipython<br />Python 2.7.1 |CUSTOM| (r271:86832, Dec  3 2010, 15:56:20) <br />Type "copyright", "credits" or "license" for more information.
IPython 0.13.2 -- An enhanced Interactive Python.<br />? -&gt; Introduction and overview of IPython's features.<br />%quickref -&gt; Quick reference.<br />help -&gt; Python's own help system.<br />object? -&gt; Details about 'object', use 'object??' for extra details.
In [1]: from TwitterAPI import TwitterAPI<br />In [2]: t = TwitterAPI(<br /> CONSUMER_KEY, CONSUMER_SECRET,
OAUTH_TOKEN, OAUTH_SECRET<br /> )</pre>
<p>Substitute the 4 horsemen into those capitalised variables and hopefully that won't give you any trouble.</p>
<p>Now you can take Twitter for a spin. There are loads of interesting things you can do listed on the <a href="https://dev.twitter.com/docs/api/1.1">Twitter REST API v1.1</a> help pages.</p>
<p>I really wanted to have a look at various #hashtags without being rate limited. The way you do this is by using the <a href="https://dev.twitter.com/docs/api/1.1/post/statuses/filter">Twitter Stream</a> and not the Twitter Search. This lets you enter hashtags, words or phrases and then sit on the stream of tweets happening which contain the words you are tracking.</p>
<pre class="lang:sh theme:son-of-obsidian">from TwitterAPI import TwitterAPI
api = TwitterAPI(TWITTER_CONSUMER_KEY, TWITTER_CONSUMER_SECRET,TWITTER_ACCESS_TOKEN_KEY, TWITTER_ACCESS_TOKEN_SECRET)<br />ts = api.request('statuses/filter', {'track': 'holiday'})<br />stop = datetime(2014,11,1,9,50,0)<br />for item in ts:<br />    print item['user']['screen_name'], datetime.strptime(item['created_at'],'%a %b %d %H:%M:%S +0000 %Y'), item['text']<br />    if datetime.now() &gt; stop:<br />        print datetime.now().isoformat()<br />        break</pre>
<p>Once you open a stream, tracking certain words, it will carry on forever. For this reason I stop the for loop which checks the stream with a timeout, in the variable <strong>stop</strong> (a datetime object).</p>
<p><strong>Tip:</strong> You can't look backwards in time in a Twitter stream, only forwards in real-time. If you want to look back in the Twitter feeds you'll have to use search.</p>
<p>Thats my recent findings. There are so many more things you can do with the Twitter API, but that is just a taste.</p>