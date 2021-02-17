{% assign practicas = site.categories["practicas"] %}

<ol reversed>
{%- for practica in practicas %}
<li>  <a href="{{site.baseurl}}{{ practica.url }}">{{ practica.title }}</a> 
{% if practica.rubrica %}
(<a href="{{ practica.url }}#rubrica">rubrica</a>)
{% endif %}
</li>
{%- endfor %}
</ol>
