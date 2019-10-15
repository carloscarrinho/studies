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

Assim, a primeira coisa que devemos fazer é pedir para que ele compile o arquivo "estilos.scss" por meio do **terminal**. O primeiro passo é entrar na pasta do projeto (em que está o arquivo a ser compilado), depois compilamos o arquivo **.scss** para criar um **.css**, através do comando:

```console
sass estilos.scss:estilos.css
```
É muito importante atentar para o nome dos arquivos, que devem estar iguais aos que estão na pasta do projeto.

Com isso, ao compilarmos, o Sass passa todas as informações de um arquivo para o outro automaticamente. Então poderemos escrever com facilidade no **.scss** que o Sass faz sozinho o trabalho passar para o **.css**.

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

```css
$raio: 0.3em;

@mixin borda-arredondada {
   -webkit-border-radius: $raio;
   -moz-border-radius: $raio;
   -o-border-radius: $raio;
   -ms-border-radius: $raio;
   border-radius: $raio;
}
@```
