{% for section in page.sections %}

## {{ section.title }}

{% if section.url%}
* [{{ section.title }}]({{site.baseurl}}/assets/temas/{{page.slug}}/{{section.url}})
{% endif %}

{% for subsection in section.subsections %}
### [{{subsection.title}}]({{site.baseurl}}/assets/temas/{{page.slug}}/{{subsection.url}})
{% endfor %}
{% endfor %}


