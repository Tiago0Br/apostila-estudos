## Pilares para a entrega de software com qualidade:

1. **Só iniciar a implementação depois que tiver certeza do que deverá ser feito:** Conversar com o PO ou responsável pela tarefa explicando para ele o que você entendeu que deve ser feito. Caso algo esteja errado, a pessoa irá te corrigir e o processo se repete até que o entendimento da tarefa seja de 100%.

Planejar entrada do programa:
![[Pasted image 20240310223228.png]]

Planejar processamento dos dados:
![[Pasted image 20240310223343.png]]

Planejar saída do programa:
![[Pasted image 20240310223426.png]]

2. **Fazer um setup mínimo do projeto:**

Configurações básicas para um ambiente de testes com NodeJS:
```json
{
	"name": "testes-automatizados",
	"version": "1.0.0",
	"description": "",
	"main": "index.js",
	"type": "module",
		"scripts": {
		"dev": "node --watch src/service.js",
		"test": "node --test test/",
		"test:coverage": "node --test --experimental-test-coverage test/",
		"test:debug": "node --inspect --test --watch test/"
	},
	"keywords": [],
	"author": "",
	"license": "ISC"
}
```

Configuração do editor de código para modo de debug (depuração):
```json
{
	"version": "0.2.0",
	"configurations": [
		{
			"name": "Run test debugger",
			"request": "launch",
			"runtimeArgs": [
				"run",
				"test:debug"
			],
			"runtimeExecutable": "npm",
			"skipFiles": [
				"<node_internals>/**"
			],
			"type": "node",
			"console": "integratedTerminal"
		}
	],
	"compounds": []
}
```

3. **Tudo que for entregue deve ser validado com testes automatizados:**

Exemplo de implementação de funcionalidade:
```js
import './types.js'
/**
* @param {IncomingUser} user
* @returns {OutcomingUser}
*/
function parseUser(user) {
	return {
		name: user.name.toUpperCase(),
		email: user.email
	}
}

export { parseUser }
```

Exemplo de teste que valida essa funcionalidade:
```js
import { describe, it } from 'node:test'
import { parseUser } from '../src/service.js'
import assert from 'node:assert'
import '../src/types.js'

describe('Service', () => {
    it('Should parse user', () => {
        /** @type {IncomingUser} */
        const user = {
            name: 'Tiago Lopes',
            email: 'tiagoltavares2002@gmail.com',
            password: 'senha123'
        }

        const result = parseUser(user)
        assert.deepStrictEqual(result, {
            name: user.name.toUpperCase(),
            email: user.email
        })
    });
})
```