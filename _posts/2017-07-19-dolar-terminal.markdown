---
title:  "¿Cómo saber el valor del dolar desde la terminal?"
date:   2017-07-19 20:39:23 -0500
categories: Python Bash
layout: single
read_time: true
comments: true
share: true
author_profile: true
author: Jhon Beltrán
related: true
excerpt: En esta ocación con un pequeño script en python3 les voy a mostar como le hice scraping a una pagina para obtener el valor del dolar en pesos (COP) en cualquier momento, escribiendo `dolar`
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

{% highlight python %}
import requests
import csv
import os
import urllib.request
from bs4 import BeautifulSoup

def main():
    try:
        online_values()
    except requests.exceptions.ConnectionError as e:
        offline_values()

def online_values():
    response_one_dollar= requests.get('http://www.xe.com/es/currencyconverter/convert/?Amount=1&From=USD&To=COP')
    soup_one_dollar = BeautifulSoup(response_one_dollar.content, 'html.parser')
    container_dollar = soup_one_dollar.find('span', 'uccResultAmount')
    one_dollar = container_dollar.contents[0]
    print('El dolar en este momento tiene un valor de: ${} COP'.format(one_dollar))
    response_one_cop= requests.get('http://www.xe.com/es/currencyconverter/convert/?Amount=1&From=COP&To=USD')
    soup_one_cop = BeautifulSoup(response_one_cop.content, 'html.parser')
    container_cop = soup_one_cop.find('span', 'uccResultAmount')
    one_cop = container_cop.contents[0]
    one_dollar_without_dot = one_dollar.replace('.', '')
    one_dollar_ready_to_parse = one_dollar_without_dot.replace(',', '.')
    one_dollar_float = float(one_dollar_ready_to_parse)
    one_cop_without_dot = one_cop.replace('.', '')
    one_cop_ready_to_parse = one_cop_without_dot.replace(',', '.')
    one_cop_float = float(one_cop_ready_to_parse)

    save(one_dollar_float, one_cop_float)
    operate(one_dollar_float, one_cop_float)

def offline_values():
    if os.path.isfile('./values.csv'):
        with open('values.csv', 'r') as f:
            reader = csv.reader(f)
            for idx, row in enumerate(reader):
                if idx == 0:
                    continue

                one_dollar_float = float(row[0])
                one_cop_float = float(row[1])

    else:
        one_dollar_float = 3000
        one_cop_float = 0.0003
    print('El dolar en este momento tiene un valor de: ${} COP'.format(one_dollar_float))
    operate(one_dollar_float, one_cop_float)

def save(one_dollar_float, one_cop_float):
    with open('values.csv', 'w') as f:
        writer = csv.writer(f)
        writer.writerow(('USD', 'COP'))
        writer.writerow((one_dollar_float, one_cop_float))

def operate(one_dollar_float, one_cop_float):

    while True:
        command = str(input('''
            ¿Qué deseas hacer?

            [d]olares a pesos
            [p]esos a dolares
            [s]alir
        '''))

        if command == 'd':
            dollar_to_cop(one_dollar_float)
        elif command == 'p':
            cop_to_dollar(one_cop_float)
        else:
            break

def dollar_to_cop(one_dollar_float):
    dollar_amount = float(input('Cantidad de dolares: '))
    result = one_dollar_float * dollar_amount
    print('${} Dolares son ${} Pesos Colombianos'.format(dollar_amount, result))

def cop_to_dollar(one_cop_float):
    cop_amount = float(input('Cantidad de pesos: '))
    result = one_cop_float * cop_amount
    print('${} Pesos Colombianos son ${} Dolares'.format(cop_amount, result))


if __name__ == '__main__':
    main()
{% endhighlight %}

### Script en Bash
Luego creamos el archivo dolar en bash con el siguiente contenido:

{% highlight bash %}
#!/bin/bash
cd ~/Documents/Estudio/Python/web_scraping
source enviroment/bin/activate
cd scraping
python3 dolar_scraping.py
{% endhighlight %}

Y lo guardamos en: `/usr/local/bin` o en cualquier otra dirección en el `$PATH` con los permisos necesarios para lo cual ejecutamos:

`chmod 750 dolar`

Y ahora ya podemos ejecutar nuestro script desde cualquier ubicacion en la terminal usando el comando

`dolar`

[Más Ejemplos de Web Scraping][repo]

[raw-script-python]: https://raw.githubusercontent.com/Jhonbeltran/web-scraping/master/dolar_scraping.py
[raw-script-bash]:  https://raw.githubusercontent.com/Jhonbeltran/web-scraping/master/dolar
[repo]: https://github.com/Jhonbeltran/web-scraping
