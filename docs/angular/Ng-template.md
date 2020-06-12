---
layout: default
title: Ng template
parent: Angular
---

# Ng-template

Esta es otra forma de pasar dinamicamente html templates a componentes hijos.

Otra forma mas simple es la que aparece explciada en `ng-container` revisar y elejir una de las opciones que mas interese.

**Empezamos**

Con ng-template lo que se quiere hacer es pasar al componente hijo un template html, esto lo que permite es definir un componente hijo con una funcionalidad determinada y ademas añadir un placeholder donde puedes meter un nuevo template sin tener que modificar el componente hijo entero.

**Ejemplo de uso**

Tengo un componente checkbox que tiene un checkbox normal

`<input type="checkbox"`

*Modificacion que se quiere hacer:*

Otro cliente en vez de querer ver los iconos por defecto del checkbox, quiere que salgan unos `custom`

Tenemos que modificar el componente checkbox y añadir logica solo para ese cliente? NO

*Solucion:* 

html componente padre

```html
<checkbox-component>
  <ng-template CustomCheckboxDirective>
        <img ...>
  </ng-template>
</checkbox-component>
```

html componente hijo

```html
<ng-container *ngIf="customCheckbox: else customHTMLCheckbox">
  <input type="checkbox">
</ng-container>
<ng-template #customHTMLCheckbox [ngTemplateOutlet]="customCheckboxTemplate">
</ng-template>
```

ts componente hijo

```typescript
@ContentChild(CustomCheckboxDirective, { static: true }) customCheckboxTemplate: TemplateRef<any>;
```

Directiva

```typescript
import { Directive, TemplateRef } from '@angular/core';
@Directive({
 selector: '[CustomCheckboxDirective]'
})
export class CustomCheckboxDirective {
 constructor(public template: TemplateRef<any>) { }
}
```

**Explicacion del codigo**

Lo que se esta haciendo aqui es pasar a traves de la directiva `CustomCheckboxDirective` un TemplateRef al componente hijo para que lo pinte en el lugar que esta definido



**Ejemplo 2 completo**

app.component.ts

> Componente padre

```typescript
import { Component, VERSION } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
  padre
  <app1>
    <ng-template>
      hijo
    </ng-template>
    <ng-template test>
      hijo2
    </ng-template>
  </app1>
  `,
  styles: [ '' ]
})
export class AppComponent  {
}
```

app1.component.ts

> Componente hijo

```typescript
 import { Component, Input, ContentChild, TemplateRef, OnInit, AfterViewInit } from '@angular/core';
import { TestDirective } from './directive.directive';

@Component({
  selector: 'app1',
  template: `
  hijo
  <ng-template [ngTemplateOutlet]="testTemplate" >
  </ng-template>
  `,
  styles: [`h1 { font-family: Lato; }`]
})
export class App1Component {
  @ContentChild(TestDirective, { static: true, read: TemplateRef }) testTemplate: TemplateRef<any>;
}
```

directive.directive.ts

```typescript
import { Directive, TemplateRef } from '@angular/core';
@Directive({
  selector: '[test]'
})
export class TestDirective {
  constructor(public template: TemplateRef<any>) { }
}
```

Resultado

![image-20200611102504914](img\image-20200611102504914.png)

> Recordatorio:
>
> Acordarse de definir en el `decalrations` del modulo la directiva