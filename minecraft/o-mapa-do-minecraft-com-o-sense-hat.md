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

1. Corre o código e deverás ver a lista de 16 IDs de blocos, a começar no bloco que estás a pisar e 7 ao teu lado, seguidos de linhas com 8 blocos afastados de ti.

1. Agora vais querer que corra um ciclo por 8 linhas e 8 colunas, garante que eset olha para a diretia, esquerda, frente e para trás. Esta versão corre o ciclo por `x` e `z` 8 vezes e devolve 64 valores:

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

1. Corre o código e deverás ver a lista de 64 IDs de blocos que cercam o teu jogador, contigo no meio (numa grelha de 8x8 não há meio, portanto deslocamos um pouco).

    ![Third get_blocks loop](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/third-get-blocks-loop.png)

1. De seguida, adiciona um ciclo `while` para imprimir o resultado do `get_blocks` a cada segundo:

    ```python
    while True:
        print(get_blocks())
        sleep(1)
    ```

1. Corre o código e vê se ele atualiza quando te moves.

    Provavelmente vais achar um pouco lento, porque estamos a pesquisar 64 blocos por cada segundo!

## Reduz a lentidão com caching

De modo a reduzires a lentidão, vais usar uma tecnica chamada de caching. Isto significa que vais guardar o valor na primeira vez que o pesquisares, e usar esse valor guardado de cada vez que precisares dele, em vez de o pesquisares de novo. Para alcançares este efeito vais usar u dicionário para guardar os blocos conhecidos, assim poderás consultar o dicinário `known_blocks` e usar apenas o `mc.getBlock()` se precisares mesmo. Esta técnica vai permitir-te poupar tempo e fazer com que o teu ciclo corra mais rápido.

1. Primeiro, cria um dicionário vazio chamado `known_blocks` antes da função `get_blocks`:

    ```python
    known_blocks = {}
    ```

1. Vais precisar de aceder ao dicionário `known_blocks` na tua função `get_blocks`. O Python vai deixar-te ler a variável declarada fora da função, mas não te vai permitir escrever. De modo a poderes escrever, precisas de a tornar numa **global** dentro da função:

    ```python
    def get_blocks():
        global known_blocks
    ```
    Global significa que estás a alterar a variável de leitura apenas para escrita/leitura.

1. Dentro da função, altera o ciclo para:

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

1. Corre o código e e caminha. Deverás perceber que ºe bastnate mais rápido a imprimir a lista. Tenta reduzir o `sleep` para `0.1` e vê se consegue ser jogável ainda.

## Cria o mapa

Agora tudo o que tens que fazer é criar o mapa.

1. Adiciona algumas variáveis de blocos:

    ```python
    # blocos
    air = 0
    grass = 2
    water = 9
    sand = 12
    ```

1. Adiciona algumas cores:

    ```python
    # cores
    white = (255, 255, 255)
    green = (0, 255, 0)
    blue = (0, 0, 255)
    yellow = (255, 255, 0)
    black = (0, 0, 0)
    ```

1. Cria um dicionário para mapear IDs de blocos com as cores:

    ```python
    # bloco: cor
    colours = {
        air: white,
        grass: green,
        water: blue,
        sand: yellow,
    }
    ```

1. Modifica o teu ciclo `while`:

    ```python
    while True:
        blocks = get_blocks()
        pixels = map_blocks_to_colours(blocks)
        print(pixels)
    ```

    Aqui obtemos os blocos na função `get_blocks` que pesquisa-os no dicionário `known_blocks` em cache ou usa o `mc.getBlock` para os descobrir. Depois tentamos converter estes IDs de blocos para cores, mas essa peça está em falta!

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
