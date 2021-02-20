---
layout: default
title: Capitulo 4 Proyectiles y timers
parent: Youtube playlist 2
grand_parent: Monogame
nav_order: 4
---

1.  Clean up code, Add Unit class
2.  Add Timer class
3.  Assign Globals.screenWidth/Height
4.  Create Projectile class
5.  Create Fireball Class
6.  Add PassObject to Globals, then Add PassProjectile to GameGlobals
7.  Add list of Projectiles to world, loop, update, and draw
8.  Have hero create Projectiles on click

---

- Gameplay → World Copiar la clase `Hero.cs` y llamarlo `Unit.cs`
- `Unit.cs` Borrar contenido de `Update()`
- `Hero.cs`cambiar clase que hereda, ya no lo hace de `Basic2d` ahora lo hace de `Unit`
- Crear carpeta Gameplay → World → Units
- Meter `Hero.cs`en carpeta Gameplay → World → Units
- Añadir este codigo a  `Main.cs` → `Initialize()`

  Globals.screenWidth = 1600;
  Globals.screenHeight = 900;
  graphics.PreferredBackBufferWidth = Globals.screenWidth;
  graphics.PreferredBackBufferHeight = Globals.screenHeight;
  graphics.ApplyChanges();

- Añadir el archivo `McTimer.cs` a Engine
- Crear en `Globals.cs` otra variable mas que se llame `public static GameTime gameTime;`
- En `Main.cs` → `Update()` añadir este codigo `Globals.gameTime = gameTime;`
- Nueva clase en Gameplay → World nombre `Projectile2d.cs`
- `Projectile2d.cs` Hacer la clase public y heredar de Basic2d

  - Copiar el constructor de Hero.cs y la variable speed y pegarlo en Projectile
  - Crear la variable `public Unit owner;`
  - Modificar el constructor y que tenga que recibir un parametro mas `…, Unit OWNER)`
  - Setear la variable de arriba owner con  la nueva variable en el constructor `owner = OWNER`
  - Crear variable `public Vector2 direction;` , `public bool done;` `public McTimer timer;`
  - Modificar el constructor y añadir `…, Vector2 TARGET)`
  - Setear en el constructor `done = false;`
  - Modificar speed a 5.0f
  - Setear direction `direction= TARGET - owner.pos;`
  - Normalizar la direccion `direction.Normalize();`
  - Setear timer `timer = new McTimer(1200)` Creo que son milisegundos
  - Crear el metodo Update y meter este codigo

  public virtual Update(Vector2 OFFSET, List<Unit> UNITS)
  {
  pos += direction \* speed;
  timer.UpdateTimer();
  if(timer.Test())
  {
  done = true;
  }
  if(HitSomething(UNITS))
  {
  done = true;
  }
  }
  public virtual bool HitSomething(List<Unit> UNITS)
  {
  return false;
  }
  public override void Draw(Vector2 OFFSET)
  {
  base.Draw(OFFSET);
  }

- Añadir carpeta GamePlay → World → Projectiles
- Crear archivo `Fireball.cs` en Projectiles y es una copia de `Projectile2d.cs`
  - Fireball hereda de Projectile2d por lo tanto hay que actualizar el constructor
  - Borrar contenido de constructor
  - Borrar contenido de Update
  - Añadir `base.Update(OFFSET, UNITS)`a Update
  - Modificar el constructor para que quede tal que asi → `public Fireball(Vector2 POS, Unit OWNER, Vector2 TARGET): base("", POS, new Vetor2(20,20), OWNER, TARJET)`
- Nueva carpeta Content → 2d → Projectiles
  - Meter el png de fireball en la carpeta Projectiles
- Modificar el constructor de Fireball, cambiar “” por “2d\\\\Projectiles//Fireball”
- Crear nueva clase `GameGlobals.cs` al mismo nivel que `Main.cs`
- Añadir este codigo en `Globals.cs`

  public delegate void PassObject(object i);
  public delegate object PassObjectAndReturn(object i);
  public class Globals
  {
  ...

- Crear en `GameGlobals.cs` una variable que es `public static PassObject PassProjectile;`
- Anadir ester codigo a `Hero.cs`

  public virtual void addProjectile(object INFO)
  {
  }

- Añadir este codigo a `World()` en `World.cs` → `GameGlobals.PassProjectile = addProjectile;`
- Crear una variable de tipo lista en `Hero.cs` → `public List<Projectile2d> projectiles = new List<Projectile2d>();`
- Añadir un proyectil a la lista de proyectiles en `Hero.cs` → `addProjectile()` → `projectiles.add((Projectile2d)INFO);`
- Crear esta variable en `Hero.cs` → `public Vector2 offset;`
- Inicializar offset en el constructor de `Hero.cs` → `offset = new Vector2(0,0);`
- Añadir este codigo en `Hero.cs` → `Update()`

  ...
  hero.Update()
  for(int i=0; i<projectiles.Count; i++)
  {
  if(projectile[i].done)
  {
  projectiles.RemoveAt(i);
  i--;
  }
  projectiles[i].Update(offset, null);
  }

- Añadir este codigo en `Hero.cs` → `Draw()`

  ...
  hero.Draw(OFFSET);
  for(int i = 0: i < projectiles.Count: i++)
  {
  projectiles[i].Draw(OFFSET);
  }

- Añadir este codigo en `Hero.cs` → `Update()` (al final del metodo)

  ...
  if(Globals.mouse.leftClick())
  {
  GameGlobals.PassProjectile(new Fireball(new Vector2(pos.X, pos.Y), this, new Vector2(Globals.mouse.newMousePos.X, Globals.mouse.newMousePos.Y)));
  }

- `Projectile2d.cs` en el constructor añadir esta linea para que rote el disparo → `rot = Globals.RotateTowards(pos, new Vector2(TARGET.X, TARGET.Y))`
