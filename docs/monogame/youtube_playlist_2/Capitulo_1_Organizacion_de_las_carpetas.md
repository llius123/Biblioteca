---
layout: default
title: Capitulo 1 Organizacion de las carpetas
parent: Youtube playlist 2
grand_parent: Monogame
nav_order: 1
---

- Primero lo que hace es copiar el contenido del archivo `Program.cs` en `Game1.cs`
- Luego borra `Program.cs`
- Renombra `Game1.cs` a `Main.cs`
- Crea subcarpetas en Content → 2d,Audio,Fonts
- Crea una carpeta Source → Engine
- Crea una clase dentro de Engine que se llama `Globals.cs`
- Boton derecho sobre references → Add reference
  - Buscamos System.Xml.Linq y seleccionamos su check
- En `Globals.cs` añadir las variables

  public static ContentManager content;
  public static SpriteBatch spriteBatch;

- En `Main.cs` cambiar en `LoadContent` spriteBatch → Globals.spriteBatch
- En `LoadContent` añadir `Globals.content = this.Content;`
- En `Main.cs` → `Draw()` hacer que pinte los sprites

  ## Globals.spriteBatch.Begin(SpriteSortMode.Deferred, BlendState.AlphaBlend);

  Globals.spriteBatch.End();

- Ha metido el archivo Hero.xmb en la carpeta 2d (8:32)
- Dentro de `Source` → Crear la clase `World.cs`
- `World.cs`

  - Añadir este codigo

  public class World
  {
  public World()
  {
  }
  public virtual void Update()
  {
  }
  public virutal void Draw()
  {
  }
  {

- Source → Engine → Crear la clase `Basic2d.cs`
- `Basic2d.cs`

  public class Basic2d
  {
  public Vector2 pos, dims;
  public Texture2D myModel;
  public Basic2d(string PATH, Vector2 POS, Vector DIMS)
  {
  pos = POS;
  dims = DIMS;
  myModel = Globals.content.Load<Texture2D>(PATH);
  }
  public virtual void Update()
  {
  }
  public virutal void Draw()
  {
  if(myModel != null)
  {
  Globals.spriteBatch.Draw(myModel, new Rectangle((int)(pos.X),(int)(pos.Y), (int)dims.X, (int)dism.Y), null, Color.White, 0.0f, new Vector2(myModel.Bounds.Width/2, myModel.Bounds.Height/2), new SpriteEffects(), 0);
  }
  }
  }

- `World.cs`

  public Basic2d hero;
  public World()
  {
  hero = new Basic2d("2d\Hero", new Vector(300, 300), new Vector(48,48))
  }
  public virtual void Update()
  {
  hero.Update();
  }
  public virtual void Draw()
  {
  hero.Draw();
  }

- En `Main.cs`

  public World world;
  ...
  public void LoadContent()
  {
  world = new World();
  }
  ... Update()
  {
  world.Update();
  }
  ... Draw()
  {
  ...Begin()
  world.Draw()
  ...End()
  }

  }
