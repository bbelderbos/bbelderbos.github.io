---
layout: post
title: Your movie site in just one minute
comments: True
summary: Rewrite/improvement of my popular script/post "Your own movie database in 5 minutes with IMDb API and Perl"
tags: [imdb, omdb, movies, api, python, coding, html, css, perl]
---

This is a rewrite/improvement of my popular script/post [Your own movie database in 5 minutes with IMDb API and Perl](http://bobbelderbos.com/2011/11/movie-database-imdb-api-perl/) that got (and still gets) quite some visits every day. I rewrote the code in Python, took out the DB dependency (goal was a static site anyways) and documented the steps.

**Disclaimer:** this is quick and dirty. If you want to build a a real movie site, use something more powerful like [themoviedb](http://themoviedb.org), I used that A. to build [sharemovi.es](http://bobbelderbos.com/2012/07/new-release-sharemovies-design-features/) and B. create a [weekly movie email script](http://bobbelderbos.com/2015/11/project-weekly-movie-email-with-tmdbsimple-python/). So keep that in mind when reading this and if you decide to use it.

## Steps

You don't have to create any text files unless you want to use your own set of movies, all files are in [this github repo](https://github.com/bbelderbos/own_movie_site).

1. copy and paste top 250 movies from [imdb](http://www.imdb.com/chart/top) and put in file called inimdb-top-rated.txt file (or use your own but use the same syntax: movie,year)

        $ head  imdb-top-rated.txt 
        1. The Shawshank Redemption (1994)  9.2   
        2. The Godfather (1972)   9.2   
        3. The Godfather: Part II (1974)  9.0   
        4. The Dark Knight (2008)   8.9   
        5. Pulp Fiction (1994)  8.9   


2. normalize the data to title,year:

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


3. run the python script that queries [omdb](http://omdbapi.com/) for movie info returning a nice html page. OK, 2% not found, I can live with that, look at the runtime :)

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


4. see example output by opening topmovies.html output file in the browser (edit CSS in this file to your liking).

---

I hope you like it and feel free to leave any comment of feedback in the comments below.
