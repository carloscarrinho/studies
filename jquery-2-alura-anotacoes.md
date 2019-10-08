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
A partir daí, podemos utilizar ```.css()``` para modificar esse valor, com o auxílio de um botão (previamente configurado no HTML) e um evento de clique:

```javascript
//busca o botao no DOM, atribui um evento de click que chama uma função 'mostraPlacar'
$('#botao-placar').click(mostraPlacar);

//cria a função 'mostraPlacar'
function mostraPlacar() {
   //modifica a propriedade no CSS de 'none' (definido antes) para 'block'
   $('.placar').css('display', 'block');
}
```
Assim, quando o botão for clicado, a propriedade será modificada no CSS que irá mostrar o elemento 'placar'

Contudo, depois que o placar for mostrado, mesmo que eu clique novamente no botão, o placar não voltará a ficar escondido. Seria necessário recarregar a página para que isso acontecesse ou criar uma lógica com a função 'if' para poder implementar essa rotina.

O jQuery, porém, possui outros recursos que facilitam a implementação dessa situação.


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


Existe, ainda, uma outra animação com o auxílio das funções **.slideDown()**, **.slideUp()** ou **.slideToggle()**. Elas funcionam na mesma lógica de 'show', 'hide' e 'toggle', todavia, elas adicionam uma animação mais suave na página, deslizando para baixo (slideDown) ou para cima (slideUp), conforme o caso.

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

   //buscando o elemento que deseja remover e atribuindo uma variável 'linha' apenas por questões semânticas
   var linha = $('.linha');

   //estabelecendo a animação com 'fadeOut'
   linha.fadeOut(1000);

   //estabelecendo um atraso na remoção final do elemento com o 'setTimeOut' e 'remove'
   setTimeOut(function (){
      linha.remove()
   }; 1000)
}
```

Também é possível ativar a função **.remove()** somente após o **.fadeOut()** chamando-a como um parâmtro dentro do fadeOut por meio de uma função anônima:

```JavaScript
var linha = $('.linha');

linha.fadeOut(function () {
   linha.remove();
})
```
Desse modo, o **remove** somente será aplicado após a finalização da animação do **fadeOut**.

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

#### Outras funções interessantes para animação
Outra função interessante para desenvolver animações a partir do JavaScript é a **.animate()**. Nela, precisamos passar dois parâmetros: o primeiro é um objeto e o segundo é o intervalo de animação.

Para fazer uso do **.animate()**, principalmente combinado com **.slideDown()** ou **.slideUp()** é comum precisarmos da posição para a qual queremos fazer esta animação.

Para isso utilizamos outra função, chamada **.offSet()**. Esta função retorna as características de um objeto, dentre elas a sua posição.

Desse modo, na ```.offSet()``` devemos indicar qual elemento do documento queremos animar e em qual ponto da posição informada queremos encerrar a animação, no 'top', no 'bottom', etc.

```javascript
function scrollPlacar() {
   //buscando o elemento 'placar', encontrando a sua posição e armazenando em uma variável semântica.
    var posicaoPlacar = $(".placar").offset().top;
}
```

A partir disso, chamamos a função ```.animate()``` passando os parâmetros que ela precisa: as propriedades do objeto que buscamos com o **.offset()** e o intervalo de animação.

```javascript
var posicaoPlacar = $(".placar").offset().top;

//chamando todo 'body' da página e animando através da propriedade 'scrollTop'
//a aplicação de propriedades nos objetos JavaScript é similar a um código em CSS
$("html, body").animate(
{
   //o valor para 'scrollTop' precisa ser passado como uma unidade de medida
   //daí a concatenação da variável 'posicaoPlacar' com 'px'
    scrollTop: posicaoPlacar+'px'
}, 1000);
```

O jQuery possui a função ```is``` que permite consultar uma pseudo class dentro do CSS. Toda vez que um elemento esta com display diferente de ```none``` ele ganha a pseudo class **:visible**.

A função ```is``` retorna ```true``` caso o elemento esteja visível. Se ele estiver visível, precisamos escondê-lo e isso é feito através da função ```hide```. Para exibir o elemento, é usada a função ```show```.

```javascript
//queremos mostrar ou esconder um elemento no DOM utilizando a função 'is'
$('#botao-promocao').click(function() {

  var promocoes = $('.promocoes');
  //testamos se o elemento com a class 'promocoes' estiver visível
  if(promocoes.is(':visible')) {

    promocoes.hide();
  } else {
    promocoes.show();
  }
});
```

De forma similar ao ```is```, o jQuery também possui a função ```hasClass``` que retorna ```true``` se um elemento possui ou não uma classe.

No exemeplo anterior, removemos a classe **invisivel** caso o elemento já a tenha e a adicionamos caso ele não a tenha. Todo esse processo é feito a cada clique do usuário.

```javascript
$('#botao-promocao').click(function() {

  var promocoes = $('.promocoes');
  //testamos se o elemento com a class 'promocoes' também possui a class 'invisivel'
  if(promocoes.hasClass('invisivel')) {
    promocoes.removeClass('invisivel');

  } else {
    promocoes.addClass('invisivel');
  }
});
```

Neste caso, o resultado destas últimas duas funções, ```is``` e ```hasClass``` é o mesmo. Mas é válido entender que o **is** testa se já uma pseudo class e o **hasClass** testa se há uma class.

### Utilizando AJAX
AJAX é o acrônimo de *'Asynchronous Javascript and XML'*, que em português significa *'Javascript e XML assíncronos'* e consiste em um recurso utilizado pela linguagem JavaScript que permite:

- Ler os dados de um servidor web, depois de a página já estar carregada;
- Atualizar os dados na página sem recarregá-la;
- Enviar os dados para um servidor web por debaixo dos panos (sem que o usuário visualize o processo).

**estudar o node.js**
