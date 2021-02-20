---
layout: default
title: Como ejecutar ngOnInit cuando extiendo de una clase padre
parent: Angular
---

```javascript
class CLASE1 implements OnInit {
  ngOnInit() {
    //does some stuff here
  }
}

class CLASE2 extends GoogleCharts implements OnInit {
  ngOnInit() {
    super.ngOnInit();
    //do my stuff here
  }
}
```

De esta forma lo que estoy haciendo en la clase 2 es ejecutar el ngOnInit de la clase 1 y despues ejecutar mis cosas sin sobreescribir

[Stackoverflow](https://stackoverflow.com/a/44546517)
