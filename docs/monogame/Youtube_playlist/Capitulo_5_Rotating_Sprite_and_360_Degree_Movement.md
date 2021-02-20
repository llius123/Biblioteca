---
layout: default
title: Capitulo 5 Rotating Sprite and 360 Degree Movement
parent: Youtube playlist
grand_parent: Monogame
nav_order: 5
---

En este video lo que hace es enseñar como rotar el sprite.

En resumidas cuentas cuando tu haces el Sprite.Draw() este metodo ya tiene de por si una variable que se llama rotate y que es un float.

Lo dificil aqui es cuadrar la rotacion con el sprite tal como se dibuja de primeras.

                // Con esto obtengo la posicion del mouse
                Vector2 mousePosition = new Vector2(Mouse.GetState().X, Mouse.GetState().Y);

                // Resto la posicion del sprite - posicion del mouse
                Vector2 dPos = sprite.Position - mousePosition;

    			// Calculo la tangente de la posicion
                sprite.Rotation = (float)Math.Atan2(dPos.Y, dPos.X) - (float)89.55;

> No se porque pero he tenido que restar `- (float)89.55;` porque por alguna razon el sprite estaba rotado 90 grados no se porque
