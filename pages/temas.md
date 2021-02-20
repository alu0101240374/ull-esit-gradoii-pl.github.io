---
layout: single
title: Temas
permalink: /temas
---

{% comment %}
{% for page in site.pages %}
{{ page.categories }} - {{ page.url }}
{% endfor %}
{% endcomment %}
{% assign temas = site.categories["temas"] | sort %}
<ol>
  {% for tema in temas %}
<li><a href="{{site.baseurl}}{{tema.url}}" title="{{ tema.hover }}">{{ tema.title }}</a></li>
  {% endfor %}
</ol>

