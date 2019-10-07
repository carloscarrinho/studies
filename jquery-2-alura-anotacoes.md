# Curso jQuery 2
## Plataforma Alura
### Animações com o jquery
O jQuery possui algumas funções que facilitam a criação de animações em nossa página.

#### Mostrar ou Esconder um elemento
Caso quisermos mostrar ou esconder um elemento na página, podemos utilizar:

- **.css()** - altera uma propriedade no CSS;
- **.show()** - mostra um elemento do DOM;
- **.hide()** - esconde um elemento do DOM;
- **.toggle()** - mostra ou esconde um elemento do DOM, conforme o seu estado no momento (se tá mostrando ele esconde, se tá escondido ele mostra).

Vamos visualizar os casos:

Caso A) Modificando uma propriedade no CSS com o **.css()**:

Primeiro criamos uma classe e no CSS escondemos o elemento que queremos:

```css
/*estabelecemos uma classe que esconde um placar */
.placar {
   display: none;
}
```
A partir daí podemos utilizar ```.css()``` para modificar esse valor, com o auxílio de um botão (previamente configurado no HTML) e um evento de clique:

```javascript
//busca o botao no DOM, atribui um evento de click que chama uma função 'mostraPlacar'
$('#botao-placar').click(mostraPlacar);

//cria a função 'mostraPlacar'
function mostraPlacar() {
   //modifica a propriedade no CSS de 'none' (definido antes) para 'block'
   $('.placar').css('display', 'block');
}
```
Assim, quando o botão for clicado, a propriedade será modificada no CSS que irá esconder o elemento 'placar'

Contudo, depois que o placar for mostrado, mesmo que eu clique novamente no botão, o placar não voltará a ficar escondido. Seria necessário recarregar a página para que isso acontecesse ou criar uma lógica com a função 'if' para poder implementar essa rotina.

Porém, o jQuery possui outros recursos que facilitam a implementação dessa situação.


Caso B) Modificando o elemento com **.show()** ou **.hide()**

O contexto seria similar ao caso A, porém utilizaríamos duas funções específicas que permitem acessar (mostrando ou escondendo) diretamente o elemento no DOM, sem precisar mexer no CSS.

```javascript
$('.placar').show();

//ou

$('.placar').hide();
```
Esse caso também exigiria que estabelecessemos uma condicional para quando o placar estivesse à mostra, utilizasse o .hide() e ao contrário, utilizasse o .show().

Existe uma forma mais fácil, que é o .toggle().


Caso C) Modificando o elemento com **.toggle()**:

Esta função funciona como o .show e .hide de uma só vez, isto é, quando o placar está à mostra ele esconde (como se fosse o 'hide') e quando está escondido ele mostra (como se fosse o 'show')

```javascript
$('.placar').toggle();
```
Bem mais simples.


Existe, ainda, uma outra animação com o auxílio das funções **.slideDown()**, **.slideUp()** ou **.slideToggle()**. Elas funcionam na mesma lígica de 'show', 'hide' e 'toggle', todavia, elas adicionam uma animação mais suave na página, deslizando para baixo (slideDown) ou para cima (slideUp), conforme o caso.

Dentro dessas funções é possível passar o tempo da animação em milisegundos

```javascript
$('.placar').slideToggle(600)
//o placar irá aparecer descendo ou sumir subindo na tela em uma animação de 2 seg.
```

#### Remover um elemento
Na implementação de uma página dinâmica podemos, em algum momento, querer remover um determinado elemento. Para isso, podemos utilizar puramente a função **.remove()**.

Contudo, essa função remove instantaneamente o elemento a medida que fazemos uso de um evento de clique, por exemplo.

Pensando na experiência do usuário, é interessante inserir algum tipo de animação que permita que essa remoção aconteça de uma forma mais suave. Para essa questão temos a função **.fadeOut()**. Com ela podemos dar uma breve suavizada na remoção do elemento.

Um ponto importante a observar, porém, é que a **.fadeOut()** não remove, de fato, o elemento, ela apenas o esconde. Isto é, o navegador vai aumentando a opacidade do elemento até implementar um ```display: none```.

Então, para remover por completo, precisamos fazer uso da função **.remove()** em conjunto com a função **.setTimeOut()**, que estabelece um tempo para que essa função seja aplicada (o tempo que o fadeOut necessita para realizar a sua animação).

O código poderia ficar assim:

```javascript
function removeLinha(event) {
   //retirando o comportamento padrão do navegador
   event.preventDefault()

   //buscando o elemento que deseja remover
   var linha = $('.linha');

   //estabelecendo a animação com 'fadeOut'
   linha.fadeOut(1000);

   //estabelecendo um atraso na remoção final do elemento com o 'setTimeOut' e 'remove'
   setTimeOut(function (){
      linha.remove()
   }; 1000)
}
```
Assim como as funções anteriores, além do **.fadeOut()**, também existe o **.fadeIn()** e o **.fadeToggle()**.


Um recurso útil para trabalhar com animações é a função **.stop()**, que permite dar um melhor comportamento às animações. Esta função encerra uma animação que está ocorrendo antes de iniciar a outra.

No exemplo com o **.slideToggle()**, caso o usuário fizesse repetidos cliques, sem o **.stop()** o navegador realizaria todas as animações. Levando em consideração que esta animação tem um pequeno delay, ficaria uma bagunça e o usuário teria que esperar terminar todas as animações até poder executar outra ação.

Assim, inserindo o **.stop()** antes do **.slideToggle()**, conseguiríamos controlar essa situação dentro da função 'mostraPlacar'

```javascript
function mostraPlacar() {
   $('.placar').stop().slideToggle(600);
}
//é importante lembrar dos parênteses.
```

Outra função interessante para desenvolver animações a partir do JavaScript é a **.animate()**. Nela, precisamos passar dois parâmetros: o primeiro é um objeto e o segundo é o intervalo de animação.

DETALHAR MELHOR A IMPLEMENTAÇÃO DO ANIMATE

Para fazer uso do **.animate()**, principalmente combinado com **.slideDown()** ou **.slideUp()** é comum precisarmos da posição para a qual queremos fazer esta animação. Para isso utilizamos outra função, chamada **.offSet()**.

Na offSet devemos indicar em qual ponto da posição informada queremos encerrar, no 'top', no 'bottom', etc.

```javascript
function scrollPlacar() {
    var posicaoPlacar = $(".placar").offset().top;

    $("html, body").animate(
    {
        scrollTop: posicaoPlacar
    }, 1000);
}
```
