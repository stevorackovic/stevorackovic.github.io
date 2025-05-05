---
permalink: /
title: "About me"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<p>
I am a Data Scientist and a Machine Learning specialist working at <a href="https://www.vegaitglobal.com/">Vega IT</a>. My praimary focus and field of interest lies within Natural Language Processing and Large Language Models.
</p>
<p>I am also a Ph.D. candidate at the Instituto Superior Técnico, enrolled in an industrial Ph.D. program <a href="http://itn-bigmath.unimi.it/">BIGMATH</a>. I work under the supervision of <a href="https://www.di.fct.unl.pt/en/pessoas/docentes/claudia-alexandra-magalhaes-soares">Cláudia Soares</a> from <a href="https://www.unl.pt/en">NOVA</a> Uni in Lisbon and <a href="https://matematika.pmf.uns.ac.rs/o-nama/imenik/dusan-jakovetic/">Dušan Jakovetić</a> from the <a href="https://www.uns.ac.rs/">University of Novi Sad</a>, and collaborate with <a href="https://www.3lateral.com/">3Lateral Studio</a> (Epic Games Company). The main focus of our research is applying machine learning and optimization techniques to improve the algorithms used in a 3D animation. Besides the animation, we are also researching the applications of reinforcement learning algorithms and recommender systems. </p>

<p> Below you can download a PDF version of my CV. </p>
<button onclick="window.location.href='images/Curriculum.pdf'" type="button" class="btn">Curriculum</button>

# Recent news
------


{% include base_path %}
{% capture written_year %}'None'{% endcapture %}
{% for post in site.posts %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year > "2021" %}
	{% include recent-news.html %}
  {% endif %}
{% endfor %}
