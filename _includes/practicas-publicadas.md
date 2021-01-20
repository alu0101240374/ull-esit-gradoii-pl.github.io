{% assign practicas = site.categories["practicas"] %}

{%- for practica in practicas %}
*  <a href="{{site.baseurl}}{{ practica.url }}">{{ practica.title }}</a> 
{%- endfor %}

