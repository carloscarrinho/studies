# Posicionamento e Layout

Vale a pena conferir: https://css-tricks.com/snippets/css/a-guide-to-flexbox/

## Formas de Posicionamento no CSS
O CSS possui algumas formas de aplicar um posicionamento aos elementos, criando assim um layout para a página. Podemos utilizar a propriedade ```display``` com diversos atributos, os mais usados são:

* **inline:**
Colocando ```display: inline``` nos elementos permite eles se posicionarem um do lado do outro, o seu problema é que os elementos não aceitam mais que seja modificada tanto a ```width``` quanto a ```height```. Isso limita MUITO nossas possibilidades.

* **block:**
O ```display: block``` até permite adicionar width e height, porém os elementos não ficam mais lado a lado. Então não é muito útil (nesse contexto de criação de layouts).

* **inline-block:**
O ```display: inline-block``` permite os elementos se posicionarem um do lado do outro porém, diferentemente do ```display: inline``` ele permite que os elementos tenham sua width e height modificadas. Por esse motivo o ```display: inline-block``` é muito mais interessante na maioria dos casos do que o ```display: inline```.

O problema de usar ```display: inline-block``` é espaçar os elementos entre si. Para fazer isso teríamos que colocar margins e fazer contas.


Podemos inclusive utilizar a propriedade ```position```

* **float: left | right:**

O ```float``` é mais complicado, ele empurra o elemento para um dos lados (left | right) e os elementos que estão embaixo sobem. Isso nem sempre é o que a gente quer. Além do mais, o ```float``` não permite que usemos a propriedade ```vertical-align: middle``` para alinhar os elementos verticalmente. Ou seja, para contornar isso uma possibilidade seria ter que colocar ```margin-top``` ou ```margin-bottom``` nos elementos e usar os temidos números mágicos!


Por tais motivos, para criar **layouts**, isto é, aplicar posicionamentos de vários elementos que darão a estrutura da página, o mais usual (e mais fácil) é combinarmos o 'display' **flex** com o **grid**.

O ```display: flex``` veio com o intuito de facilitar nossa vida nesses aspectos de posicionamento. Ele permite os elementos ficarem um do lado do outro, permite espaçar os elementos de forma mais intuitiva e sem ter que fazer cálculos. Além disso ele também permite alinhar os elementos verticalmente de forma fácil.

Pode ser um pouco mais complicado de usar tendo em vista que existem diversas propriedades que vem junto da especificação flexible box, todavia tudo isso foi feito para justamente melhorar nosso código.

## Aplicando o Flexbox
O flexbox pode ser aplicado na página simplesmente com o uso da propriedade ```display: flex``` **no elemento pai daqueles que desejamos posicionar**.

Essa ação vai criar uma caixa (daí o nome 'flexbox') com os elementos filhos dentro **lado a lado**.

### Propriedades Básicas
A partir daí, temos algumas propriedades que aplicam os estilos que desejamos aos elementos. As propriedades e respectivos atributos mais comuns são:

* **align-items:** permite alinhar os elementos no topo ('flex-start'), no meio ('center'), seguindo a linha do texto contido dentro de cada elemento ('baseline'), em baixo ('flex-end') ou 'stretch'.

* **justify-content:** dá um 'justificar' (igual no word) nos elementos e os seus atributos podem criar espaços em torno do elemento filho ('space-around'), criando uma espécie de 'margin' ou criar um espaço apenas _entre_ os elementos ('space-between').

Obs: é válido perceber que os atributos 'space' manipulam o espaço que eventualmente exista dentro da caixa criada pelo 'diplay flex', assim, se não houver espaço disponível nessa caixa, não faz sentido usar tais atributos ('space-around' e 'space-between').

Para criar um menu simples, bastante comum na internet, teríamos uma estrutura parecida com a representada abaixo, aplicando o ```display: flex```.

```html
<header class="cabecalho">
  <a class="logo" href="#">
    <img src="img/logo.png">
  </a>

  <ul class="menu">
    <li class="menu-item">Item 1 do menu</li>
    <li class="menu-item">Item 2 do menu</li>
    <li class="menu-item">Item 3 do menu</li>
    <li class="menu-item">Item 4 do menu</li>
  </ul>
</header>
```
Após a criação da estrutura no HTML, papssamos ao CSS:

```css
.cabecalho {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

Uma observação relevante é que o ```display: flex``` aplica aos elementos filhos a mesma altura (é válido sempre visualizar os elementos como caixinhas empilhadas, o flexbox as coloca lado a lado por padrão e as deixa com o mesmo tamanho).


### Direção do Flex
Já entendemos que com o ```display: flex;``` tem um comportamento de deixar as 'caixas' lado a lado por padrão. Contudo, é possível mudar isso quando necessário através da propriedade ```flex-direction```. Sendo assim, o padrão é que valor do flex-direction seja **row**.

Quando queremos mudar, utilizamos o valor **column**: ```flex-direction: column;``` Assim, os elementos ficarão um em baixo do outro.

Podemos utilizar o ```flex-wrap: wrap``` para quebrar esse fluxo vertical indicando que, quando o conjunto de elementos não couber no espaço vertical disponível pelo pai, deve-se quebrar para a próxima coluna. E isso também vale para quando os elementos estiverem em **row**, isto é, se a quantidade de elementos não couber na linha, quebra para a próxima.

Conseguimos utilizar um atalho para aplicar essas propriedades com o ```flex-flow```

```CSS
.menu {
   display: flex;
   flex-direction: column;
   flex-wrap: wrap;
}

/*ou*/

.menu {
   display: flex;
   /*economizando uma linha com o 'flex-flow'*/
   flex-flow: column wrap;
}
```

### Grid com Flexbox
É possível chegar a um comportamento de grid utilizando o ```display: flex```, para isso, precisamos fazer algumas continhas para aplicar o ```margin``` em conjunto com o seletor avançado **nth-child**.


### Responsivo
Para trabalhar a responsividade do layout com o flexbox é bastante simples, uma vez que está entendido o comportamento dos elementos com a propriedade ```flex: direction```.

Além de entender bem o uso dessa propriedade, é importante entender como utilizar os **media-queries**

Se temos um layout para telas grandes (acima de 768px) com um ```display: flex``` e a direction esteja ```row``` basta mudarmos para ```column``` dentro de uma media-query abaixo de 768px:

```
/*parte mobile*/
@media (max-width: 768px) {
   display: flex;
   flex-direction: column;   
}
```
Nesses casos também precisamos atentar para as definições de width, height e margin.


### Ordem dos Elementos
Com o flexbox podemos mudar a ordem dos elementos do HTML com a ajuda da propriedade ```order```

Isso é muito útil quando queremos fazer um layout específico para o mobile, mudando a ordem de um elemento específico.

Os elementos, por padrão, vem com um ```order``` de valor zero. Então, se quisermos alterar a ordem de um elemento, colocando-o antes dos demais, podemos fazer ```order: -1```


### Distribuindo o Espaço entre os Elementos Filhos
Com a propriedade ```flex-grow``` podemos pegar um espaço sobrando na 'caixa' criada pelo ```display: flex``` no pai e distribuir entre os elementos filhos.
