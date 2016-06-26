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

Desafortunadamente no encontre más datos. Me hubiera interesado sacar más datos sobre como influye la edad, la posicion económica, etc en los resultados (como demuestra [este artículo de FT Data](http://blogs.ft.com/ftdata/2016/06/24/brexit-demographic-divide-eu-referendum-results/)). Si alquien sabe de mas fuentes de datos (aparte del CSV mencionado), comentalo abajo. También por cualquier sugerencia de Pandas ...

---
Algunos enlaces para aprender Pandas:

* [Pandas home y docs](http://pandas.pydata.org)
* [Python’s pandas make data analysis easy and powerful with a few lines of code](https://www.oreilly.com/learning/pythons-pandas-make-data-analysis-easy-and-powerful-with-a-few-lines-of-code?imm_mid=0e520d&cmp=em-prog-na-na-newsltr_20160625) - tutorial breve y fácil para empezar.
* [Python for Data Analysis](https://www.safaribooksonline.com/library/view/python-for-data/9781449323592/) - libro del creador Wes McKinney.
* [Introduction to Pandas for Developers](https://www.safaribooksonline.com/library/view/introduction-to-pandas/9781771375764/) / [Data Wrangling and Analysis with Python](https://www.safaribooksonline.com/library/view/data-wrangling-and/9781491960820/) - ya he visto algunos videos, son buenos.


<span id="English"></span>

## English translation

In progress ... notebook already available in [English](https://github.com/bbelderbos/brexit-pandas/blob/master/Analyze_Brexit_Pandas_EN.ipynb)
