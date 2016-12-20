# Jogo dos LEDs com Scratch

O  Raspberry Pi pode ser ligado a componentes externos, tais como lâmpadas, sensores, motores, etc., e pode ser programado em várias linguagens, desde linguagens simples e introdutórias, como o Scratch, até linguagens profissionais, como o Python.

![](http://1.bp.blogspot.com/-OiSx4oIajb8/UWGSDshhp1I/AAAAAAAAAdk/1aGmQQwxXb0/s1600/IMAG0552.jpg)

## Objetivos

Ao percorreres este desafio vais aprender:

* Os princípios básicos de eletrónica e montar um sistema eletrónico simples, com recurso a uma Breadboard, LEDs e resistências
* A explorar como o RPi pode alimentar e controlar um sistema eletrónico externo com recurso aos pinos GPIO e a linha de comandos ( Shell) do RPi
* Utilizar a linguagem de programação introdutória Scratch para controlar o sistema eletrónico

Duração da atividade: `90 minutos.`

## Material

| Nome | Quantidade | Preço/Unidade |
| --- | --- | --- |
|Raspberry Pi |1 |35€ |
|Breadboard |1 |2,5€ |
|Fios de ligação |6 |0,05€ |
|LED |5 |0,02€ |
|Resistência 1KΩ |5 |0,05€ |

### Montar o circuito

Agora que já sabes montar um circuito simples, que tal irmos mais além? Para o Jogo das Luzes vais ter que montar o seguinte circuito:

![](/assets/jogo-leds.png)

Se seguires os númerso dos pinos por disposição física:

![](https://www.raspberrypi.org/learning/physical-computing-guide/images/physical-pin-numbers.png)

Vais ter fios ligados ao pino `6`, `11`, `12`, `13`, `15` e `16`.

### Fazer os LEDs piscar com o Scratch

1. Abre o `Scratch GPIO`.

1. Vamos começar por criar a ação piscar: uma ação piscar faz com que o LED seja acendido, fique aceso durante `0.05` segundos e depois se apague. Cada um dos LED deverá ter a sua ação.

1. Insere o controlo `Quando receber a ação X`, e cria uma nova ação, sendo `X` o nome da ação (ex: “x1, x2, ...”).

1. Anuncia ação `pin11high`.

1. Insere um tempo de espera de `0.05`.

1. Anuncia ação `pin11low`.

1. Repete os pontos 1 a 6 para os restantes pinos (pin12, pin13, pin15 e pin16), mudando o nome da ação para cada um dos pinos (ex: x11, x12,...)

1. Insere um controlo que ao pressionar a letra `T`, do teclado, executa as ações que definiste anteriormente, todas ao mesmo tempo (anúncio sem espera):

 1. `Controlo`->`Quando tecla t pressionada`.
 1. `Controlo`->`Anuncie x` (ex: x1, x2, ...).
 
### Fazer os LED piscar em sequência

Os LEDs devem piscar em sequência, da esquerda para a direita. 
Para isso vais usar as ações do ponto anterior.

1. Começa por definir a letra `G` do teclado, como a letra que inicia o jogo: `Controlo`->`Quando tecla g pressionada`

1. Adiciona o bloco sempre: `Controlo`->`sempre`.

1. Dentro do ciclo `sempre`, repete o seguinte 5 vezes (uma por cada LED):

 1. Anuncia ação `x_` e espera. O valor será o nome das ações criadas na primeira parte (ex: x1, x2, ...) `Controlo`->`Anuncie x e espera`.
 
### Parar quando clicar em espaço

Quando se clica na tecla espaço, o jogo deverá parar.

1. Insere um controlo que recebe a tecla `espaço`.
1. Adiciona o bloco ‘ stop all’  que está no separador  Control.
 
### Verificar se ganhou o jogo, ou não

Para verificar se ganhámos o jogo, temos que verificar que após parar LED aceso é o 3o. Para isso é preciso fazer alterações nas ações piscar para definir o LED que estamos a acender.14.Cria a variável ‘LedAtual’:  Variables > ‘ make variable’15. Em cada uma das ações piscar (x1, x2, etc..) define a variável ‘LedAtual’ com o número do LED correspondente. Por exemplo, na ação do pin11, define ‘LedAtual’ como 11. Para isso, insere este a instrução seguinte antes do ‘ pinXXhigh’:Variables > ‘ set LedAtual to X’

### Mostrar mensagem ‘Ganhou’ ou ‘Perdeu’

Ao parar, se o LED for o correto deverá aparecer a mensagem ‘Ganhou’. Caso contrário deverá aparecer a mensagem ‘Perdeu’. Faz as mudanças no bloco que está a parar o jogo para que as mensagens apareçam (‘ When space key pressed’).16.Verificar se ‘LedAtual’ é igual a 13a. Control > ‘ if __ else __’b. Dentro do bloco ‘ if AQUI else __’, adicionar: Operators > ‘ _=_’17. Se for igual, ‘ if _ AQUI else’, mostra a mensagem ‘Ganhou’ erepita 5 vezes o seguinte:a. Execute a ação do LED 13 (anuncie e espere)b. Espere 1 segundo18. Se for diferente, ‘ if _ else AQUI’, mostra a mensagem ‘Perdeu’.

### Apagar os LED e terminar

Como medida de segurança, ao parar o jogo, todos os LED devem ser desligados.19.Para cada um dos LED, execute (anuncie) a ação ‘ pinXXlow’ no bloco anterior.

### Adicionar um botão (opcional)

Introduz um sensor de pressão (botão) para parar o jogo, em vez da tecla de espaço.20. Introduz a seguinte alteração ao teu circuito:

 No programa, adiciona um controlo que recebe a letra ‘G’ doteclado22. Define um ciclo (‘ forever’) e dentro dele:a. Verifica se valor do sensor, ‘pin26’ (‘ pin26 sensor value”) é igual a 0.b. Repete os passos 15 ao 17

## E agora?

Queres perceber o que se encontra por detrás de cada bloco que usaste?
Pronto para usar uma linguagem de programação como os prós?

Então visita [esta página](https://hourofpython.trinket.io/from-blocks-to-code-with-trinket#/blocks/dragging-and-dropping)!

Se quiseres mais informações para consultares nos teus projetos futuros, visita a secção dos [Recursos](/recursos/recursos.md) deste livro.

---
Referências: 
* [Raspberry Pi Scratch GPIO Disco Lights Game](http://pdwhomeautomation.blogspot.pt/2013/04/raspberry-pi-scratch-gpio-disco-lights.html)