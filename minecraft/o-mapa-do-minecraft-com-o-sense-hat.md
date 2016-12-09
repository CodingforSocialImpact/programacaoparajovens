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

5. F

6. 

7. 

8. 

9. 

10. 

## Caminhada colorida com o Minecraft e o Sense HAT

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

5. F

6. 

7. 

8. 

9. 

10. 

## Definir LEDs individuais no Sense HAT

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

5. F

6. 

## Escreve uma função `Get_Blocks`

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

5. F

6. 

7. 

8. 

9. 

10. 

11. 

## Reduz a lentidão com caching

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

## Criar o Mapa

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

5. F

6.

7.

8.

9.

10.

 ![Mapa Sense HAT do mundo Minecraft](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/images/sense-hat-minecraft-map.jpg)
 Descarrega uma cópia do [minecraft_map.py](https://www.raspberrypi.org/learning/sense-hat-minecraft-map/code/minecraft_map.py)
## E agora?

Tenta adicionar mais funcionalidades ao Sense HAT para interagires com o Minecraft!

---
Referências: 
* [Sense HAT Minecraft Map](https://www.raspberrypi.org/learning/sense-hat-minecraft-map)

