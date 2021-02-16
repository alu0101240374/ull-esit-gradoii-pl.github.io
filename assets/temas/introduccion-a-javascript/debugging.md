---
---
# Debugging with Chrome

## Debugging Client Code with Chrome

* [Debugging in Chrome in the client in javascript.info](https://javascript.info/debugging-chrome)

## Debugging NodeJS with Chrome

En la terminal:

```
➜   node --version
v14.4.0
➜   node --inspect-brk logging-espree.js
Debugger listening on ws://127.0.0.1:9229/331b3011-c7f5-447f-8731-1371c53847a5
For help, see: https://nodejs.org/en/docs/inspector
```

the option `--inspect-brk=[host:port]` does the following:

* Enable inspector agent
* Bind to address or hostname `host` (default: 127.0.0.1)
* Listen on port `port` (default: 9229)
* Break before user code starts

En el navegador abrimos la URL `chrome://inspect` y hacemos `click` en el enlace *inspect*

![]({{site.baseurl}}/assets/images/chrome-debugging-nodejs-inspect.jpg)

You can insert `debugger` statements wherever you want to set a break-point:

![]({{site.baseurl}}/assets/images/chrome-debugging-nodejs-debug-statements.jpg)

## References

* [Node.JS Debugging Guide](https://nodejs.org/en/docs/guides/debugging-getting-started/)
* Mis viejos apuntes: [Debugging NodeJS](https://casianorodriguezleon.gitbooks.io/ull-esit-1617/content/apuntes/nodejs/)
* Debugging in 2017 with Node.js YouTube video https://youtu.be/Xb_0awoShR8
    * [Debugging in 2017 with Node.js](https://youtu.be/Xb_0awoShR8) YouTube
