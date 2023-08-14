# Apostila para automação de testes com Cypress

##  Lista de Conteúdos

**CYPRESS**<br />
[GIT](./git.md)<br />

<details>
<summary>
SUMÁRIO
</summary>

&emsp;&emsp;[Asserções](#asserções-do-cypress)</br>
- &emsp;&emsp;[Com Expect](#asserções-com-expect)</br>
	- &emsp;&emsp;[Igualdades](#igualdades)</br>
	- &emsp;&emsp;[Comparações com objetos](#comparação-com-objetos)</br>
	- &emsp;&emsp;[Comparações com arrays](#comparação-com-arrays)</br>
	- &emsp;&emsp;[Comparação de tipos](#comparação-de-tipos)</br>
	- &emsp;&emsp;[Comparação de Strings](#comparação-de-strings)</br>
	- &emsp;&emsp;[Comparação de números](#comparação-de-números)</br>
- &emsp;&emsp;[Com Should](#asserções-com-o-should)</br>
	- &emsp;&emsp;[Comparação de textos](#comparações-de-textos)</br>
	- &emsp;&emsp;[Comparando valores e propriedades de campos](#comparando-valores-e-propriedades-de-campos)</br>
	- &emsp;&emsp;[Verificar se opções estão marcadas](#verificar-se-opções-estão-marcadas)</br>
	- &emsp;&emsp;[Verificação da exibição de elementos](#verificação-da-exibição-de-elementos)</br>
&emsp;&emsp;[Interações com elementos](#interação-com-elementos)</br>
&emsp;&emsp;[Debug](#debug)</br>
&emsp;&emsp;[Hooks](#hooks)</br>
&emsp;&emsp;[Comandos Customizáveis](#comandos-customizáveis)</br>
&emsp;&emsp;[Configurações do Cypress](#configurações-do-cypress)</br>
&emsp;&emsp;[Plugins](#plugins)</br>
</details>

---

[Documentação oficial](https://docs.cypress.io/) do Cypress.

## Asserções do Cypress

### Asserções com Expect

Há algumas formas de se fazer validações utilizando o Cypress, o Expect é uma delas.  Ele possui um parâmetro obrigatório que é o valor que está sendo comparado. O segundo parâmetro é opcional e pode ser passada uma string qualquer.
Notação: `expect(valorComparado, “mensagem qualquer”);`
Possui vários métodos de comparação, os principais estão listados abaixo.

#### Igualdades

- **equal** – Verifica se um valor é exatamente igual ao outro. 

  Exemplos:

```js
expect(1).equal(1);

expect(1).to.be.equal(1);

expect(2).not.to.be.equal(1);
```

- **true/false** – Verifica se um valor ou comparação é verdadeira ou falsa.

  Exemplos:

```js
expect(0 == 0).to.be.true;

expect(1 == 0).to.be.false;
```

- **null** – Verifica se um valor é nulo

  Exemplo:
```js
  expect(null).to.be.null;
```

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

- **select** – Seleciona uma ou mais opções de um elemento do tipo “Select”. Recebe uma string ou um array de strings com o value ou o texto do element.

	Exemplos:

	`cy.get(‘#comboCidades’).select(“Campinas”);`

	`cy.get(‘#animais’).select([“gato”, “cachorro”, “peixe”]);`

- **find** – Busca por um elemento “dentro” de outro elemento.

	Exemplos:

	`cy.get(‘#listaCidades’).find(“span”);`

	`cy.get(‘#animais’).find(“[value=gato]”);`

- **wait** – Pode ser passado um número para ser usado como tempo de espera em milissegundos, ou um “alias” de alguma requisição, para esperar a sua conclusão.

	Exemplos:

	`cy.wait(5000);`

	`cy.wait(‘@requestBuscaCidades’);`

- **then** – Trabalha com ações assíncronas, utilizado para realizar determinada ação após a conclusão de uma chamada assíncrona. Recebe uma função de callback

	Exemplos:

	`cy.title().then(title => console.log(title));`

		cy.get(“.success-alert”).invoke(“text”).then(msg => {
			expect(msg).to.have.text(“Cadastro realizado!”)
		});

	**Observação:** o comando should também pode ser utilizado em chamadas assíncronas, porém possui algumas diferenças, enquanto o then aguarda a conclusão da chamada, o should fica tentando realizar a ação mesmo sem a conclusão da chamada. Além disso, o should não permite realizar novas buscas dentro dele, já o then permite.

- **wrap** – Trasforma o item passado por parâmetro em um elemento manipulável pelo Cypress, possibilitando realizar validações com o should, trabalhar com promises e realizar outras manipulações do elemento.

	Exemplos:

	`const obj = { nome: “Tiago”, sobrenome: “Lopes” };`

	`cy.wrap(obj).should(“have.property”, “nome”, “Tiago”);`

		cy.get(“#login”).then($elemento => {
			cy.wrap($elemento).type(“tiagolopes”);
		})

	`cy.wrap(10).should(“be.eql”, 10);`

- **its** – Consegue navegar pelas propriedades de um objeto, capturando os valores de cada propriedade.

	Exemplos:

	`const obj = { nome: “Tiago”, membros: { pai: “Marcos” } };`

	`cy.wrap(obj).its(“nome”).should(“be.equal”, “Tiago”);`

	`cy.wrap(obj).its(“membros”).its(“pai”).should(“contain”, Marcos);`

	`cy.wrap(obj).its(“membros.pai”).should(“contain”, “Marcos”);`

- **invoke** – Consegue invocar métodos de objetos, passando parâmetros e manipulando o valor retornado.

	Exemplos:
	
		cy.get(“.success-alert”).invoke(“text”).then(text => {
			expect(text).to.be.equal(“Cadastro finalizado!”);
		})

	`cy.get(“#inputName”).invoke(“val”, “Tiago Lopes”);`

	`cy.get(“#resultado”).invoke(“html”, “<div>Teste!</div>”);`

- **on** – Consegue manipular eventos do navegador.

	Exemplos:

	`cy.on(“window:alert”, mensagem => {
		expect(“mensagem”).contain(“Erro ao tentar salvar”);
	})`

	`cy.on(“window:confirm”, mensagem => {
		console.log(mensagem);
	})`

- **stub** – Funciona como mock para simular serviços externos e elementos que o Cypress não consegue manipular. É possível criar um stub passando ou não parâmetros.

	Exemplos:

	`const stub = cy.stub();`

	`cy.on(“window:alert”, stub);`

		cy.window().then(window => {
			cy.stub(window, “prompt”).returns(“Valor qualquer”);
		})

- **window** – Captura o objeto window da página, tendo acesso aos seus métodos e atributos.

	Exemplos:
	
	`cy.window().then(window => {
		cy.stub(window, “open”);
	});`

	`cy.window().invoke(‘alert’, “Exibindo alerta”);`

- **as** – Possibilita dar um “alias” (apelido) a elementos para encurtar a chamada deles, por exemplo: rotas da API, elementos HTML com um Seletor muito grande e mocks.

	Exemplos:

```js
	cy.get(“#form input[type=name]”).as(“name”);

	cy.get(“@name”).type(“Tiago Lopes”);

	cy.window().then(window => {
		cy.stub(window, “open”).as(“winOpen”);
	});

	cy.get(“@winOpen”).should(“be.called”);

	cy.intercept(“GET”, “/users*”).as(“rotaUsuarios”);

	cy.wait(“@rotaUsuarios”);
```
	
- **fixture** - Carrega um arquivo de Fixtures para usar como massa de teste ou mock de retorno de chamadas de APIs, por padrão, o Cypress irá buscar o arquivo dentro da pasta fixtures.

	Exemplo:
	
```js
	cy.fixture('users').then(user => {
		cy.get('#name').type(user.name);
		cy.get('#age').type(user.age);
	})
```
		
- **each** - Quando o Cypress encontra vários elementos com o mesmo seletor, é possível iterá-los utilizando o método **each**.
	
	Exemplo:
	
```js
	cy.get('#checkboxFood').each($el => {
		if ($el.val() !== 'pizza') {
			cy.wrap($el).check();
		}
	})
```
		
- **clock** - Consegue alterar a data e hora do sistema, é possível passar uma data como parâmetro e o cypress irá alterar a data e hora do sistema para o valor passado por parêmetro.

	Exemplos:
	
	`cy.clock();`
	
		dt = new Date(2021, 09, 07, 15, 23, 10);
		cy.clock(dt);
		
- **tick** - Consegue avançar o tempo do sistema, recebe como parâmetro um número em milissegundos.

	Exemplo:
	
	`cy.tick(1500); // Avança um segundo e meio no tempo`

## Debug
- **debug** – Pausa a execução de teste naquele ponto que o debug foi adicionado e abre o navegador no modo de debug, exibindo informações no console do navegador.

	Exemplo:
	
	`cy.title().should(“contain”, “Início”).debug();`

- **pause** – Simplesmente pausa a execução dos testes no ponto em que o pause foi adicionado, no painel do Cypress irá aparecer dois botões, um para continuar a execução dos testes até a próxima pausa e outro para executar o próximo comando.

## Hooks
Os hooks são utilizados para se executar determinados blocos de código antes ou depois de cada teste, um exemplo mais comum de utilização é para efetuar o login do usuário, se o login for um pré-requisito para o teste, então antes de cada teste deve ser feito o login, portanto esse comando pode ser colocado dentro de um bloco “beforeEach”.

### Tipos de hooks

- **before** – Executa uma vez antes de todos os testes.

- **after** – Executa uma vez após todos os testes.

- **beforeEach** – Executa antes de cada teste, ou seja, se houver 8 testes, ele executará o bloco beforeEach 8 vezes, uma vez antes de cada teste.

- **afterEach** – Executa depois de cada teste, ou seja, se houver 8 testes, ele executará o bloco afterEach 8 vezes, uma após cada teste.

- **describe** – O bloco “describe” representa a suíte de testes, recebe uma string como parâmetro com a mensagem do que está sendo testado.

- **it** – O bloco “it” representa um teste, recebe uma string como parâmetro com a mensagem do que está sendo testado.

## Comandos Customizáveis
É possível adicionar comandos customizáveis no Cypress, ao adicionar o comando no arquivo Commands.js, ele se torna visível em todo o projeto de teste, é bem útil para evitar repetições de código.
	
Sintaxe:
```js
	Cypress.Commands.add('nomeDoComando', (parametros) => {
		// implementação do comando
	})
```

	
Exemplo:
```js
	Cypress.Commands.add('clickAlert', (locator, message) => {
		cy.get(locator).click()
		cy.on('window:alert', msg => {
		expect(msg).to.be.equal(message)
		})
	})
```
		
Para invocar esse comando, basta chamar por `cy.clickAlert()` em qualquer arquivo de teste.

## Configurações do Cypress
As configurações do Cypress podem ser feitas via linha de comando ou no arquivo cypress.json

- **SelectorPlayground** – Essa configuração em específica, pode ser feita no arquivo index.js dentro da pasta support e serve para fazer alterações no funcionamento do SelectorPlayground (Ferramenta que consegue gerar um seletor do elemento HTML selecionado). Uma das alterações que podem ser feita, é alterar a ordem de prioridade dos seletores que ele busca, conforme o exemplo abaixo:

	Exemplo:
```js
	Cypress.SelectorPlayground.defaults({
		selectorPriority: [
			‘id’,
			‘data-testid’,
			‘data-cy’
			‘class’,
			‘attributes’,
			‘tag’,
			‘nth-child’
		];
	});
```

- **defaultCommandTimeout** – Recebe um número. Valor em milissegundos da espera do Cypress pra encontrar algum elemento ou fazer uma asserção. O valor padrão é de 4000 milissegundos (4 segundos).

	Exemplo:
```js
	{
		“defaultCommandTimeout” : 6000
	}
```

## Plugins
O Cypress possui muitas opções de plugins para aumentar as suas funcionalidades.
- **Cypress Xpath** – Por padrão, o Cypress não aceita xpath nos seus comandos de busca, esse plugin traz o comando “xpath”, que possibilita que o Cypress localize elementos utilizando essa forma de busca.

	Documentação oficial do plugin [cypress-xpath](https://www.npmjs.com/package/cypress-xpath).

	Exemplos:
	
```js
	cy.xpath(“/html/body/div/h1”);
	
	cy.xpath(“//h1”);
	
	cy.xpath(“//input[contains(@onclick, ’Francisco’)]”);
	
	cy.xpath(“//input[@id=’name’]”).type(“Tiago Lopes”);
	
	cy.xpath(“//table//td[contains(., ‘Valor’)]”);
	
	cy.xpath(“//[contains(., “Tiago”)]/following-sibling::td”);
```
	
	[Site](https://www.red-gate.com/simple-talk/development/dotnet-development/xpath-css-dom-and-selenium-the-rosetta-stone/) com exemplos de xpath.
	
