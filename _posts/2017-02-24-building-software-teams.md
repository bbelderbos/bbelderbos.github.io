---
layout: post
title: Building Software Teams, best practices for effective development
comments: True
summary: SIG published a new book that lays out ten best practices for facilitating a team of software developers, enabling them to develop high-quality code.
categories: [Software Quality]
tags: [sig, development, books, CI, testing, automation, documentation, version conrol, git, python]
image: building-software-teams.jpg
crosspost_to_medium: true
---

> You Can’t Control What You Can’t Measure - Tom DeMarco

After [Building Maintainable Software](http://bobbelderbos.com/2016/03/building-maintainable-software/), [Software Improvement Group (SIG)](https://www.sig.eu) published a follow-up work focusing on development of quality software as a team.

<h3>Building Software Teams</h3>

This short volume (136 pages) covers quite a lot. Similar to the previous book I like the practical format of Best practice short summary -> Motivation -> How to -> Measuring / Controlling -> Objections -> Metrics.

The order of the guidelines / chapters makes sense: first you need version control, tests and development environments before you can automate the process (CI, deployment).

The first chapters take a bit of effort to go through, they are quite theoretical, however it gets more fun starting chapter 4 where concrete building blocks get introduced, starting with version control.

---

<h3>A summary / digest of the book</h3>

* Chapter 1 - Introduction

	Software quality is measurable. Motivation and outline of the 10 best practices.

* Chapter 2 - Derive Metrics from Your Measurement Goals

	Not only should we measure, we should measure the right things. This chapter explains the [goal, question, metric or GQM approach](https://en.wikipedia.org/wiki/GQM) SIG uses, a technique used in subsequent chapters. Asking the right questions you get to metrics like 80% of unit test coverage for example or [McCabe unit complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity) below 5 for 75% of the code base.

* Chapter 3 - Make Definition of Done Explicit

	Define specific [SMART](https://en.wikipedia.org/wiki/SMART_criteria) objectives. For example, commits / builds without errors, 80+% test coverage, no TODOs left in code comments. In Python you could define things as: each function/ method has a docstring or compliance with the [PEP8 code style guide](http://pybit.es/pep8.html).

* Chapter 4 - Control Code Versions and Development Branches

	The day I started using git I instantly became a happier programmer: nothing gets lost, undo anything, you can branch your development, committing == documenting. With time you get smarter about your commits (less code per commit, more verbose commit message) and learn to deal with (or avoid) merge conflicts. Example SIG metrics: average branch lifespan, commit frequency, average issue resolution time. Parse your git log ...

	Surprisingly only 41% of development teams has version control "Fully applied", which is mainly due to branching complexity! Later chapters also showed quite low percentages on being fully compliant with other metrics. I'm curious if it's lack of knowledge or business context (real-life complexity) that prevents a higher compliance ratio ...

* Chapter 5 - Control Development, Test, Acceptance, and Production Environments

	This can be a challenging one: how to deal with different environments (phases): Development, Test, Acceptance, Production (DTAP). Important here: proper encapsulation (access), only push to next environment if all tests pass, make environments as similar as possible. Example GQM model (metrics): average time in each development phase, number of work items (backlog) in each phase, sum created vs resolved issues.

* Chapter 6 - Automate Tests

	This is one of my favorites. Testing creates your safety net = easier refactoring = keep your code base sane. As you want to run your tests often automation is a logical next step.

	Automated testing catches errors early reducing the number of bugs. SIG stipulates that good tests have sufficient coverage, change/grow with the code (maintenance code == maintenance tests) and are isolated (test one functionality per test). The latter has the additional benefit of better (function) API design.

	Metric examples: overall coverage (80+%), number of pass vs failed tests (number of regressions), runtime per unit test, manual test time (per development phase).

	Again still some progress to be made in the field: although the majority of measured teams has a test strategy defined, only 13% (!) have "Fully applied" (automated) requirements testing in place

	I leave the metrics out from here on to focus on the book's content.

* Chapter 7 - Use Continuous Integration (CI)

	Using a CI server gives you the ability to run your tests automatically and get instant feedback. Automation means: speed up bug fixing as issues are spotted early, reliability (humans can forget to run tests or skip them). It also enables automated deployment (Chapter 8).

	Note that this is only possible if you have automated tests, version control, a CI server and automated builds to start with. Metric examples: commit feedback time, build and test run time.

* Chapter 8 - Automate Deployment

	This chapter is quite similar to the last one. The automation benefits listed there equally apply here. Metric examples: deployment time, total saved time, reliability of deployment process (number of issues).

* Chapter 9 - Standardize the Development Environment

	Standardization means more predictability of development work and enforce best practices. Sharing a common coding style for example makes it easier to collaborate (e.g. [PEP8 for Python](https://medium.com/@bbelderbos/python-programmers-please-use-pep8-661036de6731#.c4dujyw6g)). How do you measure code quality as a team? Do you have uniformity in the tools / development environment (OS, version control software, particular test / deployment utilities, etc). Example metrics: code linters (= number of code style / quality violations), quality of standards (fairness / adherence).

* Chapter 10 - Manage Usage of Third-Party Code

	Using third-party code (libraries or frameworks) saves time and effort. In Python land a good example is [Requests](http://docs.python-requests.org/en/master/): one of the most downloaded packages of all time. It hides a lot of complexity behind a simple and elegant API, unlike other HTTP libraries. For web development you can bootstrap your app with [Django](https://www.djangoproject.com/). Building an API is quite easy with [Flask](http://flask.pocoo.org/). Metric examples: level of maintenance / commitment of libraries (number of contributors / contributions), time (or LOC) saved using the library vs learning curve or writing something from scratch.

* Chapter 11 - Document Just Enough

	Writing good documentation seems the most underrated development task, yet when doing it consistently and keeping it current, it reaps huge rewards (and satisfaction). It's an important metric to label a project professional and usable. It can explain the why of certain design decisions and sets expectation for the interface (API reference). Documentation does require active maintenance and discipline though. Example metrics: time spent on documentation, quality, completeness, conciseness, being current.

* Chapter 12 - Next Steps

	Final chapter with quick recap. Being persistent as a team is really important. You also want to move gradually, one guideline at the time. As stated earlier there are dependencies to be met. If you have nothing in place, start with version control and standardization. If no tests, build a test suite first, then automate. Then tweak automation further by using a CI server for your builds. From there you can opt for automatic deployments. SIG recommends one step at a time though.

---

<h3>A note from my experience</h3>

Personally standardization, version control, testing, a solid deployment process, and documentation have been invaluable to grow from a single developer to a small software team.

This book gives you a good foundation, but of course you have to translate it into practice and be persistent (patient) at it.

Although every business is different, these techniques are generic enough to be applicable across the board. There is a direct link between these practices and quality code and a development process that is compliant with industry standards and best practices.

<div id="instantPreviewRight">
  <iframe type="text/html" width="336" height="550" frameborder="0" allowfullscreen style="max-width:100%" src="https://read.amazon.com/kp/card?asin=149195177X&preview=inline&linkCode=kpe&ref_=cm_sw_r_kb_dp_IjQ3wb0SZJMN1&tag=bobbeld-20" ></iframe>
</div>

---

<h3>Not convinced? Some more reasons</h3>

* [Software Is Eating The World](https://www.wsj.com/articles/SB10001424053111903480904576512250915629460), increasingly critical life functions run on code. I wrote about this [here](http://bobbelderbos.com/2016/07/certified-software-quality/). Hence software quality is key but so is development as a team. Products grow in size and complexity and are rarely maintained by just one developer (even so this developer probably wants to automate his/her tests and deployment ...)

* With the growth of open source and Github, development happens in a distributed / asynchronous manner, the practices in this book can make this process more agile.

* What gets measured gets managed (Peter Drucker). Defining metrics helps to stay focussed.

* There are a lot of books on this subject, however I like the fact SIG speaks from a vast amount of experience: they analyze a ton of code in their daily consultancy practice. Thanks SIG for sharing this knowledge with the community. A lot of learning compressed in a compact and accessible book.

* Automated testing, quality documentation, version control, these are common best practices in today's software industry. This alone is reason enough to read this book and think how to apply these guidelines in your role as software developer or manager of a software team.

---

<h3>Reference material</h3>

* SIG is generous: you can download a free copy [on their website](https://www.sig.eu/lp/building-software-teams/) or buy a hardcopy on [O'Reilly](http://shop.oreilly.com/product/0636920048565.do) or [Amazon](https://www.amazon.com/Building-Software-Teams-Practices-Development/dp/149195177X).

* There is also an [O'Reilly video training](https://player.oreilly.com/videos/9781491970690) available.

* You will be able to certify in this sometime this year. Pending link here.

* Improve your individual coding skills with the companion book [Building Maintainable Software](https://www.sig.eu/insight/building-maintainable-software/). You can read my review of this book [here](http://bobbelderbos.com/2016/03/building-maintainable-software/).

* Software Improvement Group (SIG) [homepage](https://www.sig.eu)

<h3>Your experience?</h3>

I hope you liked this review. Feel free to share your experience in the comments below.
