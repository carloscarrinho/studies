# Curso de Sass e Compass - Descomplicando o CSS
## Plataforma Alura
### Introdução
As páginas web possuem uma estrutura padrão com a utilização de HTML, CSS e JavaScript.

- O HTML é responsável pela estruturação da página, com a criação dos elementos, botões, formulários, entre outros recursos;

- O CSS é aquele que responde pelo estilo, criando o layout, aplicando as cores, os efeitos _visuais_, o posicionamento dos elementos criados no HTML, efeitos de animação simples, responsividade para varios tamanhos de tela, entre outras coisas;

- O JavaScript é aquele que dá vida à página, criando as relações entre os elementos, os eventos de interação com o usuário, as validações de informações e muitas outras coisas.

Diante desses propósitos, especialmente o CSS e o JavaScript tendem a ser dinâmicos, isto é, podem ter a necessidade de mudar ao longo do tempo, por inserção/remoção de funcionalidades, mudança de layout, etc.

No JavaScript, quando o código foi feito de forma inteligente utilizando boas práticas, não é tão trabalhoso fazer modificações. Porém no CSS, mesmo que o código tenha sido bem estruturado, muitas vezes o código precisa ser alterado em vários pontos, gerando um certo retrabalho e necessidade de extrema atenção por parte do programador que está dando manutenção.

Para isso, foram criados alguns **Frameworks**, que são ferramentas de otimização do trabalho, para facilitar a criação e manutenção de códigos robustos.

O Sass é um pré-processador para trabalhar com o CSS que permite a criação de variáveis e [...] para facilitar e agilizar o trabalho.

### utilizando o Sass
Os arquivos criados em Sass utilizam a extensão .scss e precisam ser **compilados** para gerar o arquivo .css que vai ser aplicado na página. Isso porque atualmente o único tipo de arquivo entendido pelos browsers como folha de etilos é o ```.css```.

Assim, a primeira coisa que devemos fazer é pedir para que ele compile o arquivo "estilos.scss" por meio do **terminal**. O primeiro passo é entrar na pasta do projeto (em que está o arquivo a ser compilado), depois compilamos o arquivo **.scss** para criar um **.css**. Podemos fazer isso de duas formas:

```console
sass estilos.scss:estilos.css
```
ou

```console
sass input.scss output.css
```

Contudo, como quando iremos trabalhar com o Sass vamos fazendo as modificações aos poucos, podemos lançar mão de um comando que permite que o terminal fique 'assistindo' as modificações no arquivo .scss e, automaticamente, compile para o arquivo .css.

```console
sass --watch input.scss output.css
```

ou ainda

```console
sass --watch estilos.scss:estilos.css
```

Neste último caso, é muito importante atentar para o nome dos arquivos, que devem estar iguais aos que estão na pasta do projeto.

Com isso, ao compilarmos, o Sass passa todas as informações de um arquivo para o outro automaticamente. Então poderemos escrever com facilidade no **.scss** que o Sass faz sozinho o trabalho passar para o **.css**.

### Comentários no Sass
Os comentários no Sass possuem a mesma sintaxe do JavaScript, utilizamos duas barras ( // ) para comentar o código **sem que ele apareça no aquivo .css**.

### Criando Variáveis
A criação de variáveis no Sass segue uma lógica similar às linguagens de programação. Este recurso ajuda na simplificação e manutenção do código.

Para criar uma variável precisamos fazer uso do sinal de ```$```. Assim, se queremos criar uma variável que armazena uma cor que será utilizada em diversos elementos da página podemos fazer:

```CSS
/*armazenando a cor 'lightgray' na variável 'cor-padrao'*/
$cor-padrao: lightgray;

p {
   border: 1px solid $cor-padrao;
}

button {
   background-color: $cor-padrao;
}
```
Nessa criação, é importante atentar ao **escopo** da variável, isto é, se a variável for criada dentro de um determinado bloco correspondente a um elemento específico, ela não poderá ser reutilizada em outros pontos do código:

```CSS
p {
   $borda: #ccc;
   border: 1px solid $borda;
}

h1 {
   border: 3px solid $borda;
}
```
Neste caso o código retornará erro, pois a '$borda' está especificado apenas dentro do seletor da tag **p**, ou seja, a variável só existe no escopo de **p**.

Desse modo, para que a variável se aplique a toda a folha de estilos, precisamos criá-la fora de qualquer seletor.

```CSS
/*criando a variável com escopo global*/
$borda: #ccc;

p {
   border: 1px solid $borda;
}

h1 {
   border: 3px solid $borda;
}
```

### Criando 'Mixin'
A criação de variáveis é muito útil, porém pode ser necessário que criemos não só uma propriedade que se repete, mas todo um bloco de propriedades. Para isso existem os **mixins**.

Criar um **Mixin** é similar à criação de uma variável, porém, ao invés de usarmos um '$', utilizaremos um **'@mixin'**, o nome que queremos atribuir e indicaremos suas propriedades e atributos entre colchetes, como normalmente é feito no CSS.

```
$raio: 0.3em;

@mixin borda-arredondada {
   -webkit-border-radius: $raio;
   -moz-border-radius: $raio;
   -o-border-radius: $raio;
   -ms-border-radius: $raio;
   border-radius: $raio;
}
```
Após a criação do Mixin, para aplicá-lo ao código, precisamos utilizar o comando **@include** mais o nome atribuído ao mixin, no local onde desejamos inserir o bloco de propriedades armazenado.

```
$cor-padrao: #lightgray;
$raio: 0.3em;

@mixin borda-arredondada {
   -webkit-border-radius: $raio;
   -moz-border-radius: $raio;
   -o-border-radius: $raio;
   -ms-border-radius: $raio;
   border-radius: $raio;
}

button {
   background-color: $cor-padrao
   /* inserindo o Mixin */
   @include borda-arredondada;
}
```
Após criado e inserido o **Mixin**, a medida que cresce nosso código e ele fica mais complexo, pode acontecer de essa padronização gerada pelo mixin precisar ser quebrada em algum elemento específico.

Por exemplo: definimos um valor de ```0.3em``` para a borda dos botões da página, porém, depois de um tempo chega uma orientação do designer de que apenas o botão da seção 'destaques' da página deveria ter um valor de ```.5em```.

Isso nos gera a necessidade de inserir uma _exceção_ apenas para o botão do 'destaques'.

Assim, na criação do **Mixin**, podemos definir um valor padrão (parâmetro) para todos os botões e no momento de chamar o ```@include``` apenas no botão 'destaques' passaremos a exceção.

Para criar o valor padrão inserimos um parênteses com a variável e seu valor padrão. Depois no 'include' passamos a exceção, também entre parênteses.

```
$cor-padrao: lightgray;

/*passando o parâmetro padrão '.3em' para a variável '$raio'*/
@mixin borda-arredondada($raio: .3em) {
   -webkit-border-radius: $raio;
   border-radius: $raio;   
}

/*parâmetro exceção de '.5em' apenas para o botão na seção 'destaques'*/
.destaques button {
   @include borda-arredondada(.5em);
}

/*valor padrão para os demais botões da página */
button {
   @include borda-arredondada;
}
```
### Aninhamento
Um recurso muito comum nas linguagens de programação é o chamado 'aninhamento', que consiste ir fazendo um encadeamento de blocos de código dentro de outros, isto é, como no HTML que coloca-se uma tag filha dentro de outra tag pai.

Entretando, infelizmente esse recurso não existe por padrão no CSS.

Assim o Sass nos ajuda nessa questão, permitindo que façamos encadeamento de seletores para facilitar a manutenção do código. Isso porque, realizando o aninhamento, quando for necessário modificar o elemento pai, não precisaremos ir modificando todos os elementos filhos, o Sass já faz essas modificações automaticamente.

```css
.social {
   bottom: 0;
   right: 0;

   li {
      float: left;

      a {
         display: block;
         width: 55px;
         height: 55px;
         margin-left: 1em;
      }
   }   
}
```
No exemplo de código CSS acima, criado no Sass, indica que selecionamos o elemento com a class 'social' colocamos algumas propriedades, depois selecionamos os 'li' dentro deste mesmo elemento, aplicamos um 'float: left' e selecionamos ainda os 'a' dentro das 'li' e aplicamos mais outras propriedades.

Este mesmo bloco de código no CSS seria apresentado da seguinte forma:

```css
.social {
   bottom: 0;
   right: 0;  
}
.social li {
   float: left;
}
.social li a {
   display: block;
   width: 55px;
   height: 55px;
   margin-left: 1em;
}
```
O que gera redundância e torna a manutenção mais custosa.

Uma observação importante na aplicação do aninhamento é que, para aninhar **pseudo classes** como ```a:hover``` precisamos fazer uso do **&**:

```CSS
.social {
   bottom: 0;
   right: 0;

   li {
      float: left;

      a {
         display: block;
         width: 55px;
         height: 55px;
         margin-left: 1em;

         &:hover {
            color: $cor-padrao;
         }         
      }      
   }
}
```
Contudo, é importante tomar cuidado com o aninhamento, observando sempre as boas práticas de uso, visto que um encadeamento longo de seletores pode gerar um CSS bastante confuso no final.

Como boa prática de CSS, não devemos ultrapassar três ou quatro itens no seletor, algo como ```.menu ul li a span``` não é performático.

### Modularizando com o Sass
Uma boa prática em qualquer linguagem de programação 'modularizar' o código, isto é, criar arquivos separados para cada funcionalidade, componente ou 'tema' presente no software.

O Sass permite essa modularização de forma bem fácil através do comando '@import'.

Assim, se nosso site possui um **index**, um **serviços** e um **contato**, uma organização possível é dividir em três arquivos com estes mesmos nomes, mais um **geral** que contém os códigos comuns a todas as páginas e importá-los num arquivo principal **estilos.scss**:

```
//depois de criar cada arquivo 'nomedoarquivo.scss', importamo-os no arquivo 'estilos.scss'
@import 'geral';
@import 'index';
@import 'servicos';
@import 'contato';
//não é necessário indicar a extensão do arquivo
```
Assim, cada modificação feita nos arquivos separados é importada pelo 'estilos.scss' que por sua vez compila para o 'estilos.css'.

Quando queremos organizar ainda mais, separando os arquivos em pastas diferentes, basta indicar o caminho como é comum no HTML com uma barra (/) para separar cada nível de pasta.

Assim, se, por exemplo, nossos arquivos estivessem dentro de uma pasta chamada 'paginas', precisaríamos passar para o 'estilos.scss':

```
@import 'geral'

//arquivos dentro da pasta 'páginas'
@import 'paginas/index'
@import 'paginas/servicos'
@import 'paginas/contato'
```
