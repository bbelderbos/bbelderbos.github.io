---
layout: post
title: Analyzing Brexit data with Pandas
comments: True
summary: I wanted to learn Pandas for quite some time. As usual on this blog I start with a practical exercise / goal, UK's EU referendum, and use (and learn) Pandas to analyze the results, including UK census data.
categories: [Data Science]
tags: [pandas, numpy, matplotlib, brexit, data, analysis, mining, scatterplot]
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

### Añadiendo datos demograficos

Vinculé los datos del voto con los [datos de censo](http://www.ons.gov.uk/census/2011census/2011censusdata) publicamente disponibles (como sugerió [Pybonacci](https://twitter.com/Pybonacci), gracias). Encontré unas correlaciones interesantes (y aprendí algunas cosas de matplotlib usandolo), puedes ver el notebook [aquí](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb):

#### Como influye la edad en el voto por salir / quedar? 

![median_age.png]({{ site.baseurl }}/assets/median_age.png)

#### Como influye el porcentaje de paro?

![perc_unemployed.png]({{ site.baseurl }}/assets/perc_unemployed.png)

#### Como influye un nivel más alto de estudios (educación)? 

![perc_high_education.png]({{ site.baseurl }}/assets/perc_high_education.png)

#### Y como influye el porcentaje de gente nacida fuera de Inglaterra? 

![perc_born_outside_uk.png]({{ site.baseurl }}/assets/perc_born_outside_uk.png)

Claramente areas con una población mayor y una taza de paro más alto votan por salir. Por otro lado, areas con un alto porcentaje de estudios superiores, y regiones donde más gente nacieron fuera de Inglaterra prefieren (por lo general) que Inglaterra se quede en la unión. 

Lo dicho, para ver como llegué a estos resultados con Pandas el notebook está [aquí](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb).

### Bonus: datos de ingresos por región

Datos de ingresos (sueldo) eran más dificiles de obtener en [los datos del censo](http://webarchive.nationalarchives.gov.uk/20160105160709/http://www.ons.gov.uk/ons/publications/re-reference-tables.html?edition=tcm%3A77-286262) entonces usé [este enlace](https://www.gov.uk/government/statistics/income-and-tax-by-county-and-region-2010-to-2011) para comprobar la relación entre la mediana de ingresos y el voto. Encontré un patrón interesante: 

![median_income.png]({{ site.baseurl }}/assets/median_income.png)

(el parsing de los datos está documento en el [mismo notebook](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb))

Se ve claramente que regiones con una mediana de ingresos mas baja prefieren salir de la unión, aunque no es 100% consistente: Irlanda tiene una mediana relativamente baja sino vota por quedarse, y South East tiene un sueldo mediano más alto, no obstante vota por salir. Es interesante como se ve este tipo de tendencias combinando varias fuentes de datos.

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

### Bonus: income data by region

Income data was harder to get from the [standard census data](http://webarchive.nationalarchives.gov.uk/20160105160709/http://www.ons.gov.uk/ons/publications/re-reference-tables.html?edition=tcm%3A77-286262) so I used [this link](https://www.gov.uk/government/statistics/income-and-tax-by-county-and-region-2010-to-2011) to check the relation of median income on voting. I found an interesting pattern:

![median_income.png]({{ site.baseurl }}/assets/median_income.png)

(the parsing of the data is documented in the [same notebook](https://github.com/bbelderbos/brexit-pandas/blob/master/brexit_demographics.ipynb))

We can clearly see that regions with a relatively smaller median income are more in favor of leaving the EU, although it is not 100% consistent: Northen Ireland has a lower median income but voted Remain, South East has a higher median income but wants to leave. Interesting though how general trends become visible by merging different data sets.
