---
layout: default
title: Capitulo 2 mover el sprite
parent: Youtube playlist
grand_parent: Monogame
nav_order: 2
---

# Capitulo 2 mover el sprite

Para mover el sprite.

---

Hay que hacerlo en la funcion `Update()`

Es un simple if que modifique la posicion del sprite.

```
if(Keyboard.GetState().IsKeyDown(Keys.W))
{
    _position.Y -= 1;
}
if (Keyboard.GetState().IsKeyDown(Keys.S))
{
    _position.Y += 1;
}
if (Keyboard.GetState().IsKeyDown(Keys.A))
{
    _position.X -= 1;
}
if (Keyboard.GetState().IsKeyDown(Keys.D))
{
    _position.X += 1;
}
```
