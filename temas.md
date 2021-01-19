---
layout: single
title: Introducción a PL
sidebar:
  title: "Prueba de barra"
  nav: sidebar-sample
toc: true
toc_label: "Tabla de Contenidos"
toc_icon: "list"
---

# Temas

{% assign temas = site.categories["temas"] | sort %}
<ul>
  {% for tema in temas %}
<li><a href="{{site.baseurl}}{{tema.url}}" title="{{ tema.hover }}">{{ tema.title }}</a></li>
  {% endfor %}
</ul>

