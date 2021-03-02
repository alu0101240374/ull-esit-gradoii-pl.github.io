---
layout: single
title: Clases
permalink: /clases
---
 
 <ol>
  {%- assign previousMonth = "0" %}
  {%- for post in site.categories["clases"]  %}
      {%- assign currentMonth = post.date | date: "%B" %}
      {%- if currentMonth != previousMonth %}
</ol>
<h3> Classes during the month of {{ currentMonth }}</h3>

<ol reversed>
      {%- endif %}
<li> <a href="{{site.baseurl}}{{ post.url }}">{{ post.title }}</a>  {%- if post.video %} <a href="{{post.video}}">(Vídeo)</a> {%- endif %} <a href= "{{site.organization.master}}/{{post.path}}">📝</a></li>
  {%- if post.summary %}
  <ul><li>{{ post.summary }}</li></ul>
  {%- endif -%}
      {%- assign previousMonth = currentMonth %}
  {%- endfor %}

