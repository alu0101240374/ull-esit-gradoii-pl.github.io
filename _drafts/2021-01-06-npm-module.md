---
title: Práctica npm Module
published: true
rubrica: false
categories: [ "practica" ]
---

## Objetivos

Partiendo de la práctica [Espree Logging]({{site.baseurl}}/practicas/esprima-logging) y usando el repo de la asignación de esta tarea construya un paquete npm y 
publíquelo como paquete en npmjs con ámbito `@aluAtgitHub`  y con nombre `addlogging`

El módulo además de exportar la función `addLogging` provee un ejecutable `add-logging` que inserta los mensajes de logs a la entrada de las funciones que casan con el patrón  y  el fichero de entrada especificados en línea de comandos.

```
add-logging --pattern 'temperature' --output salida.js input.js
```

La mayor parte de los conceptos y habilidades a adquirir con esta práctica se explican en la sección [Creating and publishing a node.js module en GitHub y en NPM]({{site.baseurl}}/assets/introduccion-a-javascript/creating-and-publishing-npm-module). 


## Pruebas

Deberá añadir pruebas usando [Mocha y Chai]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module#testing-with-mocha-and-chai) o [Jest]({{site.baseurl}}/assets/temas/introduccion-a-javascript/jest)

## Documentación

[Documente]({{site.baseurl}}/assets/temas/introduccion-a-javascript/documentation)
el módulo incorporando un `README.md` y la documentación de la función exportada.

## Pruebas de Producción

Publíquelo como paquete en npmjs con ámbito `@aluAtgitHub`  y con nombre `addlogging`

En el repo asignado `testing-addlogging-aluXXX` añada las pruebas
para comprobar que el paquete publicado se instala y puede ser usado correctamente.

Usando `git submodule` configure como super-project para que contenga
a ambos repos: el del módulo npm `addlogging-aluAtXXX` y el repo de pruebas de producción `testing-addlogging-aluXXX`.

## Semantic Versioning

Publique una mejora en la funcionalidad del módulo.  
Por ejemplo puede hacer que el ejecutable `add-logging` admita como especificación de patrón  una expresión regular o admita mas de un fichero de entrada.
¿Como debe en tal caso cambiar el nº de versión?

## Referencias

* Sección [Creating and publishing a node.js module en GitHub y en NPM]({{site.baseurl}}/tema1-introduccion-a-javascript/creating-and-publishing-npm-module)
* [Jest]({{site.baseurl}}/tema1-introduccion-a-javascript/jest)
* Sección [GitHub Registry]({{site.baseurl}}/assets/temas/introduccion-a-javascript/github-registry)
* Sección [GitHub Actions]({{site.baseurl}}/assets/temas/introduccion-a-javascript/github-actions)
* Sección [Módulos]({{site.baseurl}}/assets/temas/introduccion-a-javascript/modulos)
* Sección [Node.js Packages]({{site.baseurl}}/assets/temas/introduccion-a-javascript/nodejspackages)
* Sección [Documentation]({{site.baseurl}}/assets/temas/introduccion-a-javascript/documentation)


## References

* [Creating and Publishing a node.js Module in GitHub and NPM Registries]({{site.baseurl}}/assets/temas/introduccion-a-javascript/creating-and-publishing-npm-module)
* [Instalación de Módulos desde GitHub]({{site.baseurl}}/assets/temas/introduccion-a-javascript/nodejspackages.html#instalaci%C3%B3n-desde-github)
* [Introducción a los Módulos en JS](https://lenguajejs.com/automatizadores/introduccion/commonjs-vs-es-modules/) por Manz
* Talk [NODE.JS module patterns using simple examples](https://darrenderidder.github.io/talks/ModulePatterns). Trasparencias. Muestra ejemplos/patrones de exportación-importación (Reveal Slides)
* [Authoring CommonJS modules](http://know.cujojs.com/tutorials/modules/authoring-cjs-modules)  (CommonJS modules were conceived during the early days of server-side JavaScript environments such as node.js and Narwhal. As a result, CommonJS modules are optimized for these environments, not browser environments)

* [A Beginner’s Guide to npm — the Node Package Manager](https://www.sitepoint.com/beginners-guide-node-package-manager/)
* [npm](npm.html)
* [10 Tips and Tricks That Will Make You an npm Ninja](https://www.sitepoint.com/10-npm-tips-and-tricks/)

* [Creating and Publishing a Node.js Module](creating-and-publishing-npm-module) 
* El paquete de ejemplo usado en este tutorial [@ull-esit-dsi-1617/scapegoat](https://www.npmjs.com/package/@ull-esit-dsi-1617/scapegoat) en npm
* El paquete de ejemplo usado en este tutorial [@ull-esit-dsi-1617/scapegoat](https://github.com/ULL-ESIT-DSI-1617/scapegoat) en GitHub
* See [How to install an npm package from GitHub directly?](https://stackoverflow.com/questions/17509669/how-to-install-an-npm-package-from-github-directly) in StackOverflow

* [Working with scoped packages](https://docs.npmjs.com/getting-started/scoped-packages)
* [npm-scope manual: Scoped packages](https://docs.npmjs.com/misc/scope#publishing-public-scoped-packages-to-the-public-npm-registry)
* [Working with npm private modules. YouTube Video](https://youtu.be/O6JoXGnHK_Y)

* [Package.json documentation en npm site](https://docs.npmjs.com/files/package.json)


* Semantic versioning and npm
    * [Semantic versioning and npm](https://docs.npmjs.com/getting-started/semantic-versioning)
    * [Semantic Versioning: Why You Should Be Using it](https://www.sitepoint.com/semantic-versioning-why-you-should-using/) SitePoint
    * [YouTube Video: Semantic versioning and npm](https://youtu.be/kK4Meix58R4)
    * [El comando npm version](https://docs.npmjs.com/cli/version)

* npm Organizations /npm Organizaciones
    *   [Introduction](https://www.npmjs.com/docs/orgs/./)
    *   [Getting Started](https://www.npmjs.com/docs/orgs/getting-started.html)
    *   [Roles and Privileges](https://www.npmjs.com/docs/orgs/roles-and-privileges.html)
    *   [Managing Members](https://www.npmjs.com/docs/orgs/managing-members.html)
    *   [The Developers Team](https://www.npmjs.com/docs/orgs/the-developers-team.html)
    *   [Managing Teams](https://www.npmjs.com/docs/orgs/managing-teams.html)
    *   [Publishing an Org Scoped Package](https://www.npmjs.com/docs/orgs/publishing-an-org-scoped-package.html)
    *   [Configuring npm for your Org](https://www.npmjs.com/docs/orgs/configuring-npm-for-your-org.html)
    *   [Managing Package Access](https://www.npmjs.com/docs/orgs/managing-package-access.html)
    *   [Migrating a User Account](https://www.npmjs.com/docs/orgs/migrating-a-user-account.html)
    *   [Managing Billing](https://www.npmjs.com/docs/orgs/managing-billing.html)
    *   [Upgrading and Downgrading](https://www.npmjs.com/docs/orgs/upgrading-and-downgrading.html)
    *   [Renaming and/or Deleting an Org](https://www.npmjs.com/docs/orgs/renaming-and-or-deleting-an-org.html)
    * [Publishing an Org Scoped Package](https://www.npmjs.com/docs/orgs/publishing-an-org-scoped-package.html)
    * [The developers team](https://www.npmjs.com/docs/orgs/the-developers-team.html)
    - The Developers Team is a special Team that is automatically created when you create an Organization. 
    - Members are automatically added to the Developers team:
        - The user who created the Organization is added to this team automatically.
        - Any member added to the Organization is also added to this team automatically.
        - If an Owner adds a new Member to an Organization and does not want that Member to be on the Developers team, an Owner can remove them. ([Learn more about managing teams](https://www.npmjs.com/docs/orgs/managing-teams.html)).
    * [npm-team: Manage organization teams and team memberships](https://docs.npmjs.com/cli/team)
    * [npm-access: Set access level on published packages](https://docs.npmjs.com/cli/access)

* NPM: Herramientas de ayuda: release-it
    * [release-it: Interactive release tool for Git repositories](https://github.com/webpro/release-it)
    * [release-it: GitHub Page](https://webpro.github.io/release-it/)
