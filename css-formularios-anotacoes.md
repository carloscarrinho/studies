# Formulários e Tabelas
## Plataforma Alura
### Funcionamento de Formulários
Os formulários são recursos imprescindíveis para qualquer tipo de aplicação. Fazemos uso deste tipo de funcionalidade quando:

1. Queremos capturar dados informados pelo usuário;
2. Queremos enviar dados para um servidor;
3. Queremos enviar dados para outra página.

### Estrutura Básica de um Formulário
Para criar a estrutura básica de um formulário no documento HTML fazemos uso das seguintes tags:

- <form></form>
- <label></label>
- <input>

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
Se passarmos algum texto dentro da tag textarea ao carregar a página o campo de mensagem estará preenchido com este texto e o usuário poderá apagá-lo para começar a escrever. É interessante para auxiliá-lo no preenchimento do campo, porém o mais indicado é ...

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



Perceba que, ao definir no CSS que o display do input será **block** os radio buttons também se comportam como blocks, afinal eles estão na tag input. Diante disso, é válido fazer essa separação no CSS utilizando classes.
