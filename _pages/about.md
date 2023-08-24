---
permalink: /
title: "About me"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<p>I am a Ph.D. candidate at the Instituto Superior Técnico, enrolled in an industrial Ph.D. program <a href="http://itn-bigmath.unimi.it/">BIGMATH</a> (This project has received funding from the European Union’s Horizon 2020 research and innovation program under the Marie Skłodowska-Curie Grant Agreement No 812912). I work under the supervision of <a href="https://www.di.fct.unl.pt/en/pessoas/docentes/claudia-alexandra-magalhaes-soares">Cláudia Soares</a> from <a href="https://www.unl.pt/en">NOVA</a> Uni in Lisbon and <a href="https://matematika.pmf.uns.ac.rs/o-nama/imenik/dusan-jakovetic/">Dušan Jakovetić</a> from the University of Novi Sad, and collaborate with <a href="https://www.3lateral.com/">3Lateral Studio</a> (Epic Games Company). The main focus of our research is applying machine learning and optimization techniques to improve the algorithms used in a 3D animation.</p>

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