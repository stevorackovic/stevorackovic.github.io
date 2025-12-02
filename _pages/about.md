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
	A Data Scientist and Machine Learning specialist with extensive experience across academia and industry. My portfolio spans natural language processing (NLP), large language models (LLMs), computer animation, deep reinforcement learning (DRL), and health tech, among other domains. I am experienced in designing and training ML models, as well as creating tests and use cases for benchmarking and evaluating results. With many completed projects behind me, I'm comfortable tackling new problems and adapting to new team structures and domain applications. 
</p>

<p>
	I completed my Ph.D. studies within the <a href="http://itn-bigmath.unimi.it/">BIGMATH</a> program at Instituto Superior Técnico, where I was awarded a diploma with distinction. The main subject of my thesis was applying machine learning and optimization techniques to improve algorithms used in 3D animation, carried out in collaboration with <a href="https://www.3lateral.com/">3Lateral Studio</a> (an Epic Games company).
</p>

<p>
	Below you can download a PDF version of my CV.
</p>

<button onclick="window.location.href='images/Curriculum.pdf'" type="button" class="btn">Curriculum</button>

# Recent news
------


{% include base_path %}
{% capture written_year %}'None'{% endcapture %}
{% for post in site.posts %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year > "2023" %}
	{% include recent-news.html %}
  {% endif %}
{% endfor %}
