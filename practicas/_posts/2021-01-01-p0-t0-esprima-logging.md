---
layout: single
title: p0-t0-esprima-logging
myurl: https://campusvirtual.ull.es/1920/mod/assign/view.php?id=187733
name: p0-t0-esprima-logging
permalink: /tema0-introduccion-a-pl/practicas/p0-t0-esprima-logging/
category: practicas
published: false
---

# Práctica {{ page.title }}

El programa `logging-espree.js`  implementa una función `addLogging` que cuando se llama 
modifica el código de entrada 
produciendo como salida un código que inserta  mensajes de `console.log` a la entrada de cada 
función. Por ejemplo, cuando se llama con esta entrada:

```js
addLogging(`
function foo(a, b) {   
  var x = 'blah';   
  var y = (function () {
    return 3;
  })();
}     
foo(1, 'wut', 3);
`);
```

* [AST de la función de entrada usada como ejemplo](https://astexplorer.net/#/gist/b5826862c47dfb7dbb54cec15079b430/latest)

produce una salida como esta:

```
[~/javascript-learning/esprima-pegjs-jsconfeu-talk(private)]$ node logging-espree.js 

```
```js
function foo(a, b) {
    console.log('Entering foo()');
    var x = 'blah';
    var y = function () {
        console.log('Entering <anonymous function>()');
        return 3;
    }();
}
foo(1, 'wut', 3);
```

Este es el código de `logging-espree.js`: 

```
[~/javascript-learning/esprima-pegjs-jsconfeu-talk(private)]$ cat logging-espree.js 

```

```js
const escodegen = require('escodegen');
const espree = require('espree');
const estraverse = require('estraverse');

function addLogging(code) {
    const ast = espree.parse(code);
    estraverse.traverse(ast, {
        enter: function(node, parent) {
            if (node.type === 'FunctionDeclaration' ||
                node.type === 'FunctionExpression') {
                addBeforeCode(node);
            }
        }
    });
    return escodegen.generate(ast);
}

function addBeforeCode(node) {
    const name = node.id ? node.id.name : '<anonymous function>';
    const beforeCode = "console.log('Entering " + name + "()');";
    const beforeNodes = espree.parse(beforeCode).body;
    node.body.body = beforeNodes.concat(node.body.body);
}

console.log(addLogging(`
function foo(a, b) {   
  var x = 'blah';   
  var y = (function () {
    return 3;
  })();
}
foo(1, 'wut', 3);
`));
```

[Trasparencias explicando este código](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk/blob/master/jsconfeu-logging.pdf)

Se pide:

1. Acepte la asignación Classroom de esta tarea
2. Rellene su entrada en este formulario poniendo su código de github junto a su alu 
3. En la tarea del Campus basta con entregar el enlace al repositorio
4. Ejecute paso a paso el código de `logging.js` usando el debugger de chrome, intentando comprender el funcionamiento de la transformación realizada. Haga un resumen de lo que ha aprendido en el fichero Markdown: `README.md` 
5. Modifique el programa para que los `console.log` insertados informen de los valores de los parámetros pasados a la función.
   
Vea el siguiente ejemplo de como debe funcionar una solución:

```
$ ./p0-t0-esprima-logging-sol.js 
Usage: p0-t0-esprima-logging-sol [options] <filename> [...]
 
Options:
  -V, --version            output the version number
  -o, --output <filename>  
  -h, --help               output usage information
[~/javascript-learning/esprima-pegjs-jsconfeu-talk(private)]$ cat input.js 
```

El programa usado hace un parsing de la línea de comandos mediante el módulo npm [commander.js](https://www.npmjs.com/package/commander). Puede encontrar ejemplos en el directorio
[examples](https://github.com/tj/commander.js/tree/master/examples) del repo del modulo
[commander.js](https://www.npmjs.com/package/commander).

Cuando lo ejecutamos con la opción `-V` nos da la versión:

```
$ ./p0-t0-esprima-logging-sol.js -V
0.1.0
```

Con la  opción `-o input-log.js` especificamos el fichero de salida. El programa 
muestra los contenidos del fichero de entrada:

```
$ ./p0-t0-esprima-logging-sol.js -o input-log.js input.js 
input:
```
```js
function foo(a, b) {
  var x = 'blah';
  var y = (function (z) {
    return z+3;
  })(2);
}
foo(1, 'wut', 3);
```

Al volcar la salida, vemos que el fichero de entrada ha sido transformado correctamente:

```
---
Output in file 'input-log.js'
$ cat input-log.js
```
```js
function foo(a, b) {
    console.log(`Entering foo(${ a },${ b })`);
    var x = 'blah';
    var y = function (z) {
        console.log(`Entering <anonymous function>(${ z })`);
        return z + 3;
    }(2);
}
foo(1, 'wut', 3);
---
```

Si ejecutamos la salida obtenemos la traza esperada:

```
$ node input-log.js 
Entering foo(1,wut)
Entering <anonymous function>(2)
```

## Q & A

### Question: Backticks in espree

> Trabajando y experimentando con el método `parse()` del compilador `espree`, he comprobado que es incapaz de procesar cadenas de caracteres que posean en su interior el signo  \`,  que es usado en JS para crear cadenas de caracteres que pueden aprovecharse de la interpolación de expresiones. 

> En concreto, y a modo de ejemplo, el error me ha surgido al intentar ejecutar 
`parse()` pasando como argumento:  

```js
"console.log(`prueba`)"
```

> Me preguntaba si el analizador léxico carece verdaderamente de la capacidad para interpretar dicho símbolo y, en caso afirmativo, cómo aprovechar la mecánica de interpolación de expresiones al utilizar el analizador.
En concreto, el error que se obtiene es:  

```
SyntaxError: Unexpected character '`'.
```

### Answer: Use option `{ecmaVersion:6}`

```js

[~/javascript-learning/esprima-pegjs-jsconfeu-talk(private)]$  node
Welcome to Node.js v12.10.0.
Type ".help" for more information.
> code3 = "console.log(`prueba`)"
'console.log(`prueba`)'
> const { parse } = require('espree')
undefined
> parse(code3, {ecmaVersion:6})
Node {
  type: 'Program',
  start: 0,
  end: 21,
  body: [
    Node {
      type: 'ExpressionStatement',
      start: 0,
      end: 21,
      expression: [Node]
    }
  ],
  sourceType: 'script'
}
```

## Recursos

* [Una Solución](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk-private/blob/private/p0-t0-esprima-logging-sol.js) (No disponible)