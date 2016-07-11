---
layout: post
title: Analyzing Brexit data with Pandas
comments: True
summary: I wanted to learn Pandas for quite some time. As usual on this blog I start with a practical exercise / goal, UK's EU referendum, and use (and learn) Pandas to analyze the results. I included the UK census data in my analysis which led to some interesting findings.
categories: [Data Science]
tags: [pandas, numpy, matplotlib, brexit, data, analysis, mining, scatterplot]
image: pandas_brexit_data.png
---

Since quite some time I wanted to learn [Pandas](http://pandas.pydata.org). Finally I grabbed a recent opportunity: Brexit = data.

As usual I started with a practical exercise / objective. I used Pandas to analyze the CSV data published by [electoralcommission.org.uk](http://www.electoralcommission.org.uk/find-information-by-subject/elections-and-referendums/upcoming-elections-and-referendums/eu-referendum/electorate-and-count-information).

Although I wanted to answer more questions, this CSV was enough to get my feet wet with Pandas (it's huge!). Moreover I learned to use [Jupyter notebook](http://jupyter.readthedocs.io/en/latest/) to document my progress. You can [see / download the notebook at Github](https://github.com/bbelderbos/brexit-pandas/blob/master/Analyze_Brexit_Pandas_EN.ipynb).

I achieved my goal of representing the data shown [here](https://ig.ft.com/sites/elections/2016/uk/eu-referendum/index.html). Here are some screenshots of the notebook:

---

![notebook_screenshot1]({{ site.baseurl }}/assets/notebook_screenshot1b.png)

...

---

![notebook_screenshot2]({{ site.baseurl }}/assets/notebook_screenshot2.png)

...

---

![notebook_screenshot3]({{ site.baseurl }}/assets/notebook_screenshot3b.png)

...

---

![notebook_screenshot4]({{ site.baseurl }}/assets/notebook_screenshot4.png)

...

---

### Adding demographics

I matched the data with publicly available [census data](http://www.ons.gov.uk/census/2011census/2011censusdata) (as suggested by [Pybonacci](https://twitter.com/Pybonacci), thanks). I found some cool correlations (and learned quite some matplotlib along the way), see the full notebook [here](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb):

#### How does age influence the leave / remain vote?

![median_age.png]({{ site.baseurl }}/assets/median_age.png)

#### How does unemployment influence?

![perc_unemployed.png]({{ site.baseurl }}/assets/perc_unemployed.png)

#### How does higher education influence?

![perc_high_education.png]({{ site.baseurl }}/assets/perc_high_education.png)

#### And how does being born outside UK influence?

![perc_born_outside_uk.png]({{ site.baseurl }}/assets/perc_born_outside_uk.png)

Clearly elderly people and areas with a higher unemployment rate tend to vote for "Leave". On the other hand, areas with a higher percentage of highly educated people, and regions with more people born outside the UK, (generally) prefer that UK remains in the EU. 

Again, to see how I got to these results with Pandas you can see the full notebook [here](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb).

### And last but not least: income data by region

Income data was harder to get from the [standard census data](http://webarchive.nationalarchives.gov.uk/20160105160709/http://www.ons.gov.uk/ons/publications/re-reference-tables.html?edition=tcm%3A77-286262) so I used [this link](https://www.gov.uk/government/statistics/income-and-tax-by-county-and-region-2010-to-2011) to check the relation of median income on voting. I found an interesting pattern:

![median_income.png]({{ site.baseurl }}/assets/median_income.png)

(the parsing of the data is documented in the [same notebook](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb))

We can clearly see that regions with a relatively smaller median income are more in favor of leaving the EU, although it is not 100% consistent: Northen Ireland has a lower median income but voted Remain, South East has a higher median income but wants to leave. Interesting though how general trends become visible by merging different data sets.

<h3>Reference links to learn Pandas</h3>

* [Pandas home and docs](http://pandas.pydata.org)
* [Python’s pandas make data analysis easy and powerful with a few lines of code](https://www.oreilly.com/learning/pythons-pandas-make-data-analysis-easy-and-powerful-with-a-few-lines-of-code?imm_mid=0e520d&cmp=em-prog-na-na-newsltr_20160625) - short and easy tutorial to start.
* [Python for Data Analysis](https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/) - book by Panda's creator Wes McKinney.
* [Introduction to Pandas for Developers](https://www.safaribooksonline.com/library/view/introduction-to-pandas/9781771375764/) / [Data Wrangling and Analysis with Python](https://www.safaribooksonline.com/library/view/data-wrangling-and/9781491960820/) - I have seen some videos of these courses already, they are pretty good.
