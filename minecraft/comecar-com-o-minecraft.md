# Começar com o Minecraft

O Minecraft é um jogo de mundo aberto onde existe uma versão gratuita para Raspberry Pi que inclui uma interface de programação. Isto significa que podes escrever comandos e programas em código Python para construir coisas no jogo automáticamente. É um modo muito bom para aprenderes Python!

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/minecraft-pi-banner.png)

## Objetivos

Ao percorreres este desafio vais aprender:

* Como aceder ao Minecraft e a criar um novo mundo
* Como usar o ambiente de desenvolvimento do Python para ligar ao Minecraft
* Como controlar o mundo do Minecraft com a API do Python
* Como usar variáveis para guardar IDs para diferentes tipos de blocos
* Experimentar com a colocação de diferentes tipos de blocos com atributos especiais

Duração da atividade: `90 minutos`.

## Material

| Nome | Quantidade | Preço |
| --- | --- | --- |
|Raspberry Pi | 1 | 35€ |

## Correr o Minecraft

Para correr o Minecraft, abre-o a partir do menu no ambiente de trabalho, ou escreve `minecraft-pi` no terminal.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/menu.png)

Quando o Minecraft Pi estiver carregado, clica em `Start Game` (Iniciar Jogo), seguido de `Create New` (Criar Novo).

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-game.png)

Encontras-te agora num jogo do Minecraft! Podes caminhar, e construir coisas!

Usa o rato para olhares à tua volta e usa a teclas seguintes no teu teclado:


| Tecla | Ação |
| :--- | :--- |
| W | Para a frente |
| A | Para a esquerda |
| S | Para trás |
| D | Para a direita |
| E | Inventário |
| Espaço | Saltar |
| Duplo Espaço (Rápido) | Voar/Cair |
| Esc | Pausa/Menu de Jogo |
| Tab | Soltar a Seta do Rato |

Podes selecionar um item do painel rápido com: a roda do rato, usar os número no teu teclado, ou a tecla `E` e selecionar algo do teu inventário.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-inventory.png)

Podes ainda fazer um duplo `Espaço` para voar. Irás parar de voar quando soltares a tecla Espaço e se fizeres novamente duplo `Espaço` cais em direção ao chão.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-flying.png)

Com a espada na mão, podes clicar nos blocos à tua frente para os remover (ou para escavar). Com um bloco na tua mão, podes usar o `clique direito` do rato para colocar esse bloco à tua frente, ou o `clique esquerdo` do rato para o remover.

## Usar a Interface de Programação em Python

Com o Minecraft a correr, e o mundo criado, clica em `Tab` para que possas mover o rato para fora da janela do Minecraft. Abre o `Python 3` a partir do menu de aplicacões no ambiente de trabalho e coloca as janelas lado a lado.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/helloworld.gif)

Podes escrever comandos diretamente na janela do Python ou criar um ficheiro para que possas guardar e correr o teu código numa outra vez.

Se quiseres criar um ficheiro, vai a `File > New File` (Novo Ficheiro) e `File > Save` (Guardar). Guarda numa pasta à tua escolha.

Começa por importar a libraria do Minecraft, o que irá criar uma ligação do Python ao jogo, podes testá-la com a mensagem `Olá Mundo` no ecrâ.

```python
from mcpi.minecraft import Minecraft

mc = Minecraft.create()

mc.postToChat("Olá Mundo")
```

Se estiveres a a escrever diretamente na janela do Python carrega no `Enter` no final de cada linha.

Se estiveres a guardar num ficheiro, guarda com `CTR + S` e corre com `F5`. Quando o teu código correr irás ver uma mensagem na janela do jogo.

### Encontrar a tua localização

Para encontrares a tua localização, escreve:

```python
pos = mc.player.getPos()
```
`pos` contém a tua localização. Podes aceder a cada componente das coordenadas com `pos.x`,`pos.y`e `pos.z`.

Alternativamente, podes guardar as compoenentes em variáveis separadas tirando partido da técnica de desempacotagem do Python:

```python
x, y, z = mc.player.getPos()
```

Agora `x`,`y`e `z` contêm cada parte da posição das tuas coordenadas. `x` e `z` são as direções de caminhada (para trás/frente e esquerda/direita) e o `y` é cima/baixo.

Nota que `getPos()` devolve a localização do jogador naquela altura e se mexeres a posição tens que chamar novamente a função ou usar a localização guardada.

### Teletransportar

Podes também especificar uma localização para te teletransportares para ela.

```python
x, y, z = mc.player.getPos()
mc.player.setPos(x, y+100, z)
```

Isto fará com que o jogador se teletransporte para 100 espaços no ar. O que significa que irás teletransportar-te para o meio do céu e começarás a cair para onde começaste.

Tenta teletransportar-te para outro local!

### Definir blocos

Podes colocar um bloco num sítio específico com `mc.setBlock()`:

```python
x, y, z = mc.player.getPos()
mc.setBlock(x+1, y, z, 1)
```

Agora uma pedra vai aparecer ao teu lado, ou mesmo à tua frente (roda a vista com o rato para o encontares)!

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-setblock.png)

Os argumentos passados para `set block` são `x`, `y`, `z` e `id`. O `(x,y,z)` corresponde à tua posição no mundo (nós especificamos um bloco de distância a partir de onde se encontra o jogador com `x+1`) e o `id` corresponde ao tipo de bloco que quisemos colocar, neste caso `1` é pedra.

Outros blocos que podes experimentar:

```python
Air:   0
Grass: 2
Dirt:  3
```

Agora com o bloco em vista, tenta altera-lo para algo diferente:

```python
mc.setBlock(x+1, y, z, 2)
```

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-setblock2.png)

Deverás ver o bloco cinzento mudar mesmo à tua frente!

### Constantes dos Blocos

Podes usar as constantes de blocos imbutidas, se souberes o nome delas.
Vais precisar de outra linha de `import` primeiro.

```python
from mcpi import block
```

Agora podes escrever o seguinte para criares um bloco de pedra (`STONE`):

```python
mc.setBlock(x+3, y, z, block.STONE.id)
```

Os IDs (identificadores) são bastante fáceis de adivinhar, usa letras maiúsculas sempre, ficam aqui alguns exemplos:

|IDs |Tradução |
|---|---|
|WOOD_PLANKS |Madeira |
|WATER_STATIONARY |Água |
|GOLD_ORE |Minério de Ouro |
|GOLD_BLOCK |Bloco de Ouro |
|DIAMOND_BLOCK |Bloco de Diamante |
|NETHER_REACTOR_CORE |Núcleo do Neather Reactor |

#### Blocos como variáveis

Se souberes o ID de um bloco pode ser útil defini-lo como variável.
Podes usar o nome ou número inteiro do id.

```python
# Nome -> DIRT
dirt = block.DIRT.id
mc.setBlock(x, y, z, dirt)

# OU

# Id -> 3
dirt = 3
mc.setBlock(x, y, z, dirt)
```
#### Blocos especiais

Existem alguns blocos que possuem propriedades extra, como a lã (`wool`) que tem uma propriedade extra onde podes especificar a cor.
Para usares este parâmetro edita o teu `setBlock`do seguinte modo:

```python
wool = 35
mc.setBlock(x, y, z, wool, 1)
```
Aqui o quarto parâmetro `1` define a cor como laranja. Sem o quarto parâmetro assume o valor pré-definido (`0`) que é branco. Mais algumas cores:

|ID |Cor |
|---|---|
|0 |Branco |
|1 |Laranja |
|2 |Magenta |
|3 |Azul claro |
|4 |Amarelo |

Experimenta mais alguns número para veres as cores do bloco alterarem-se!

Outros blocos que também possuem propriedades extra são: a madeira (`wood`), a erva (`tall grass`), a chama (`torch`). Podes consultar mais na [API do Minecraft](http://www.stuffaboutcode.com/p/minecraft-api-reference.html).

#### Definir blocos múltiplos

Tal como defines um único bloco com o `setBlock`, também podes definir vários de uma só vez com o `setBlocks`:

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-setblocks.png)

```python
# Isto vai criar um bloco de 10x10x10 de pedra
stone = 1
x, y, z = mc.player.getPos()
mc.setBlocks(x+1, y+1, z+1, x+11, y+11, z+11, stone)
```

Podes criar volumes maiores com o `setBlocks` mas poderá demorar mais tempo a ser gerado.

## Deixar cair blocos enquanto andas

Agora que já sabes criar blocos, vamos usar a nossa localização em movimento para ir deixando um rasto de blocos enquanto caminhamos.

```python
from mcpi.minecraft import Minecraft
from time import sleep

mc = Minecraft.create()

# O código seguinte irá deixar uma flor atrás do jogador enquanto caminhas
flower = 38

while True:
    x, y, z = mc.player.getPos()
    mc.setBlock(x, y, z, flower)
    sleep(0.1)
```

Agora caminha um pouco e vira-te para trás para veres as flores no teu caminho.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-flowers.png)

Como usamos um ciclo `while True` (enquanto Verdadeiro) este ciclo nunca irá terminar. 

Para o parar pressiona `CTRL + C`na janela do Python para interromper.

Experimenta voar e vê as flores que deixas no céu.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-flowers-sky.png)

E se quiséssemos que apenas deixar cair flores quando estivéssemos a andar em erva? Podemos usar o `getBlock` para descobrir que tipo de bloco é.

```python
# A posição em que o jogador se encontra (x,y,z)
x, y, z = mc.player.getPos()
# O identificador do bloco
this_block = mc.getBlock(x, y, z)  
# Imprime o Id do bloco
print(this_block) 
```

Isto diz a localização do bloco que o jogador está, se for `0` é porque o jogador encontra-se no ar.
Como queremos saber em que bloco estamos mesmo a pisar, subtraímos `1` ao valor do `y` e usamos o `getBlock()` para determinar que tipo de bloco estamos a pisar mesmo.

```python
# A posição em que o jogador se encontra (x,y,z)
x, y, z = mc.player.getPos()
# O identificador do bloco
this_block = mc.getBlock(x, y-1, z) 
# Imprime o Id do bloco
print(this_block) 
```

Isto diz a localização do bloco que o jogador está **a pisar**.
Podes testar isto se criares um ciclo que vai imprimindo o ID do bloco enquanto vais caminhando.

```python
while True:
    x, y, z = mc.player.getPos()
    block_beneath = mc.getBlock(x, y-1, z)
    print(block_beneath)
```

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/blockbeneath.gif)

Podemos usar um condicional `if` para escolher se plantamos, ou não, uma flor.

```python
grass = 2
flower = 38

while True:
    x, y, z = mc.player.getPos()  # player position (x, y, z)
    block_beneath = mc.getBlock(x, y-1, z)  # block ID

    # Se o bloco que estás a pisar é erva
    if block_beneath == grass:
        # Então cria uma flor
        mc.setBlock(x, y, z, flower)
    sleep(0.1)
```

Talvez de seguida podemos alterar o cubo que estamos a pisar em erva, se já não for erva.

```python
# Se o bloco que estás a pisar é erva
if block_beneath == grass:
    # Então cria uma flor
    mc.setBlock(x, y, z, flower)
# Caso contrário
else:
    # Transforma o bloco em erva
    mc.setBlock(x, y-1, z, grass)
```

Agora podemos andar e se estivermos a pisar erva, deixamos uma flor. Se o próximo bloco não for erva, ele vai ser transformado em erva. Quando nos virarmos e voltarmos a esse bloco, vamos deixar lá uma flor.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-flowers-grass.png)

## Brincar com blocos de TNT

Outro bloco interessante é o TNT!
Para criarmos um bloco de TNT usamos:

```python
tnt = 46
mc.setBlock(x, y, z, tnt)
```

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-tnt.png)

No entanto este bloco de TNT é algo aborrecido. Tenta definir `data` como `1`:

```python
tnt = 46
mc.setBlock(x, y, z, tnt, 1)
```

Agora usa a tua espada e faz `clique esquerdo` no bloco de TNT: ele vai ficar ativo e explodir numa questão de segundos!

Agora tenta construir um bloco gigante de TNT!


```python
tnt = 46
mc.setBlocks(x+1, y+1, z+1, x+11, y+11, z+11, tnt, 1)
```

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-tnt-blocks.png)

Agora vais ver um bloco gigante de TNT.
Vai lá e ativa um dos blocos, não te esqueças de fujir e apreciar o espetáculo! Pode ser um pouco lento por termos muita informação para processar.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/mcpi-tnt-explode.png)

## Diversão com lava a fluir

Um bloco que é bastante divertido de brincar é a lava que flui.

```python
from mcpi.minecraft import Minecraft

mc = Minecraft.create()

x, y, z = mc.player.getPos()

lava = 10

mc.setBlock(x+3, y+3, z, lava)
```

Encontra o bloco que acabaste de criar e deverás ver lava a fluir do bloco para o chão.

A parte interessante da lava é que quando arrefece torna-se pedra.
Move-te para outra localização do mundo e experimenta o seguinte:

```python
from mcpi.minecraft import Minecraft
from time import sleep

mc = Minecraft.create()

x, y, z = mc.player.getPos()

lava = 10
water = 8
air = 0

mc.setBlock(x+3, y+3, z, lava)
sleep(20)
mc.setBlock(x+3,y+5, z, water)
sleep(4)
mc.setBlock(x+3, y+5, z, air)
```

Podes ajustar o `sleep` (esperar) para deixar mais, ou menos, lava fluir.

![](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/images/lava.png)

## E agora?

Há muita coisa que podes explorar no Minecraft ainda por cima agora já sabes usar o Python para criares os teus mundos mais depressa!

Podes criar um jogo em rede com os teus colegas, de modo a poderem todos ver-se no mesmo mundo. Basta para isso que se liguem todos os Raspberry Pis na mesma rede.

Para saberes mais sobre as opções de programação do Minecraft podes consultar [stuffaboutcode.com](http://www.stuffaboutcode.com/p/minecraft-api-reference.html).

---
Referências: 
* [Getting started with Minecraft](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi)
