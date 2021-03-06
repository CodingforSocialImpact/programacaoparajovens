# Halterofilista Olímpico com Scratch

Com este tutorial vais conseguir desenvolver um jogo de levantamento de pesos com Scratch, usando para isso o teclado ou butões ligados ao teu Raspberry Pi.

![](https://www.raspberrypi.org/learning/resources/scratch-olympics-weightlifter/cover.png)

## Objetivos

Ao percorreres este desafio vais aprender:

* Como animar disfarces no Scratch
* Como usar seleção condicional e operadores booleanos para criares alterações no programa
* Como usar ciclos condicionais num jogo

Duração da atividade: `90 minutos.`

## Material

| Nome | Quantidade | Preço |
| --- | --- | --- |
|Raspberry Pi |1 |35€ |
|Botão (opcional) |2 |1€ |
|Breadboard (opcional) |1 |2,5€ |
|Fios de ligação (opcional) |4 |0.5€ |

## Obter os atributs do jogo

Para este projeto, vais precisar de uma `sprite` e de um `background`. Podes descarregar um ficheiro com todos os atributos do jogo [aqui](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/scratch_olympics_weightlifter.zip).

Descomprime o ficheiro.

Deverás ver 2 pastas: uma que contem a roupa da personagem e outra que contém o fundo.

## Importar para o Scratch

Abre o Scratch (`Menu` > `Desenvolvimento` > `Scratch`).

Agora clica em **Palco** e arrasta o fundo `Olympics background` para **Fundos de tela**. Podes apagar o fundo original.

De seguida, clica em **Sprite1** e um a um, arrasta os fatos do levantador de pesos para **Trajes**. Podes apagar os fatos que já estavam lá.

![screencap](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/screencap.gif)

## Testar a animação

Clica na bandeira verde para testar a tua animação:

![capture1](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture1.png)

## Capturar a velocidade com carregas no teclado

O progresso da personagem vai ser controlado pela velocidade a que os jogadores carregam na tecla `z` e `x`, portanto precisas de criar alguns comandos para capturar esta informação.

Vais precisar de 2 **variáveis** neste jogo. A primeira chamada `progress` vai ser usada para gravar o quão longe a personagem conseguiu ir. A segunda chamada `last_key`, vai ser usada para guardar a última tecla pressionada no jogo.

1. Cria as 2 variáveis clicando em **Variáveis** e depois **Nova variável**.
1. Depois, começas os teus comandos por definir `progress` como `1` e `last_key` como `x` quando o jogo começar:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture2.png)

1. O jogador tem que alternar entre `x` e `z` para que `progress` aumente, portanto quando o `x` é pressionado, o teu programa precisa de verificar se a última tecla pressionada foi o `z`. Se foi, então `progress` pode ser aumentado e `last_key` pode ser alterada para `x`. A isto chama-se **seleção condicional**.

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture3.png)
	
1. Claro que queres que o mesmo aconteça quando carregas em `z`. Podes duplicar os comandos com o `clique direito` do rato, alterando depois do seguinte modo:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture4.png)

1. Experimenta se o teu jogo funciona ao clicares na bandeira verde e ao carregares repetidamente no `x` e `z` no teclado. Deverás ver a variável `progress` aumentar.

## Fazer com que a personagem levante

1. Existem 29 fatos para a tua personagem no jogo. A sprite do fato pode ser feita de um modo contínuoThe sprite's costume can be continually set so that it's the same as the `progress` variable. That way, as `progress` increases, the costume will change. When `progress` reaches `29`, the game can end.

1. You will need a `forever` loop for the main logic of the game. Find a `forever` loop in the **Control** section and add it to the bottom of your main script:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture5.png)

1. Now place another conditional block within the `forever` loop; this time, you can use an `if else` block. If `progress` reaches `29` then the sprite can `say "I win"`, the costume can be set back to costume 1, and the script can be stopped. If `29` has not yet been reached, then the costume can be set to the same value as `progress`.
1. You can't actually set a costume to a specific number in Scratch, but you can use the `round` operator from **Operators** to set the costume to a specific number:

    ![capture](images/capture6.png)
	
1. Have a go at testing your script. Click the green flag and then start hitting the `x` and `z` keys alternately to watch the weightlifter go.
1. It's a good idea to reset the costume back to number 1 each time the script starts:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture7.png)

## Making it a little trickier

1. If you stop hitting the `x` and `z` keys, then the weightlifter just stops lifting. It would be good if he started to put the weight back down if the player's speed on the keyboard decreases. This can be done by decreasing the value of `progress` every once in a while. To start with, create a new variable and call it `difficulty`. This can be set to -1 in the main script:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture8.png)
	
1. Grab a new `when green flag clicked` block and place it into the Scripts area. You can now use a `forever if` loop, which will run as long as a variable is at a certain value. You want it to run as long as `progress` is greater than `1`:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture9.png)

1. Inside the `forever if` loop, you'll need to keep changing `progress` by the value of `difficulty`. As difficulty is a negative number, this will keep reducing progress until it reaches 1. You'll need to use a little `wait` command as well, since computers are so fast there's no way a player could keep up with the computer otherwise. Waiting for `0.4` seconds will do to start with:
    
	![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture10.png)

1. Test your game to see the weightlifter pick up the weight as you hit the keys, but lower it again if you stop pressing them.

1. If it's not working, have a look at the scripts below and make sure yours are the same:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture11.png)

## Looping the animation

Let's make the game a little more interesting now. You can start off by using a little loop effect at the start of the game. Pay attention to this next part, as you'll be using the same techniques later on.

1. The first four costumes can be looped to make the sprite look like he's getting ready to start. You'll need to get a `when I receive` block. Click on the little black arrow and create a new broadcast called `starting`:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture12.png)

1. The first thing that happens in `starting` is a switch to the first costume. This broadcast block should then contain a `repeat until` block. You can make the code inside it run until the game begins. You'll know the game has begun because `progress` will increase above `1`. Use a `>` operator from **Operators** to help you build the script below:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture13.png)

1. You can change the costume inside this loop. If the costume reaches number `4`, then it needs to be reset back to costume `1` again. You'll need a couple of `wait` blocks as well, so you can actually see the costume changing:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture14.png)
	
1. If you click on this block, it should have a halo of white around it, and the sprite should start looping.

1. To finish this section off, the `starting` block needs to be triggered from within the main script whenever `progress` is `1`, `2`, `3` or `4`. Another way of saying this is that `progress` is `< 5 and > 0`. If it is, then `starting` can be triggered and the script can wait until `progress` is greater than `4`. This all goes into the main script as shown below:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture15.png)

1. Run your script and the weightlifter should glance left and right. When you start hitting the `x` and `z` keys then he should start to lift. If you stop hitting the keys, he'll return the weight to the floor and then start glancing left and right again.

## Adding in a "strain" stage

1. There are more sections that can be looped over. Create a new `when I receive` block and change it to `stage1`:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture16.png)

1. When this is triggered, the game will get more difficult, so set `difficulty` to `-2`:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture17.png)
	
1. This little script will be very similar to `starting`, except it will loop through costumes 9 to 12 and will stay working as long as `progress` is `< 9 or > 12`. Have a go at building the script shown below:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture18.png)
	
1. This script can be triggered whenever `progress` is between 8 and 12 (`progress > 8 and progress < 13`). It should then wait until progress is no longer between 8 and 12 (`progress < 9 or progress > 12`):

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture19.png)

1. Test your script again to make sure that the animation rolls at the correct point. You might need to adjust the `wait` in the block below to a different number to test it properly:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/images/capture20.png)

## More rolls

There are a few more opportunities to roll the animation. Costumes 15, 16, 17, and 18 can be looped, as can 23, 24, 25, 26, and 27.

1. To do this, you can duplicate the scripts you have already used and just alter the values and broadcasts. Try and build the blocks below and then put the broadcasts into your main script:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture21.png)
	
	![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture22.png)
	
1. To test the script, you might want to alter the `wait` value which controls how quickly `progress` is decreased:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture23.png)

1. If your scripts aren't working, have a look at the completed game below to make sure you haven't made any errors:

    ![capture](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter/images/capture24.png)


## E agora?

Queres perceber o que se encontra por detrás de cada bloco que usaste?
Pronto para usar uma linguagem de programação como os prós?

Então visita [esta página](https://hourofpython.trinket.io/from-blocks-to-code-with-trinket#/blocks/dragging-and-dropping)!

Se quiseres mais informações para consultares nos teus projetos futuros, visita a secção dos [Recursos](/recursos/recursos.md) deste livro.

---
Referências: 
* [The Scratch Olympics Weightlifter](https://www.raspberrypi.org/learning/scratch-olympics-weightlifter)