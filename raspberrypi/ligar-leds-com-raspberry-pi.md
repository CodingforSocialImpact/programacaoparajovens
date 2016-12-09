## Ligar LEDs com o Raspberry Pi

O  Raspberry Pi pode ser ligado a componentes externos, tais como lâmpadas, sensores, motores, etc., e pode ser programado em várias linguagens, desde linguagens simples e introdutórias, como o Scratch, até linguagens profissionais, como o Python.

![](https://www.raspberrypi.org/documentation/usage/gpio/images/gpio-led.png)

### Objetivos

Ao percorreres este desafio vais aprender:

* Princípios básicos de eletrónica e montar um sistema eletrónico simples, com recurso a uma Breadboard, LEDs e resistências
* Explorar como o RPi pode alimentar e controlar um sistema eletrónico externo com recurso aos pinos GPIO e a linha de comandos (`Shell`) do RPi

Duração da atividade: `90 minutos.`

### Material

| Nome | Quantidade | Preço |
| --- | --- | --- |
|Raspberry Pi |1 |35€ |
|Breadboard |1 |2,5€ |
|Fios de ligação |4 |0.1€ |
|LED |1 |0.1€ |
|Resitência 1kΩ |1 |0.01€ |

## Conetar um LED com uma breadboard

Na breadboard os buracos junto à linha vermelha estão todos ligados entre si, assim como os da linha azul, os burcaos horizontais entre as colunas vermelho-azul, estão também ligados entre si.

![Pinos GPIO](https://www.raspberrypi.org/learning/physical-computing-guide/images/gpio-numbers-pi2.png)

1. Pega num `fio de ligação` e liga-o ao pino GPIO `Ground` no `RPi` e liga a outra ponta num buraco na `coluna azul` na `breadboard`, como demonstrado na imagem.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/gpio-connect-ground.png)

2. Agora pega num LED, uma das pernas é mais comprida (ânodo) do que a outra (cátodo). 
3. Coloca a `ânodo` na coluna `E` na `breadboard` (Por exemplo `E3`), e o `cátodo` no buraco seguinte (por exemplo `E2`).

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/gpio-connect-red-led.png)

4. Coloca a `resistência` com uma perna na `coluna azul` e outra a ligar ao `cátodo` do `LED`.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/gpio-connect-resistor.png)

5. Agora para completar o circuito e a corrente fluir vais precisar de outro fio de ligação.
Pega nesse `fio de ligação` e liga-o ao `GPIO 18` no `RPi`, depois liga a outra ponta ao `ânodo` do `LED`.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/gpio-complete-circuit.png)

6. Vamos agora programar o LED para acender, para isso abrimos a `linha de comandos` (Menu->Acessórios->LXTerminal).

 ![LXTerminal](https://www.raspberrypi.org/documentation/usage/terminal/images/lxterminal.png)

7. Agora que vais ter que inserir instruções para controlar o RPi.
Define o `GPIO 18` para modo de escrita (`out`). Escreve a seguinte instrução na consola que abriste:
```
gpio -g mode 18 out
```

8. Liga o `GPIO 18`:

 ```
gpio –g write 18 1
```
Acabaste de informar o RPi que deve passar energia ao circuito (daí o número 1 no final das instrução). O LED irá acender!

9. Para desligar o LED, vamos deixar de lhe passar energia. Como? Desliga o `GPIO 18`.

 ```
gpio –g write 18 0
```

10. Agora que já acendeste um LED, podes adicionar ainda mais, sendo sempre preciso uma resistência para cada LED, fica aqui um exemplo com 3 LEDs ligados aos pinos GPIO `18`, `7` e `20`.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/gpio-complete-circuit2.png)

### Programar LEDs com Scratch

Agora vamos usar o Scratch para programar o nosso LED.

1. Com o teu circuito feito anteriormente no passo 9 completo, estás agora pronto para usar o Scratch. Inicia o `Scratch` (Menu->Desenvolvimento->Scratch).

 ![Iniciar o Scratch](https://www.raspberrypi.org/learning/physical-computing-guide/images/scratch-icon.png)

 ![Scratch](https://www.raspberrypi.org/learning/physical-computing-guide/images/Scratch-interface.png)
2. Clica em `Controle` no painel esquerdo e arrasta o `quando clicado` para a área de comandos.

 ![Bandeira Verde](https://www.raspberrypi.org/learning/physical-computing-guide/images/green_flag.png)

3. Arrasta um bloco `anuncie` para a tua area de comandos e junta-o ao bloco `quando clicado`, edita a caixa de texto dentro do `anuncie` (`novo`) e escreve `gpioserveron` (ligar servidor GPIO).

4. Arrasta outro bloco `anuncie` e escreve `config18output`, isto configura o Pino 18 como saída de informação.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/scratch_config.png)

5. Arrasta outro bloco `anuncie` e escreve `gpio18on` (ligar GPIO 18).

6. Arrasta um bloco `espere 1 segundos` e liga-o aos blocos anteriores.

7. Arrasta outro bloco `anuncie` e escreve `config18off` (desligar GPIO 18).

8. Guarda o teu trabalho como `Teste LED` (File->Salvar Como).

9. Clica na `bandeira verde` no canto superior direito.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/green_flag_icon.png)

 Deverás ver o LED a acender e a apagar.

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/scratch_complete.png)

10. Mas e se quisermos que acenda e apague consecutivamente (como uma árvore de natal)?
Adiciona um bloco `espere 1 segundos` no último lugar e um bloco `sempre` no topo do nosso programa.

11. Guarda o teu trabalho como `Teste LED` (File->Salvar Como).

12. Clica na `bandeira verde` no canto superior direito.
Deverás ver o LED a acender e a apagar, de 1 em 1 segundo!

### Programar LEDs com Python

Agora vamos usar Python para programar o nosso LED.

1. Abre o `Python 3` (Menu->Desenvolvimento->Python 3).

 ![](https://www.raspberrypi.org/learning/physical-computing-guide/images/open_idle.png)

2. Cria um novo programa (File->New File).

3. Escreve lá o seguinte código:

 ```python
 import time
 import RPi.GPIO as GPIO
 GPIO.setmode(GPIO.BCM)
 GPIO.setwarnings(False)

 led = 18

 GPIO.setup(led,GPIO.OUT)
 ```

4. Debaixo do código que escreveste adiciona:
 ```python
 print("LED ligado")
 GPIO.output(led,GPIO.HIGH)
 ```

5. O código até aqui apenas liga o LED, vamos agora adicionar o código para o desligar após algum tempo:

 ```python
 time.sleep(1)
 print("LED Desligado")
 GPIO.output(led,GPIO.LOW)
 ```

6. A parte final do teu programa é:

 ```python
 GPIO.cleanup()
 ```

7. Guarda o teu código (File->Save)

8. Corre o teu programa `F5`. Ele só acendeu uma vez.

9. Para acender consecutivamente temos que adicionar uma espera após desligar (para estar 1 segundo apagado) e adicionar um ciclo ao nosso programa:

 ```python
 import time
 import RPi.GPIO as GPIO
 GPIO.setmode(GPIO.BCM)
 GPIO.setwarnings(False)

 led = 18
 GPIO.setup(led,GPIO.OUT)

 # Este ciclo não termina
 while True:
    
     print("LED ligado")
     GPIO.output(led,GPIO.HIGH)
     time.sleep(1)
     print("LED Desligado")
     GPIO.output(led,GPIO.LOW)
     time.sleep(1)
    
 GPIO.cleanup()
 ```
10. Guarda o teu código (File->Save)

11. Corre o teu programa `F5`. Parabéns ele já pisca!

## E agora?

Podes experimentar ligar mais LEDs ao teu circuito e faze-los alternar!

---
Referências: 
* [Connecting and Controlling an LED with a Breadboard](https://www.raspberrypi.org/learning/physical-computing-guide/connect-leds/)
* [Testing a Connected LED in Scratch](https://www.raspberrypi.org/learning/physical-computing-guide/test-led-scratch/)
* [Testing a Connected LED in Python](https://www.raspberrypi.org/learning/physical-computing-guide/test-led-python/)