---
layout: single
title: Clases
permalink: /clases
toc: true
---
 
 <ol>
  {%- assign previousMonth = "0" %}
  {%- for post in site.categories["clases"]  %}
      {%- assign currentMonth = post.date | date: "%B" %}
      {%- if currentMonth != previousMonth %}
</ol>
### Classes during the month of {{ currentMonth }}

<ol reversed>
      {%- endif %}
<li> <a href="{{site.baseurl}}{{ post.url }}">{{ post.title }}</a></li>
  <ul>
    {%- if post.summary %}<li>{{ post.summary | markdownify }}</li>{%- endif -%}
    {%- if post.video %}<li> 
      {% if post.video.first%}
        {% for video in post.video %}
            <a href="https://youtu.be/{{video}}">Vídeo {{ forloop.index }}</a> 
            {% unless forloop.last%},{% endunless %}
        {% endfor %}
        
      {% else %}
           <a href="https://youtu.be/{{post.video}}">Vídeo</a> 
      {% endif %}
    </li>
    {%- endif %}
  </ul>
      {%- assign previousMonth = currentMonth %}
  {%- endfor %}

