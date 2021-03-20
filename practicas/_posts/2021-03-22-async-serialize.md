---
title: AsyncSerialize
published: true
categories: ["practicas"]
rubrica: 
---

## Introducción

Encontrará parte del material de esta práctica en el [Repo ULL-ESIT-PL/async-js-series-webpack](https://github.com/ULL-ESIT-PL/async-js-series-webpack).

Se dispone de una función `loadScript` que permite la carga de un script:

```js
    function loadScript(src, callback) {
        let script = document.createElement('script');
        script.src = src;
      
        script.onload = () => callback(null, script);
        script.onerror = () => callback(new Error(`Script load error for ${src}`));
      
        document.head.append(script);
      }
```

Que puede ser usada para cargar varios scripts. Supongamos que el segundo script usa funciones definidas en el primero. Tenemos que asegurarnos que el segundo script sólo se carga una vez terminada la carga del primero. 

En este ejemplo de uso [load-script.html](https://github.com/ULL-ESIT-PL/async-js-series-webpack/blob/master/load-script.html) cargamos tres scripts, 
1. [script-1.js](https://github.com/ULL-ESIT-PL/async-js-series-webpack/blob/master/script-1.js), 
2. [script-2.js](https://github.com/ULL-ESIT-PL/async-js-series-webpack/blob/master/script-2.js) y
3. [script-3.js](https://github.com/ULL-ESIT-PL/async-js-series-webpack/blob/master/script-3.js):

cada uno de los scripts cargados usa el código del anterior. Es necesario anidar las callbacks:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
    <p id="out"></p>
    <script>
      'use strict';
      let out = document.querySelector('p');

      function loadScript(src, callback) {
        let script = document.createElement('script');
        script.src = src;
      
        script.onload = () => callback(null, script);
        script.onerror = () => callback(new Error(`Script load error for ${src}`));
      
        document.head.append(script);
      }
           
      loadScript('script-1.js', (error, script) => {
        if (error) {
          console.error( error ); 
        } else {
          const message = `Cool!, the script '${script.src}' is loaded: "${hello()}"`;
          out.innerHTML = message;
          console.log(message);

          loadScript('script-2.js', (error, script) => {
            if (error) {
              console.error( error ); 
            } else {
              const message = `Great!, the script '${script.src}' is loaded: "${world()}"`;
              out.innerHTML += `<br/>${message}`;
              console.log(message);
              loadScript('script-3.js', (error, script) => {
                if (error) {
                  console.error( error );
                } else {
                  const message = `Unbelievable!, the script '${script.src}' is loaded: "${ull()}"`;
                  out.innerHTML += `<br/>${message}`;
                  console.log(message);
                  // ...continue after all scripts are loaded 
                }
              });
            }
          })
        }
      });
      </script>      
  </body>  
</html>
```

Puede ver este código en funcionamiento visitando [https://ull-esit-pl.github.io/async-js-series-webpack/load-script.html](https://ull-esit-pl.github.io/async-js-series-webpack/load-script.html). Si lo hace, recuerde abrir las herramientas de desarrollador para ver los mensajes en la cónsola. Juegue con el debugger para entender el funcionamiento.

Puede encontrar mas detalles sobre este ejercicio en el tutorial del profesor en [https://github.com/ULL-ESIT-PL/async-js-series-webpack](https://github.com/ULL-ESIT-PL/async-js-series-webpack).


## Escriba una función `loadScripts` 
 
Escriba una función `loadScripts([ array-of-urls ], callback)` que se llama así:

```js
let out = document.querySelector('p');

function loadScript(src, callback) {
  ...
}
      
function loadScripts(scripts, cb) {
  ...
}

loadScripts(
['script-1.js', 'script-2.js', 'script-3.js'], 
(err, results) => out.innerHTML = results.map(s => s.src).join("<br/>")
)
```

y que carga los scripts especificados en el array **en secuencia** y llama a la callback pasada como último argumento bien con un error si lo hubo o con el array de argumentos pasados como resultados a las callbacks (en este ejemplo los objetos DOM del tipo `script` creados).

## Serialización de Callbacks

Generalize la solución anterior para que secuencialice cualquier array de funciones asíncronas.
Esto es, debe funcionar tal como lo hace la función `series`  del módulo [Async.js]({{site.baseurl}}/assets/temas/introduccion-a-javascript/async-js)).

Estudie el módulo [Async.js]({{site.baseurl}}/assets/temas/introduccion-a-javascript/async-js) y resuma en el informe lo aprendido.

Esta es la forma de uso de la función `series`:

```js
series(
    [
        cb => loadScript('script-1.js', cb),
        cb => loadScript('script-2.js', cb),
        cb => loadScript('script-3.js', cb)
    ],
    (err, results) => p.innerHTML = results.map(s => s.src).join("<br/>")
);
```

### Ejemplos de prueba  

Si hace las pruebas de funcionamiento con scripts de similar tamaño la probabilidad de que su algoritmo produzca una salida que respeta el orden especificado es alta, **incluso si su algoritmo es erróneo**.

Puede simular que los scripts son de distinto tamaño **retrasando la iniciación de las cargas** con un `setTimeout` que espere por un número aleatorio de milisegundos:

```
  [~/.../load-script-seq(private)]$ pwd
/Users/casiano/local/src/javascript/learning/async/load-script-seq
[~/.../load-script-seq(private)]$ sed -ne '12,23p' load-scripts.html
```

```js
      const ir = (min, max) =>  Math.round((Math.random() * (max - min) + min))
      let out = document.querySelector('p');

      function loadScript(src, callback) {
        let script = document.createElement('script');
        setTimeout(() => script.src = src, ir(500,2000));

        script.onload = () => callback(null, script);
        script.onerror = () => callback(new Error(`Script load error for ${src}`));

        document.head.append(script);
      }
```

## Usando el Módulo npm Async en el Navegador

En el repo  [ULL-ESIT-PL/async-js-series-webpack](https://github.com/ULL-ESIT-PL/async-js-series-webpack) encontrara el fichero `dist/index.html`:

```
➜  load-script-seq git:(master) ✗ cat dist/index.html 
```

```html
<!doctype html>
<html>
 <head>
   <title>Getting Started</title>
 </head>
 <body>
    <p id="out"></p>
    <script src="main.js"></script>
 </body>
</html>
```

Este fichero contiene en su `body` además del párrafo vacío  `<p id="out"></p>` 
la carga de un script `main.js`. El fichero `main.js` se genera mediante el empaquetador
[webpack](https://webpack.js.org/guides/getting-started/) a partir de este otro fichero `src/index.js`
que importa  la función `series` del módulo [Async]({{site.baseurl}}/assets/temas/introduccion-a-javascript/async-js) usando sintáxis es6:

```
➜  load-script-seq git:(master) ✗ cat src/index.js 
```
```js
import { series } from "async-es";

function loadScript(src, callback) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => callback(null, script);
    script.onerror = () => callback(new Error(`Script load error for ${src}`));

    document.head.append(script);
}

let p = document.querySelector('p');

series(
  [
     cb => loadScript('script-1.js', cb),
     cb => loadScript('script-2.js', cb),
     cb => loadScript('script-3.js', cb)
   ],
   (err, results) => p.innerHTML = results.map(s => s.src).join("<br/>")
);
```

Puede ver el resultado de la ejecución en el [despliegue en `gh-pages`](https://ull-esit-pl.github.io/async-js-series-webpack/). Abriendo la ventana del desarrollador verá los mensajes en la cónsola.

## Bundlers

Cuando instalamos la dependencia del módulo [Async]({{site.baseurl}}/assets/temas/introduccion-a-javascript/async-js) este acaba en el directorio `node_modules/`. 
Para usarlo desde el navegador es conveniente usar un *bundler*. 
Un bundler en JavaScript es una herramienta que pone todo el código y  sus dependencias juntas en unos pocos archivos. Hay muchos de ellos en estos días, siendo los más populares [Browserify](http://browserify.org/), [Webpack](https://webpack.js.org), [Rollup](https://rollupjs.org/guide/en/) ... Históricamente, JavaScript no ha tenido un estándar para requerir dependencias de su código y de ahí la necesidad de los *bundlers*.

## Webpack

Siga el tutorial [Getting Started with Webpack](https://webpack.js.org/guides/getting-started/) y familiarícese con webpack. Resuma lo aprendido en el informe.

En el repo [ULL-ESIT-PL/async-js-series-webpack](https://github.com/ULL-ESIT-PL/async-js-series-webpack) hemos usado Webpack para procesar la solución que usa el módulo Async:

Si ejecutamos webpack con `npm run build` o bien `npx webpack`, este pasa a copiar los scripts de ejemplos `script-*.js`, `load-script.html` etc. a la carpeta `dist` y a compilar el fichero `./src/index.js` empaquetándolo con sus dependencias en el fichero `dist/main.js`:


```
➜  load-script-seq git:(master) ✗ npm run build

> sol@1.0.1 build /Users/casianorodriguezleon/campus-virtual/2021/learning/asyncjs-learning/load-script-seq
> webpack

assets by path *.js 67.7 KiB
  asset main.js 67.5 KiB [emitted] (name: main)
  asset script-3.js 66 bytes [emitted] [from: script-3.js] [copied]
  asset script-2.js 61 bytes [emitted] [from: script-2.js] [copied]
  asset script-1.js 52 bytes [emitted] [from: script-1.js] [copied]
asset favicon.ico 15.1 KiB [emitted] [from: favicon.ico] [copied]
asset load-script.html 1.72 KiB [compared for emit] [from: load-script.html] [copied]
orphan modules 159 KiB [orphan] 85 modules
runtime modules 670 bytes 3 modules
cacheable modules 16.3 KiB
  modules by path ./node_modules/async-es/internal/*.js 7.81 KiB 13 modules
  modules by path ./node_modules/async-es/*.js 7.89 KiB
    ./node_modules/async-es/series.js 2.58 KiB [built] [code generated]
    ./node_modules/async-es/asyncify.js 3.21 KiB [built] [code generated]
    ./node_modules/async-es/eachOfSeries.js 955 bytes [built] [code generated]
    ./node_modules/async-es/eachOfLimit.js 1.16 KiB [built] [code generated]
  ./src/index.js 572 bytes [built] [code generated]
webpack 5.26.3 compiled successfully in 322 ms
```

Los ficheros resultantes quedan en la carpeta `dist`:

```
➜  load-script-seq git:(master) ✗ tree dist 
dist
├── favicon.ico
├── index.html
├── load-script.html
├── main.js
├── script-1.js
├── script-2.js
└── script-3.js

0 directories, 7 files
```

Todo este proceso ha sido gobernado por el fichero de configuración `webpack.config.js`

```
➜  load-script-seq git:(master) ✗ cat webpack.config.js 
```
```js
const path = require('path');
const CopyPlugin = require('copy-webpack-plugin');

module.exports = {
  entry:  path.resolve('.', 'src', 'index.js'),
  mode: 'development',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  },
  devServer: {
    contentBase: path.join(__dirname, 'dist'),
    compress: true,
    port: 9000
  },
  plugins: [
    new CopyPlugin({ patterns: [
      { from: 'script-*.js' },
      { from: "favicon.ico" },
      { from: "load-script.html"}
    ]}),
  ],
  devtool: 'eval-cheap-module-source-map',
  module: {
    rules: [
      {
        test: /\.js$/,
        enforce: 'pre',
        use: ['source-map-loader'],
      },
    ],
  },
};
```

Una de las cosas  que ha hecho webpack es que ha empaquetado las dependencias instaladas en `node_modules/*` y el fichero `src/index.js` en el fichero `dist/main.js`:

```
➜  load-script-seq git:(master) ✗ sed -ne '1,13p' dist/main.js 
```
```js
/*
 * ATTENTION: An "eval-source-map" devtool has been used.
 * This devtool is neither made for production nor for readable output files.
 * It uses "eval()" calls to create a separate source file with attached SourceMaps in the browser devtools.
 * If you are trying to read the output file, select a different devtool (https://webpack.js.org/configuration/devtool/)
 * or disable the default devtool with "devtool: false".
 * If you are looking for production-ready output files, see mode: "production" (https://webpack.js.org/configuration/mode/).
 */
/******/ (() => { // webpackBootstrap
/******/        "use strict";
/******/        var __webpack_modules__ = ({

/***/ "./node_modules/async-es/asyncify.js":
```

## Escriba su solución como un módulo es6

Reescriba su solución al apartado [Serialización de Callbacks](#serialización-de-callbacks) en un módulo `src/lib/solution.js`

```
  [~/.../async/load-script-seq(private)]$ tree src
  src
  ├── index.js
  └── lib
      └── solution.js

  1 directory, 2 files
```
que sea usado por `src/index.js`

```js
import { loadScript, loadScripts, mySeries } from "./lib/solution.js";

let p = document.querySelector('p');

console.log("Using mySeries");
mySeries(
  [
      cb => loadScript('script-1.js', cb),
      cb => loadScript('script-2.js', cb),
      cb => loadScript('script-3.js', cb)
  ],
  (err, results) => out.innerHTML = results.map(s => s.src).join("<br/>")
);
```

## Loaders

Webpack enables use of <a href="https://webpack.js.org/concepts/loaders">loaders</a> to preprocess files. 

Loaders are transformations that are applied to the source code of a module. They allow you to pre-process files as you `import` or “load” them. Thus, loaders are kind of like “tasks” in other build tools and provide a powerful way to handle front-end build steps. 

Loaders can 

* transform files from a different language (like TypeScript) to JavaScript or 
* load inline images as data URLs. 
* Loaders even allow you to do things like `import` CSS files directly from your JavaScript modules

## Debugging con Webpack

En Webpack cuando estamos aplicando una serie de loaders o de transformaciones a nuestro código, el código generado dista mucho del original: El debugging se convierte en un problema.  Para facilitar la depuración es conveniente  configurar `/webpack.config.js` con  la opción `devtool` puesta a `eval-cheap-module-source-map`

    ```js
    +  devtool: 'eval-cheap-module-source-map',
    +  module: {
    +    rules: [
    +      {
    +        test: /\.js$/,
    +        enforce: 'pre',
    +        use: ['source-map-loader'],
    +      },
    +    ],
    +  },
    };
   ```
   Un *source map* es una correspondencia que se realiza entre el código original y el código transformado.

   Véase [source-map-loader](https://webpack.js.org/loaders/source-map-loader/)

## Referencias

* [Repo ULL-ESIT-PL/async-js-series-webpack](https://github.com/ULL-ESIT-PL/async-js-series-webpack)
* La sección [The Async Module]({{site.baseurl}}/assets/temas/introduccion-a-javascript/async-js) de estos apuntes
* [A pure ESM version of Async](https://www.npmjs.com/package/async-es)
* [Webpack: Getting started](https://webpack.js.org/guides/getting-started/)
* [Webpack devserver](https://webpack.js.org/configuration/dev-server/)

<!--
## Soluciones

* [Solución](https://github.com/ULL-ESIT-PL/async-js-series-webpack-private/blob/private/load-scripts.html)
* ```
      [~/.../load-script-seq(private)]$ pwd -P
      /Users/casiano/local/src/javascript/learning/async/load-script-seq
  ```
* `/Volumes/2020/sytws/sytws2021/p8-t2-async-serialize-12-03-2020-09-16-48/alu0101040882` Daniel Labena
-->