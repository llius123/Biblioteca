---
layout: default
title: Angular_[(ngModel)]_vs_[ngModel]_vs_(ngModel)
parent: Angular
---

Super interesante lo del ngModel.

    // This syntax:
    [(ngModel)]="expression"

    // is unwrapped by the compiler into
    [ngModel]="expression" (ngModelChanged)="expression=$event"

Link de [stack](https://stackoverflow.com/a/46123215)

Esto es interesante ya que ahora se el porque se usa `[(ngModel)]` o `[ngModel]`
