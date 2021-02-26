---
title: Práctica npm Module
published: true
rubrica: false
categories: [ "practica" ]
---

## Objetivos

Partiendo de la práctica [Espree Logging]({{site.baseurl}}/practicas/esprima-logging) construya un paquete npm y 
publíquelo en [npmjs](https://www.npmjs.com/) con ámbito `@aluXXX` y con nombre `addlogging` 

El módulo además de exportar la función `addLogging` provee un ejecutable `add-logging` que se llama así:

```
add-logging --pattern 'temperature' --output salida.js input.js
```

e inserta los mensajes de logs a la entrada de las funciones que casan con el patrón `temperature` que aparecen en  el fichero de entrada especificado `input.js`.


La mayor parte de los conceptos y habilidades a adquirir con esta práctica se explican en la sección [Creating and publishing a node.js module en GitHub y en NPM]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module). Léala con detenimiento antes de hacer esta práctica. 

## Ámbitos

Deberá publicar el paquete en [npmjs](https://www.npmjs.com/) con ámbito `@aluXXX` y con nombre `addlogging`.

Para saber sobre ámbitos, vea la sección [Scopes and Registries]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#scopes-and-registries).

## Pruebas

Deberá añadir pruebas usando [Mocha y Chai]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#testing-with-mocha-and-chai) o [Jest]({{site.baseurl}}/assets/temas/introduccion-a-javascript/jest).
Repase las secciones [Testing with Mocha and Chai]({{site.baseurl}}/assets/temas/introduccion-a-javascript/#testing-with-mocha-and-chai) y [Jest]({{site.baseurl}}/assets/temas/introduccion-a-javascript/jest).

## Documentación

[Documente]({{site.baseurl}}/assets/temas/introduccion-a-javascript/documentation)
el módulo incorporando un `README.md` y la documentación de la función exportada.
Repase la sección [Documenting the JavaScript Sources]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#documenting-the-javascript-sources)

## Pruebas de Producción

En el repo asignado `testing-addlogging-aluXXX` añada las pruebas necesarias
para comprobar que la última versión del paquete publicado se instala y puede ser usado.
Repase la sección [Testing in Production]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#testing-in-production)

## Superproject with Git Submodule

Usando `git submodule` configure como super-project el repo asignado `super-addloggin-aluXXX` para que contenga
a a los dos repos: en el que ha desarrollado el módulo npm `addlogging-aluXXX` y el repo para las pruebas en tiempo de producción `testing-addlogging-aluXXX`.

Repase la sección [Making a Project with the two repos: git submodule]({{site.baseurl}}//assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#making-a-project-with-the-two-repos-git-submodule)

## Semantic Versioning

Publique alguna mejora en la funcionalidad del módulo.  
Por poner algunos ejemplos 
* puede hacer que el ejecutable `add-logging` admita como especificación de patrón  una expresión regular, 
* que admita mas de un fichero de entrada,  
* que admita un directorio (en cuyo caso procesaría todos los ficheros `*.js` en el directorio),
* etc.

¿Como debe en tales casos cambiar el nº de versión?

Repase la sección [Semantic Versioning]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#semantic-versioning)

## References

* [Creating and Publishing a node.js Module in GitHub and NPM Registries]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module)
* [Jest]({{site.baseurl}}/assets/temas/introduccion-a-javascript/jest)
* [Módulos]({{site.baseurl}}/assets/temas/introduccion-a-javascript/modulos)
* [Node.js Packages]({{site.baseurl}}/assets/temas/introduccion-a-javascript/nodejspackages)
* [Documentation]({{site.baseurl}}/assets/temas/introduccion-a-javascript/documentation)
* [Instalación de Módulos desde GitHub]({{site.baseurl}}/assets/temas/introduccion-a-javascript/nodejspackages.html#instalaci%C3%B3n-desde-github)
* [Introducción a los Módulos en JS](https://lenguajejs.com/automatizadores/introduccion/commonjs-vs-es-modules/) por Manz
* [@ull-esit-dsi-1617/scapegoat](https://www.npmjs.com/package/@ull-esit-dsi-1617/scapegoat) en npm
* [How to install an npm package from GitHub directly?](https://stackoverflow.com/questions/17509669/how-to-install-an-npm-package-from-github-directly) in StackOverflow
* [Working with scoped packages](https://docs.npmjs.com/getting-started/scoped-packages)
* [npm-scope manual: Scoped packages](https://docs.npmjs.com/misc/scope#publishing-public-scoped-packages-to-the-public-npm-registry)
* [Package.json documentation en npm site](https://docs.npmjs.com/files/package.json)
* Semantic versioning and npm
    * [Semantic versioning and npm](https://docs.npmjs.com/getting-started/semantic-versioning)
    * [Semantic Versioning: Why You Should Be Using it](https://www.sitepoint.com/semantic-versioning-why-you-should-using/) SitePoint
    * [YouTube Video: Semantic versioning and npm](https://youtu.be/kK4Meix58R4)
    * [El comando npm version](https://docs.npmjs.com/cli/version)
