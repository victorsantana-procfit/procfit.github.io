# Api Web Portal Cosmos Pro

## Sobre a API

A API Web do Portal Cosmos Pro segue as diretivas da versão 4 do protocolo [OData](http://www.odata.org/).

## Versões

Atualmente uma unica versão (V1) da API está dísponivel.

## Ambientes

#### Produção



#### SandBox

## Autenticação

A autenticação da API Cosmos Pro se da através de envio de token de identificação no cabeçalho de todas as requisições enviadas ao endereço da API.

## Rotas

### Rota para Recursos Gerais do Portal

HDSHDJSHDJKSHDJHDJKSHDJKSHDSJKhDKS

### Rota para dados de Formulários Customizados no Portal

O Comos Data
Para utilização da API para acesso a recursos do módulo de Formulários Customizados no Portal Cosmos Pro, as requisições devem 
ser direcionadas ao recurso TableDataRows, esse recurso Odata possui a inteligencia de efetivar as operações CRUD nos objetos customizados de acordo com os parametros
fornecidos para a API.

#### Post

Requisições com método post devem ser utilizados para a inserção de novos dados em uma entidade do Cosmos Pro.

##### Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br/api/**[Versão]**/odata/custom/**[tenant]**/TableDataRows

- **Parametros da Query:**

	| Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| TableName | string | Nome da Tabela para Operação de Inserção.


- **Método** 

	Post

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/json | Tipo de Conteúdo da requisição.
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	No corpo da requisição deve-se enviar um objeto JSON com um nó para cada propriedade que se deseja inserir na entidade alvo da requisição.O Nome do elemento JSON deve
	corresponder ao nome da propriedade existente na entidade alvo da inserção.

	Exemplo:

	```JSON
	{
		"UniqueKeyId": 0,
		"TableId": 1,
		"N_CampoTeste": 958787.56,
		"A_CampoTeste": "Teste",
		"DT_CampoTeste": "2017-07-24T18:05:59.977",
		"L_CampoTeste": true,
		"BI_CampoTeste": 1
	}
	```

##### Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 201 | Dados criados com Sucesso. | Tipo de Conteúdo da requisição.
	| 400 | Requisição mau Formatada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON que representa os dados inseridos na entidade são retornados no corpo da requisição do Tipo Post.

	Exemplo:

	```JSON
	{
		"@odata.context": "http://sandbox.cosmospro.com.br/odata/Inquilino%20Padr%C3%A3o/$metadata#TableDataRows/$entity",
		"UniqueKeyId": 115,
		"TableId": 1,
		"InTransactionState": "Unchanged",
		"Id": 115,
		"N_CampoTeste": 958787.56,
		"BI_CampoTeste": 1,
		"A_CampoTeste": "Teste",
		"DT_CampoTeste": "2017-07-24T18:05:59.977Z",
		"L_CampoTeste": true
	}
	```

> **Nota**
O objeto JSON retornado pela operação POST possui um elemento com nome **UniqueKeyId**, esse elemento possui o valor da chave primaria gerada para os dados inseridos no armazenamento de dados do Cosmos Pro.


#### Get


API's que implementam o protocolo [OData](http://www.odata.org/) são [RestFull](https://en.wikipedia.org/wiki/Representational_state_transfer) por natureza, e por padrão, requisições que utilizam o método GET são destinadas a operação de leitura em recursos na API.Utilize metodo GET para receber dados de Entidades da Portal Cosmos Pro.

##### Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br/api/**[Versão]**/odata/custom/**[tenant]**/TableDataRows

- **Parametros da Query:**

	| Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| TableName | string | Nome da Tabela para Operação de Inserção.


- **Método** 

	Post

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/json | Tipo de Conteúdo da requisição.
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	No corpo da requisição deve-se enviar um objeto JSON com um nó para cada propriedade que se deseja inserir na entidade alvo da requisição.O Nome do elemento JSON deve
	corresponder ao nome da propriedade existente na entidade alvo da inserção.

	Exemplo:

	```JSON
	{
		"UniqueKeyId": 0,
		"TableId": 1,
		"N_CampoTeste": 958787.56,
		"A_CampoTeste": "Teste",
		"DT_CampoTeste": "2017-07-24T18:05:59.977",
		"L_CampoTeste": true,
		"BI_CampoTeste": 1
	}
	```
