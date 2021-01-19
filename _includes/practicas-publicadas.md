{% assign practicas = site.categories["practicas"] %}

{%- for practica in practicas %}
*  <a href="{{site.baseurl}}{{ practica.myurl }}">{{ practica.title }}:  {{ practica.name }}</a> 
{%- endfor %}

