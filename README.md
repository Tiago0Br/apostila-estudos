# Apostila de comandos do Cypress
[Documentação oficial](https://docs.cypress.io/) do Cypress.
## Asserções do Cypress
### Asserções com Expect
Há algumas formas de se fazer validações utilizando o Cypress, o Expect é uma delas.  Ele possui um parâmetro obrigatório que é o valor que está sendo comparado. O segundo parâmetro é opcional e pode ser passada uma string qualquer.
Notação: `expect(valorComparado, “mensagem qualquer”);`
Possui vários métodos de comparação, os principais estão listados abaixo.

#### Igualdades

- **equal** – Verifica se um valor é exatamente igual ao outro. 

  Exemplos:

  `expect(1).equal(1);`

  `expect(1).to.be.equal(1);`

  `expect(2).not.to.be.equal(1);`

- **true/false** – Verifica se um valor ou comparação é verdadeira ou falsa.

  Exemplos:

  `expect(0 == 0).to.be.true;`

  `expect(1 == 0).to.be.false;`

- **null** – Verifica se um valor é nulo

  Exemplo:

  `expect(null).to.be.null;`

- **undefined** – Verifica se um valor de uma variável não foi definido.

  Exemplo:

  `expect(undefined).to.be.undefined;`

#### Comparação com Objetos

- **deep.equal** – Verifica se o conteúdo do objeto é exatamente igual ao conteúdo de outro objeto.

  Exemplo:

  `expect({nome: “Tiago”}).to.be.deep.equal({nome: “Tiago”});`

- **eql** – Verifica se um item é igual a outro. Pode ser utilizado para realizar a mesma comparação do exemplo acima.
- **include** – Verifica se o objeto possui determinado valor.

  Exemplo:

  `expect({nome: “Tiago”, idade: 19}).to.include({idade: 19});`

- **have.property** – Verifica se esse objeto possui tal propriedade. Também é possível passar o conteúdo da propriedade verificada.

  Exemplos:

  `expect({nome: “Tiago”}).to.have.property(“nome”);`

  `expect({nome: “Tiago”}).to.have.property(“nome”, “Tiago”);`

- **empty** – Verifica se o objeto está ou não vazio.

  Exemplos:

  `expect({}).to.be.empty;`

  `expect({nome: “tiago”}).to.not.be.empty;`

#### Comparação com arrays

- **have.members** – Verifica se o array tem exatamente os mesmos elementos.

	Exemplo:
	
	`expect([“maçã”, “uva”]).to.have.members([“maçã”, “uva”]);`

- **include.members** – Verifica se o array possui os elementos passados.
	
	Exemplo:
	
	`expect([“maçã”, “uva”]).to.include.members([“uva”]);`

#### Comparação de tipos

 - **a/an** – Verifica o tipo daquela variável/conteúdo. O funcionamento do a e do an são é exatamente o mesmo, eles só diferem-se na semântica.

	Exemplos:
	
	`expect(5).to.be.a(“number”);`
  
	`expect([]).to.be.an(“array”);`
  
	`expect({}).to.be.an(“object”);`
  
	`expect(“”).to.be.a(“string”);`

#### Comparação de Strings

-	**have.length** – Verifica se a string possui determinado tamanho.

	Exemplo:
	
	`expect(“oi”).to.have.length(2);`

- **contains** – Verifica se a string contém uma outra string dentro dela.

	Exemplo:
	
	`expect(“Salvo com sucesso!”).to.contains(“sucesso”);`

- **match** – Para comparações mais complexas utilizando Regex, é utilizado o método “match”.

	Exemplos:
	
	`expect(“Salvo com sucesso!”).to.match(/sucesso/);`
  
	`expect(“Salvo com sucesso!”).to.match(/^Salvo/);`
  
	`expect(“Salvo com sucesso!”).to.match(/sucesso!$/);`
  
	`expect(“Salvo com sucesso!”).to.match(/*com/);`
  
#### Comparação de números

- **above** – Verifica se um número é maior do que outro.

	Exemplo:
	
	`expect(5).to.be.above(4);`

- **below** – Verifica se um número é menor do que outro.

	Exemplo:

	`expect(5).to.be.below(6);`

- **closeTo** – Verifica se um número com casas decimais possui um valor próximo de outro número.

	Exemplo:

	`expect(3.141592).to.be.closeTo(3.1, 0.1);`

### Asserções com o should
Também é possível realizar asserções com o should, funciona basicamente da mesma forma, apenas possui uma sintaxe diferente, também possui os métodos de comparação do expect. O primeiro parâmetro do should é a string contendo a forma de comparação. Dependendo da comparação pode ou não receber mais parâmetros.

Notação: `cy.get(“elemento”).should(“comparação”, resultadoEsperado);`

#### Comparações de textos

- **contain** – Verifica se o elemento contém um texto ou outros elementos HTML dentro dele.

	Exemplo:
	
	`cy.get(“.alert-success”).should(“contain”,”cadastro realizado”);`

- **have.text** – Verifica se o elemento possui o texto exato.

	Exemplo:
	
	`cy.get(“.error”).should(“have.text”,”Data inválida!”);`

- **have.not.text** – Verifica se o elemento NÃO possui determinado texto.

	Exemplo:

	`cy.get(“.success”).should(“have.not.text”,”Data inválida!”);`

- **include.text** – Verifica se o elemento contém esse texto, mas não precisa ser exato.

	Exemplo:

	`cy.get(“.alert”).should(“include.text”,”sucesso!”);`
  
#### Comparando valores e propriedades de campos

- **have.value** – Verifica se o elemento possui determinado valor no atributo “value”.

	Exemplo:

	`cy.get(“input#name”).should(“have.value”,”Tiago Lopes”);`

#### Verificar se opções estão marcadas

- **be.checked** – Verifica se o radio button ou checkbox está marcado.

	Exemplo:

	`cy.get(“#formOpcao”).should(“be.checked”);`

- **not.be.checked** – Verifica se a opção não está marcada.

	Exemplo:

	`cy.get(“#formOpcao”).should(“not.be.checked”);`

#### Verificação da exibição de elementos

- **exist** – Verifica se um elemento existe na página.

	Exemplo:

	`cy.get(“.error”).should(“exist”);`

- **not.exist** – Verifica se um elemento não existe na página.

	Exemplo:

	`cy.get(“.error”).should(“not.exist”);`

	**Observação:** A asserção “not.exist” retorna nulo, então não dá pra encadear uma nova asserção depois desse comando.
  
## Interação com elementos
- **visit** – Visita uma página da web. Caso esteja configurado com uma baseUrl, pode passar o caminho relativo da página.

	Exemplos:

	`cy.visit(“https://www.google.com/”);`

	`cy.visit(“/login”);`

- **title** – Captura o título da página.

	Exemplo:
	
	`cy.title();`

- **get** – Captura elementos da página, recebe como parâmetro o seletor CSS desse elemento.

	Exemplos:

	`cy.get(“#password”);`
	
	`cy.get(“.container”);`
	
	`cy.get(“div”);`
	
	`cy.get(“input[name=’email’]”);`
	
	`cy.get(“div h1 > a”);`

	[Jogo](https://flukeout.github.io/) para praticar seletores CSS.
	
	[Documentação](https://www.w3schools.com/jquery/jquery_ref_selectors.asp) da W3Schools de seletores do Jquery.
  
  **Parâmetro** `timeout`:
	Recebe um número, é o tempo em milissegundos que o Cypress espera caso não encontre o elemento. Esse parâmetro é útil nos casos em que o elemento demora a ser exibido na página. O timeout padrão do Cypress é de 4 segundos.
	
	Exemplos:
	
	`cy.get(“.success-alert”, { timeout: 10000 });`
  
- **contains** – Captura elementos da página com base no seletor CSS ou no texto que esse elemento possui.

  Exemplo:

  `cy.contains(“Salvar”);`

  `cy.contains(“button”, “Salvar”);`

- **click** – Clica em elementos, como links ou botões.

  Exemplo:

  `cy.get(“button”).click();`

  `cy.get(“a[href=’/salvar’]”).click();`

	**Parâmetro** `multiple`:
	Se houver mais de um elemento com o mesmo seletor, ele clica em ambos os elementos. Recebe um valor booleando (true/false) , caso não seja passado o padrão é “false”.
	
	Exemplo:
	
	`cy.get(“button”).click({ multiple: true });`

- **reload** – Recarrega a página.

	Exemplo:

	`cy.reload();`

- **type** – Preenche um campo com o conteúdo que for passado como parâmetro.

	Exemplos:

	`cy.get(‘#user’).type(“admin”);`
	
	`cy.get(‘#password’).type(“senha123”);`

	É possível simular algumas teclas passando o nome da tecla entre chaves.
	
	Exemplos:
	
	`cy.get(‘#password’).type(“admin{enter}”);`
	
	`cy.get(‘#name’).type(“Tiagoo{backspace}”);`
	
	`cy.get(‘#user).type(“{selectall}admin”);`

	**Parâmetro** `delay`:
	Recebe um número, digita o conteúdo mais lentamente conforme o número passado pelo usuário em milissegundos.
	
	Exemplo:
	
	`cy.get(‘#name’).type(“Tiago”, { delay: 100 });`

- **clear** – Apaga o conteúdo que foi preenchido em um input.

	Exemplo:
	
	`cy.get(‘#name’).clear().type(“novo nome”);`
