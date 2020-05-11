---
layout: default
title: Docs
parent: ElectronJS
---

# Docs

## Aplicacion con angular + electron + nodegit

### Para ejecutar un script desde el electron

```javascript
const exec = require("child_process").exec;

function execute(command, callback) {
  exec(command, (error, stdout, stderr) => {
    callback(stdout);
  });
}

// call the function
execute("ping -c 4 0.0.0.0", (output) => {
  console.log(output);
});
```

https://tortoisegit.org/docs/tortoisegit/tgit-automation.html

### Fix 'X-Frame-Options' to 'deny'.

En main.js añadir esto:
```javascript
window.webContents.session.webRequest.onHeadersReceived(
  {urls: ['*://*/*']},
  (details, callback) => {
    Object.keys(details.responseHeaders).filter(x => x.toLowerCase() === 'x-frame-options')
          .map(x => delete details.responseHeaders[x])

    callback({
      cancel: false,
      responseHeaders: details.responseHeaders,
    })
  },
)
```

### Como activar el componente webview en electronJS
1. ir a main.js/main.ts y añadir una propiedad a BrownserWindow
```javascript
  win = new BrowserWindow({
  ...
    webPreferences: {
      webviewTag: true,
    },
  });
  ```
2. Ir al componente que queramos y añadirlo
> Yo en este caso lo que he hecho a sidop añadirlo dinamicamente desde el .ts
```javascript
    let webview = document.createElement("webview");
    webview.setAttribute("src", "https://github.com/");
    webview.style.display = "flex";
    webview.style.width = "100%";
    webview.style.height = "100%";
    webview.setAttribute("id", "https://github.com/");
    webview.setAttribute("partition", "persist:github");
    this.elementRef.nativeElement
      .querySelector(".webview-container")
      .appendChild(webview);
```
> [Documentacion webview de electron](https://www.electronjs.org/docs/api/webview-tag)

### Como leer las cookies
1. Esto solo se puede hacer si estoy usando este [repo](https://github.com/maximegris/angular-electron)
```javascript
      this.electronService.remote.session
        .defaultSession
        .cookies.get({})
        .then((cookie) => {
          cookie.forEach((element) => {
            console.log(element);
          });
        })
```
> [Documentacion de electronjs cookies](https://www.electronjs.org/docs/api/cookies)
