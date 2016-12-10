# O mapa do Minecraft com o Sense HAT

Usa o Sense HAT apra criares um mapa do mundo à volta do teu jogador no Minecraft.

![](https://www.raspberrypi.org/learning/resources/sense-hat-minecraft-map/cover.png)

## Objetivos

Ao percorreres este desafio vais aprender:

* Como definir a cor de todos os pixeis do display do Sense HAT, através da libraria do Sense HAT para Python
* Como descobri os IDs dos blocos do mundo do Minecraft com a libraria `mcpi` do Python
* Como é que as cores são criadas com valores RGB (Vermelho, Verde, Azul)
* Como definir LEDs individuais no Sense HAT
* O uso apropriado de estruturas de dados em Python: túpulos e dicionários
* Como criar uma função em Python
* Como lidar com a exceção `KeyError` em Python
* Como guardar dados em cache para otimizar a velocidade de um programa

Duração da atividade: `90 minutos`.

## Material

| Nome | Quantidade | Preço |
| --- | --- | --- |
|Raspberry Pi | 1 | 35€ |
|Sense HAT |1 |29€ |

## Começar com o display de LEDs do Sense HAT

O Sense HAT tem uma matriz de 8x8 LEDs, ou seja, 64 LEDs que podem assumir todas as cores RGB.

1. [Monta o teu Sense HAT](/sensehat/sense-hat.md) no Raspberry Pi.

2. Abre o `LXTerminal` (Menu->Acessórios->LXTerminal)

 ![](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/terminal-app-menu.png)

3. Cria uma nova pasta com o comando seguinte:

 ```bash
 mkdir minecraft-map
 ```
 `mkdir` significa criar diretoria (ou pasta).

4. Abre o `Python 3` (Menu->Desenvolvimento->Python 3). 
 
 ![](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/python3-app-menu.png)

5. No `Python 3` cria um novo ficheiro `File > New File`, vai abrir uma janela, é aí que vais introduzir o teu código.

6. Guarda o ficheiro (`CTRL+S`) como `colours.py` na tua pasta `minecraft-map`.

7. Adiciona o seguinte código:

 ```python
 # Permite usar o módulo do Sense HAT
 from sense_hat import SenseHat

 # Cria uma ligação com o Hardware chamada sense
 sense = SenseHat()
 
 # Varre o ecrã com a cor vermelha
 sense.clear(255, 0, 0)
 ```

8. Guarda as alterações (`CTRL+S`) e corre o código (`F5`).
Os teus LEDs do Sense HAT deverão estar todos vermelhos!

 Descarrega uma cópia do [colour.py](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/code/colour.py).

## Explorar o mundo do Minecraft

Agora que já experimentaste as cores do Sense HAT, vamos abrir o Minecraft e explorar que tipos de blocos podes encontrar.

1. Abre o Minecraft `Menu`->`Jogos`:

    ![Open Minecraft](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/minecraft-app-menu.png)

1. Clica **Start Game** e cria um novo mundo, ou entra num já criado.

1. Carrega em `Tab` para poderes mover o cursor do rato fora do Minecraft.

1. Volta à tua janela do `Python`. Abre um novo ficheiro e guarda-o com o nome `minecraft-colours.py` dentro da mesma pasta.

1. Coloca a janela do `Python` e do `Minecraft` lado-a-lado.

1. Introduz o seguinte código:

    ```python
    from sense_hat import SenseHat
    from mcpi.minecraft import Minecraft
    from time import sleep

    sense = SenseHat()
    mc = Minecraft.create()

    mc.postToChat("Olá Minecraft!")
    sense.clear(0, 255, 0)
    ```

1. Guarda `CTR + S` e corre o código `F5`!
 Deverás ver o texto `Olá Minecraft!` na janela do Minecraft o Sense HAT deverá ficar verde!

1. Agora que criaste uma ligação entre o Sense HAT e o mundo do Minecraft, vamos analisar como podemos determinar que tipo de bloco é que estamos a pisar. Reomve as linhas `postToChat` (postar para o chat) e `sense.clear` (limpar o Sense HAT) e adiciona o seguinte código:

    ```python
    while True:
        x, y, z = mc.player.getTilePos()
        block = mc.getBlock(x, y-1, z)
        print(block)
        sleep(0.1)
    ```

1. Guarda `CTR + S` e corre o código `F5`!
 Deverás ver números a aparecer na `linha de comandos` do Python. Estes números representam os IDs dos blocos que o teu jogador está a pisar. Caminha pelo mapa com a tua personagem, em diferentos blocos e deverás ver o número alterar-se.

1. Precisas de saber o que representam os diferentes tipos de números (IDs), ficam aqui alguns mais comuns:

    ```
    Ar: 0
    Pedra: 1
    Erva: 2
    Terra: 3
    Água: 8
    Areia: 12
    Gelo: 79
    ```

    Vê que tipos de blocos consegues identificar ao caminhar no Minecraft.

## Caminhada colorida com o Minecraft e o Sense HAT

Agora que já exploraste o mundo do Minecraft e viste os diferentes tipos de blocos, vais aprender a mostrar no Sense HAT cores diferentes dependendo do tipo de bloco que estás a pisar.

1. Vais precisar de criar um modo de mapear o ID do bloco a uma cor; Por exemplo erva (grass) deverá ser verde, portanto o bloco com o ID `2` deverá corresponder ao código de cor `(0, 255, 0)`.

    Começa por adicionar algumas variáveis para identificar os IDs dos blocos. Acrescenta o seguinte código em cima do teu ciclo `while`:

    ```python
    # blocos
    grass = 2
    water = 9
    sand = 12
    ```

1. Em baixo do que escreveste, adiciona as cores que representam esses blocos:

    ```python
    # cores
    green = (0, 255, 0)
    blue = (0, 0, 255)
    yellow = (255, 255, 0)
    ```

1. De seguida, em baixo das cores,cria um dicionário que mapeia cada tipo de bloco a uma cor:

    ```python
    # Bloco: cor
    colours = {
        grass: green,
        water: blue,
        sand: yellow,
    }
    ```
    Um dicionário é um tipo de dados usado para guardar relações com vários objetos, por exemplo um nome a um número de telefone. Os elementos no dicionário chamam-se pares key-value (valores-chave), portanto numa lista telefónica o nome é uma chave e o número de telefone é o valor.

1. Agora só falta procurar o bloco que estás a pisar, ver que cor é que corresponde e usar o `sense.clear` para mudar a cor do Sense HAT!

    Para procurar um valor no dicionário, passa-se a chave. Se o dicionário fosse uma lista telefónica passavas-lhe um nome e recebia o número dessa pessoa. Portanto, para ler o tipo `grass` usarias `colours[2]` ou `colours[grass]` e recebias o valor para `green` que é `(0, 255, 0)`.

    Modifica o teu ciclo `while` do seguinte modo:

    ```python
    while True:
        x, y, z = mc.player.getTilePos()
        block = mc.getBlock(x, y-1, z)
        colour = colours[block]
        print(colour)
        sleep(0.1)
    ```
    Aqui procuramos o ID do bloco que o jogador está a pisar, e como anteriormente, e depois procuras no dicionário `colours`, depois imprimes o par do código da cor.

1. Guarda `CTR + S` e corre o código `F5` e caminha no Minecraft.

    Deverás ver o código da cor do bloco que estás a pisar. Caminha para veres os diferentes códigos.

1. Se caminhares num bloco que não se encontar no dicionário, vais ter uma mensagem de erro. Se ainda não te aconteceu isto salta no ar com a tecla de `ESPAÇO` e devrás ver:

    ![Dictionary KeyError](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/dictionary-keyerror.png)

    Este erro é um `KeyError`, que é uma exceção do Python, o que significa que tentaste procurar um valor que não existe no dicionário, como, por exemplo, procurar um contato que não existe na tua lista telefónica.

1. Primeiro vamos lidar com o `KeyError`. Modifica a tua pesquisa de cores do seguinte modo:

    ```python
    if block in colours:
        colour = colours[block]
        print(colour)
    else:
        print("Não conheço o bloco com o ID %s" % block)
    sleep(0.1)
    ```

    Agora vamos verificar se a chave já se enconta no dicionário antes de procurar o seu valor. Se não existir, vai dizer-te o ID do bloco.

1. Agora que já tens um valor de uma cor a representar o bloco que o jogador está a pisar, podes dizer ao Sense HAT para mostrar essa cor, alterando simplesmente a linha `print(colour)` para:

    ```python
    sense.clear(colour)
    ```

1. Guarda `CTR + S` e corre o código `F5` e caminha no Minecraft e o teu Sense HAT deverá alterar a cor de acordo com o que pisares.

1. Agora adiociona mais blocos e cores ao teu dicionário!

**Descarrega uma cópia do [minecraft_colour.py](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/code/minecraft_colour.py)**

## Definir LEDs individuais no Sense HAT

Até agora, usaste o mostrador inteiro do Sense HAT para mostrar apenas uma cor. É possível alterar cada pixel individualmente, com o método do módulo do Sense HAT, `set_pixel`.

1. Cria um ficheiro Python novo e guarda-o como `pixels.py`.

1. Escreve o código seguinte:

    ```python
    from sense_hat import SenseHat
    from time import sleep

    sense  = SenseHat()

    sense.clear()
    sense.set_pixel(0, 0, 255, 255, 255)
    ```

1. Guarda `CTR + S` e corre o código `F5`. Deverá limpar o mostrador e mudar o pixel do topo esquerdo para branco.

    **Como funciona?**

    O método `sense.set_pixel` é usado para alterar um pixel específico para uma cor particular. O pixel é definido como x` e `y` e a cor é dada como `R`, `G` e `B`. Existem 2 maneira de usar este método:

    - passar os valores `R`, `G` and `B` separadamente:

    ```python
    sense.set_pixel(x, y, r, g, b)
    ```

    - passar os valores numa variável, definindo primeiro os valores:

    ```python
    white = (255, 255, 255)
    sense.set_pixel(x, y, white)
    ```

1. Experimenta o seguinte ciclo:

    ```python
    sense.clear()
    for y in range(8):
        for x in range(8):
            sense.set_pixel(x, y, 255, 0, 0)
            sleep(0.1)
    ```

    **Coisas a experimentar:**

    - O que será que acontece quando alteramos a ordem dos ciclos? Experimenta `for x in range(8)` e depois `for y in range(8)`.
    - O que será que acontece quando adicionamos `sense.clear()` antes de `sense.set_pixel()`?
    - O que será que acontece quando experimentamos `range(8, -1, -1)`?

1. Experimenta este exemplo que usa linhas de cores:

    ```python
    white = (255, 255, 255)
    red = (255, 0, 0)
    green = (0, 255, 0)
    blue = (0, 0, 255)
    yellow = (255, 255, 0)

    colours = [white, red, white, green, white, blue, white, yellow]

    sense.clear()
    for y in range(8):
        colour = colours[y]
        for x in range(8):
            sense.set_pixel(x, y, colour)
            sleep(0.1)
    ```

1. Podes sempre usar o método `set_pixels()` que recebe uma lista de 64 cores. Experimenta o seguinte exemplo:

    ```python
    r = red
    b = blue

    pixels = [
        r, b, r, b, r, b, r, b,
        b, r, b, r, b, r, b, r,
        r, b, r, b, r, b, r, b,
        b, r, b, r, b, r, b, r,
        r, b, r, b, r, b, r, b,
        b, r, b, r, b, r, b, r,
        r, b, r, b, r, b, r, b,
        b, r, b, r, b, r, b, r,
    ]

    sense.set_pixels(pixels)
    ```

    Isto deverá devolver um tabuleiro de xadrez azul e vermelho.

**Descarrega uma cópia do [pixels.py](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/code/pixels.py)**

## Escreve uma função `Get_Blocks`

Agora tens o teu Sense HAT a mostrar a cor do bloco que estás a pisar, podes usar a mesma lógica para mostar uma cor diferente para cada bloco à tua volta para criares um mini mapa do Minecraft em 8x8.

De modo a criares um mapa de 8x8, vais precisar de saber os IDs dos bloco imediatamente à tua volta. A API do Minecraft API tem um função `mc.getBlocks()`, mas infelizmente não funciona, portanto vamos escrever a nossa própria função.

1. Cria um ficheiro Python file e guarda-o como `minecraft-map.py`.

1. Escreve o código seguinte:

    ```python
    from sense_hat import SenseHat
    from mcpi.minecraft import Minecraft
    from time import sleep

    sense = SenseHat()
    mc = Minecraft.create()

    def get_blocks():
        blocks = []

        return blocks
    ```

    A função `get_blocks` que criamos devolve uma lista vazia de momento.

1. Agora vamos ter que implementar a nossa função `get_blocks`. Seria positivo termos uma função genérica `get_blocks` que devolvesse para qualquer extensão de `x`, `y` e `z` e devolvesse um cubo com IDs de blocos, mas tal não vai ser preciso pois só precisamos de 8x8 no mesmo eixo `y`.

    Vamos começar com uma versão simples, queremos saber que bloco estamos a pisar e os 3 blocos imediatamente à direita do jogador, o que nos devolverá uma lista de 4 IDs de blocos:

    ![First get_blocks loop](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/first-get-blocks-loop.png)

    Adiciona o código seguinte à tua função:

    ```python
    def get_blocks():
        blocks = [] # Cria uma lista vazia
        x, y, z = mc.player.getTilePos() # Obtem a posição do jogador
        y -= 1 # Subtrai 1 à coordenada y do jogador para ver o nível a baixo deste
        for dx in range(x, x+4): # Usa x valores do jogador até 3 blocos dele
            block = mc.getBlock(dx, y, z) # Procura o bloco nestas coordenadas
            blocks.append(block) # Adiciona este bloco à lista
        return blocks # Aqui devolve 4 blocos porque o ciclo correu 4 vezes
    ```

1. Adiciona uma linah no final do código para imprimir o resultado da função `get_blocks`:

    ```python
    print(get_blocks())
    ```

1. Corre o código e deverás ver a lista com 4 números (IDs de blocos), que serão o bloco que estás a pisar e os 3 blocos à tua direita.

1. Agora vais alterar a tua função para fazer o mesmo, mas para 2 dimensões. Esta versao corre o ciclo em `x` e `z` 4 vez e devolve 16 valores:

    ```python
    def get_blocks():
        blocks = []
        x, y, z = mc.player.getTilePos()
        y -= 1
        for dz in range(z, z+4):
            for dx in range(x, x+4):
                block = mc.getBlock(dx, y, dz)
                blocks.append(block)
        return blocks
    ```

1. Run the code and you should see a list of 16 block IDs, starting with the block you're standing on and the 7 to the side of you, followed by each row of 8 blocks away from you.

1. Now you'll want to make it loop over 8 rows and 8 columns, and make sure it looks to the left and right, and both behind and ahead of you. This version loops over `x` and `z` 8 times and returns 64 values:

    ```python
    def get_blocks():
        blocks = []
        x, y, z = mc.player.getTilePos()
        y -= 1
        for dz in range(z-3, z+5):
            for dx in range(x-3, x+5):
                block = mc.getBlock(dx, y, dz)
                blocks.append(block)
        return blocks
    ```

    **What does it do?**

    - `for dz in range(z-3, z+5):`: use `z` values from 3 behind the player up to 5 ahead (8 rows in total).
    - `for dx in range(x-3, x+5):`: use `x` values from 3 left of the player over to 5 to the right (8 columns in total).
    - `return blocks` - by the time the program gets to this line, this contains 64 blocks as it's been through each loop 8 times.

1. Run the code and you should see a list of 64 block IDs. This time they should be the 8x8 grid of blocks surrounding your player, with you in the middle (there's no centre point of an 8x8 grid so you're just off-centre):

    ![Third get_blocks loop](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/third-get-blocks-loop.png)

1. Next, add a `while` loop to print the result of `get_blocks` every second:

    ```python
    while True:
        print(get_blocks())
        sleep(1)
    ```

1. Run the code and see it update as you walk around.

    You will probably find that it's 

## Reduz a lentidão com caching

In order to reduce the lag, you'll need to use a technique called caching. This means you record a value the first time you look it up, and refer to the saved value when you need it the next time, rather than look it up again. To do this, you're going to use a dictionary to store the known blocks. That way, you can look up a set of coordinates in the `known_blocks` dictionary, and only use `mc.getBlock()` if you need to. This will save lots of time and make your lookup run much faster.

1. First, create an empty dictionary called `known_blocks` before your `get_blocks` function:

    ```python
    known_blocks = {}
    ```

1. You'll need to access the `known_blocks` dictionary from within your `get_blocks` function. Python will let you read a variable you declared outside the function, but not write to it. In order to write to it, you'll need to make it a **global** within the function like so:

    ```python
    def get_blocks():
        global known_blocks
    ```
    Global means you're changing the scope of the variable from being read-only to read/write.

1. Inside the function, modify the loop to look like this:

    ```python
    for dz in range(z-3, z+5):
        for dx in range(x-3, x+5):
            b = (dx, y, dz)
            if b in known_blocks:
                block = known_blocks[b]
            else:
                block = mc.getBlock(dx, y, dz)
                known_blocks[b] = block
            blocks.append(block)
    ```

    **What does it do?**

    - `b = (dx, y, dz)`: create a 3-tuple of the current coordinates.
    - `if b in known_blocks`: check if the block has already been looked up.
    - `block = known_blocks[b]`: look up the block by its coordinates.
    - `known_blocks[b] = block`: once a block is looked up for the first time, add it to the `known_blocks` dictionary.

1. Run the code and walk around. You should see it's a lot quicker at printing the blocks list out. Try reducing the `sleep` down to `0.1` and see if it can still cope.

## Cria o mapa

Now all that's left to do is create the map. You've already learned how to look up a colour from a block ID and set colours to display on the Sense HAT so this should be easy!

1. Add in some block variables:

    ```python
    # blocks
    air = 0
    grass = 2
    water = 9
    sand = 12
    ```

1. Add some colours:

    ```python
    # colours
    white = (255, 255, 255)
    green = (0, 255, 0)
    blue = (0, 0, 255)
    yellow = (255, 255, 0)
    black = (0, 0, 0)
    ```

1. Create a dictionary mapping block IDs to colours:

    ```python
    # block: colour
    colours = {
        air: white,
        grass: green,
        water: blue,
        sand: yellow,
    }
    ```

1. Modify your `while` loop like so:

    ```python
    while True:
        blocks = get_blocks()
        pixels = map_blocks_to_colours(blocks)
        print(pixels)
    ```

    Here we get the blocks from the `get_blocks` function which looks them up in the cached `known_blocks` dictionary or uses `mc.getBlock` to find them out. Then we try to convert these block IDs into colours, but that's currently a missing piece!

1. Now you'll need a `map_blocks_to_colours` function which takes a list of block IDs and returns a list of corresponding colours. Add this after your `get_blocks` function:

    ```python
    def map_blocks_to_colours(blocks):
        return [lookup_colour(block) for block in blocks]
    ```

    **How does it work?**

    This function is a one-liner, but it's quite complex. It uses a concept called list comprehension, which is a way of building up a list in a loop in a concise way.

    The whole thing is wrapped in square brackets, representing a list, and the definition is to call the `lookup_colour` function for each block in `blocks`. The list builds up as it loops over the list of blocks passed in, and is returned as a list of 64 colours.

    However, we don't have a `lookup_colour` function yet either!

1. Next you'll need to create a new `lookup_colour` function that takes a block and returns a colour. You could just use `colours[block]` but that will fail if you try to look up a colour which you haven't yet set in your directory.

    Here's a function that will return white if the block does not have a colour set:

    ```python
    def lookup_colour(block):
        if block in colours:
            return colours[block]
        else:
            return white
    ```

1. Now you have a 64 item `pixels` list, print it out to see what it looks like. It should contain 64 3-tuples representing different colour values.

1. You'll also need to define the variable `player_pos`. It'll need to be the number between `0` and `63` - the pixel which is the defined centre point of the grid. Since we used the range `x-3` to `x+5` and `z-3` to `z+5` the centre point will be the `(3, 3)` coordinate on the LED matrix, which is pixel number `27` as shown:

    ![Sense HAT grid centre point](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/sense-hat-grid-centre-point.png)

    Add the line `player_pos = 27` before your `while` loop.

1. Now add a line to your `while` loop to modify the `pixels` list to set a black pixel where your player is standing:

    ```python
    pixels[player_pos] = black
    ```

1. Everything's set up now and the last thing to do is send the list of pixels to the Sense HAT. Swap out the `print` line for a `set_pixels` one:

    ```python
    sense.set_pixels(pixels)
    ```

    O teu ciclo `while` deverá parecer-se com o seguinte:

    ```python
    while True:
        blocks = get_blocks()
        pixels = map_blocks_to_colours(blocks)
        pixels[player_pos] = black
        sense.set_pixels(pixels)
    ```

    Isto deverá mostar agora um mapa de uma pequena parte do mundo do Minecraft à tua volta. Caminha e vê-o atualizar!

 ![Mapa Sense HAT do mundo Minecraft](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/sense-hat-minecraft-map.jpg)

 **Descarrega uma cópia do [minecraft_map.py](code/minecraft_map.py)**

## E agora?

Tenta adicionar mais funcionalidades ao Sense HAT para interagires com o Minecraft!

---
Referências: 
* [Sense HAT Minecraft Map](https://www.raspberrypi.org/learning/sense-hat-minecraft-map)

