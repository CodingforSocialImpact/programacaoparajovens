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
            bg = [0, 100, 0]  # green
        else:
            bg = [100, 0, 0]  # red

        msg = "Temperature = {0}, Pressure = {1}, Humidity - {2}".format(t, p, h)

        sense.show_message(msg, scroll_speed=0.05, back_colour=bg)
    ```

1. Click **File** -- **Save As**, give your program a name e.g. [`scrolling_env.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/scrolling_env.py), then press **F5** to run.

    <iframe src="https://trinket.io/embed/python/2f03745830" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### Ideas

- Currently, the scrolling program only warns about abnormal temperature. Can you add the same behaviour for pressure and humidity?
- You could create a simple graphical thermometer which outputs different colours / patterns depending on the temperature.
- If you haven't done so already, experiment with a bottle and the [pressure sensor](https://www.raspberrypi.org/learning/astro-pi-guide/sensors/pressure.md).

## Detecting movement

The Sense HAT has a set of sensors that can detect movement. It has an IMU (inertial measurement unit) chip which includes:

- A gyroscope (for detecting which way up the board is)
- An accelerometer (for detecting movement)
- A magnetometer (for detecting magnetic fields)

Before you start experimenting with motion sensing, it's important to understand three key terms covered in the [guide](https://github.com/raspberrypilearning/astro-pi-guide/blob/master/sensors/movement.md) and in this [video](https://www.youtube.com/watch?v=pQ24NtnaLl8).

The three axes uses to describe motion are:

- Pitch (like a plane taking off)
- Roll (the plane doing a victory roll)
- Yaw (imagine steering the plane like a car)

![Sense HAT Orientation](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/images/orientation.png)

The IMU sensor is not yet supported on trinket.io, but will be coming soon!
You can find out the orientation of the Sense HAT using the `sense.get_orientation()` method:

```python
orientation = sense.get_orientation()
pitch = orientation['pitch']
roll = orientation['roll']
yaw = orientation['yaw']
```

This would get the three orientation values (measured in degrees) and store them as the three variables `pitch`, `roll` and `yaw`.

1. You can explore these values with a simple program:

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

1. Click **File** -- **Save As**, give your program a name e.g. [`orientation.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/orientation.py), then press **F5** to run.

    **Note: When using the movement sensors it is important to poll them often in a tight loop. If you poll them too slowly, for example with `time.sleep(0.5)` in your loop, you will see strange results. This is because the code behind needs lots of measurements in order to successfully combine the data coming from the gyroscope, accelerometer and magnetometer.**

1. Another way to detect orientation is to use the `sense.get_accelerometer_raw()` method which tells you the amount of g-force acting on each axis. If any axis has ±1g then you know that axis is pointing downwards.

    In this example, the amount of gravitational acceleration for each axis (x, y, and z) is extracted and is then rounded to the nearest whole number:

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

1. Click **File** -- **Save As**, give your program a name e.g. [`acceleration.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/acceleration.py), then press **F5** to run.

    As you turn the screen you should see the values for x and y change between -1 and 1. If you place the Pi flat or turn it upside down, the z axis will be 1 and then -1.

1. If we know which way round the Raspberry Pi is, then we can use that information to set the orientation of the LED matrix. First you would display something on the matrix, then continually check which way round the board is, and use that to update the orientation of the display.

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

1. Click **File** -- **Save As**, give your program a name e.g. [`rotating_letter.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/rotating_letter.py), then press **F5** to run.

    In this program you are using an `if, elif, else` structure to check which way round the Raspberry Pi is. The `if` and `elif` test three of the orientations, and if the orientation doesn't match any of these then the program assumes it is the "right" way round. By using the `else` statement we also catch all those other situations, like when the board is at 45 degrees or sitting level.

1. If the board is only rotated, it will only experience 1g of acceleration in any direction; if we were to shake it, the sensor would experience more than 1g. We could then detect that rapid motion and respond. For this program we will introduce the `abs()` function which is not specific to the Sense HAT library and is part of standard Python. `abs()` gives us the size of a value and ignores whether the value is positive or negative. This is helpful as we don't care which direction the sensor is being shaken, just that it is shaken.

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

1. Click **File** -- **Save As**, give your program a name e.g. [`shake.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.pycode/shake.py), then press **F5** to run.

    You might find this is quite sensitive, but you could change the value from 1 to a higher number.

### Ideas

  - You could write a program that displays an arrow (or other symbol) on screen; this symbol could be used to point to which way is down. This way the astronauts (in low gravity) always know where the Earth is.
  - You could improve the dice program from earlier in this activity, so that shaking the Pi triggers the dice roll.
  - You could use the accelerometer to sense small movements; this could form part of a game, alarm system or even an earthquake sensor.

## Putting it all together

Now that you've explored most of the features of the Sense HAT, you could combine them to create a project. Here's an example reaction testing game, which could be used by the astronauts to test their reflexes.

The game will display an arrow on the LED matrix and select a random orientation for it. The player must rotate the board to match the arrow. If they match it in time the arrow turns green and their score increases; if not their arrow turns red and the game ends, telling them their score. The game keeps showing arrows in new orientations until the player loses, and each turn gets faster.

This idea combines:

  - Showing messages and images on the LED matrix
  - Setting and detecting the orientation
  - Use of variables, randomisation, iteration, and selection

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

If you turned this into Python it could look like this:

```python
from sense_hat import SenseHat
from time import sleep
from random import choice

sense = SenseHat()

# set up the colours (white, green, red, empty)

w = [150, 150, 150]
g = [0, 255, 0]
r = [255, 0, 0]
e = [0, 0, 0]

# create images for three different coloured arrows

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

sense.show_message("Keep the arrow pointing up", scroll_speed=0.05, text_colour=[100,100,100])

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

msg = "Your score was %s" % score
sense.show_message(msg, scroll_speed=0.05, text_colour=[100, 100, 100])
```

Click **File** -- **Save As**, give your program a name e.g. [`reaction_game.py`](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/code/reaction_game.py), then press **F5** to run.

### Ideias

There are lots of potential developments for this game:
- Include shake actions as well as orientation.
- Make use of the humidity sensor to detect breath; the player could be prompted to breathe on the board as an action.
- Include more than 4 directions; players have to hold at 45 degrees.

## E agora?

Experimenta ligar o Sense HAT ao Minecraft!

---
Referências: 
* [Guetting Started with the Sense HAT](https://www.raspberrypi.org/learning/getting-started-with-the-sense-hat/)