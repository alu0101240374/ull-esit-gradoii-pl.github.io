---
---
## Esprima/Espree Examples

En el [Repo ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk](https://github.com/ULL-ESIT-GRADOII-PL/esprima-pegjs-jsconfeu-talk) encontrará el material de esta lección


Espree started out as a fork of [Esprima](http://esprima.org) v1.2.2, the last stable published released of Esprima before work on ECMAScript 6 began. Espree is now built on top of [Acorn](https://github.com/ternjs/acorn), which has a modular architecture that allows extension of core functionality. The goal of Espree is to produce output that is similar to Esprima with a similar API so that it can be used in place of Esprima.

### REPL example

```js
> esprima = require('esprima')
{ parse: [Function: parse],
  parseModule: [Function: parseModule],
  parseScript: [Function: parseScript],
  tokenize: [Function: tokenize],
  Syntax: 
   { ... },
  version: '4.0.1' }

> esprima.tokenize('answer = 42', { range: true })
[ { type: 'Identifier', value: 'answer', range: [ 0, 6 ] },
  { type: 'Punctuator', value: '=', range: [ 7, 8 ] },
  { type: 'Numeric', value: '42', range: [ 9, 11 ] } ]

> esprima.parseScript('const answer = 42', { tokens: true })
Script {
  type: 'Program',
  body: 
   [ VariableDeclaration {
       type: 'VariableDeclaration',
       declarations: [Array],
       kind: 'const' } ],
  sourceType: 'script',
  tokens: 
   [ { type: 'Keyword', value: 'const' },
     { type: 'Identifier', value: 'answer' },
     { type: 'Punctuator', value: '=' },
     { type: 'Numeric', value: '42' } ] }

> inspect = require('util')
{ ... }

> console.log(util.inspect(esprima.parseScript('answer = 42'), {depth: null}))
Script {
  type: 'Program',
  body: 
   [ ExpressionStatement {
       type: 'ExpressionStatement',
       expression: 
        AssignmentExpression {
          type: 'AssignmentExpression',
          operator: '=',
          left: Identifier { type: 'Identifier', name: 'answer' },
          right: Literal { type: 'Literal', value: 42, raw: '42' } } } ],
  sourceType: 'script' }
undefined
> 
```

### PEG.js Example

`altjs.coffee` is the code for the "AltJS language in 5 minutes" section
presented in the second half of the talk.

### Extra Special Bonus!

`idgrep.coffee` (and `idgrep.js`) is another example of using Esprima
to do static analysis on JavaScript code.


## ASTExplorer

* <a href="https://astexplorer.net/" target="_blank">astexplorer.net demo</a>
* <a href="https://astexplorer.net/#/gist/b5826862c47dfb7dbb54cec15079b430/latest" target="_blank">AST de <code>answer = 42</code></a>

* [More Advanced examples from the talk *Master the Art of the AST*](master-the-art-of-the-ast)

