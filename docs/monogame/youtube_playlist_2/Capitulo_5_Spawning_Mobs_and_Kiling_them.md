---
layout: default
title: Capitulo 5 Spawning Mobs and Kiling them
parent: Youtube playlist 2
grand_parent: Monogame
nav_order: 5
---

1.  Crear la clase Mobs, pintarla y updatearla
2.  Añadir AI
3.  Pasar la lista de mobs a los proyectiles, trestear los hits
4.  Crear spaw mobs

---

- Crear clase en Gameplay→World → Units `Mob.cs` (se puede copiar la clase hero)
- Eliminar la declaracion de la variable speed en `Hero.cs` (al heredarse de Unit no hace falta)
- Eliminar el contenido de la funcion `Update()` en `Mob.cs`
- Crear metodo `public virtual Ai()` en `Mob.cs`
- Setear el metodo `Ai()` dentro de Update()
- Crear una lista de mobs en `World.cs` → `public List<Mob> mobs = new List<Mob>();`
- Pasar la lista de mobs a los proyectiles

> En `World.cs` → `Update()`
>
> `projectiles[i].Update(offset, mobs.toList<Unit>())`

- Crear un metodo en `World.cs`

  public virtual void AddMob(object INFO)
  {
  mobs.Add((Mob)INFO);
  }

- Ir a `GameGlobals.cs` crear una variable que se llame `public static PassMob;`
- Ir a `World.cs` setearlo en el constructor de igual forma que `PassProjectile` → `GameGlobals.PassMob = AddMob;`
- Ir a `Unit.cs` y añadir las variables → `public bool dead;` y `public float hitDist`
- Ir a `Unit.cs` y setear las 2 variables nuevas → `dead = false;` y `hitDist = 35.0f;`
- Ir a `World.cs` → `Update()` y copiar el for que hay y cambiarlo por el de mobs
- Ir a `Mob.cs` → `Update()` actualizar la funcion añadiendo un parametro mas `Update(Vector2 OFFSET, Hero HERO)`
  - Actualizar `AI(HERO)` pasandole un parametro mas
- Ir a `World.cs` →`Draw()` y añadir un  for mas, copiar el que ya hay de proyectiles y duplicarlo para el de mobs
- Ir a `Unit.cs` y crear un metodo `GetHit(){ dead = true}`
- Ir a `Projectile2d` → `HitSomething()` y hacer un bucle for

  for(int i=0; i< UNITS.COunt; i++)
  {
  if(Globals.GetDistance(pos, UNITS[i].pos) < UNITS[i].hitDist)
  {
  UNITS[i].GetHit();
  return true;
  }
  return false;
  }

- Ir a `Globals.cs` y pegar el metodo `RadialMovement()` que me da el tio
- Ir a `Mobs.cs` →`IA(Hero hero)` añadir el siguiente codigo

  pos += Globals.RadialMovement(HERO.pos, pos, speed);
  rot = Globals.RotateTowards(pos, HERO.pos);

- Crear carpeta Gameplay → Units → Mobs crear la clase `Imp.cs` (es una copia de `Mobs.cs` pero con el contenido de `Update()` limpio)
- Copiar la clase `Unit.cs` en GamePlay → World que se llama `SpawnPoint.cs`

  - Quitart speed
  - Añadir una variable timer `public McTimer spawnTimer = new McTimer(2200);`
  - En `Update()` añadir este codigo

  spawnTimer.UpdateTimer();
  if(spawnTimer.Test())
  {
  SpawnMob();
  spawnTimer.ResetToZero();
  }
  ...
  public virtual void SpawnMob()
  {
  GameGlobals.PassMob(new Imp(new Vector2(pos.X, pos.Y)));
  }

- En `World.cs` crear una variable que sea los spawns → `public List<SpanwPoint> spawnPoint = new List<SpanwPoint>();`
  - En el constructor añadir spawns → `spawnPoint.add(new SpawnPoint("", new Vector2(50,50), new Vector2(35, 35)))`
  - En `Update()` copiar el bucle for y hacerlo igual pero con spawnPoint
  - En `Draw()` copiar y pegar el bucle con spawnPoint
  - En `Update()` en el bucle de mobs modificarlo asi → `mobs[i].Update(offset, hero);`
