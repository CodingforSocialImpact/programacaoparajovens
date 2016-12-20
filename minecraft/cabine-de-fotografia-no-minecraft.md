# Cabine de Fotografia no Minecraft

Cria uma Cabine de Fotografias no Minecraft com blocos, quando o jogador entrar na cabine tira uma fotografia tua no mundo real.  
Não te esqueças de sorrir!

![](https://www.raspberrypi.org/learning/resources/minecraft-photobooth/cover.png)

## Objetivos

Ao percorreres este desafio vais aprender:

* Como controlar o mundo do Minecraft com a API do Python
* Como encontrar as coordenadas `x`,`y` e `z`
* Como usar as coordenadas para desencadear o módulo da câmara
* Como usar funções, ciclos `while`, e declarações `if`

Duração da atividade: `90 minutos.`

## Material

| Nome | Quantidade | Preço |
| --- | --- | --- |
|Raspberry Pi |1 |35€ |
|Pi Camera |1 |25€ |

## Ligar a Câmera

Antes de ligar o Raspebrry Pi, vais precisar de igar a câmera.  
Podes encontrar instruções de como fazer isto na [página de instalação da câmera](https://www.raspberrypi.org/learning/getting-started-with-picamera/worksheet/).

## Importar os Módulos do Minecraft e da Câmera

A primeira coisa que precisas de fazer é importar a API do Minecraft. Isto possibilita-te ligar o Minecraft com código em Python. Também vais precisas de importar o módulo `PiCamera` para controlar a câmara e módulo `time`(tempo) para adicionar uma pequena espera quando tira uma foto e a próxima foto.

1. Abre o Minecraft a partir do menu, entra num mundo já existente, ou cria um novo.
2. Desloca a janela do Minecraft para um lado do ecrã. Vais precisar de usar a tecla `Tab` para poderes usar o rato fora da janela do Minecraft.
3. Abre o `Python 3` a partir do menu. É aqui que vais escrever o teu programa!![](https://www.raspberrypi.org/learning/minecraft-photobooth/images/python3-app-menu.png)
4. Clica em `New > Window` para abrir uma janela nova.
5. Introduz o seguinte código:

   ```python
   from mcpi.minecraft import Minecraft
   from picamera import PiCamera
   from time import sleep
   # Criar o mundo Minecraft
   mc = Minecraft.create()
   # Chamar a câmara
   camera = PiCamera()
   # Mensagem para o mundo do Minecraft
   mc.postToChat("Olá Mundo")
   ```

6. Guarda com `CTRL + S` e corre o programa com `F5`. Deverá aparecer a mensagem `Olá Mundo` na janela do Minecraft.


## Testar o módulo da Câmara

De seguida, vais escrever algum código para testares a câmara.

1. Adiciona as linhas seguintes ao final do teu programa:  
  ```python

   # Começas a ver a pré-visualização
   camera.start_preview()

   # Espera 2 segundos
   sleep(2)

   # Tira a fotografia e guarda nos documentos
   camera.capture('/home/pi/selfie.jpg')

   # Termina a pré-visualização
   camera.stop_preview()  
   ```

2. Guarda e corre o teu programa para tirar uma fotografia.
3. Abre o esplorador de ficheiros para veres a foto que tiraste.

## Contruir a Cabine de Fotografias

Agora vais precisar de criar uma cabine no mundo do Minecraft. Isto é feito manuelmente e a cabine pode ser contruída onde quiseres.  
Usando qualquer tipo de bloco, constrói a tua cabine. Pode ser de qualquer forma que pretendas, mas deve ter um bloco de largura de espaço livre dentro, para que o jogador possa entrar, como uma porta ou portão.

![](https://www.raspberrypi.org/learning/minecraft-photobooth/images/photobooth.png)

Assim que tenhas criado a tua cabine, precisas de mover o teu jogador para dentro para o bloco que desencadeia a ação. Este é o bloco que o jogador pisa para correr a função que escreveste anteriormente, que desencadeia a câmara.  
No mundo do Minecraft a tua posição é dada em referência aos eixos `x`,`y` e `z`.    
Olha para o canto superior esquerdo da janela e vais encontrar as coordenadas `x`,`y` e `z` do teu jogador, por exemplo `10.5`, `9.0` e `-44.3`. Assumindo que ainda estás na cabine, então estas são as coordenadas `x`,`y` e `z` do bloco que desencadeia a ação na tua cabine.

1. Desloca-te até à tua cabine
2. Regista as coordenadas `x`,`y` e `z` do bloco que desencadeia a ação da câmara.

## Encontrar a tua posição

Quando estás a jogar Mincraft, o teu programa irá precisar de verificar que te encontras dentro da cabine. Se estiveres, então vai desencadear a função `take_the_pic` que vai tirar uma fotografia com a câmara. Para fazeres isto o Minecraft precisa de saber onde estás no mundo.

Para encontrar a tua localização, usas o código `x, y, x = mc.player.getPos()`, que guarda as coordenadas `x`,`y` e `z` da tua localização nas variáveis `x`,`y` e `z`. Podes depois usar `print(x)` para imprimir a coordenada `x`, ou `print(x, y, z)` para veres todas. 
Agora que sabes as posições da tua personagem, podes testar para veres se este está na cabine.

Como estamos a usar o Minecraft podemos usar também `mc.postToChat` para vermos as coordenadas na janela do Minecraft.

1. Muda a mensagem `Olá mundo` para `Encontra a cabine` depois da linha `Minecraft.create()`:

   ```python
   mc = Minecraft.create()

   mc.postToChat("Encontra a cabine")
   ```

2. Adiciona no final do teu código:

   ```python
   while True:
    x, y, z, = mc.player.getPos()
    mc.postToChat((x, y, z))
   ```

3. Guarda e corre o código e verás as coordenadas na janela do Minecraft.

4. Clica na janela do Python e carrega `CTRL + C` para interromper o código.

## Testar se estás na cabine de fotografias

Neste ponto temos uma cabine, as coordenadas do bloco que desencadeia a ação, e código para controlar o módulo da câmara e tirar uma fotografia.  
O próximo passo é testar se o programa consegue identificar quando estás na cabine. Para alcançares isto tens que criar um ciclo que verifica se as coordenadas do teu jogador correspondem às coordenadas do bloco que desencadeia a ação. Caso estas coincidam, então estás na cabine. Para fazeres isto basta um simples `if` (se), que nós chamamos uma instrução ***condicional***.

1. Altera as linhas dentro teu ciclo `while` (enquanto) para que correspondam ao código em baixo.

  ```python
  while True:
  x, y, z = mc.player.getPos()

  sleep(3)
  # Garante que as coordenadas que inseres são as coordenadas da tua cabine.
  # Repara que o if verifica se o x é maior ou igual do que 10.5, isto é para verificar que apanha o bloco que pode ter o valor de 10.6.
  if x >= 10.5 and y == 9.0 and z == -44.3:
  mc.postToChat("Estás na tua cabine!")
  ```

2. Guarda e corre o código, para o testar caminha em direção à tua cabine e deverás ver uma mensagem `Estás na tua cabine!` no mundo do Minecraft.


## Montar tudo

Agora que tens uma cabine a funcionar precisamos de adicionar o módulo da câmara para tirar uma fotografia. Vamos adicionar um lembrete para sorrir e depois chamar o código de captura da câmara.

1. Adiciona as instruções para enviar mensagens para o Minecraft e o `capture()` dentro do teu `if` para tirar a fotografia:

```python
if x >= 10.5 and y == 9.0 and z == -44.3:
    mc.postToChat("Estás na tua cabine!")
    sleep(1)
    mc.postToChat("Sorri!")
    sleep(1)
    camera.start_preview()
    sleep(2)
    camera.capture('/home/pi/selfie.jpg')
    camera.stop_preview()

sleep(3)
```

Isto vai verificar constantemente a tua localização. Quando a tua localização coincidir com a cabine, vai tirar uma fotografia com a câmara.

## E agora?

1. Tenta adicionar um bloco específico no Minecraft que tire a fotografia
2. Tenta adicionar mais blocos para controlar as propriedades da câmara, tais como fazer um vídeo ou aplicar um filtro
3. Tenta usar blocos para começar e parar a gravação de vídeo

---
Referências: 
* [Minecraft Photobooth](https://www.raspberrypi.org/learning/minecraft-photobooth)
