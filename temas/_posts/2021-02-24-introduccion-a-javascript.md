---
layout: single
title: "Fundamentos"
published: true
excerpt: "Introducción a JavaScript y otras Herramientas"
sections:
  herramientas:
    - title: IAAS
      url: iaas
    - title: Editors
      url: editors
    - title: "GitHub Command Line Interface"
      url: gh
    - title: Jekyll
      url: jekyll
    - title: "GitHub Actions"
      url: github-actions
    - title: "GitHub Apps"
      url: github-apps
    - title: Azure
      url: azure
  javascript:
    - title: Módulos
      url: modulos
    - title: "The Event Loop"
      url: event-loop
    - title: Promises
      url: promises
    - title: Promise Examples
      url: promise-examples
    - title: Node.JS
      url: node
    - title: "Pruebas, Integración y Calidad"
      url: pruebas
    - title: "Object Oriented Programming: OOP"
      url: oop
    - title: "Functional Programming"
      url: functional
    - title: "Diseño, Principios"
      url: design
    - title: "JAM Stack"
      url: jam
    - title: "Build Tools"
      url: build-tools
    - title: TypeScript
      url: typescript
---

## Herramientas

{% for section in page.sections.herramientas %}

### [{{section.title}}]({{site.baseurl}}/assets/temas/introduccion-a-javascript/{{section.url}})

{% endfor %}

## JavaScript

{% for section in page.sections.javascript %}

### [{{section.title}}]({{site.baseurl}}/assets/temas/introduccion-a-javascript/{{section.url}})

{% endfor %}


