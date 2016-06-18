---
layout: post
title: How to create a simple Twitter bot with Python 
comments: True
summary: In this post I show you how to create a Twitter bot. In this case it is a solution that hourly tweets a randomly retrieved design quote to a dedicated Twitter account (bot). It is a small script you can easily adjust for your own needs.
categories: [Coding]
tags: [Python, Twitter, API, bot, quotes, design, requests, html, logging]
image: twitter_bot.png
---

Creating a Twitter bot is a nice exercise in programming because it touches upon many aspects: APIs, url / text parsing, automation (cronjobs), logging. Some time ago I created two Twitter bots:

1. [@newsafaribooks](https://twitter.com/newsafaribooks): tweets every day what new book get added to [safaribooksonline](http://safaribooksonline.com/).
2. [@cine_tv_es](https://twitter.com/cine_tv_es): tweets every hour what movies are broadcasted on Spanish TV. It matches/embeds the trailer for each movie.

To refresh my memory and share the knowledge I went through the motions again today creating another bot. For this post I created [@quotes_ondesign](https://twitter.com/quotes_ondesign), a bot that sends out design quotes retrieved from the [Quotes on Design API](http://quotesondesign.com/api-v4-0/). The code is on [github](https://github.com/bbelderbos/quotes_on_design) if you want to check it out.

### Steps:

1. Create a twitter account (or use your own, it depends your needs)

2. Add (confirm) a phone number. This is required to create a Twitter app, however the good news is that you can use your phone number for multiple accounts.

3. If you use my code copy config.py-example to config.py

4. Go to [apps.twitter.com](http://apps.twitter.com) and create a new app, you need to put the following keys in config.py:

* Consumer Key (API Key) 
* Consumer Secret (API Secret) 

5. Create an access token (button) and paste these two keys in config.py as well: 

* Access Token 
* Access Token Secret 


6. I use [tweepy](http://www.tweepy.org) for Twitter API handling, so you need to: $ pip install tweepy

7. Some comments about the code:
* I use requests to retrieve the data from the API
* I parse the returned JSON to create the tweet. As tweets can be max. 140 chars I have some math going on in create_tweet(), when the quote text is too long I shorten it, appending 3 dots (...), I link to the source of the quote ([quotesondesign.com](http://quotesondesign.com)).
* Posting to Twitter is very simple with tweepy (api = get_twitter_api() and api.update_status(tweet))
* As the API returns some encoded HTML (it seems it was build for web use), I unescape html for which I used HTMLParser
* I use the logging module which is very easy to set up (logging.basicConfig...) and which gets you the imported module's logging out-of-the-box.
* I also played a bit with defining customized exceptions. The nice thing about trying this kind of exercise is that you learn a lot of Python related stuff.
* Again the script is on [github](https://github.com/bbelderbos/quotes_on_design/blob/master/quotes.py), any questions or comments, use the comments below.


8. The last step is to put the script in a cronjob to have it run every hour:

    0 * * * * $HOME/code/quotebot/quotes.py 2>&1 >> botlog

* 0 * * * * makes it run every hour
* cron jobs tend to send email so I direct everything to a text file (and the logging bit of the scripts writes to $HOME/quotes.log)
* if you installed tweepy as your user you might get an ImportError back from the cronjob. In that case you need to prepend it with the following (or wherever you have the Python installed you want to use): 

    export PYTHONPATH=$HOME/bin/python/lib/python2.7/site-packages && $HOME/bin/python/bin/python2.7 


---
And the result: auto-generated quote tweets (frequency is greater due to testing, but should post once a hour): 

![twitter bot results, nice]({{ site.baseurl }}/assets/twitter_bot_result.png)

Use the comments below if you have coded a Twitter bot yourself that you want to share, or if you have any good ideas for other Twitter bots.
