---
title: Jekyll, GitHub Pages y Netlify
published: true
rubrica: 
---

Durante esta práctica desarrollará un web-site usando Jekyllrb como *static site generator* y lo desplegará en GitHub y en Netlify. 

## Instale Jekyll

* Instale [Jekyll](https://jekyllrb.com/docs/) en su máquina o en la máquina del servicio [iaas.ull.es]({{site.baseurl}}/tema1-introduccion/practicas/p01-t1-iaas/) si no dispone de máquina. Instrucciones en [Jekyll Installation](https://jekyllrb.com/docs/installation/)
* Si no se acuerda de como funciona Ruby le pueden venir las instrucciones en [Ruby 101](https://jekyllrb.com/docs/ruby-101/)

## Estudie las secciones del Tutorial de jekyllrb

Realice el [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) en Jekyllrb:

*   [Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)
*   [Liquid](https://jekyllrb.com/docs/step-by-step/02-liquid/)
*   [Front Matter](https://jekyllrb.com/docs/step-by-step/03-front-matter/)
*   [Layouts](https://jekyllrb.com/docs/step-by-step/04-layouts/)
*   [Includes](https://jekyllrb.com/docs/step-by-step/05-includes/)
*   [Data Files](https://jekyllrb.com/docs/step-by-step/06-data-files/)
*   [Assets](https://jekyllrb.com/docs/step-by-step/07-assets/)
*   [Blogging](https://jekyllrb.com/docs/step-by-step/08-blogging/)
*   [Collections](https://jekyllrb.com/docs/step-by-step/09-collections/)

## Themes

Elige un tema para tu web site. Puedes obtener información en [Jekyll Themes](https://jekyllrb.com/docs/themes/).

Recomiendo [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/). 
Configure el tema elegido.

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

## 404

Lea el tutorial [Custom 404 Page](https://jekyllrb.com/tutorials/custom-404-page/) y añada una página 404 personalizada

## DOM, Promesas y Async Await

Tienes un ejemplo de `404.md` en estos apuntes [404.md](https://raw.githubusercontent.com/ULL-ESIT-GRADOII-PL/ull-esit-gradoii-pl.github.io/main/pages/404.md)


```md
---
layout: single
title: Error
permalink: /404.html
toc: false
---
# ¡Ay Diós mío!

## Aún no he escrito esta página. 
```
```html
<div>
<style>
```
```css
img, #quote, #comment-cat {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
#author {
  float: right;
}
```
```html
</style>


<div id="comment-cat"></div>
<div id="cat"></div>
<br/>
<div id="quote"></div>
<div id="author"></div>


<script type="text/javascript">
```
```js
/*
  https://docs.thecatapi.com/ 
*/
const URL = 'https://api.thecatapi.com/v1/images/search?size=full';

(async function() {
  try {
    
    // CAT 
    let divTitle = document.getElementById("comment-cat");
    
    let divcat = document.getElementById("cat");
    let response = await fetch(URL, {
       headers: {
       'x-api-key': "blah"
       }
    });
    let cat = await response.json();
    // console.log(cat);   
    let img = document.createElement("img");
    let title = document.createElement("h2");
    title.innerText = "Consuélate con un gatito";   
    divTitle.append(title);
    img.src = cat[0].url;
    divcat.appendChild(img);   

    // QUOTE
    const quoteDiv = document.getElementById("quote");
    const authorDiv = document.getElementById("author");
    
    const quoteRes = await fetch('https://api.quotable.io/random');
    const data = await quoteRes.json();
    quoteDiv.innerHTML = `<h2>${data.content}</h2>`;
    authorDiv.innerHTML = `<h3>—${data.author}</h3><br/><br/>`;
  }
  catch(e) { 
    console.log(e);
  }
})();
```
```html
</script>

</div>
```

que se verá así 
[{{site.baseurl}}/noexiste]({{site.baseurl}}/noexiste).

La página hace un request a [The Cat API](https://thecatapi.com/) para mostrar una imagen de  gatitos obtenida al azar.

### Que es el DOM

Intenta  entender un poco el código anterior. El ejemplo combina unos cuantos conceptos importantes en 
el manejo de las tecnologías web. 

Uno de los conceptos es el DOM (Document Object Model). Cuando nuestro browser descarga una página HTML lo primero que hace es un análisis sintáctico de la misma y construye un AST según un formato estándard que es conocido como DOM. 
Los nodos de ese AST disponen de numerosos métodos que permiten 
* la búsqueda de nodos (`let divTitle = document.getElementById("comment-cat");`),
* el recorrido, 
* la creación  de nodos (`document.createElement("img")`), 
* la modificación de nodos (`img.src = cat[0].url`) y 
* la transformación del AST (`divTitle.append(title);`) 


Si estos conceptos son nuevos, estos capítulos pueden ayudarte a conocer el estandard del DOM:  

* [DOM tree](https://javascript.info/dom-nodes) 
* [DOM navigation](https://javascript.info/dom-navigation)
* [DOM modification](https://javascript.info/modifying-document)


### Asíncronia

El código anterior hace también mucho uso de [fetch](https://javascript.info/fetch) para hacer solicitudes (*requests*)a un par de servidores. La llamada

```js
fetch(URL, {
       headers: {
       'x-api-key': "blah"
       }
    });
```

retorna un objeto de la clase [Promise](https://javascript.info/promise-basics). Los objetos `Promise` tienen tres estados:

1. `pending`: No se ha iniciado el proceso de carga 
2. `fulfilled`: La carga del recurso comienza con éxito y  la promesa se resuelve a un objeto de la clase [Response](https://fetch.spec.whatwg.org/#response-class) que permite manejar el flujo de datos. La carga realmente no tiene porque haber terminado  
3. `rejected`: The promise **rejects** if the fetch was unable to make HTTP-request, e.g. network problems, or there’s no such site. Abnormal HTTP-statuses, such as 404 or 500 do not cause an error.

La palabra [await](https://javascript.info/async-await) después del `fetch` hace que JS espere al *fulfillment* de la promesa devuelta por `fetch` de modo que en `response` queda el resultado de la promesa. 

```js
let response = await fetch(URL, {
       headers: { 'x-api-key': "blah" }
    });
```

Si la promesa es rechazada se ejecutará el `catch`:

```js
(async function() {
  try {
    ...
    let response = await fetch(URL, {
       headers: { 'x-api-key': "blah" }
    });
    ...
  }
  catch(e) { 
    console.log(e);
  }
})();
```

Véase el capítulo [Promises]({{ site.baseurl}}/assets/temas/introduccion-a-javascript/promises#promises) para mas información

Existe una API similar para los amantes de los perros [Dog API](https://dog.ceo/dog-api/). Puedes usarla en tu `404.md`


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

