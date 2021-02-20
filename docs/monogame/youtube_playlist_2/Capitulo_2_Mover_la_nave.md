---
layout: default
title: Capitulo 2 Mover la nave
parent: Youtube playlist 2
grand_parent: Monogame
nav_order: 2
---

1.  Crear la Keyboard class
2.  Crear variables globales para el Keyboard e inicializarlo
3.  Crear la clase nave
4.  Usar el teclado para mover la nave

---

- Crear una carpeta llamada Input (Source → Engine → Input)
- Crear otra llamada Keyboard (Source → Engine → Source → Input → Keyboard)
- Meter `McKeyboard.cs` en Input
- Meter `McKey.cs` en Keyboard

> Estas 2 clases las deja el tio para descargar en el youtube

- Cambiar arriba en el nameespace el nombre ya que no tendran el mio
- Crear una variable en `Global.cs` → `public static McKeyboard keyboard`
- Cargarlo en `Main.cs` → `LoadContent()` → `Globals.keyboard = new McKeyboard();`
- `Main.cs` → `Update()`

  ...Update()
  {
  Globals.keyboard.Update();
  world.update()
  Globals.keyboard.UpdateOld();
  }

- Crear carpeta Gameplay (Source → Gameplay)
- Dentro de Gameplay World (Source → Gameplay → World)
- Mover `World.cs` a la carpeta Gameplay
- Crear clase `Hero.cs`en la carpeta World
- Añadir el codigo en `Hero.cs`

  public class Hero : Basic2d
  {
  public Hero(string PATH, Vector2 POS, Vector DIMS): base(PATH, POS, DIMS)
  {
  }
  public override void Update()
  {
  base.Update();
  }
  public override void Draw()
  {
  base.Draw();
  }
  }

- Modificar la clase `World.cs`

  public Base2d hero; -> public Hero hero;
  hero = new Base2d(...) -> hero - new Hero(...)

- Modificar `Hero.cs`

  ...Update()
  {
  if (Globals.keyboard.GetPress("A"))
  {
  pos = new Vector2(pos.X -1, pos.Y)
  }
  if (Globals.keyboard.GetPress("D"))
  {
  pos = new Vector2(pos.X +1, pos.Y)
  }
  if (Globals.keyboard.GetPress("W"))
  {
  pos = new Vector2(pos.X, pos.Y -1)
  }
  if (Globals.keyboard.GetPress("S"))
  {
  pos = new Vector2(pos.X, pos.Y + 1)
  }
  }
