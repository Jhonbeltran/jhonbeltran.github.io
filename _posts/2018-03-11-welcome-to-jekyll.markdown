---
layout: single
title:  "¿Cómo saber el valor del dolar desde la terminal?"
date:   2017-07-19 20:39:23 -0500
categories: jekyll update
share: yes
author_profile: true
author: Jhon Beltrán
excerpt: En esta ocación con un pequeño script en python3 les voy a mostar como le hice scraping a una pagina para obtener el valor del dolar en pesos (COP) en cualquier momento, escribiendo `dolar`
comments: yes
header:
  overlay_color: "#333"
  cta_label: "See on Github"
  cta_url: "https://github.com/Jhonbeltran/web-scraping"
---
A medida que voy aprendiendo mas acerca de la terminal (de mi sistema basado en unix) me dan ganas de sacarle mas provecho, en esta ocación con un pequeño script en python3 les voy a mostar como le hice scraping a una pagina para obtener el valor del dolar en pesos (COP) en cualquier momento, escribiendo `dolar`
## Requisitos
* Un sistema basado en linux o alguna forma para emular el bash (en mi caso Ubuntu 17.04)
* Python3 el cual trae instalado `venv` para el entorno virtual que usaremos o Python2 con la libreria `virtualenv`
* Pip
* Editor de texto (`vim, sublime text, atom ...`)

### Entorno virtual
* Creamos la carpeta en la cual vamos a contener todo nuestro proyecto:
`mkdir web_scraping`
* Creamos nuestro entorno virtual(en este caso usando venv)
`python3 -m venv enviroment`
* Accedemos al entorno virtual
`source enviroment/bin/activate`
* cremos una carpeta donde crearemos el script y accedemos a ella
`mkdir scraping\ncd scraping`
* instalamos las librerias necesarias usando:
`pip install beautifulsoup4 requests`
### Script en Python
Dentro de la carpeta /scraping creamos el siguiente script
[Ver el codigo del Script en Python][raw-script-python]

### Script en Bash
Luego creamos el archivo dolar en bash con el siguiente contenido:
[Ver el codigo del Script en Bash][raw-script-bash]
Y lo guardamos en: `/usr/local/bin` o en cualquier otra dirección en el `$PATH` con los permisos necesarios para lo cual ejecutamos:\n`chmod 750 dolar`
Y ahora ya podemos ejecutar nuestro script desde cualquier ubicacion en la terminal usando el comando\n`dolar`
[Mas Ejemplos de Web Scraping](https://github.com/Jhonbeltran/web-scraping)

{% highlight python %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

[raw-script-python]: https://raw.githubusercontent.com/Jhonbeltran/web-scraping/master/dolar_scraping.py
[raw-script-bash]:  https://raw.githubusercontent.com/Jhonbeltran/web-scraping/master/dolar
