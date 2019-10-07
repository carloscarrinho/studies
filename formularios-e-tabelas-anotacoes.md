# Formulários e Tabelas
## Plataforma Alura
### Funcionamento de Formulários
Os formulários são recursos imprescindíveis para qualquer tipo de aplicação. Fazemos uso deste tipo de funcionalidade quando:

1. Queremos capturar dados informados pelo usuário;
2. Queremos enviar dados para um servidor;
3. Queremos enviar dados para outra página.

### Estrutura Básica de um Formulário
Para criar a estrutura básica de um formulário no documento HTML fazemos uso das seguintes tags:

- **form**
- **label**
- **input**

As tags **label** e **input** sempre andam juntas, isto é, você possui uma entrada de dados e uma etiqueta para ela.

Então é preciso, não só criar tais tags, mas também definir um tipo e um atributo identificador (id) para o **input** e depois atribuir este determinado campo de entrada a sua **label** correspondente através do atributo **for**.


```html
<form>
   <label for="nome">Nome</label>
   <input type="text" id="nome">
</form>
```
Mas também é possível criar a tag **input** dentro da tag **label**, assim não precisamos utilizar o atributo **for**.

```html
<form>
   <label>Nome
      <input type="text" id="nome">
   </label>

</form>
```
Após a criação de um formulário, sempre será necessário criar um botão de envio, existem várias formas de fazer, porém a mais básica é através do atributo **type="submit"** dentro de uma outra tag input.

Para definir o texto do botão, devemos inserir um outro atributo chamado **value** dentro da tag input. Caso não coloquemos este atributo, o navegador irá preencher o botão com o texto 'enviar' no idioma utilizado pelo usuário ('submit', em inglês por exemplo).

```html
<form>
   <label for="">Nome</label>
   <input type="text" id="nome">
   <!-- criação de um botão para envio dos dados capturados no formulário -->
   <input type="submit" value="Enviar dados">
</form>
```

### Estilo do Formulário
Todo formulário, por padrão, possui a propriedade **display** com valor **inline**, isto é, os campos criados primeiramente terão um comportamento lado a lado na página.

Desse modo, para criar um layout comum da internet, onde os campos ficam um abaixo do outro, devemos utilizar o CSS com a propriedade display com valor **block**.

```css
form label {
   display: block;
}
form input {
   display: block;
}
```
Para continuar com a estilização do formulário deve-se fazer uso das propriedades **width**, **margin**, **padding**, **font-size**, entre outras que permitem dar a cara que se deseja ao formulário.

### Tipos de Dados
Nossos formulários costumam ter vários tipos de dados e o html permite configurar nossos campos para receber cada um desses tipos.

#### Área de Texto
Para capturar um volume maior de texto, ao invés da tag input deve-se utilizar a tag **textarea**. Nela precisamos indicar sua largura através do atributo **cols** (colunas) e sua altura através do atributo **rows** (linhas).

```html
<label for="msg">Mensagem</label>
<textarea id="msg" rows="8" cols="80"></textarea>
```
Se passarmos algum texto dentro da tag ```textarea``` ao carregar a página o campo de mensagem estará preenchido com este texto e o usuário poderá apagá-lo para começar a escrever. É interessante para auxiliá-lo no preenchimento do campo, porém o mais indicado é utilizar o atributo **placeholder**:

```html
<label for="msg" placeholder="Escreva sua mensagem aqui">Mensagem</label>
<textarea id="msg" rows="8" cols="80"></textarea>
```
Com essa ação o texto 'Escreva sua mensagem aqui' aparecerá preenchendo o campo texto, porém quando o usuário ativar o campo ele some automaticamente, sem a necessidade do usuário apagar o texto.

#### Radio Buttons
Em alguns casos precisamos dar opções para o usuário marcar, sendo que só pode ser marcada/escolhida uma opção, para isso fazemos uso do type **radio**.

```html
<!-- digamos que queremos dar oções para o usuário escolher como deseja ser contatado  -->
<label for="radio-email">E-mail</label>
<input id="radio-email" type="radio" value="e-mail">

<label for="radio-telefone">Telefone</label>
<input id="radio-telefone" type="radio" value="Telefone">

<label for="radio-whatsapp">WhatsApp</label>
<input id="radio-whatsapp" type="radio" value="WhatsApp">
```
É válido observar o comportamento do atributo **value** neste caso. Ele funciona como um valor pre-definido para a opção, isto é, caso o usuário marque esta opção o valor retornado será 'e-mail'. Assim, quando formos manipular esses dados através do JavaScript poderemos utilizar esta informação.

Para visualizar melhor essa questão, seria como se tivéssemos criado um campo de entrada 'text' com uma pergunta aberta 'Como você prefere ser contatado?' e o usuário respondesse 'e-mail'.

Porém, como sabemos que é melhor ter dados padronizados, o type radio nos ajuda nessa questão.

Contudo, somente definir os radio buttons não é suficiente, pois assim o usuário conseguiria marcar todos eles, tirando o sentido desse recurso.

Portanto, temos que passar um outro atributo chamado **name** para criar uma espécie de grupo, fazendo com que o usuário só possa escolher uma das opções apresentadas.

```html
<label for="radio-email">E-mail</label>
<input id="radio-email" type="radio" value="e-mail"  name="contato">

<label for="radio-telefone">Telefone</label>
<input id="radio-telefone" type="radio" value="Telefone" name="contato">

<label for="radio-whatsapp">WhatsApp</label>
<input id="radio-whatsapp" type="radio" value="WhatsApp" name="contato">
```

Um recurso simples e bastante utilizado nos radio buttons é ter, por padrão, uma das opções marcadas. Para isso, basta adicionar o atributo **checked** na opção que se deseja apresentar marcada de início.

```html
<label for="radio-email">E-mail</label>
<input id="radio-email" type="radio" value="e-mail"  name="contato" checked>

<label for="radio-telefone">Telefone</label>
<input id="radio-telefone" type="radio" value="Telefone" name="contato">

<label for="radio-whatsapp">WhatsApp</label>
<input id="radio-whatsapp" type="radio" value="WhatsApp" name="contato">
```
No exemplo acima, o radio butto com valor **email** foi indicado como opção padrão.

Obs: o atributo **checked** também funciona com outros types, como o checkbox e o menu supenso, explicados a seguir.

#### Checkbox
Os radio buttons, quando configurados corretamente, apenas permitem a escolha de uma opção da lista. Porém, muitas vezes queremos permitir que o usuário marque mais de duas ou mais opções.

Para isso utilizamos o type **checkbox**:

```html
<p>Quais tipos de conteúdos você deseja receber por e-mail?</p>

<label><input type="checkbox">Economia</label>
<label><input type="checkbox">Games</label>
<label><input type="checkbox">Música</label>
<label><input type="checkbox">Séries e Filmes</label>
```

#### Menu Suspenso
Para criar um outro tipo de entrada de dados por meio de um menu suspenso, não fazemos uso da tag ```input``` mas sim da tag ```select```. Dentro dela, colocamos cada opção do menu dentro de tags ```option```:

```html
<p>Qual horário você prefere ser contatado?</p>
<select>
   <option value="manha">Manhã</option>
   <option value="tarde">Tarde</option>
   <option value="noite">noite</option>
</select>
```

### Responsividade e Padronização do Formulário
Os usuários mobile podem ser ajudados a partir de uma melhor utilização dos tipos de input dentro do HTML com recursos trazidos pelo HTML5. Para visualizar exemplos de aplicação de tais atributos existe um site bacana chamado: **mobileinputtypes.com**. Nele podemos entender melhor qual o comportamento do formulário na tela de celulares a partir dos tipos que inserimos no documento.

Os **type** utilizados com a tag **input** mais usados são:
- text - insersão de um texto curto;
- email - insersão de um e-mail;
- tel - insersão de telefone;
- number - insersão de um número (como cpf, cep, nº de casa, etc.);
- date - insersão de uma data;
- datetime - insersão de data e hora;
- month - insersão do mês;
- search - insersão de um campo de busca;

Com a utilização desses atributos o comportamento da tela e teclado do usuário muda, facilitando a sua insersão dos dados, facilitando a sua padronização e validação.

No caso da validação, utilizar o input type do tipo **email**, por exemplo, faz com que o navegador não permita que o usuário digite qualquer valor no campo. Assim, ele precisa enviar um e-mail válido no campo.

### Campos Obrigatórios
É muito comum nos formulários que tenhamos campos de preenchimento obrigatório. Para fazer isso é simples, basta utilizar o atributo **required** dentro dos inputs que se deseja tornar obrigatórios.

```html
//tornando os campos 'nome' e 'email' obrigatórios enquanto o 'telefone' não
<input type="text" id="nome" class="input-padrao" required>

<label for="email">E-mail</label>
<input type="email" id="email" class="input-padrao" required>

<label for="telefone">Telefone</label>
<input type="tel" id="telefone" class="input-padrao">
```

### Semântica
Um aspecto muito importante dentro do HTML é utilizar corretamente as tags. É possível chegar a um determinado aspecto visual que queremos de várias formas utilizando a dupla HTML e CSS, mas quanto mais semântico for o documento, mais fácil será construí-lo e suportá-lo.

Para isso, na elaboração de um formulário, para organizar os códigos dos seus campos, ao invés de utilizar ```div``` e ```p``` para agrupar e dar nome a campos com um mesmo 'tema', é recomendável utilizar a tag **fieldset** (no lugar da div) em conjunto com a **legend** (no lugar do p).

```html
<!-- agrupando os radio buttons para definir a forma de contato  -->
<fieldset class="radio-buttons">
   <!-- legenda do conjunto de campos -->
   <legend>Como prefere o nosso contato?</legend>
   <label for="radio-email">
      <input type="radio" value="e-mail" id="radio-email" name="contato">
      E-mail
   </label>
   <label for="radio-telefone">
      <input type="radio" value="Telefone" id="radio-telefone" name="contato">
      Telefone
   </label>
   <label for="radio-whatsapp">
      <input type="radio" value="WhatsApp" id="radio-whatsapp" name="contato">
      WhatsApp
   </label>
</fieldset>
```
### Estilizando o botão
Com CSS3 é possível deixar os elementos do formulário com os mais variados designs. O botão é um dos principais elementos com o papel de dar 'a cara do formulário'. Utilizando bibliotecas como o Bootstrap e o Materialize é possível chegar a um resultado bastante satisfatório de forma bem rápida, porém, caso não se deseje utilizar essas ferramentas, vale a pena destacar três propriedades e um recurso do CSS que permitem dar uma estilizada bacana no botão, são elas:

**Propriedades:**
- cursor;
- transition;
- transform;

**Recurso:**
- hover;

```css
/* digamos que atribuímos uma class 'botao-enviar' para o botão do formulário */
.botao-enviar {
   width: 40%;
	padding: 10px 0;
	font-weight: bold;
	font-size: 18px;
	border: none;
	border-radius: 2px;
	background: orange;
	color: white;
   /* aqui estamos mudando o cursor do mouse para aparecer a maozinha ao invés da seta */
	cursor: pointer;
   /* neste transition fazemos com que a cor de fundo mude durante 1 seg*/
	transition: 1s background;
}
/* aqui estabelecemos que a animação ocorre quando passamos o mouse em cima do botão */
.botao-enviar:hover {
	background: darkorange;
   /* aqui definimos que ao passar o mouse por cima o botão crescerá em 20% */
   transform: scale(1.2);
}
```
Vale a pena dar uma olhada nos valores possíveis para a propriedade **transform**.

### Tabelas
Para criar tabelas é preciso, apesar de trivial, ter em mente que ela é feita de **linhas** e **colunas**. Posto isso, para criar a tabela utilizamos a tag ```table```, as linhas a tag ```tr``` 't row' e as células (que ditam a quantidade de colunas) a tag ```td```.

Assim, a estrutura mais básica de uma tabela consiste em:

```html
<table>
   <tr>
      <td></td>
      <td></td>
   </tr>
</table>
```
Contudo, normalmente precisamos fazer algo mais complexo, com cabeçalho, mais linhas e colunas e, eventualmente, até uma linha de 'total' ao final da tabela.

Diante disso, precisamos ser, mais uma vez, semânticos e dividir a tabela em 'cabeça', 'corpo' e 'pé', assim como é feito na página HTML. Esses blocos são representados por ```thead```, ```tbody``` e ```tfoot```.

Nosso código ficaria:

```html
<table>
   <thead>
      <tr>
         <!-- perceba que ao invés de 'td' usamos 'th' para as células do cabeçalho -->
         <th></th>
         <th></th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td></td>
         <td></td>
      </tr>
   </tbody>
   <tfoot>
      <tr>
         <!-- perceba que para as células do foot usamos 'tf' e não 'td' -->
         <tf></tf>
         <tf></tf>
      </tr>
   </tfoot>
</table>
```
As tabelas também nos oferecem a possibilidade de mesclar células. Esse efeito é conseguido através da propriedade **colspan = X**, onde X é o número de células que você quer agrupar.

Portanto, em uma tabela de 5 colunas, para ter uma célula única na linha, usamos um código assim:

```html
<table>
   <thead>
      <tr>
         <th colspan="3">Rio de Janeiro</th>
      </tr>
      <tr>
         <th>Dia</th>
         <th>Horário</th>
         <th>Barbeiro</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>Seg</td>
         <td>8h ~ 20h</td>
         <td>Glaucio</td>
      </tr>
      <tr>
         <td>Qua</td>
         <td>8h ~ 20h</td>
         <td>Glaucio</td>
      </tr>
      <tr>
         <td>Sex</td>
         <td>8h ~20h</td>
         <td>Glaucio</td>
      </tr>
   </tbody>
</table>
```

Por hoje é só!
