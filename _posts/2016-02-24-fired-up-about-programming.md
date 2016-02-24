---
layout: post
title: How I got fired up about programming
comments: True
summary: The Excel VBA script that got me hooked to coding back in 2006. This is a fun story to read and probably some of you programmers out there recognize the initial spark of passion for the craft. Enjoy!
tags: [programming, motivation, automation, Excel, macros, VBA, Spain, brute force, algorithms, story, learning]
image: fired_up_programming.png
---

I just tried to figure out where my passion for coding started. I can find two anchors:

* an early affinity / passion for automating tasks (since my Business Economics cost control dissertation)

* [an Excel game](http://juegosexcel.com/foro/viewtopic.php?t=6396) that I hacked/ automated to solve. For the first time I share the story behind this, I'm glad I did not forget.

### The hack

<div class="container"><iframe src="https://www.youtube.com/embed/ZLPr4Q7KACQ" frameborder="0" allowfullscreen class="video"></iframe></div>

### The story

It was 2006, I worked as a financial analyst. We were hard workers, but we also wanted to relax from time to time. Hence funny emails. One day though [this Excel game](http://juegosexcel.com/foro/viewtopic.php?t=6396) was sent around. It contained photos of 52 Spanish cities which you had to guess:

![That funny game that was sent around in '06]({{ site.baseurl }}/assets/spanish_cities_start.png)

Folks spent quite some time on it getting to 50% quickly then 80% but the last 20% caused a lot of head-banging. I thought: "this is an opportunity to automate". Solve the puzzle with a Macro, get the skills, wow my colleagues.

And that was what I did.  Here is the result: the macro automatically fills in all the 52 fields with solutions in seconds. It is pretty simple in hindsight:

1. store all cities in an array (I think I got them from the web somewhere and I think this took some trial and error honestly, these day I would call a web API for sure!),

2. loop in loop (brute force): loop over the cells trying each city from an array and continue to next when match.

For all its simplicity though it took me quite some time to write! I had to learn loops, variables, etc. from scratch, and there was the added complexity of having to go into a cell and match the "Correcto!" in another cell to know when to break the loop. But when I saw this I knew it had paid off!

![Resolved in seconds with the Excel VBA macro]({{ site.baseurl }}/assets/spanish_cities_done.png)

---

### Pivotal moment

It was then that I knew this was MY THING.

Apart from a couple of jaws dropping when seeing this, this taught me my first programming skills in Excel VBA and more importantly the empowerment of what programming can do. It instilled in me a deep passion I feel very fortunate to carry with me every day. As people who know me witness: I get stoked about applying coding skills to solve boring stuff to make their lives easier, freeing them up to work on the more important stuff.

### Learn by doing

Programming can have a steep learning curve but once you practice, fail, get better, it's fun and interesting. Once you start to build stuff that saves other people tons of hours it is a highly rewarding activity to emerge in.

I just read a [great post](https://sivers.org/learn-js) on how to learn Javascript. One piece of advice: read books, yes, but start to build stuff. Just solve a problem you or one of your friends/colleagues have and gain practice.

You can find plenty of examples on this blog, just a couple: [safaribooks notification email](http://bobbelderbos.com/2015/11/new-safari-books-notification-email/), [podcast feed downloader](http://bobbelderbos.com/2013/12/podcast-scripting-golf/), [search stackoverflow inside Vim](http://bobbelderbos.com/2013/01/search-copy-stackoverflow-data-in-vim-with-conque/), [your movie site in one minute](http://bobbelderbos.com/2016/02/movie-site-in-minute-omdb-api-python/), [tweet with PHP](http://bobbelderbos.com/2010/12/twitter-api-tweet-with-php/), or sites I managed to built like [sharemovi.es](http://bobbelderbos.com/2010/11/sneak-preview-sharemovies/) and [my reading list](http://bobbelderbos.com/2011/03/new-facebook-app-my-reading-list/).

### Reference material

You can get the Excel VBA code [here](https://github.com/bbelderbos/Codesnippets/tree/master/vba) and the game is still [here](http://juegosexcel.com/descargas/?did=280). Note though this is my first ever script so it is ugly (seeing those meaningless variable names anybody?), I would structure it much better now. But you have to start somewhere and this one did the job nicely.

Last but not least: enjoy coding! :)
For additional motivation I highly recommend you read [The Passionate Programmer](http://bobbelderbos.com/2011/04/advance-career-read-passionate-programmer/) by Chad Fowler. To learn more about the craft of writing solid code I recommend reading [The Pragmatic Programmer: From Journeyman to Master](http://bobbelderbos.com/2011/02/great-book-about-software-engineering/).

### What about you?

Feel free to share your first exposure to programming in the comments below. Any anecdotes? Where did you get started and how is the journey going? Thanks in advance.
