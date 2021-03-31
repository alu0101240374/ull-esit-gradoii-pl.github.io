{% assign practicas = site.categories["practicas"] %}

<ol reversed>
{%- for practica in practicas %}
<li> <a href="{{site.baseurl}}{{ practica.url }}">{{ practica.title }}</a> 
  <ul>
    {% if practica.rubrica %}<li><a href="{{ practica.url }}#rubrica">rubrica</a></li>{% endif %}
    <li>Published: {{practica.date | date_to_long_string }}</li>
  </ul>
</li>
{%- endfor %}
</ol>
