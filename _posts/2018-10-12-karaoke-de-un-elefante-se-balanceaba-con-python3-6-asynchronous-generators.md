---
title:  "Karaoke de “Un Elefante se Balanceaba” con Python3.6 (Asynchronous generators)"
date:   2018-10-12 20:04:23 -0500
categories: Python
layout: single
read_time: true
comments: true
share: true
author_profile: true
author: Jhon Beltrán
related: true
excerpt: ¿Alguna vez han necesitado cantar la asombrosa canción de “Un Elefante se Balanceaba” y no han tenido a la mano la letra?
teaser: /assets/images/index.jpg
header:
  overlay_color: "#333"
  cta_label: "Ver Repositorio"
  cta_url: "https://github.com/jbeltranleon/python-basics/tree/master/sugar"
---

¿Alguna vez han necesitado cantar la asombrosa canción de “Un Elefante se Balanceaba” y no han tenido a la mano la letra?

![“gray elephant with calf standing on ground at daytime” by [Chen Hu](https://unsplash.com/@huchenme?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/8806/0*hz7qiaMQGV_tDEHO)*“gray elephant with calf standing on ground at daytime” by [Chen Hu](https://unsplash.com/@huchenme?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

Cómo asumo que muy pocos han tenido esa necesidad pero conocen la canción he decidido usarla para contarles que python desde su versión **3.5 **introdujo la sintaxis de generadores asíncronos *async /await *pero sólo desde la versión **3.6** nos ha permitido usar las funciones de rendimiento y de espera en el mismo “cuerpo”. Te dejo el enlace por si quieres leer más sobre sobre [Generadores Asíncronos en Python](https://docs.python.org/3.6/whatsnew/3.6.html#pep-525-asynchronous-generators).

Ahora sin más preámbulo mi ejemplo:
```python
#!/usr/bin/env python3.6
import asyncio
async def turno(espera, cantidad):
    """Produce números de 0 a *cantidad* cada *espera* segundos."""
    for i in range(cantidad):
        yield i
        await asyncio.sleep(espera)
async def main():
    async for x in turno(4,10):
        print("🐘"*(x+1))
        if x < 1:
            print (f"{x+1} Elefante se balanceaba sobre la tela de un araña")
            print("como la tela se resistía fue a llamar otro elefante 🎶")
        else:
            print (f"{x+1} Elefantes se balanceaban sobre la tela de un araña")
            print("como la tela se resistía fueron a llamar otro elefante 🎶")
            
if __name__ == "__main__":
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
```
Si quieren conocer un poco más de azucar sintáctica pueden ver la siguiente historia: [https://medium.com/the-python-corner/syntax-sugar-in-python-3-6-776178ce51f4](https://medium.com/the-python-corner/syntax-sugar-in-python-3-6-776178ce51f4)
