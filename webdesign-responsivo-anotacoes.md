# Webdesign Responsivo
## Design Fluido
O começo de um design fluido é um sistema de colunas com porcentagens (medidas flexíveis).

## Medidas Flexíveis
* **Porcentagem (principal)**: os tamanhos (width, height, padding, margin, etc.) levam em consideração o tamanho do elemento pai. Assim, é preciso tomar cuidado, pois os estilos são aplicados em cascata.

* **em**: tem um comportamento bastante similar ao da medida de Porcentagem (levar em consideração o tamnho do elemento pai). Contudo, quando aplicado para os tamanhos **width e height**, eles passam a ser baseados no tamanho da fonte, isto é, se defino, por exemplo, um ```height: 1.25em``` quer dizer que a altura do meu elemento terá 125% do tamanho da fonte do elemento, assim, se minha fonte tem 16px, meu elemento terá 20px de altura.

Apesar do ```em``` não ser fluído por natureza, sua característica permite que uma alteração na fonte base do texto escale proporcionalmente outros elementos na página.

## Lidando com vários tamanhos de tela
O ```max-width``` e ```min-width``` são ótimas formas de limitar a fluidez de elementos na página (afinal, é difícil fazer tudo fluir bem de 0 até infinitos pixels).

Com eles podemos aplicar estilos para telas com no máximo _n_ pixels (max-width) ou no mínimo _y_ pixels (min-width).

O ```máx-width``` também é muito útil para trabalhar com **imagens**, evitando deixar que a imagem cresça mais do que o seu tamanho original, mantendo a sua qualidade, por exemplo em dispositivos com resolução maior que 1200px (como monitores grandes e SmarTVs).

É possível chegar a um layout responsivo, aplicando apenas o conceito de **design fluido**, ou seja, utilizando as medidas flexíveis e com auxílio de valores de display como inline-block, flex, grid, etc. para lidar com os tamanhos de tela.

Entretanto, na maioria dos casos de criação de sites responsivos, precisaremos em algum momento criar um 'layout condicional', isto é, estilos que se aplicam de acordo com determinadas condições que, obviamente, serão os tamanhos de tela.

Para isso fazemos uso das famosas **media queries**.

## CSS3 Media Queries
As media queries nos auxiliam na criação de estilos específicos associados a determinada condição (tamanho de tela) que desejamos atender.

Existem várias media queries, é válido consultar a documentação.

Contudo, as mais utilizadas são:

* min-width e max-width;
* orientation: portrait e orientation: landscape;

Dessa forma, para criar rapidamente um layout responsivo para três dispositivos com telas diferentes, poderíamos fazer:

```
/* tela de um smartphone: 1 coluna */
main {
   width: 100%
}

/* tela de um tablet: 2 colunas */
@media (min-width: 400px) {
   width: 50%;
}

/* tela de um notebook ou PC: 3 colunas */
@media (min-width: 1024px) {
   width: 33.33%;
}
```
Os pontos onde ocorrem as mudanças de layout para cada dispositivo são chamados de **breakpoints**.

Para definir bem um **breakpoint** a boa prática é visualizar como o **conteúdo** do nosso site se comporta em diferentes telas. Sabendo bem quais são os objetivos do site, em quais dispositivos ele pode ser acessado e como ele se comporta em cada um deles, fica mais fácil estabelecer o ponto de quebra (ou de mudança) do design.

### Mobile First


### Inserindo o responsivo
Para, de fato, fazer o navegador entender que nós preparamos a nossa página para diversos tipos de tela, precisamos fazer uso de uma tag no HTML.

Inserimos a tag ```meta``` com ```name="viewport"``` mais o content="width=device-width"

```html
<meta name="viewport" content="width=device-width">
```

Existe um bug conhecido no iOS que faz com que o ```viewport``` não se adapte ao rotacionar o dispositivo. Uma gambiarra que evita o bug é colocar o ```viewport``` como:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">.
```

## Testes
Os navegadores desktop ajudam muito durante a codificação por permitir testes rápidos, fáceis e com ferramentas boas (dev tools de chrome e firefox). Todavia, não eliminam a necessidade de teste num dispositivo real e em emuladores móveis. Os navegadores são diferentes e a experiência do usuário é diferente.

## Menu Responsivo
Normalmente quando fazemos um design responsivo, o menu sofre modificações mais profundas do que o resto da página, um exemplo disso é o site da globo.com, cria-se um menu lateral que é acionado quando o botão de menu é clicado (normalmente aquelas três barrinhas horizontais).

Como sempre em programação, existem diversas formas de fazer, uma delas consiste em criar uma media query estabelecendo um ```max-width``` de aproximadamente 600px (dispositivos com até 600px de largura) e inserir as propriedades para criação desse menu lateral.

A partir disso, não existe mistério, são as propriedades do CSS que vão construir esse layout.

O destaque fica para a utilização das propriedades ```position```, ```z-index```, e ```transition```

O ```position: fixed``` + ```z-index: 1``` irão posicionar esse menu lateral sobre o resto da página. Neste ponto, será necessário inserir um ```left: -90%``` (caso o menu seja posicionado à esquerda da página) para escondê-lo por padrão.

Com isso utilizamos o transition: ```left .3s ease-out``` para inserir uma animação para quando o botão de menu for clicado.

É importante observar que precisaremos utilizar um código em JavaScript para acionar o evento de clique que faz aparecer o menu lateral.

Dessa forma, o código em CSS ficaria algo como:

```
@media (max-width: 600px) {
   .barra-nav {
      background: #f0f0f0;
      padding: 1em;
      margin: 0;

      height: 100%;
      width: 90%;
      max-width: 320px;

      position: fixed;
      z-index: 1;
      top: 0;
      left: -90%;

      transition: left .3s ease-out;
   }

   .menu-ativo .barra-nav {
      left: 0;
   }

   .menu-principal li {
      padding: 1em 0;
      width: 100%;
   }
}
```
Depois disso, ficaria faltando apenas tratar o caso das telas maiores, onde não deverão aparecer os botões criados para o menu responsivo.

Para isso, um recurso importante é a negação da media query criada anteriormente

### Negação de Media Query
Se antes tínhamos ```@media (max-width:600px)``` e agora queremos o inverso dela. Como fazer?

A primeira reação é fazer ```@media (min-width:600px)```, mas isso está errado. Como os valores são inclusive, no ponto 600px, as 2 media queries vão ser executadas.

Então, pensamos em ```@media (min-width:601px)```. É quase certo. Realmente a media query anterior vai executar até 600px inclusive, e essa vai de 601px em diante. Mas isso só funcionaria se assumirmos que não existe nenhum valor entre 600px e 601px, como deveria ser. Mas não é. As telas de alta resolução e o zoom do usuário afetam essa conta e criam o conceito de subpixels. Em CSS, um px não é um pixel físico na tela, mas uma medida que depende de vários fatores (e pode ser flutuante).

Assim, a única forma é negar a media query com not. Um detalhe é que ```@media not (max-width:600px)``` é uma sintaxe inválida. Precisamos fazer ```@media not all and (max-width:600px)```. Note que o **not** nega a media query toda e não só a parte do **all**.
