---
permalink: /
title: "About me"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I am a Post-doctoral Researcher at [NOVA School of Science and Technology](https://www.fct.unl.pt/en) with [NOVA LINCS](https://nova-lincs.di.fct.unl.pt/).
My main interests include Machine Learning, Optimization, 3D Shape Modelling, Gaussian Processes. I received my PhD in <b>Mathematical Sciences</b> form the [University of Milan](https://www.unimi.it/en) (2022) and BSc and MSc (2018) in <b>Aerospace Engineering</b> from [Instituto Superior Técnico](https://tecnico.ulisboa.pt/pt/). 
The PhD program was part of  [BIGMATH](http://itn-bigmath.unimi.it/) - an EU funded project in the areas of optimization, statistics, and large-scale linear algebra for Big Data.
My PhD thesis [Gaussian Processes for 3D Shape Modelling of Noisy and Incomplete Data. An Application to Human Ears Reconstruction](https://air.unimi.it/handle/2434/947830), focused on the application of Gaussian Processes 
to 3D shape modelling of challenging point clouds.

<br/><br/>

# Recent news
------


{% include base_path %}
{% capture written_year %}'None'{% endcapture %}
{% for post in site.posts %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year > "2019" %}
	{% include recent-news.html %}
  {% endif %}
{% endfor %}