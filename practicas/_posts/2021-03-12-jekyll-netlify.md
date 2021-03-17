---
title: Jekyll, GitHub Pages y Netlify
published: true
rubrica: 
  - Funciona en local
  - Está desplegada en GitHub Pages
  - Está desplegada en Netlify
  - Tiene un 404 personalizado
  - Se ha experimentado con las Categories y los tags
  - Se ha experimentado con Liquid
  - Contiene Data files y esta bien configurado el `config.yml`
  - Se ha experimentado con los Layouts
  - Se hace uso de las Collections 
  - La *User Experience*,la navegación y la estética son aceptables
  - Pruebas
  - Se ha añadido una GitHub Action para las pruebas
  - "Opcional: Ha añadido un sistema de comentarios"
---

Durante esta práctica desarrollará un web-site usando Jekyllrb como *static site generator* y lo desplegará en GitHub y en Netlify. Un buen tópico para el Web Site es una página CV personal o un Web Site sobre un tópico de tu interés.

## Instale Jekyll

* Instale [Jekyll](https://jekyllrb.com/docs/) en su máquina o en la máquina del servicio [iaas.ull.es]({{site.baseurl}}/tema1-introduccion/practicas/p01-t1-iaas/) si no dispone de máquina. Instrucciones en [Jekyll Installation](https://jekyllrb.com/docs/installation/)
* Si no se acuerda de como funciona Ruby le pueden venir las instrucciones en [Ruby 101](https://jekyllrb.com/docs/ruby-101/)

## Estudie las secciones del Tutorial de jekyllrb

Realice el [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) en Jekyllrb:

* [Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)
* [Liquid](https://jekyllrb.com/docs/step-by-step/02-liquid/)
* [Front Matter](https://jekyllrb.com/docs/step-by-step/03-front-matter/)
* [Layouts](https://jekyllrb.com/docs/step-by-step/04-layouts/)
* [Includes](https://jekyllrb.com/docs/step-by-step/05-includes/)
* [Data Files](https://jekyllrb.com/docs/step-by-step/06-data-files/)
* [Assets](https://jekyllrb.com/docs/step-by-step/07-assets/)
* [Blogging](https://jekyllrb.com/docs/step-by-step/08-blogging/)
* [Collections](https://jekyllrb.com/docs/step-by-step/09-collections/)
    - For the use of collections, see how this template for academic websites uses collections [academicpages.github.io](https://github.com/academicpages/academicpages.github.io) and [the corresponding GitHub deployment](https://academicpages.github.io/)

Es conveniente que el Web Site desarrollado contenga uso de los apartados estudiados, esto es haga uso de
Collections, se haga separación de los datos en `_data` y `_config.yml`, que extienda algún layout en `_layout`, algún ejemplo de procesamiento con Liquid, uso de `_includes`, que haga uso de `categories` y `tags`, etc.

## Themes

Elige un tema para tu web site. Puedes obtener información en [Jekyll Themes](https://jekyllrb.com/docs/themes/).

Recomiendo [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/). Si lo eliges, deberás leer las instrucciones de Minimal Mistakes.

Configura y extiende el tema elegido (por ejemplo, los layouts).

<!--
## Algunos tips si trabaja en la máquina del iaas.ull.es

* [Creating a personal access token for the command line](https://help.github.com/es/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) para trabajar con git y GitHub vía https
* Para que las instrucciones anteriores funcionen:

  ```
  usuario@ubuntu$ git config --global credential.helper  store
  usuario@ubuntu$ ls -ltr ~/.git-credentials 
  -rw------- 1 usuario usuario 68 nov 27 13:27 /home/usuario/.git-credentials
  usuario@ubuntu$ cat ~/.git-credentials 
  https://crguezl:este-no-es-el-token@github.com
  ```
* Ejecutando en una máquina del iaas.ull.es:

    ```
    usuario@ubuntu:~/src/ull-mii-sytws-1920.github.io$ bundle exec jekyll serve -H 10.6.128.216 -P 8080
    ```
-->

## Despliegue en GitHub Pages


Despliegue el proyecto en GitHub Pages. Puede usar la rama `master`, la carpeta `docs` en `master`o bien
Puede hacerlo usando la rama `gh-pages` con la gema [github-pages](https://jekyllrb.com/docs/github-pages/#deploying-jekyll-to-github-pages) o el paquete npm [gh-pages](https://www.npmjs.com/package/gh-pages)


Also, read the section [*Deployment*](https://jekyllrb.com/docs/step-by-step/10-deployment/) of the *Step by Step Tutorial*

<!--
## Navigation

* Lea del tutorial [Navigation](https://jekyllrb.com/tutorials/navigation/) los escenarios [Basic List](https://jekyllrb.com/tutorials/navigation/#scenario-1-basic-list) y [Sorted List](https://jekyllrb.com/tutorials/navigation/#scenario-2-sorted-list) e implementelos en su site
-->

## Deploying in different environments

[Working with different environments: url and baseurl and more]({{site.baseurl}}/assets/temas/introduccion-a-javascript/baseurl)

## 404

Lea el tutorial [Custom 404 Page](https://jekyllrb.com/tutorials/custom-404-page/) y añada una página 404 personalizada.

Tienes un ejemplo de `404.md` en estos apuntes [404.md](https://raw.githubusercontent.com/ULL-ESIT-GRADOII-PL/ull-esit-gradoii-pl.github.io/main/pages/404.md)

* Intento de explicar como funciona [El 404 de estos apuntes]({{site.baseurl}}/assets/practicas/jekyll-netlify/404-explained). Una brevísima introducción al DOM, a las Promesas y al Async Await

Existe una API similar a la de los gatos usada en el ejemplo para los amantes de los perros [Dog API](https://dog.ceo/dog-api/). Puedes usarla en tu `404.md`


## Test the Deployment with html-proofer and GitHub Actions

* Se puede probar el buen funcionamiento del Blog haciendo pruebas en GitHub Actions. 
Repase la sección [Testing HTML pages](https://ull-esit-gradoii-pl.github.io/assets/temas/introduccion-a-javascript/jekyll#testing) de estos apuntes


<!--
# Despliegue en GitHub usando Github Actions

Despliegue su proyecto en GitHub usando GitHub Actions. Véase:

* [A GitHub Action for Custom Jekyll Builds on GitHub Pages](https://github.com/BryanSchuetz/jekyll-deploy-gh-pages)

## Question: Why not just let GitHub Pages build it? 
## Answer: Because this way we can use our own custom Jekyll plugins and build scripts.
-->

## Despliegue en Netlify

* Lea el tutorial [A Step-by-Step Guide: Jekyll 3.0 on Netlify](https://www.netlify.com/blog/2015/10/28/a-step-by-step-guide-jekyll-3.0-on-netlify/) y despliegue el correspondiente Jekyll blog en [Netlify](https://www.netlify.com/)

* [Jekyll + NetlifyCMS](https://www.youtube.com/playlist?list=PLWjCJDeWfDdcU8zbZZrr6L1zpf_2Eqt_w) 14 Youtube videos Thomas Bradley

