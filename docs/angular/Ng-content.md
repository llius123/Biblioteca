---
layout: default
title: Ng content
parent: Angular
---

# Ng-content

*You use the **<ng-content></ng-content>** tag as a placeholder for that dynamic content, then when the template is parsed Angular will replace that placeholder tag with your content*

Que significa esto, que ng-content es un placeholder para que desde el componente padre inyectar elementos html al componente hijo.

Ejemplo de uso de esta propiedad.

Yo tengo un componente que es una tabla.

Por defecto la celda de esta tabla mostrara datos.

El componente quedaria asi:

`table.component.ts`

`<tableCustom>`

```html
<table>
    <tr>
    	<th>
    		titulo
		</th>
	</tr>
    <tr>
    	<th *ngIf="contenido">
    		{{contenido.value}}
		</th>
        <th *ngIf="!contenido">
    		<ng-content></ng-content>
		</th>
	</tr>
</table>
```

Esto lo que hace es mostrar un titulo, y si hay contenido muestro su valor.

El valor de contenido es un string, number etc..., vamos es texto plano.

Yo ahora lo que quiero hacer es meter en contenido un datepicker, para que el usuario seleccione una fecha

La solucion es facil, desde el padre meto el datepicker asi:

`app.component.ts`

```html
<tableCustom>
    <datepicker></datepicker>
</tableCustom>
```

Y el resultado que se mostrara en el DOM sera el siguiente:

```html
<table>
    <tr>
    	<th>
    		titulo
		</th>
	</tr>
    <tr>
    	<th *ngIf="contenido">
    		{{contenido.value}}
		</th>
        <th *ngIf="!contenido">
    		<datepicker></datepicker>
		</th>
	</tr>
</table>
```

