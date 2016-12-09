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



---
Referências: 
* [Connecting and Controlling an LED with a Breadboard](https://www.raspberrypi.org/learning/physical-computing-guide/connect-leds/)