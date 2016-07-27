---
layout: post
title: 10 cool Python tricks for more elegant code
comments: True
summary: I have been reading Python Cookbook 3rd ed. It is full of useful tips and tricks to write better Python code. In this post I share some things I have learned, some have become daily good practices making my code better.
categories: [Python]
tags: [Python, cookbook, tricks, idioms]
image: python_tricks.png
---

I am halfway through [Python Cookbook, 3rd Edition](http://shop.oreilly.com/product/0636920027072.do) and I already took quite some notes. The following 10 tricks I find pretty useful in my daily Python work. I also added a few I stumbled upon lately. 

### 1. Use collections 

This really makes your code more elegant and less verbose, a few examples I absorbed this week:

Named tuples:

    >>> Point = collections.namedtuple('Point', ['x', 'y'])
    >>> p = Point(x=1.0, y=2.0)
    >>> p
    Point(x=1.0, y=2.0)

Now you can index by keyword, much nicer than offset into tuple by number (less readable)

    >>> p.x
    1.0
    >>> p.y
    2.0

Elegantly used when looping through a csv:

    with open('stock.csv') as f:
        f_csv = csv.reader(f)
        headings = next(f_csv)
        Row = namedtuple('Row', headings)
        for r in f_csv:
            row = Row(*r) # note the star extraction
            # ... process row ...


I like the unpacking star feature to throw away useless fields: 

    line = 'nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false'
    >>> uname, *fields, homedir, sh = line.split(':')
    >>> uname
    'nobody'
    >>> homedir
    '/var/empty'
    >>> sh
    '/usr/bin/false'

Superconvenient: the defaultdict: 

    from collections import defaultdict
    rows_by_date = defaultdict(list)
    for row in rows:
        rows_by_date[row['date']].append(row)",

Before I would init the list each time which leads to needless code:
    
    if row['date'] not in rows_by_date:
      rows_by_date[row['date']] = []

You can use OrderedDict to leave the order of inserted keys:

    >>> import collections
    >>> d = collections.OrderedDict()
    >>> d['a'] = 'A'
    >>> d['b'] = 'B'
    >>> d['c'] = 'C'
    >>> d['d'] = 'D'
    >>> d['e'] = 'E'
    >>> for k, v in d.items():
    ...     print k, v
    ... 
    a A
    b B
    c C
    d D
    e E

Another nice one is Counter:

    from collections import Counter
    words = [
      'look', 'into', 'my', 'eyes', 'look', 'into', 'my', 'eyes',
      'the', 'eyes', 'the', 'eyes', 'the', 'eyes', 'not', 'around', 'the',
      'eyes', ""don't"", 'look', 'around', 'the', 'eyes', 'look', 'into',
      'my', 'eyes', ""you're"", 'under'
    ]
    word_counts = Counter(words)
    top_three = word_counts.most_common(3)
    print(top_three)
    # Outputs [('eyes', 8), ('the', 5), ('look', 4)]",

Again, before I would write most_common manually. Not necessary, this is all done already somewhere in the stdlib :)

### 2. sorted() accepts a key arg which you can use to sort on something else

Here for example we sort on surname: 

    >>> sorted(names, key=lambda name: name.split()[-1].lower())
    ['Ned Batchelder', 'David Beazley', 'Raymond Hettinger', 'Brian Jones']


### 3. Create XMl from dict

Creating XML tags manually is usually a bad idea, I bookmarked this simple dict_to_xml helper: 

    from xml.etree.ElementTree import Element

    def dict_to_xml(tag, d):
        '''
        Turn a simple dict of key/value pairs into XML
        '''
        elem = Element(tag)
        for key, val in d.items():
            child = Element(key)
            child.text = str(val)
            elem.append(child)
        return elem"

### 4. Oneliner to see if there are any python files in a particular directory

Sometimes 'any' is pretty useful:

    import os
    files = os.listdir('dirname')
    if any(name.endswith('.py') for name in files):


### 5. Use set operations to match common items in lists

    >>> a = [1, 2, 3, 'a']
    >>> b = ['a', 'b', 'c', 3, 4, 5]
    >>> set(a).intersection(b)
    {3, 'a'}

### 6. Use re.compile

If you are going to check a regular expression in a loop, don't do this:

    for i in longlist:
      if re.match(r'^...', i)

yet define the regex once and use the pattern:

    p = re.compile(r'^...')
    for i in longlist: 
      if p.match(i)

### 7. Printing files with potential bad (Unicode) characters

The book suggested to print filenames of unknown origin, use this convention to avoid errors:

    def bad_filename(filename):
        return repr(filename)[1:-1]

    try:
        print(filename)
    except UnicodeEncodeError:
        print(bad_filename(filename))

Handling unicode chars in files can be nasty because they can blow up your script. However the logic behind it is not that hard to grasp. A good snippet to bookmark is the encoding / decoding of Unicode: 

    >>> a
    'pýtĥöñ is awesome\n'
    >>> b = unicodedata.normalize('NFD', a)
    >>> b.encode('ascii', 'ignore').decode('ascii')
    'python is awesome\n'

O'Reilly has a course on [Working with Unicode in Python](http://shop.oreilly.com/product/0636920049067.do).

### 8. Print is pretty cool (Python 3)

I am probably not the only one writing this kind of join operations:

    >>> row = ["1", "bob", "developer", "python"]
    >>> print(','.join(str(x) for x in row))
    1,bob,developer,python

Turns out you can just write it like this: 

    >>> print(*row, sep=',')
    1,bob,developer,python

Note again the * unpacking.

### 9. Functions like sum() accept generators / use the right variable type

I wrote this at a conference to earn me a coffee mug ;)

    sum = 0
    for i in range(1300):
        if i % 3 == 0 or i % 5 == 0:
            sum += i
    print(sum)

Returns 394118, while handing it in I realized this could be written much shorter and efficiently: 

    >>> sum(i for i in range(1300) if i % 3 == 0 or i % 5 == 0)
    394118

A generator: 

    lines = (line.strip() for line in f)

is more memory efficient than: 

    lines = [line.strip() for line in f] # loads whole list into memory at once

And concatenating strings is inefficient:

    s = "line1\n"
    s += "line2\n"
    s += "line3\n"
    print(s)

Better build up a list and join when printing:

    lines = []
    lines.append("line1")
    lines.append("line2")
    lines.append("line3")
    print("\n".join(lines))

Another one I liked from the cookbook: 

    portfolio = [
      {'name':'GOOG', 'shares': 50},
      {'name':'YHOO', 'shares': 75},
      {'name':'AOL', 'shares': 20},
      {'name':'SCOX', 'shares': 65}
    ]
    min_shares = min(s['shares'] for s in portfolio)

One line to get the min of a numeric value in a nested data structure :)

### 10. Enumerate lines in for loop

You can number lines (or whatever you are looping over) and start with 1 (2nd arg), this is a nice debugging technique

    for lineno, line in enumerate(lines, 1): # start counting at 0
        fields = line.split()
        try:
            count = int(fields[1])
            ...
        except ValueError as e:
            print('Line {}: Parse error: {}'.format(lineno, e))

This is the tip of the iceberg. The second half of the book goes into more advanced concepts. I probably do one or more follow-up posts as I keep learning more Python goodness :)

The best you can do is take a topic and write code in it. I used defaultdict, Counter, and named tuples in one script and was thrilled it was so much shorter and elegant, but above all you commit it to muscle memory. 

Have fun! Thanks for reading.
