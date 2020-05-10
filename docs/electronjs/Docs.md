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
