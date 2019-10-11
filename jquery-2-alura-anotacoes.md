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

Então, para remover por completo, precisamos fazer uso da função **.remove()** em conjunto com a função **.setTimeout()**, que estabelece um tempo para que essa função seja aplicada (o tempo que o fadeOut necessita para realizar a sua animação).

O código poderia ficar assim:

```javascript
function removeLinha(event) {
   //retirando o comportamento padrão do navegador
   event.preventDefault()

   //buscando o elemento que deseja remover e atribuindo uma variável 'linha' apenas por questões semânticas
   var linha = $('.linha');

   //estabelecendo a animação com 'fadeOut'
   linha.fadeOut(1000);

   //estabelecendo um atraso na remoção final do elemento com o 'setTimeout' e 'remove'
   setTimeout(function (){
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

Diante dos objetivos/propósitos do AJAX, o jQuery disponibiliza algumas funções que nos permitem aplicar esse conceito nos nossos sistemas.

#### Buscando informações

A função mais básica é a **$.get()**, que serve para realizar requisições HTTP do tipo GET para um determinado endereço de servidor que possui os dados que queremos buscar.

A sintaxe da função pede dois parâmetros: o primeiro é o **endereço para o qual faremos a requisição** e o segundo a **ação (função) que deverá ser executada** após o recebimento da resposta do servidor.

Então fica: ```$.get(endereço, acao)```

Quando a função ```$.get``` vai retornar dados para que sejam utilizados pelo usuário, é preciso colocar nos argumentos da função que é chamada ao sucesso da requisição uma variável que irá conter os dados recebidos. Normalmente colocamos um nome semântico, como **dados** ou **data**, para indicar que aquele é o resultado obtido da requisição AJAX

A forma como estes dados estão dispostos pode variar, mas um caso comum é que eles estejam no formato **JSON**, que consiste em um objeto, contendo as propriedades de cada item da lista. Esses itens por sua vez, são representados por índices, partindo de zero.

Uma possibilidade é o segundo parâmtro do 'get' como uma função anônima:

```javascript
$('#botao-frase').click(fraseAleatoria)
//passando o segundo parâmetro do '$.get' como função anônima
$.get('http://localhost:3000/frases', function (data) {
   //buscamos o elemento com a class 'frase' no DOM e o guardamos na variável 'frase'
   var frase = $('.frase')

   //pegamos a propriedade 'texto' contida no item guardado no índice zero do objeto
   //e a inserimos no lugar da frase que estava no elemento
   frase.text((data[0]).texto);
})
```
Perceba que estabelecemos que o retorno da requisição se chama 'data' (poderia ser 'retorno', 'dados', 'informações', etc.) e o passamos como parâmetro da função, assim podemos passar esse retorno dentro da função, indicando que estamos fazendo uso de tais dados contidos no banco de dados do servidor.

Outra possibilidade é passar o segundo parâmetro como uma função nomeada:

```javascript
$('#botao-frase').click(fraseAleatoria);

function fraseAleatoria() {
   //passando o segundo parâmetro do '$.get' como função nomeada
   $.get('http://localhost:3000/frases', trocaFraseAleatoria);
}

function trocaFraseAleatoria(data) {
   var frase = $('.frase').text
   frase.text((data[0]).texto);   
}

```

--

##### Fique de olho

Duas funções úteis do JavaScript comumente utilizadas no trabalho com AJAX são as funções **Math.random()** e **Math.floor()**. Elas servem para criar números aleatórios.

A ```Math.random()``` gera um número aleatório, porém este número vem completo, com várias casas decimais (0.XXXXXXXXXXX). Como normalmente precisamos de um número inteiro, precisamos utilizar a ```Math.floor()``` que arredonda este número para baixo.

--

#### Tratando erros
No trabalho envolvendo sistemas web é muito comum haver erros, seja porque houve alguma falha de codificação, no servidor ou meramente por conta da internet do usuário, os erros são diversos.

O jQuery possui uma função complementar à função **$.get** chamada ```.fail()``` que identifica um erro na requisição e retorna algum tipo de resultado, a ser estabelecido dentro da função.

```javascript
$('#botao-frase').click(fraseAleatoria);

function fraseAleatoria() {
   $.get('http://localhost:3000/frases', trocaFraseAleatoria)
   //estabelecendo um 'alert' para o usuario caso a requisição 'get' falhe
   .fail(function () {
      alert('Ocorreu um erro, por favor tente novamente!');
   })
}
```

#### Experiência do usuário
Assim como os erros, existem outros recursos complementares à função **$.get** que permitem melhorar a experiência do usuário na utilização do sistema.

Uma delas é a função ```.always()``` que executa uma determinada ação sempre que terminar a requisição, seja ela bem sucedida ou não.

Isso nos permite, por exemplo, inserir elementos visuais na tela que deem um feedback para o usuário sobre o que está acontecendo na página. Isto é, em alguns casos pode haver demora no retorno da requisição, assim, esse pequeno (ou não tão pequeno) intervalo de tempo entre a solicitação e a resposta poderia ter uma informação de que a solicitação está sendo processada.

Um elemento visual comum é o 'spinner' que consiste naquelas barrinhas de 'loading' que existem de variadas formas na internet.

Para implementar esta ideia, pode ser criada uma ```div``` no documento que contém uma imagem de spinner e inicia com um ```display: none```. A partir daí, em nosso código JavaScript criamos a função **.always()** que vai trocar o display para 'show' enquanto o retorno da função **$.get** não acontece:

```javascript
$('#botao-frase').click(fraseAleatoria);

function fraseAleatoria() {
   //mostra o 'spinner' quando a função 'fraseAleatoria' for ativada (início da requisição)
   $('#spinner').show()

   $.get('http://localhost:3000/frases', trocaFraseAleatoria)
   //estabelecendo um 'alert' para o usuario caso a requisição 'get' falhe
   .fail(function () {
      alert('Ocorreu um erro, por favor tente novamente!');
   })
   .always(function () {
      //esconde o 'spinner' quando receber o retorno da requisição
      $('#spinner').hide();
   })
}
```
A principal ideia de implementar um spinner como um elemento visual após uma requisição AJAX é informar ao usuário que o pedido dele está sendo processado, e exibir visualmente um ícone clássico que simboliza isto. É uma questão de melhorar a **UX(User eXperience)** do usuário na aplicação, algo que é muito importante na construção de qualquer sistema hoje em dia.

#### Enviando informações com GET
Em sistemas web complexos, não só precisamos buscar informações, mas também enviamos determinadas informações. No jQuery a função ```$.get``` também pode funcionar com este objetivo.

Para que possamos buscar uma informação específica no nosso banco de dados, utilizamos o **$.get()** novamente, porém agora passamos três parâmetros, sendo o primeiro o **endereço** do servidor no qual iremos buscar, o segundo o **parâmetro** do dado que queremos encontrar e o terceiro a ação que desejamos executar após o retorno.

Então fica assim: ```$.get(endereco, parametro do dado, acao)```

Seguindo um exemplo prático, imaginemos que queremos buscar uma frase, por meio do seu índice (parametro) no array, a partir de um input e clique do usuário na página.

Primeiro criamos o campo para input e o botão no HTML e depois partimos para o código JavaScript que implementa tal dinâmica.

Para conseguirmos enviar dados via AJAX, com jQuery, precisamos passar os dados como uma **String** ou um **Objeto JavaScript** simples, como o segundo parâmetro da função $.get(). Este objeto é informado entre chaves {}, qual o tipo de dado (parametro) que se deseja buscar (id, texto, number, nome, etc.) e o valor a ser procurado.

```javascript
//quando clicar no botão, executa a função 'buscaFrase'
$('#botao-frase-id').click(buscaFrase);

function buscaFrase() {
   //busca o valor digitado pelo usuário no campo 'frase-id' e armazena na variável 'fraseId'
   var fraseId = $('#frase-id').val()

   //indicamos que o objeto que queremos possui o valor de 'id' igual ao valor armazenado em 'fraseId'
   var dados = {id: fraseId};
   //no endereço, busca objeto especificado e quando retornar, executa a função 'trocaFrase'
   $.get('http://localhost:3000/frases', dados, trocaFrase);
}

function trocaFrase (data) {
   var frase = $('frase');
   //indicando qual parametro do objeto encontrado deve-se imprimir na tela
   frase.text(data.texto)   
}
```
É válido dizer que para consumirmos dados de um servidor precisamos conhecê-lo bem. Geralmente quem construiu o servidor gera uma documentação que lista todos os endereços possíveis, quais verbos do HTTP usar e seus devidos parâmetros.

A documentação fornecida pelo programador Back-End pode variar de empresa para empresa, mas devemos ter a absoluta certeza que essa informação precisa ser passada. Não é obrigação do programador Front-End adivinhar os endereços e quais parâmetros eles recebem.

Por exemplo, se for um cadastro de funcionários, eu preciso saber que o objeto na posição de id[0] está o Alexandre, no id[1] a Andressa, e por aí vai. Além disso, deve estar especificado quais outros parâmetros existem, por exemplo, a idade, a formação, o endereço, entre outros.

Assim, conseguiremos buscar a informação que queremos a partir desses parâmetros, utilizando 'data.nome', 'data.idade', 'data.formacao', 'data.endereco', etc.

#### Enviando informações com POST
Para relembrar, enquanto o verbo ```GET``` nos permite **buscar** uma determinada informação no banco de dados, o verbo ```POST``` nos permite **gerar um registro** em tal banco.

Portanto, caso a nossa página não possua um mecanismo de armazenar as informações passadas pelo usuário, quando ele recarregar a página, todos os seus dados são perdido e a aplicação volta a ter o banco original.

Se em nossa aplicação web temos a intenção que o usuário interaja de uma forma que seja necessário (ou interessante) o armazenamento de suas informações, precisaremos utilizar o verbo **POST**. Para utilizá-lo, a sintaxe é identica ao do verbo GET.

Precisamos indicar ```$.post(endereco, dados a enviar)```

Antes de fazer esse envio, porém, existem algumas 'premissas' que precisam ser atendidas.

A primeira delas é que precisamos de um evento que inicie esta requisição POST, pode ser, por exemplo, um botão. A segunda diz respeito ao formato do dado que enviaremos, isto é, os dados precisam ser um **Objeto JavaScript**.

```javascript
//exemplo de objeto JavaScript
{
   //parametro: valor
   id: '0'
   usuario: 'carloscarrinho'
   placar: '5'
}
```


#### Função EACH
A função ```.each()``` do jQuery serve para percorrer a lista de itens em um array.

```javascript
$('li').each(function () {
   var texto = $(this).text();
   console.log(texto);
})
```
Neste caso, primeiro todos os elementos ```li``` são selecionados e para cada um deles é executada a função ```console.log() ``` que é passada como parâmetro do método ```each()```.

A primeira iteração do ```this``` representará o primeiro elemento do array, na segunda iteração representará o segundo elemento e assim por diante. Imprimindo o conteúdo ```text``` de cada uma das **li** da página em questão.

Lembrando que existe a função ```.forEach()``` no JavaScript 'puro' que nos permite executar ações como essa.

```javascript
var pessoas = ['Cadu', 'Emili', 'Ana', 'Carlos', 'Aparecida', 'Raphael'];

pessoas.forEach(function (pessoa) {
   console.log(pessoa);
})
```
Nesse caso, será impresso no console do navegador cada um dos itens do array, isto é, o nome de cada pessoa.

Aqui o array foi definido dentro do próprio aquivo .js, porém, também podemos selecionar a partir de um elemento html, como no exemplo anterior.

```javascript
var pessoas = getElementsByTagName('li');

pessoas.forEach(function (pessoa) {
   console.log(pessoa);
})
```
Aqui o resultado seria o mesmo, porém buscando os itens de uma lista no HTML.

#### Same Origin Policy
*Same Origin* significa que por padrão o navegador não permite chamar um outro servidor que não é da mesma origem. Ou seja, se a aplicação foi carregada pelo endereço 'http://localhost:3000', o navegador só permite requisições para o domínio 'localhost' na porta '3000', pelo protocolo 'http'.

Então, se tentarmos fazer um AJAX (buscar ou inserir dados) em uma página que esteja, por exemplo, nos endereços 'https://localhost:3000', 'http://alura/3000' ou 'http://localhost/2000' o navegador retornará um erro dizendo que não é permitido o acesso a tal servidor.

Isso porque nós não fizemos uma requisição para o mesmo host (localhost), pelo mesmo protocolo (http) ou para a mesma porta (3000).

Isso tudo existe para evitar fraudes e é uma forma de impedir que o usuário use um site que na verdade não representa a origem.

#### CORS - Cross-Origin Resource Sharing
Então é impossível carregar as frases do outro servidor? Não! Mas nesse caso é preciso configurar as outras origens permitidas no servidor que se pretende acessar via AJAX.

Assim o outro servidor (não a origem que já funciona com AJAX) adiciona um cabeçalho na resposta HTTP e baseado nessa resposta o navegador permite uma requisição feita de outra origem.

O cabeçalho é bem simples e faz parte do protocolo HTTP:

```javascript
Access-Control-Allow-Origin: http://localhost:3000, http://192.168.0.83:3000
```
Essa forma de permitir chamar uma outra origem também é chamado de **Cross-Origin Resource Sharing** ou **CORS**.

Repare então que isso não é uma configuração do jQuery ou AJAX em geral. Isso é algo que o servidor precisa se preocupar e adicionar na resposta HTTP. Como nosso foco aqui é jQuery não vamos dar muitos detalhes pois depende muito da linguagem e framework utilizado no lado do servidor.

Contudo, um exemplo de como poderia ser feito se escrevermos a aplicação servidora em **node.js (JavaScript) usando o framework Express**. Para habilitar CORS com Express bastaria utilizar:

```javascript
app.use(function(req, res, next) {
  res.header("Access-Control-Allow-Origin", "http://localhost:3000, http://192.168.0.83:3000");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});
```
Percebemos então que o processo de habilitar ou não CORS é de responsabilidade do programador back-end. Sendo assim, o programador front-end pode solicitar sua habilitação, mas claro, quando o desenvolvedor back-end ver sentido nisso.
