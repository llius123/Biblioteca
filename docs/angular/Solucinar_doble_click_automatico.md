---
layout: default
title: Evitar doble click automatico
parent: Angular
---

# Evitar doble click automatico

## Problema

Por ejemplo este trozo de codigo

```html
<children-component (click)="click()">
</children-component>
```

Lo que estoy haciendo aqui es ejecutar el `ng-click` directamente desde el componente hijo.

El problema esta en que no se porque, la funcion `click()` se ejecuta 2 o mas veces.

## Solucion

En internet he encontrado esta solucion para angular 1x, que por casualidad tambien funciona en angular 2x.

[Stackoverflow](https://stackoverflow.com/a/45773028)

La solucion que proponen es la siguiente:

```html
<children-component (click)="click();$event.preventDefault()">
</children-component>
```

La solucion no es de angular si no del propio js.

[MDN](https://developer.mozilla.org/es/docs/Web/API/Event/preventDefault)

Lo que yo he entendido de MDN es que lo que hace `preventDefault()` es parar la ejecucion del evento.

Por lo tanto yo hago click y `preventDefault()` para la repeticion de la ejecucion del evento hasta que yo le vuelva a dar