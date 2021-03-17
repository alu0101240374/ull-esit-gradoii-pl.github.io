---
title: "404 explained: A Brief Intro to the DOM, Promises and Asyn Await"
---

### The Code


See the code at [https://github.com/ULL-ESIT-GRADOII-PL/ull-esit-gradoii-pl.github.io/edit/main/pages/404.md](https://github.com/ULL-ESIT-GRADOII-PL/ull-esit-gradoii-pl.github.io/edit/main/pages/404.md)

que se verá así 
[{{site.baseurl}}/noexiste]({{site.baseurl}}/noexiste).

La página además de mostrar el mensaje de error hace un par de requests: 

1. Un request a [The Cat API](https://thecatapi.com/) para mostrar una imagen de gatitos obtenida al azar.
2. Un request a <https://api.quotable.io/random> para mostrar una cita al azar

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

### API keys

See:

* Stackoverflow: [Hide api key for a Github page](https://stackoverflow.com/questions/21939713/hide-api-key-for-a-github-page)

The question is:

*I have a github page for my organization where I would like to call data from a 3rd party api where I need an auth token. Can I publish this github page without having the auth token displayed on the public repo?*

And here is the most voted answer:

> In short, no. If your GitHub repo is public, all its assets are public. You can make the repo private and it will still publish on GitHub Pages if named with the `username.github.io` convention or if it has a `gh-pages` branch. While that's an option, that's not necessarily the right thing to do.

> If your key is in your GitHub Pages repo, it sounds like it's used for client-side API calls in JavaScript. If so, your auth token is publicly visible whether it's in your public repo or sent in your client-side files to the browser. **This is usually fine. The third-party API might have generated the auth token based on your website's domain, and restrict calls using that token to pages originating on your domain. Otherwise, they might require the auth token only for logging requests and monitoring usage.**

> If the auth token is truly meant to be private, **then you may need to write private server-side code to call the third-party API**. Your GitHub Pages site could then hit your service for the data it needs. I've had to do that before where the web API had security concerns, but I still needed to retrieve non-sensitive data from the client-side.