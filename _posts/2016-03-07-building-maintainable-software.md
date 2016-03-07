---
layout: post
title: 10 guidelines that will make you write more maintainable software
comments: True
summary: Review the book "Building Maintainable Software" which presents then guidelines to write better software. This is a very pratcial hands-on guide I will refer back to on a regular basis. Thanks Software Improvement Group.
categories: [Software Development]
tags: [coding, software, best practices, java, sig, development, maintainability, refactoring, guidelines]
image: building_maint_sw.png
---

### Building Maintainable Software

[Software Improvement Group](https://www.sig.eu/en) (SIG) recently released [Building Maintainable Software, Ten Guidelines for Future-Proof Code](https://www.sig.eu/en/building-maintainable-software). I am the happy owner of a signed copy for review :) 

![Signed copy of the book]({{ site.baseurl }}/assets/signed_book_copy.jpg)

In this post I will summarize the ten guidelines and look at some of my code to see where I improved and what I can do better. 

This short guide (134 pages, excl. appendix) is a compact guide to help you write maintainable code. Why is this important? Maintaining source code takes at least twice as long when maintainability is below average (as measured by SIG). Maintainable software can evolve! On the contrary, if code is not maintainable any changes to the codebase are considered too risky even leading to systems being written off before a 1.0 release. 

I think most important is that maintainability is not an afterthought, you need to start early and have the discipline to make every contribution (commit) count. The book mentions the "Boy Scouts" rule that says "leave the campground cleaner than you found it."

### The 10 guidelines

Each guideline has concrete / easy-to-understand Java code samples. At the end of each guideline chapter the author tries to take away common misunderstandings (e.g. "our domain is very complex, therefore hight code complexity is unavoidable") and shows how SIG rates the guidelines on real source code. It is really hands-on.

Without further ado, the guidelines. For each one I looked up some code and share what I learned:

#### 1. Write short units of code: limit the length of methods and constructors

> Shorter units are easier to analyze, test, and reuse.

Most of my refactoring falls into this code. The book prescribes a simple rule: methods of 15 lines or less.

I think I get better at which explains why I find more recent code easier to maintain :)

Before:

    $ python countMethodLines.py codesnippets/python/music_autofill.py 
    x)  auto_fill                 | 27 => need to refactor
    v)  path_exists_check         | 3
    v)  select_genres             | 3
    x)  parse_cli                 | 19 => same
    v)  list_mp3_files            | 7
    x)  get_mp3_data              | 23 => same
    v)  copy_mp3_to_usb           | 12
    v)  retrieve_cached_output    | 7
    v)  cache_outputs             | 6
    v)  __init__                  | 13

    $ python countMethodLines.py codesnippets/python/themoviedb_crawler.py
    v)  print_html                | 1
    v)  mail_html                 | 15
    v)  get_url                   | 6
    x)  get_digest                | 40 => too much going on here
    v)  write_html                | 4
    x)  __init__                  | 23 => refactor into smaller methods

Big methods usually mix different responsabilities, "get_digest" for example mixes data parsing and preparing html:

    def get_digest(self):
      self.html = "<div id='content' style='font: 85%/1.6 Verdana, sans-serif;'>"
      self.html += "<h1 style='background-color: #840015;color: #fff;'><a href='%s'><img src='%s/i/banner.jpg'></a></h1>" % (self.baseurl, self.baseurl)
      self.html += "<h4>%s</h4>" % self.digestTitle
      ..
          [urlstr, poster, title, score, genres, cast] = [var.decode('utf-8') for var in m.groups()]
          themoviedbUrl  = "%s%s" % (self.moviedb, urlstr)
          sharemoviesUrl = "%s%s" % (self.baseurl, urlstr)
          if self.genreFilter and not list(set(self.genreFilter).intersection(set(genres.lower().split(", ")))):
            continue
      ..

... so this should be broken apart: have a list or dict with all elements, then load in the html as template from storage (file) and populate placeholders with another class/method. At least 3 different methods. It is cool to see that pure metrics (LOC per method) reveals these kind of issues.

Lately I got the lines per method better (see also 7. / code balance)

    $ python countMethodLines.py countMethodLines.py 
    v)  print_line                | 5
    v)  get_method_name           | 1
    v)  count_method_len          | 14
    v)  line_is_comment           | 3
    v)  file2list                 | 3

I wrote countMethodLines.py for this post, it is for Python and should be further tested/ enhanced. You can get it [here](https://github.com/bbelderbos/Codesnippets/blob/master/python/countMethodLines.py). I might expand it to check other guidelines as well (if time).

#### 2. Write simple units of code: limit the number of branch points per method

> Units with fewer decision points are easier to analyze and test.

I think we have all experienced deep nesting if statements in our first programming attempts ;) 

I still get them occasionally when the architecture is not well defined upfront or requirements change dramatically. I hate ending up with code that has deep nesting, because it is inherently complex. 

The book has a great refactoring example of a switch statement (getFlagColors) to a Map data structure with a method to retrieve a flag from it. It comes down to splitting growing methods (size and nesting) into smaller methods.

#### 3. Write code once, rather than risk copying buggy code

> Duplication causes regression bugs and all kinds of issues as you have to update several pieces of code for each change, bad!

This is probably the easiest to grasp / fix, however I am surprised how often I see repetition of some kind.

Bad (very trivial example just to make a point):

    def do_sport():
      if day in weekend:
        print "wake up and go for a swim"
      else:
        print "wake up and go for a walk"

Imagine I want to say "wake up at 6am" for some reason. Now I need to update two lines.
So it is better to have the "wake up" in only one place:

    def go_out(activity):
      return "wake up and go for a " + activity

    def do_sport():
      print go_out("swim") if day in weekend else print go_out("walk")

Note that this also invites the shorter "" if ... else "" notation :)

Now waking up early only requires a chane in the go_out method:

    def go_out(activity):
      return "wake up at 6 am and go for a " + activity

I try to be ruthless when coding and address even trivial examples as above. Code needs to be DRY!

#### 4. Keep unit interfaces small by extracting parameters into objects

> Units with fewer parameters are easier to test and reuse.

A valuable lesson here is to keep list of parameters to a method small, I found this in my code which is relatively complex: 

    class BlogImporter(object):

      def __init__(self, url, poststart, postend, sitemap="sitemap.xml"):
        ..

.. why not passing in blog object that holds all the data, but only causes a single parameter to be passed along?

     ..
     def __init__(self, blog): # easier to maintain
      self.url = blog.url
      self.sitemap = blog.sitemap
      ..

#### 5. Separate concerns to avoid building large classes

> Loosely coupled modules (classes) are easier to modify and lead to a more modular system.

Keep classes small and limit he number of places where class is alled by code outside the calss itself.

#### 6. Couple architecture components loosely

> Same as last rule but at a higher level, strive for loose coupling, also on a component level

For example when you have classes Input -> Output -> Logging -> FileHandling -> XMLParsing -> etc. - make sure these components operate independently, passing the Logging object to all the other modules and vice versa creates more dependencies (is not loose coupling).

The book shows an example of the [abstract factory design pattern](https://en.wikipedia.org/wiki/Abstract_factory_pattern). TODO: find an example from my code for this one.

#### 7. Balance the number and size of top-level components in your code

> A well-balanced architecture of uniform size is most modular and enables easy modification through separation of concerns.

I think I get this better these days, compare an old project:

    $ wc -l safari/*py
     228 safari/safarinew.py

= all in one module / class, vs a newer project: 

    $ wc -l *py
      32 crawler.py
      34 linkparser.py
      36 main.py
      47 parsehtml.py
      19 stats.py
      41 store.py
      11 utils.py
     220 total

= number of top-level components.

Going back to the 15-line-per-method rule, checking this against the better balanced project I see even shorter methods: 

    $ for i in *py; do echo $i; python countMethodLines.py $i; done
    crawler.py
    v)  download                  | 12
    v)  __init__                  | 1
    linkparser.py
    v)  extract_links             | 7
    v)  _extract_sm               | 6
    v)  __init__                  | 5
    main.py
    parsehtml.py
    v)  strip_chars               | 3
    v)  get_followers             | 7
    v)  __init__                  | 8
    stats.py
    v)  __repr__                  | 4
    v)  __init__                  | 3
    store.py
    v)  save                      | 4
    v)  has_key                   | 4
    v)  retrieve                  | 7
    v)  __init__                  | 1
    utils.py
    v)  file_to_list              | 4
    v)  __init__                  | 1

I will confirm but when touching this code (maybe in a couple of weeks or months) it should be painless.

#### 8. Keep your codebase as small as possible

> A large system is difficult to maintain, because more code needs to be analyzed, changed and tested.

I have not a quick example of this, because most projects for this blog are relatively small, but I know from experience that the bigger the codebase the more complex it gets. I also am conscious what goes into the code base, sometimes whole components/subdirectories justify a seperate project (version control) and should be separated.

#### 9. Automate tests for your codebase

> Manual tests do not scale. Automated tests enable near-instantaneous feedback on the effectiveness of modifcations.

Here I need to get a bit more into the TDD-habit yet. I have been adding tests being late in the development cycle, ideally you do this when writing the code or even drive your design by testing, because you get in the habit of thinking about how your code can be tested. I can confirm that the inmediate feedback and safety net of a regression suite, makes you less afraid to make changes which often is required on active projects.

#### 10. Write clean code, avoiding code smells that indicate deeper problems

> Watch out for dead code and outdated comments. Good code documents itself.

True, I still use comments to document not so obvious things, but you should wonder: if it requires comments, shouldn't it be refactored / redesigned? And yes, uncommented code leads to confusion (no worries, git still has copies of everything!) and comments tend to get outdated only adding up to the confusion of the ones that need to maintain the code.

For example you could make this more explanatory: 

    ..
      for li in lines:
      ...
        # ignore blank lines or lines that start with comments
        if not li or li.startswith("#"):
          continue

... by creating a method: 

    def ignore_line(li):
      if not li.strip():
        return True 
      if li.startswith("#"):
        return True
      return False

    ..
      for li in lines:
        if ignore_line(li):
          continue 

This has the additional advantage of controlling the "ignore lines" logic in one place so you can easily add more conditions. It takes some more lines of code, but it is all about keep it maintainable.

See [my reading page]({{ site.baseurl }}/books) for other good books on software quality.

---

And that's it: 10 simple guidelines, however just so much for reading, this is a book to go back to from time to time to make sure this becomes second nature.

### Resources

* Check out the [book's page](https://www.sig.eu/en/building-maintainable-software)
* You can certify in this! Check out [Quality Software Developer Foundation Certificate in Maintainability](https://www.sig.eu/en/services/trainingcertification/).
* There is a [video training](https://player.oreilly.com/videos/9781491950791) available as well.
* Article: [Why Measuring Code Quality Matters](https://www.sig.eu/en/about-sig/blogs/why-measuring-code-quality-matters/).
* Software Improvement Group: [About SIG](https://www.sig.eu/en/about-sig).
