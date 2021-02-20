---
layout: default
title: Capitulo 3 Rotate hero Towards mouse
parent: Youtube playlist 2
grand_parent: Monogame
nav_order: 3
---

1.  Crear una clase Raton
2.  Inicializar la clase
3.  Edit basic2d to add offset and origin to draw, and draw the cursor
4.  Adsd rot to Basic2d, adn speed to hero
5.  Add rotate Towards() to global
6.  Use the mouse position and rotate hero

---

- Añadir `McMouseControl.cs` a Input
- Añadir este codigo a `Globals.cs`

  public static int screenHeight, creenWidth;

  public static McMouseControl mouse;
  public static float GetDistance(Vector2 pos, Vector2 target)
  {
  return (float)Math.Sqrt(Math.Pow(pos.X - target.X, 2) + Math.Pow(pos.Y - target.Y, 2));
  }

- Añadir en `Main.cs`

  - `LoadContent()` → `Globals.mouse = new McMouseControl();`
  - `Update()`

  Globals.mouse.Update();
  ...
  Globals.mouse.UpdateOld();

- Añadir `public float rot;` en `Basic2d.cs`
- Modificar `Basic2d.cs` asi

  public virtual void Draw() -> public virtual void Draw(Vector2 OFFSET)
  new Rectangle(pos.X, pos.Y) -> new Rectangle((int)(pos.X + OFFSET.X), (int)(pos.Y + OFFSET.Y))

- Crear el metodo `Draw(Vector2 OFFSET, Vector2 ORIGIN)`

> Copiar el metodo que ya existe de Draw() y modificar `new Vector2(myModel.Bounds…. → new Vector2(ORIGIN.X, ORIGIN.Y)`
>
> Y `0.0f` a `rot`

- Saltara un error en `Hero.cs` → `Draw()`. Se aregla tal que asi `…Draw(Vector2 OFFSET)` y `base.Draw(OFFSET)`
- En `World.cs` tambien saltara error y se aregla tal que asi `…Draw(Vector2 OFFSET)` y `base.Draw(OFFSET)`
- En `Main.cs` tambien saltara error y se aregla tal que asi `world.Draw(Vector2.Zero);`
- En `Main.cs` en `Draw(…)` añadir `cursor.Draw(new Vector2(Globals.mouse.newMousePos.X, Globals.mouse.newMousePos.Y), new Vector2(0,0));`
- En `Main.cs` en `LoadContent()` → `cursor = new Basic2d("2d\\Misc\\CursorArrow", new Vector2(0,0), new Vector2(28,28))`
- En `Hero.cs` → `public float speed;`
- Modificar y añadir a todas las posiciones la velocidad (`pos = new Vector2(pos.X + speed , pos.Y)`)
- Inicializar en el contructor la velocidad → `speed = 2.0f;`
- Ir a `Hero.cs` en Update() → `rot = Globals.RotateTowards(pos, new Vector2(Globals.mouse.newMousePos.X, Globals.mouse.newMousePos.Y))`
