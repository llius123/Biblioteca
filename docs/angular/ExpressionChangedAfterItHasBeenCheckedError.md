---
layout: default
title: ExpressionChangedAfterItHasBeenCheckedError
parent: Angular
---

# ExpressionChangedAfterItHasBeenCheckedError

Este es el famoso error que siempre sale y nunca consigo arreglarlo.

```javascript
ERROR Error: ExpressionChangedAfterItHasBeenCheckedError: Expression has changed after it was checked. Previous value: 'null: [
  {
```

***Que significa este error***

(Yo creo que significa:) Que estoy cambiando las propiedades de un objeto mucho mas 'rapido' de lo que angular es capaz de verificarlo.

*Por asi decirloe stoy cambiando la propiedad de un objeto (ejemplo un boolean) de true a false y luego otra vez a true, todo seguido sin dejar tiempo a angular o a que los componentes hijos de angular se enteren de este cambio*

***Solucion***

La solucion que he ecnontrado a este problem viene de la mano de ChangeDetector de angular.

Ejemplo de solucion:

*app.component.html*

```html
<app1>
	<app2
		[input]="input"
    >
    <app2/>
<app1>
```

*app2.component.html*

```html
<ng-container *ngIf="input">
	hola
<ng-container/>
<ng-container *ngIf="!input">\
	adios
<ng-container/>
```

Hay que imaginar que en app.component hay funciones que estan cambiando el valor de `input` .

Si alguna vez el valor de `input` cambia muy rapido el componente hijo `app2` tambien se tendra que actualizar y entonces saltara el siguiente error `ExpressionChangedAfterItHasBeenCheckedError`

***Solucion***

Si el error te lleva a una parte concreta del ts mejor si no hay que revisar donde puede cambiar el valor de `input` y añadir esta linea

` this.cd.detectChanges(); (cd === protected cd: ChangeDetectorRef)`.

Donde `cd` esta definido en el constructor de `app.component.ts`.

> Esto se tiene que hacer en el componente padre, que es el que esta cambiando el valor de input

***Links a leer sobre este tema***

[Que es el error ExpressionChangedAfterItHasBeenCheckedError y como solucionarlo](https://medium.com/better-programming/expressionchangedafterithasbeencheckederror-in-angular-what-why-and-how-to-fix-it-c6bdc0b22787)

[Entiendiendo la deteccion de cambios](https://blog.maestriajs.com/blog/angular/Angular-Detect-Changes/)

