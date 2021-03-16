---
title: "404 explained: A Brief Intro to the DOM, Promises and Asyn Await"
---

## The Code



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
img, #quote, #comment-cat {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
#author {
  float: right;
}
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
* la búsqueda de nodos 
  
  ```js
  let divTitle = document.getElementById("comment-cat");
  ```
* el recorrido, 
* la creación  de nodos 
  ```js
  document.createElement("img")
  ```
* la modificación de nodos 
  ```js 
  img.src = cat[0].url
  ```  
* la transformación del AST 

  ```js
  divTitle.append(title);
  ```

Si estos conceptos son nuevos, estos capítulos pueden ayudarte a conocer el estandard del DOM:  

* [DOM tree](https://javascript.info/dom-nodes) 
* [DOM navigation](https://javascript.info/dom-navigation)
* [DOM modification](https://javascript.info/modifying-document)

### Asíncronia

El código anterior hace también mucho uso de [fetch](https://javascript.info/fetch) para hacer solicitudes (*requests* ) a un par de servidores. La llamada

```js
fetch(URL, {
       headers: {
       'x-api-key': "blah"
       }
    });
```

retorna un objeto de la clase [Promise](https://javascript.info/promise-basics). 
Los objetos `Promise` tienen tres estados:

1. `pending`: No se ha iniciado el proceso de carga 
2. `fulfilled`: La carga del recurso comienza con éxito y  la promesa se resuelve a un objeto de la clase [Response](https://fetch.spec.whatwg.org/#response-class) que permite manejar el flujo de datos. La carga realmente no tiene porque haber terminado  
3. `rejected`: The promise **rejects** if the fetch was unable to make HTTP-request, e.g. network problems, or there’s no such site. Abnormal HTTP-statuses, such as 404 or 500 do not cause an error.

La palabra [await](https://javascript.info/async-await) después del `fetch` hace que JS espere al *fulfillment* de la promesa devuelta por `fetch` de modo que en `response` queda el objeto resultado de la promesa. 

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

El objeto `response` tiene un método `json` que cuando es llamado `response.json()` devuelve una promesa. 
Esa promesa se cumple (*is fulfilled*) cuando finalmente obtenemos
el cuerpo (*body*) de la respuesta desde el servidor. El resultado de la promesa es el JSON retornado en el *body*:

```js
let cat = await response.json();
```

Véase el capítulo [Promises]({{ site.baseurl}}/assets/temas/introduccion-a-javascript/promises#promises) para mas información

