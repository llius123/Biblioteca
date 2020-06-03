---
layout: default
title: Enumerados en html
parent: Angular
---

# Enumerados en html

En esta ocasion se me planteo una tarea donde tenia que usar enumerados y hacer un `ngSwitch` en la parte de html.

Ejemplo del problema

html

```html
<div [ngSwitch]="switch">
  <button *ngSwitchCase="TEST_ENUM.uno" (click)=cambiar(TEST_ENUM.dos)>1</button>
  <button *ngSwitchCase="TEST_ENUM.dos" (click)=cambiar(TEST_ENUM.tres)>2</button>
  <button *ngSwitchCase="TEST_ENUM.tres" (click)=cambiar(TEST_ENUM.uno)>3</button>
</div>
```

ts

```javascript
import { Component, VERSION } from '@angular/core';
export enum test{
  uno,dos,tres
}
@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent  {
  switch= test.uno;

  cambiar(test: test){
    this.switch = test;
  }
}
```

Error

```
Error in src/app/app.component.html (2:23)
Property 'test' does not exist on type 'AppComponent'.
```

Esto que significa?

Que no se puede poner a piñon el enumerado que he definido en el ts en la parte de html.

**Solucion**

Crear una variable y inicializarla con el enumerado, tal que asi:

ts

```javascript
import { Component, VERSION } from '@angular/core';
export enum TEST_ENUM{
  uno,dos,tres
}
@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent  {
  switch = TEST_ENUM.uno;
  // Aqui esta creada
  enumAux = TEST_ENUM;

  cambiar(test: TEST_ENUM){
    this.switch = test;
  }
}
```

html

```html
<div [ngSwitch]="switch">
  <button *ngSwitchCase="enumAux.uno" (click)=cambiar(enumAux.dos)>1</button>
  <button *ngSwitchCase="enumAux.dos" (click)=cambiar(enumAux.tres)>2</button>
  <button *ngSwitchCase="enumAux.tres" (click)=cambiar(enumAux.uno)>3</button>
</div>
```

Y ahora ya no sale el error y ademas funciona correctamente.

> Curiosidad:
>
> No se puede tipar esta variable `enumAux: TEST_ENUM = TEST_ENUM;`
>
> Tampoco se puede hacer esto `enumAux: TEST_ENUM;` ya que la variable esta 'vacia' y salta error.