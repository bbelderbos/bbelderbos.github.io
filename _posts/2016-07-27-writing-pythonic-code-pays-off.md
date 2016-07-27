---
layout: post
title: Writing Pythonic code pays off
comments: True
summary: In this post I will show you an example of non-Pythonic vs. Pythonic code. The latter is more concise and readable thus more maintainable. We will see two nice tricks, the negative list index stride, and optional key arg of the max builtin. These two language features aid us in writing more Pythonic code. Enjoy ...
categories: [Python]
tags: [Python, tricks, idioms, Pythonic, cleancode]
image: pythonic_code.png
crosspost_to_medium: true
---

## Pythonic == easier to read / maintain

In video 6: "Problem solving using more than one solution method" of [Intermediate Python programming](https://www.safaribooksonline.com/library/view/intermediate-python-programming) I stumbled upon a great example of less vs. more Pythonic code. 

I like to post this example here to demonstrate that Pythonic code is so much easier to read and maintain (not to mention the satisfaction of writing it!). 

Although I was already familiar with [reversing a list by using -1 as stride](http://stackoverflow.com/questions/509211/explain-pythons-slice-notation), it was a great reminder that language idioms matter. It makes your code more concise. It leads to more readable code. And more readable code equals more maintainable code!

I posted the example (with explanation and extension) in [this notebook](https://github.com/bbelderbos/python_notebooks).

## Summary:

![palindrome notebook]({{ site.baseurl }}/assets/palindrome1.png)

![palindrome notebook]({{ site.baseurl }}/assets/palindrome2.png)

![palindrome notebook]({{ site.baseurl }}/assets/palindrome3.png)

This is where the training video ended. I made two additions: 

- A. use max with key=len to get the longest palindrome, and

![palindrome notebook]({{ site.baseurl }}/assets/palindrome4.png)

- B. wrap the two pieces of functionalities in two methods. 

![palindrome notebook]({{ site.baseurl }}/assets/palindrome5.png)

One note on naming. Uncle Bob has a [great video on naming](https://cleancoders.com/episode/clean-code-episode-2/show). One subtle trick is to name boolean methods as is_, so is_palindrome makes you expect a boolean being returned. Which is useful as Python (unlike Java for example) does not force you to specify the return type. get_longest_palindrome clearly expresses the intent to retrieve one value, the longest palindrome. Naming is communication!

## Conclusion:

The initial code cannot be considered Pythonic, the final code can be in my opinion. 

We achieved a couple of things:

- the code is shorter (from 8 to 4 lines)
- the code is more readable and maintainable (using methods that express their intent)
- we can be at pease: we have used two neat language features, making the code more concise
- last but not least, it feels great writing Pythonic code :)

---

If you liked this post consider joining my new [Python Facebook group](https://www.facebook.com/groups/1305028816183522/) to learn some more Python together ...
