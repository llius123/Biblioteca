---
layout: default
title: Como debugear AngularReactVue con vscode
parent: Angular
---

- Instalar la extension de chrome: [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
- Añadir la siguiente configuracion al launch.json del proyecto

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "Launch Chrome against localhost",
      "url": "http://localhost:4200",
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```
