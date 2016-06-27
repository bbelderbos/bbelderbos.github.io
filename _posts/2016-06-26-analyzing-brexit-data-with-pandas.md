---
layout: post
title: Analyzing Brexit data with Pandas
comments: True
summary: I wanted to learn Pandas for quite some time. As usual on this blog I start with a practical exercise / goal, UK's EU referendum, and use (and learn) Pandas to analyze the results.
categories: [Data Science]
tags: [pandas, brexit, data, numpy, matplotlib]
image: pandas_brexit_data.png
---

<a href="#English">English version below / versión en inglés abajo</a>

---

Desde hace tiempo quería aprender [Pandas](http://pandas.pydata.org). Por fin llegó la oportunidad: Brexit = datos.

Como siempre empecé con un ejercicio / objetivo practico, en este caso procesar los datos del referéndum. Usé Pandas para analizar los datos (CSV) publicados por [electoralcommission.org.uk](http://www.electoralcommission.org.uk/find-information-by-subject/elections-and-referendums/upcoming-elections-and-referendums/eu-referendum/electorate-and-count-information).

Aunque quería responder a más preguntas este CSV era suficiente para estrenarme con Pandas (es inmenso!). Además aprendí usar [Jupyter notebook](http://jupyter.readthedocs.io/en/latest/) para documentar todo. El notebook [puedes ver / bajar en Github](https://github.com/bbelderbos/brexit-pandas/blob/master/Analyze_Brexit_Pandas_ES.ipynb).

Consegui mi objetivo de representar los datos mostrados [aquí](https://ig.ft.com/sites/elections/2016/uk/eu-referendum/index.html). Aquí algunos pantallazos del notebook:

---

![notebook_screenshot1]({{ site.baseurl }}/assets/notebook_screenshot1.png)

...

---

![notebook_screenshot2]({{ site.baseurl }}/assets/notebook_screenshot2.png)

...

---

![notebook_screenshot3]({{ site.baseurl }}/assets/notebook_screenshot3.png)

...

---

![notebook_screenshot4]({{ site.baseurl }}/assets/notebook_screenshot4.png)

...

---

Algunos enlaces para aprender Pandas:

* [Pandas home y docs](http://pandas.pydata.org)
* [Python’s pandas make data analysis easy and powerful with a few lines of code](https://www.oreilly.com/learning/pythons-pandas-make-data-analysis-easy-and-powerful-with-a-few-lines-of-code?imm_mid=0e520d&cmp=em-prog-na-na-newsltr_20160625) - tutorial breve y fácil para empezar.
* [Python for Data Analysis](https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/) - libro del creador Wes McKinney.
* [Introduction to Pandas for Developers](https://www.safaribooksonline.com/library/view/introduction-to-pandas/9781771375764/) / [Data Wrangling and Analysis with Python](https://www.safaribooksonline.com/library/view/data-wrangling-and/9781491960820/) - ya he visto algunos videos, son buenos.

---

#### Actualizacion 27.06.2016

Un analisis más avanzado sería la inclusión de [datos de censo](http://www.ons.gov.uk/census/2011census/2011censusdata) (como sugerió [Pybonacci](https://twitter.com/Pybonacci)). Si ves por ejemplo [el analisis de FT Data](http://blogs.ft.com/ftdata/2016/06/24/brexit-demographic-divide-eu-referendum-results/), ellos integraron datos de demografia de manera interesante.

Lo intenté, pero como no tengo mucha experiencia con Pandas y matplotlib no me salió aún. Puedes ver en [este notebook](https://github.com/bbelderbos/brexit-pandas/blob/master/census_data.ipynb) lo que intenté. Si has sido capaz de generar graficos como FTData con estos datos, por favor compartelo en los comentarios.

<span id="English"></span>

---

## English translation

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
Some links to learn Pandas:

* [Pandas home and docs](http://pandas.pydata.org)
* [Python’s pandas make data analysis easy and powerful with a few lines of code](https://www.oreilly.com/learning/pythons-pandas-make-data-analysis-easy-and-powerful-with-a-few-lines-of-code?imm_mid=0e520d&cmp=em-prog-na-na-newsltr_20160625) - short and easy tutorial to start.
* [Python for Data Analysis](https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/) - book by its creator Wes McKinney.
* [Introduction to Pandas for Developers](https://www.safaribooksonline.com/library/view/introduction-to-pandas/9781771375764/) / [Data Wrangling and Analysis with Python](https://www.safaribooksonline.com/library/view/data-wrangling-and/9781491960820/) - I have seen some videos of these courses already, they are pretty good.

---

#### Update 27.06.2016

A more advanced analysis would be to combine [census data](http://www.ons.gov.uk/census/2011census/2011censusdata) (as suggested by [Pybonacci](https://twitter.com/Pybonacci)). See for example [FT Data's analysis](http://blogs.ft.com/ftdata/2016/06/24/brexit-demographic-divide-eu-referendum-results/) where they neatly integrate demographic data. 

I took a stab at it but as I am new to Pandas and matplotlib I could not pull it off yet. See the notebook [here](https://github.com/bbelderbos/brexit-pandas/blob/master/census_data.ipynb) to see what I tried. If you are able to generate FTData-like graphs with this data please share how you did it in the comments ...

---

