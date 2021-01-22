---
layout: single
title: Temas
toc: true
toc_label: "Tabla de Contenidos"
toc_icon: "list"
---

# Temas

{% comment %}
{% for page in site.pages %}
{{ page.categories }} - {{ page.url }}
{% endfor %}
{% endcomment %}
{% assign temas = site.categories["temas"] | sort %}
<ul>
  {% for tema in temas %}
<li><a href="{{site.baseurl}}{{tema.url}}" title="{{ tema.hover }}">{{ tema.title }}</a></li>
  {% endfor %}
</ul>

