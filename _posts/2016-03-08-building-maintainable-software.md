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

[Software Improvement Group](https://www.sig.eu/en) (SIG) recently released [Building Maintainable Software, Ten Guidelines for Future-Proof Code](https://www.sig.eu/en/building-maintainable-software). In this post I will summarize the ten guidelines and look at some of my code to see where I improved and what I can do better. 

<div id="instantPreviewRight">
  <iframe type="text/html" width="336" height="550" frameborder="0" allowfullscreen style="max-width:100%" src="https://read.amazon.com/kp/card?asin=B01B6WS86I&preview=inline&linkCode=kpe&ref_=cm_sw_r_kb_dp_IjQ3wb0SZJMN1&tag=bobbeld-20" ></iframe>
</div>

This short guide (134 pages, excl. appendix) is a compact guide to help you write maintainable code. It also serves as preparation for the [Quality Software Developer Foundation Certificate in Maintainability](https://www.sig.eu/en/services/trainingcertification/).

Why is maintainability important? Maintaining source code takes at least twice as long when maintainability is below average (as measured by SIG). If code is not maintainable changes to the codebase are risky and easily introduce bugs. This can even lead to the system being written off before initial release. 

I think the most important lesson is that maintainability is not an afterthought: you need to start early and have the discipline to make every contribution (commit) count. The book mentions the "Boy Scouts" rule that says "leave the campground cleaner than you found it."

### The 10 guidelines

Each guideline has concrete / easy-to-understand Java code samples. At the end of each guideline chapter the author tries to take away common misunderstandings (statements like "our domain is very complex, therefore hight code complexity is unavoidable") and shows how SIG rates the guidelines on real source code. It is really hands-on.

Without further ado, the guidelines. I tried to link to my own code to better commit the concepts to muscle memory:

#### 1. Write short units of code (Chapter 2)

> Shorter units (that is, methods and constructors) are easier to analyze, test, and reuse.

Most of my refactoring falls into this guideline I think. The book prescribes a simple rule: methods of 15 lines or less.

I think I get better at this which explains why I find more recent code easier to maintain :)

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

I (quickly) wrote countMethodLines.py for this post, it targets Python code. If you want to play with it, grab it [here](https://github.com/bbelderbos/Codesnippets/blob/master/python/countMethodLines.py). I might expand it to check other guidelines as well ...

Big methods usually mix different responsibilities, the get_digest method above for example mixes data parsing and preparing html:

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

So this should be broken apart into two or more methods. It is cool to see how metrics (LOC per method) reveal these kind of issues.

In the very countMethodLines.py script I improved the LOC per method (see also 7. / code balance)

    $ python countMethodLines.py countMethodLines.py 
    v)  print_line                | 5
    v)  get_method_name           | 1
    v)  count_method_len          | 14
    v)  line_is_comment           | 3
    v)  file2list                 | 3

#### 2. Write simple units of code (Chapter 3)

> Units with fewer decision points are easier to analyze and test.

I think we have all experienced deep nested if statements in our first programming attempts ;) 

I still get them occasionally when the architecture is not well defined upfront or requirements change dramatically in the process. I hate ending up with code that has deep nesting, because it is inherently complex. 

The book has a great refactoring example of a switch statement (getFlagColors) to a Map data structure with a method to retrieve a flag from it. It comes down to splitting growing methods (size and nesting) into smaller methods. Hence it overlaps with the previous guideline.

#### 3. Write code once (Chapter 4)

> Duplication of source code should be avoided at all times, since changes will need to be made in each copy. Duplication is also a source of regression bugs.

This is probably the easiest to grasp / fix, however I am surprised how often I see repetition of some kind when I look at code.

Bad (very trivial example just to make a point):

    def do_sport():
      if day in weekend:
        print "wake up and go for a swim"
      else:
        print "wake up and go for a walk"

Imagine I want to say "wake up at 6am" for some reason. Now I need to update two print statements.
So it is better to have the "wake up" in only one place:

    def go_out(activity):
      return "wake up and go for a " + activity

    def do_sport():
      print go_out("swim") if day in weekend else print go_out("walk")

Note that this also invites the shorter "" if ... else "" notation for compactness :)

Now waking up early only requires a change in the go_out method:

    def go_out(activity):
      return "wake up at 6 am and go for a " + activity

I try to be ruthless when coding and address even trivial examples as above. Get rid of "code smell", keep it DRY!

#### 4. Keep unit interfaces small (Chapter 5)

> Units (methods and constructors) with fewer parameters are easier to test and reuse.

A valuable lesson here is to keep list of parameters to a method small, I found this in my code which is relatively complex: 

    class BlogImporter(object):

      def __init__(self, url, poststart, postend, sitemap="sitemap.xml"):
        ..

Why not passing in blog object that holds all the data, but only causes a single parameter to be passed along?

     ..
     def __init__(self, blog):
      self.url = blog.url
      self.sitemap = blog.sitemap
      ..

#### 5. Separate concerns in modules (Chapter 6)

> Modules (classes) that are loosely coupled are easier to modify and lead to a more modular system.

This guideline can be applied by splitting classes to separate concerns. For example in the earlier moviedb crawler example different responsibilities were in one class:

    $ python countMethodLines.py codesnippets/python/themoviedb_crawler.py
    v)  print_html                | 1
    v)  mail_html                 | 15
    v)  get_url                   | 6
    x)  get_digest                | 40 
    v)  write_html                | 4
    x)  __init__                  | 23

We should split these functionalities into different classes: GetData(), ParseData(), CreateOutput(), PrintOutput(), MailOutput(). This makes it more modular. Also note that I kept the class names generic so when we decide to print/mail plain text instead of html it is easy to add.

In a more recent project I did this better: 

    $ wc -l *py
       52 book.py
       27 crawler.py
       27 mail.py
       68 main.py
       34 store.py
       28 utils.py
      236 total

#### 6. Couple architecture components loosely (Chapter 7)

> Top-level components of a system that are more loosely coupled are easier to modify and lead to a more modular system.

For example when you have classes Input -> Output -> Logging -> FileHandling -> XMLParsing -> etc. - make sure these components operate independently, passing the Logging object to all the other modules and vice versa creates more dependencies (is not loose coupling). Keep interfaces on a high level of abstraction to avoid components knowing too much about the implementation details (and thus become too interdependent). The book shows an example of the [abstract factory](https://en.wikipedia.org/wiki/Abstract_factory_pattern) which is described as a design pattern that successfully limits the amount of interface code exposed by a component.

#### 7. Keep architecture components balanced (Chapter 8)

> A well-balanced architecture, with not too many and not too few components, of uniform size, is the most modular and enables easy modification through separation of concerns.

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

= a number of more or less balanced top-level components.

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

Updating this codebase will be much easier! Cool how improvement of one guideline leads to improvement in another one.

#### 8. Keep your codebase small (Chapter 9)

> A large system is difficult to maintain, because more code needs to be analyzed, changed and tested. Also maintenance productivity per line of code is lower in a large system than in a small system.

I have not a quick example of this, because most projects for this blog are relatively small, but I know from experience that the bigger the codebase the more complex it gets. This guideline recommends to not copy and paste code, refactor existing code, and use third-party libraries and frameworks to avoid unnecessary over-engineering.

#### 9. Automate development pipeline and tests (Chapter 10)

> Automated tests (that is, test that can be executed without manual intervention) enable near-instantaneous feedback on the effectiveness of modifications. Manual tests do not scale.

Here I need to get a bit more into the TDD-habit yet. I have been adding tests being late in the development cycle, ideally you do this when writing the code or even drive your design by testing, because you get in the habit of thinking about how your code can be tested. The immediate feedback and safety net of a regression suite, makes you less afraid to make changes which is an important requirement with ever-changing business rules.

#### 10. Write clean code (Chapter 11)

> Having irrelevant artifacts such as TODOs and dead code in your codebase makes it more difficult for new team members to become productive. Therefore, it makes maintenance less efficient.

True, I still use comments to document not so obvious things, but you should wonder: if it requires comments, shouldn't it be refactored / redesigned? Especially commented code can be very confusing. No worries: git still has copies of everything! More importantly long comments don't tend to stay up2date with code changes turning well-intended comments into lies. 

For example you could make the following more explanatory by creating a method with a meaningful name: 

Old: 

    ..
      for li in lines:
      ...
        # I need a 2 line comment here to explain
        # the line below because it is very complex
        if some very complex conditions with && and || blabla:
          continue

New:

    def new_method(arg):
      if blabla:
        return True
      elif blabla:
        return True
      return False

    ..
      for li in lines:
        if new_method(arg):
          continue 

Apart from taking away the need for commenting you got the complex logic in a method which is now easier to change or expand. Yes, it adds some lines of code, but I rather pay in length than having code that is harder to read and maintain.

---

And that's it: 10 simple guidelines. Reading about them however only helps you so much, the real benefit comes from reminding yourself on a daily basis as you code. It should become an attitude, a way of crafting software. As with everything: practice, practice a lot and this will become second nature.

I am the happy owner of a signed copy I got for this review :) 

![Signed copy of the book]({{ site.baseurl }}/assets/signed_book_copy.jpg)

### Resources

* Check out the [book's page](https://www.sig.eu/en/building-maintainable-software)
* As said this book is preparation for the [Quality Software Developer Foundation Certificate in Maintainability](https://www.sig.eu/en/services/trainingcertification/).
* There is an accompanying [video training](https://player.oreilly.com/videos/9781491950791) available as well.
* Article: [Why Measuring Code Quality Matters](https://www.sig.eu/en/about-sig/blogs/why-measuring-code-quality-matters/).
* Software Improvement Group: [About SIG](https://www.sig.eu/en/about-sig).
* See [my reading page]({{ site.baseurl }}/books) for more books on software quality.
