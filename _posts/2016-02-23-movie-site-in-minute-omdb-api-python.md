---
layout: post
title: Your movie site in just one minute
comments: True
summary: Improvement of my popular post "Your own movie database in 5 minutes with IMDb API and Perl", rewritten in Python you can now have your own static movie html site in less than one minute!
tags: [imdb, omdb, movies, api, python, coding, html, css, perl]
excerpt_separator: <!--more-->
---

This is a rewrite/improvement of my popular script/post [Your own movie database in 5 minutes with IMDb API and Perl](http://bobbelderbos.com/2011/11/movie-database-imdb-api-perl/) that got (and still gets) quite some visits every day. I rewrote the code in Python, took out the DB dependency (goal was a static site anyways) and documented the steps.

**Disclaimer:** this is quick and dirty. If you want to build a a real movie site, use something more powerful like [themoviedb](http://themoviedb.org), I used that A. to build [sharemovi.es](http://bobbelderbos.com/2012/07/new-release-sharemovies-design-features/) and B. create a [weekly movie email script](http://bobbelderbos.com/2015/11/project-weekly-movie-email-with-tmdbsimple-python/). So keep that in mind when reading this and if you decide to use it.

<!--more-->

---

## Steps

You don't have to create any text files unless you want to use your own set of movies, all files are in [this github repo](https://github.com/bbelderbos/own_movie_site).

* copy and paste top 250 movies from [imdb](http://www.imdb.com/chart/top) and put in file called inimdb-top-rated.txt file (or use your own but use the same syntax: movie,year)

        $ head  imdb-top-rated.txt
        1. The Shawshank Redemption (1994)  9.2
        2. The Godfather (1972)   9.2
        3. The Godfather: Part II (1974)  9.0
        4. The Dark Knight (2008)   8.9
        5. Pulp Fiction (1994)  8.9

* normalize the data to title,year:

        $ grep -v "^ *$" imdb-top-rated.txt |perl -pe 's/ *\d+\.\s+(.*)\s+.*\((\d+)\).*/\1,\2/g' > movielist.txt

        $ wc -l movielist.txt
        250 movielist.txt

        $ head movielist.txt
        The Shawshank Redemption,1994
        The Godfather,1972
        The Godfather: Part II,1974
        The Dark Knight,2008
        Pulp Fiction,1994
        Schindler's List,1993
        12 Angry Men,1957
        The Lord of the Rings: The Return of the King,2003
        The Good, the Bad and the Ugly,1966
        Fight Club,1999

* run the python script that queries [omdb](http://omdbapi.com/) for movie info returning a nice html page. OK, 2% not found, I can live with that, look at the runtime :)

        $ time python your_moviedb.py movielist.txt
        ERR2: cannot find movie: Old Boy (year: 2003)
        ERR2: cannot find movie: Érase una vez en América (year: 1984)
        ERR2: cannot find movie: M (year: 1931)
        ERR2: cannot find movie: Nader y Simin, una separación (year: 2011)
        ERR2: cannot find movie: Relatos salvajes (year: 2014)
        Done, 245 processed, created static html movie page: topmovies.html

        real 0m13.348s
        user 0m0.755s
        sys 0m0.420s

* see example output by opening topmovies.html output file in the browser (edit CSS in this file to your liking). One issue I found though was that the IMDB poster URLs get 403 (forbidden) when hosting this output html on a domain (on localhost it works). So you need to use another API (themoviedb, facebook) for this, see [here](http://stackoverflow.com/questions/151272/given-an-imdb-movie-id-how-do-i-programmatically-get-its-poster-image/).

* to quickly test this you can run this (assuming Mac)

        $ mkdir movie_test && cd $_
        $ wget https://raw.githubusercontent.com/bbelderbos/own_movie_site/master/test.sh
        --2016-02-23 18:39:50--  https://raw.githubusercontent.com/bbelderbos/own_movie_site/master/test.sh
        Resolving raw.githubusercontent.com... 23.235.43.133
        Connecting to raw.githubusercontent.com|23.235.43.133|:443... connected.
        HTTP request sent, awaiting response... 200 OK
        Length: 1004 [text/plain]
        Saving to: ‘test.sh’

        100%[=========================================================>] 1,004       --.-K/s   in 0s

        2016-02-23 18:39:52 (479 MB/s) - ‘test.sh’ saved [1004/1004]

        $ chmod 755 test.sh
        $ ./test.sh
        Test script for { Your movie site in just one minute }
        See http://bobbelderbos.com/2016/02/movie-site-in-minute-omdb-api-python/ for more info

        1. creating textfile my_movies_1456249202.txt with 10 movies in it

        2. importing required html template
        --2016-02-23 18:40:02--  https://raw.githubusercontent.com/bbelderbos/own_movie_site/master/template.html
        Resolving raw.githubusercontent.com... 185.31.18.133
        Connecting to raw.githubusercontent.com|185.31.18.133|:443... connected.
        HTTP request sent, awaiting response... 200 OK
        Length: 1362 (1.3K) [text/plain]
        Saving to: ‘template.html’

        100%[=========================================================>] 1,362       --.-K/s   in 0s

        2016-02-23 18:40:02 (433 MB/s) - ‘template.html’ saved [1362/1362]

        3. run the movie site creation script (via github)
        Done, 9 processed, created static html movie page: mymovies.html in 1 seconds

        4. open the generated html site in default browser (mac, other OS, click on generateed mymovies.html)

        _____________________________ 
        < Thanks bbelderb for testing >
        ----------------------------- 
                \   ^__^
                \  (oo)\_______
                    (__)\       )\/\
                        ||----w |
                        ||     ||


---

## Resulting page

![Resulting movie html page]({{ site.baseurl }}/assets/moviepage_result.png)

---

I hope you like it and feel free to leave any comment of feedback in the comments below.
