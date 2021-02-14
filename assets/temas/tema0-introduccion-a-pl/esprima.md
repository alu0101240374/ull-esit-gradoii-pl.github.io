---
---
## Esprima/Espree Examples

En el [Repo ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk) encontrará el material de esta lección.
**Clone este repo**.


[Espree](https://github.com/eslint/espree) started out as a fork of [Esprima](http://esprima.org) v1.2.2, the last stable published released of Esprima before work on ECMAScript 6 began. [Espree](https://github.com/eslint/espree) is now built on top of [Acorn](https://github.com/ternjs/acorn), which has a modular architecture that allows extension of core functionality. The goal of [Espree](https://github.com/eslint/espree) is to produce output that is similar to Esprima with a similar API so that it can be used in place of Esprima.

### REPL example

Una vez clonado el [repo ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk), arranque el bucle REPL de Node.JS:

```
➜  esprima-pegjs-jsconfeu-talk git:(master) node
Welcome to Node.js v14.4.0.
Type ".help" for more information.
```

Cargamos `espree`:

```js
> const espree = require('espree')
undefined
> espree.version
'7.3.1'
> espree.latestEcmaVersion
12
> espree.supportedEcmaVersions
[
  3,  5,  6,  7, 8,
  9, 10, 11, 12
]
```
Hagamos un análisis léxico:

```js
> espree.tokenize('answer = /* comment*/ 42', { range: true })
[
  Token {
    type: 'Identifier',
    value: 'answer',
    start: 0,
    end: 6,
    range: [ 0, 6 ]
  },
  Token {
    type: 'Punctuator',
    value: '=',
    start: 7,
    end: 8,
    range: [ 7, 8 ]
  },
  Token {
    type: 'Numeric',
    value: '42',
    start: 22,
    end: 24,
    range: [ 22, 24 ]
  }
]
```

Hagamos ahora un análisis sintáctico:

```js
> espree.parse('const answer = 42', { tokens: true })
Uncaught [SyntaxError: The keyword 'const' is reserved
] {
  index: 0,
  lineNumber: 1,
  column: 1
}
```
La versión por defecto de `espree` es la 5 y no admite `const`

Especifiquemosle la versión ECMA que queremos:

```js
> espree.parse('const answer = 42', { ecmaVersion: espree.latestEcmaVersion, tokens: true })
Node {
  type: 'Program',
  start: 0,
  end: 17,
  body: [
    Node {
      type: 'VariableDeclaration',
      start: 0,
      end: 17,
      declarations: [Array],
      kind: 'const'
    }
  ],
  sourceType: 'script',
  tokens: [
    Token { type: 'Keyword', value: 'const', start: 0, end: 5 },
    Token { type: 'Identifier', value: 'answer', start: 6, end: 12 },
    Token { type: 'Punctuator', value: '=', start: 13, end: 14 },
    Token { type: 'Numeric', value: '42', start: 15, end: 17 }
  ]
}
```

Observe que el Árbol no aparece completo. El log que usa el bucle REPL de Node lo trunca en el hijo `declarations` (sólo nos muestra que es un array `[Array]` sin expandirlo) para que la salida no sea excesivamente larga.

Para que nos muestre el árbol vamos a usar el método `util.inspect` del módulo `util` 
que convierte un objeto en una string:

```js
> const util = require('util')
undefined
> console.log(util.inspect(espree.parse('const answer = 42',{ecmaVersion: 6}), {depth: null}))
Node {
  type: 'Program',
  start: 0,
  end: 17,
  body: [
    Node {
      type: 'VariableDeclaration',
      start: 0,
      end: 17,
      declarations: [
        Node {
          type: 'VariableDeclarator',
          start: 6,
          end: 17,
          id: Node {
            type: 'Identifier',
            start: 6,
            end: 12,
            name: 'answer'
          },
          init: Node {
            type: 'Literal',
            start: 15,
            end: 17,
            value: 42,
            raw: '42'
          }
        }
      ],
      kind: 'const'
    }
  ],
  sourceType: 'script'
}
undefined
```



## ASTExplorer

* <a href="https://astexplorer.net/" target="_blank">astexplorer.net demo</a>
* <a href="https://astexplorer.net/#/gist/b5826862c47dfb7dbb54cec15079b430/latest" target="_blank">AST de <code>answer = 42</code></a>

* [More Advanced examples from the talk *Master the Art of the AST*](master-the-art-of-the-ast)

### PEG.js Example

[altjs.js](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk/blob/master/altjs.js) is the code for the "AltJS language in 5 minutes" section
presented in the second half of the [talk Parsing, Compiling, and Static Metaprogramming](http://2013.jsconf.eu/speakers/patrick-dubroy-parsing-compiling-and-static-metaprogramming.html) by Patrick Dubroy

### Extra Special Bonus!

`idgrep.coffee` (and [idgrep.js](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk/blob/master/idgrep.js) is another example of using Esprima
to do static analysis on JavaScript code.

```
➜  esprima-pegjs-jsconfeu-talk git:(master) node idgrep.js 
2:11:   function hacky_function() {
3:9:      var hack = 3;
```



