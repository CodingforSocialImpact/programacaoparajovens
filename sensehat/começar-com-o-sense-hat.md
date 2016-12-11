# Começar com o Sense HAT

Com este desafio vais explorar o hardware do Sense HAT e a sua libraria de Python.

![](https://www.raspberrypi.org/learning/resources/getting-started-with-the-sense-hat/cover.png)

## Objetivos

Ao percorreres este desafio vais aprender:

* Como controlar a matriz de LEDs
* Como recolher informação dos sensores do Sense HAT
* Como combinar pequenas ideias em projetos

Duração da atividade: `90 minutos.`

## Material

| Nome | Quantidade | Preço |
| --- | --- | --- |
|Raspberry Pi |1 |35€ |
|Sense HAT |1 |29€ |


## Mostrar texto

Abre o `Python 3` (Menu->Desenvolvimento->Python3) e cria um novo ficheiro (File->New File).

Testa o programa seguinte para colocares texto a corres no mostrador do Sense HAT.

```python
from sense_hat import SenseHat

sense = SenseHat()
```

Adiciona a a linha seguinte para escrever o teu texto:

```python
sense.show_message("Olá Sense HAT!")
```

<div><iframe src="https://trinket.io/embed/python/308a373b5c" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

1. Podemos adicionar alguns parâmetros extra no comando `sense.show_message` para alterarem o comportamento da mensagem:

    | Parâmetro | Efeito |
    |---|---|
    | **scroll_speed** | O *scroll_speed* afeta a velocidade a que o texto corre no mostrador. Por definição é 0.1. Quanto maio o número, mais lenta será a velocidade |
    | **text_colour** | O *text_colour* altera a cor do texto com valores RGB |
    | **back_colour** | O *back_colour* altera a cor do fundo com valores RGB |

    Este programa mostra o texto `Astro Pi is awesome!!` mais lentamente, com o texto amarelo **[255,255,0]** e o fundo em azul **[0,0,255]**:

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    sense.show_message("Astro Pi is awesome!!", scroll_speed=0.05, text_colour=[255,255,0], back_colour=[0,0,255])
    ```

    <div><iframe src="https://trinket.io/embed/python/d62aa7f30a" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

    Podes fazer a mensagem repetir com um ciclo:

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    while True:
        sense.show_message("Astro Pi is awesome!!", scroll_speed=0.05, text_colour=[255,255,0], back_colour=[0,0,255])
    ```

    <div><iframe src="https://trinket.io/embed/python/f833a60218" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

1. Clica `File`->`Save As`, dá um nome ao teu programa [`loop_text.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/loop_text.py) e carrega `F5` para correr.

1. A matriz de LED pode também mostrar uma letra apenas com a função `sense.show_letter`

    Experimenta:

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    sense.show_letter("J",text_colour=[255, 0, 0])
    ```

    Este programa mostra letras separadas por uma pausa, graças à função `sleep`:

    ```python
    from sense_hat import SenseHat
    from time import sleep

    sense = SenseHat()

    sense.show_letter("O",text_colour=[255, 0, 0])
    sleep(1)
    sense.show_letter("M",text_colour=[0, 0, 255])
    sleep(1)
    sense.show_letter("G",text_colour=[0, 255, 0])
    sleep(1)
    sense.show_letter("!",text_colour=[0, 0, 0], back_colour=[255, 255, 255])
    sleep(1)
    sense.clear()
    ```

    Clica `File`->`Save As`, dá um nome ao teu programa [`omg.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/omg.py) e carrega `F5` para correr.


    <div><iframe src="https://trinket.io/embed/python/ccb58a3d9d" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>


    Podes adicionar números aleatórios para escolher as cores, com números entre `0` e `255`:

    ```python
    from sense_hat import SenseHat
    from time import sleep
    from random import randint

    sense = SenseHat()

    r = randint(0,255)
    sense.show_letter("O", text_colour=[r, 0, 0])
    sleep(1)

    r = randint(0,255)
    sense.show_letter("M", text_colour=[0, 0, r])
    sleep(1)

    r = randint(0,255)
    sense.show_letter("G", text_colour=[0, r, 0])
    sleep(1)

    sense.show_letter("!", text_colour=[0, 0, 0], back_colour=[255, 255, 255])
    sleep(1)
    sense.clear()
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`random_omg.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/random_omg.py) e carrega `F5` para correr.

    Em âmbos os programas o método `sense.clear()` foi usado para limpar a matriz.
    
    <div><iframe src="https://trinket.io/embed/python/45b0f19b65" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

## Mostrar imagens

A matriz de imagens pode mostrar mais do que texto! Nós conseguimos controlar cada pixel individualmente para criar uma imagem. Há vários modos de conseguirmos isto.

1. A primeira abordagem é definir `pixeis` individualmente. Basta usar o método `sense.set_pixel()`.

    O Sense HAT usa um sistema de coordenadas como o mostrado em baixo, começa em `0` e a origem é no topo esquerdo.

    ![Coordinates](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/images/coordinates.png)

    - O `pixel` azul está nas coordenadas (0, 2)
    - O `pixel` vermelho está nas coordenadas (7, 4)

    Experimenta!

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    sense.set_pixel(0, 2, [0, 0, 255])
    sense.set_pixel(7, 4, [255, 0, 0])
    ```

    <div><iframe src="https://trinket.io/embed/python/9a4266d360" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

    Consegues adivinhar o que o código seguinte faz? Edita-o e experimenta!

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    sense.set_pixel(2, 2, [0, 0, 255])
    sense.set_pixel(4, 2, [0, 0, 255])
    sense.set_pixel(3, 4, [100, 0, 0])
    sense.set_pixel(1, 5, [255, 0, 0])
    sense.set_pixel(2, 6, [255, 0, 0])
    sense.set_pixel(3, 6, [255, 0, 0])
    sense.set_pixel(4, 6, [255, 0, 0])
    sense.set_pixel(5, 5, [255, 0, 0])
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`simple_image.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/simple_image.py) e carrega `F5` para correr.

1. Definir pixeis individualmente pode funcionar bastante bem, mas torna-se complexo se quiseres definir mais pixeis. Existe outro método para definir pixeis chamado `sense.set_pixels`. Basta dar-lhe uma cor para cada pixel da matriz.

    Algo do género...

    ```python
    sense.set_pixels([[255, 0, 0], [255, 0, 0], [255, 0, 0], [255, 0, 0],......])
    ```

    ...mas isto iria demorar muito tempo.

    Em vez disso podemos usar variáveis para definir as cores:

    ```python
    r = [255, 0, 0]
    o = [255, 127, 0]
    y = [255, 255, 0]
    g = [0, 255, 0]
    b = [0, 0, 255]
    i = [75, 0, 130]
    v = [159, 0, 255]
    e = [0, 0, 0]  # e stands for empty/black
    ```

    E podemos descrever a nossa matriz 2D com cores apenas:

    ```python
    image = [
    e,e,e,e,e,e,e,e,
    e,e,e,r,r,e,e,e,
    e,r,r,o,o,r,r,e,
    r,o,o,y,y,o,o,r,
    o,y,y,g,g,y,y,o,
    y,g,g,b,b,g,g,y,
    b,b,b,i,i,b,b,b,
    b,i,i,v,v,i,i,b
    ]
    ```

    Depois, passamo a _imagem_ ao método `sense.set_pixels` e programa ficará alo do género:

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    r = [255,0,0]
    o = [255,127,0]
    y = [255,255,0]
    g = [0,255,0]
    b = [0,0,255]
    i = [75,0,130]
    v = [159,0,255]
    e = [0,0,0]

    image = [
    e,e,e,e,e,e,e,e,
    e,e,e,r,r,e,e,e,
    e,r,r,o,o,r,r,e,
    r,o,o,y,y,o,o,r,
    o,y,y,g,g,y,y,o,
    y,g,g,b,b,g,g,y,
    b,b,b,i,i,b,b,b,
    b,i,i,v,v,i,i,b
    ]

    sense.set_pixels(image)
    ```
    
1. Clica `File`->`Save As`, dá um nome ao teu programa [`rainbow.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/rainbow.py) e carrega `F5` para correr.    
    
    <div><iframe src="https://trinket.io/embed/python/8f36929035" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>


### Ideias

- Podes alternar entre imagens apra criar animaçõe? Vê este vídeo: {% youtube %}https://www.youtube.com/watch?v=b84EywkQ3HI{% endyoutube %} video for some inspiration.

## Definir orientação

Podes alterar a orientação do display com o método `sense.set_rotation()` e dentro dos parêntesis introduz um dos ângulos (0, 90, 180, 270).

Por exemplo 180º:

```python
sense.set_rotation(180)
```

1. Quando usado no programa do arco-íris:

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    r = [255, 0, 0]
    o = [255, 127, 0]
    y = [255, 255, 0]
    g = [0, 255, 0]
    b = [0, 0, 255]
    i = [75, 0, 130]
    v = [159, 0, 255]
    e = [0, 0, 0]

    image = [
    e,e,e,e,e,e,e,e,
    e,e,e,r,r,e,e,e,
    e,r,r,o,o,r,r,e,
    r,o,o,y,y,o,o,r,
    o,y,y,g,g,y,y,o,
    y,g,g,b,b,g,g,y,
    b,b,b,i,i,b,b,b,
    b,i,i,v,v,i,i,b
    ]

    sense.set_pixels(image)
    sense.set_rotation(180)
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`rainbow_flip.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/rainbow_flip.py)e carrega `F5` para correr.

1. Podes criar um texto que roda com um ciclo `for`:

    ```python
    from sense_hat import SenseHat
    from time import sleep

    sense = SenseHat()

    sense.show_letter("J")

    angles = [0, 90, 180, 270, 0, 90, 180, 270]
    for r in angles:
        sense.set_rotation(r)
        sleep(0.5)
    ```


1. Clica `File`->`Save As`, dá um nome ao teu programa [`spinning_j.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/spinning_j.py)e carrega `F5` para correr.

    <div><iframe src="https://trinket.io/embed/python/2f48e31b56" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

1. Podes ainda inverter a imgem verticalmente ou horizontalmente:

    ```python
    sense.flip_h()
    ```

    ou

    ```python
    sense.flip_v()
    ```

    Por exemplo:

    ```python
    from sense_hat import SenseHat
    from time import sleep

    sense = SenseHat()

    w = [150, 150, 150]
    b = [0, 0, 255]
    e = [0, 0, 0]

    image = [
    e,e,e,e,e,e,e,e,
    e,e,e,e,e,e,e,e,
    w,w,w,e,e,w,w,w,
    w,w,b,e,e,w,w,b,
    w,w,w,e,e,w,w,w,
    e,e,e,e,e,e,e,e,
    e,e,e,e,e,e,e,e,
    e,e,e,e,e,e,e,e
    ]

    sense.set_pixels(image)

    while True:
        sleep(1)
        sense.flip_h()
    ```

1. 1. Clica `File`->`Save As`, dá um nome ao teu programa [`eyes.py`](code/eyes.py) e carrega `F5` para correr.

<div><iframe src="https://trinket.io/embed/python/27b25ac047" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

## Sentir o ambiente

O Sense HAT possui sensores ambientais para detetar condições que o rodeiam. Consegue medir:

- Pressão
- Temperatura
- Humidade

Podemos ler esta informação com 3 métodos simples:

- `sense.get_temperature()` - Temperatura em Celsius.
- `sense.get_pressure()` - Pressão em milibars.
- `sense.get_humidity()` - Humidade em percentagem.

1. Podemos criar um exemplo com esta informação:

    ```python
    from sense_hat import SenseHat
    sense = SenseHat()

    while True:
        t = sense.get_temperature()
        p = sense.get_pressure()
        h = sense.get_humidity()

        t = round(t, 1)
        p = round(p, 1)
        h = round(h, 1)

        msg = "Temperatura = {0}, Pressão = {1}, Humidade = {2}".format(t,p,h)

        sense.show_message(msg, scroll_speed=0.05)
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`env.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/env.py) e carrega `F5` para correr.

    <div><iframe src="https://trinket.io/embed/python/a246815131" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

1. Podes usar cores para saber se os valores:

    - Temperatura (18.3 - 26.7 Celsius)
    - Pressão (979 - 1027 milibars)
    - Humidade (aprox. 60%)

    Podes usar um`if` para verificar as condições:

    ```python
    if t > 18.3 and t < 26.7:
        bg = [0, 100, 0] # verde
    else:
        bg = [100, 0, 0] # vermelho
    ```

    O programa completo:

    ```python
    from sense_hat import SenseHat
    sense = SenseHat()

    while True:
        t = sense.get_temperature()
        p = sense.get_pressure()
        h = sense.get_humidity()

        t = round(t, 1)
        p = round(p, 1)
        h = round(h, 1)

        if t > 18.3 and t < 26.7:
            bg = [0, 100, 0]  # verde
        else:
            bg = [100, 0, 0]  # vermelho

        msg = "Temperatura = {0}, Pressão = {1}, Humidade - {2}".format(t, p, h)

        sense.show_message(msg, scroll_speed=0.05, back_colour=bg)
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`scrolling_env.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/scrolling_env.py) e carrega `F5` para correr.

    <div><iframe src="https://trinket.io/embed/python/2f03745830" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe></div>

## Detetar movimento

O Sense HAT tem vários sensores que possibilitam a deteção de movimento como explicado [aqui](./sense-hat.md)

Podes descobrir a orientação do Sense HAT com `sense.get_orientation()`:

```python
orientation = sense.get_orientation()
pitch = orientation['pitch']
roll = orientation['roll']
yaw = orientation['yaw']
```

1. Testa o seguinte programa:

 ```python
 from sense_hat import SenseHat

 sense = SenseHat()

 while True:
    orientation = sense.get_orientation()
    pitch = orientation['pitch']
    roll = orientation['roll']
    yaw = orientation['yaw']
    print("pitch={0}, roll={1}, yaw={}".format(pitch,yaw,roll))
 ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`orientation.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/orientation.py) e carrega `F5` para correr.


1. Outro modo para detetar a orientação é usando o `sense.get_accelerometer_raw()` que te diz a quantidade de força G a atuar nos eixos. Se um eixo tem ±1g então saberás que está a apontar para baixo.

   Por exemplo:

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    while True:
	    acceleration = sense.get_accelerometer_raw()
        x = acceleration['x']
		y = acceleration['y']
		z = acceleration['z']

        x=round(x, 0)
        y=round(y, 0)
        z=round(z, 0)

        print("x={0}, y={1}, z={2}".format(x, y, z))
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`acceleration.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/acceleration.py) e carrega `F5` para correr.

    Se virares o RPi de pernas para o ar o z axis vai ser 1 e depois -1.

1. Podemos usar esta informação para mandar na orientação do display do Sense HAT.

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    sense.show_letter("J")

    while True:
        x = sense.get_accelerometer_raw().['x']
		y = sense.get_accelerometer_raw().['y']
		z = sense.get_accelerometer_raw().['z']

        x = round(x, 0)
        y = round(y, 0)

        if x == -1:
            sense.set_rotation(180)
        elif y == 1:
            sense.set_rotation(90)
        elif y == -1:
            sense.set_rotation(270)
        else:
            sense.set_rotation(0)
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`rotating_letter.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/rotating_letter.py) e carrega `F5` para correr.

 Neste programa estamos a usar um `if elseif elseif else` para testar as 4 posições possíveis.


1. Se o RPi está apenas rodado podemos experenciar 1g de aceleração em qualquer direção se o abanar-mos, o sensor mediria mais do que 1g. Neste programa vamos introduzir a função `abs()`, que no dá o tamanho do valor e ignora se é positivo ou negativo, é importante dado que não queremos saber em que direção é abanado, apenas se foi, ou não, abanado.

    ```python
    from sense_hat import SenseHat

    sense = SenseHat()

    while True:
	    acceleration = sense.get_accelerometer_raw()
        x = acceleration['x']
		y = acceleration['y']
		z = acceleration['z']
        
        x = abs(x)
        y = abs(y)
        z = abs(z)

        if x > 1 or y > 1 or z > 1:
            sense.show_letter("!", text_colour=[255, 0, 0])
        else:
            sense.clear()
    ```

1. Clica `File`->`Save As`, dá um nome ao teu programa [`shake.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/shake.py) e carrega `F5` para correr.

## Juntar tudo

Podemos agora combinar todas estas ideias num só projeto, como por exemplo num jogo para testar os reflexos!

The game will display an arrow on the LED matrix and select a random orientation for it. The player must rotate the board to match the arrow. If they match it in time the arrow turns green and their score increases; if not their arrow turns red and the game ends, telling them their score. The game keeps showing arrows in new orientations until the player loses, and each turn gets faster.

Esta ideia combina:

  - Mostrar imagens e mensagens
  - Definir e detetar orientação
  - Uso de variáveis, aleatórios, iteração e seleção

As this is more complicated than previous programs it's worth planning out the steps involved in **pseudocode**.

  > import the required libraries (sense_hat, time, random)  
  > create a sense object
  >
  > Set up the colours needed  
  > Create 3 different arrows (white, green, red)  
  > Set a variable **pause** to 3 (the initial time between turns)  
  > Set variables **score** and **angle** to 0  
  > Create a variable called **play** set to `True` (this will be used to stop the game later)  
  >  
  > Begin a loop which continues while `play == True`  
  > Set a new random angle (use **random.choice()** method)  
  > Show the white arrow and sleep for current pause length  
  > Check whether orientation matches the arrow  
  > ---if it does then add a point and turn the arrow green  
  > ---otherwise set play to `False` and turn the arrow red  
  > Shorten the pause duration slightly  
  > Pause before the next arrow  
  >  
  > When loop is exited, display a message with the score  

Fica aqui o jogo:

```python
from sense_hat import SenseHat
from time import sleep
from random import choice

sense = SenseHat()

# Definir cores
w = [150, 150, 150]
g = [0, 255, 0]
r = [255, 0, 0]
e = [0, 0, 0]

# Criar as imagens

arrow = [
e,e,e,w,w,e,e,e,
e,e,w,w,w,w,e,e,
e,w,e,w,w,e,w,e,
w,e,e,w,w,e,e,w,
e,e,e,w,w,e,e,e,
e,e,e,w,w,e,e,e,
e,e,e,w,w,e,e,e,
e,e,e,w,w,e,e,e
]

arrow_red = [
e,e,e,r,r,e,e,e,
e,e,r,r,r,r,e,e,
e,r,e,r,r,e,r,e,
r,e,e,r,r,e,e,r,
e,e,e,r,r,e,e,e,
e,e,e,r,r,e,e,e,
e,e,e,r,r,e,e,e,
e,e,e,r,r,e,e,e
]

arrow_green = [
e,e,e,g,g,e,e,e,
e,e,g,g,g,g,e,e,
e,g,e,g,g,e,g,e,
g,e,e,g,g,e,e,g,
e,e,e,g,g,e,e,e,
e,e,e,g,g,e,e,e,
e,e,e,g,g,e,e,e,
e,e,e,g,g,e,e,e
]

pause = 3
score = 0
angle = 0
play = True

sense.show_message("Mantem a seta para cima", scroll_speed=0.05, text_colour=[100,100,100])

while play:
    last_angle = angle
    while angle == last_angle:
        angle = choice([0, 90, 180, 270])
    sense.set_rotation(angle)
    sense.set_pixels(arrow)
    sleep(pause)
	acceleration = sense.get_accelerometer_raw()
    x = acceleration['x']
	y = acceleration['y']
	z = acceleration['z']
        
    x = round(x, 0)
    y = round(y, 0)

    print(angle)
    print(x)
    print(y)

    if x == -1 and angle == 180:
        sense.set_pixels(arrow_green)
        score += 1
    elif x == 1 and angle == 0:
      sense.set_pixels(arrow_green)
      score += 1
    elif y == -1 and angle == 90:
      sense.set_pixels(arrow_green)
      score += 1
    elif y == 1 and angle == 270:
      sense.set_pixels(arrow_green)
      score += 1
    else:
      sense.set_pixels(arrow_red)
      play = False

    pause = pause * 0.95
    sleep(0.5)

msg = "A tua pontuação foi %s" % score
sense.show_message(msg, scroll_speed=0.05, text_colour=[100, 100, 100])
```

Clica `File`->`Save As`, dá um nome ao teu programa [`reaction_game.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.py) e carrega `F5`.

## E agora?

Experimenta ligar o Sense HAT ao Minecraft!

---
Referências: 
* [Guetting Started with the Sense HAT](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/)