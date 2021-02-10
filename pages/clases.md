---
layout: single
title: Clases
permalink: /clases
---

  {%- assign previousMonth = "0" %}
  {%- for post in site.categories["Clases"] %}
     {%- assign currentMonth = post.date | date: "%B" %}
      {%- if currentMonth != previousMonth %}

### Classes during the month of {{ currentMonth }}

      {%- endif %}
* [{{ post.title }}]({{site.baseurl}}{{ post.url }})  {%- if post.video %} ([Vídeo]({{post.video}})) {%- endif %} [📝]({{site.organization.master}}/{{post.path}})
      {%- assign previousMonth = currentMonth %}
  {%- endfor %}

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3MTE2Njg1MF19
-->