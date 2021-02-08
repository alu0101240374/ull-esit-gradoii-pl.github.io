{% assign practicas = site.categories["practicas"] %}

<ol reversed>
{%- for practica in practicas %}
<li>  <a href="{{site.baseurl}}{{ practica.url }}">{{ practica.title }}</a></li>
{%- endfor %}
</ol>
