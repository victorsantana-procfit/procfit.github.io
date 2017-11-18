# Introdução a 'Generic Cosmos Pro Web API' (V1)

## Sobre a API


1. **Restfull**  
A Cosmos Pro Web API é desenvolvida no padrão Restfull.
2. **OData**  
A API Web do Portal Cosmos Pro segue as diretivas da versão 4 do protocolo [OData](http://www.odata.org/).
3. **Propósito**  
A 'Generic Cosmos Pro Web API' prove acesso a dados do módulo de Formulários Customizados do Portal Cosmos Pro, as requisições devem ser direcionadas ao endpoint *TableDataRows* da API, esse recurso OData possui a inteligencia de efetivar as operações CRUD nos objetos customizados do portal Cosmos Pro de acordo com os parametros fornecidos para a API.


## Autenticação

A autenticação da API Cosmos Pro se da através de envio de token de identificação no cabeçalho de todas as requisições enviadas ao endereço da API.
O token é obtido através do portal Cosmos Pro Web, na seção de configurações de segurança.


## Ambientes

* Produção
* Homologação


## Tenant (inquilino)

Para consumir a API de maneira adequada, na composição url será necessário a utilização do nome do *tenant* do portal Cosmos Pro.Caso não possua o nome do *tenant* fornecido no momento da aquisição de acesso ao portal Cosmos Pro, contate o administrador de sua organização.


## Operações Suportadas

####  :pushpin: Inserção

API's que implementam o protocolo [OData](http://www.odata.org/) são [RestFull](https://en.wikipedia.org/wiki/Representational_state_transfer) por natureza, e por padrão, requisições que utilizam o método POST são destinadas a operação de inserção/criação de dados na API.Utilize método POST para gravar dados de Entidades no Portal Cosmos Pro.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows*
	
---

- **Parametros da Query:**

	| Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| TableName | string | Nome da Tabela para Operação de Inserção.

---

- **Método** 

	*Post*
---

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/json | Tipo de Conteúdo da requisição.
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro

---

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

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 201 | Dados criados com Sucesso. | Tipo de Conteúdo da requisição.
	| 400 | Requisição mau Formatada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.
---

- **Corpo**

	Um objeto JSON que representa os dados inseridos na entidade são retornados no corpo da requisição do Tipo Post.

	Exemplo:

	```JSON
	{
		"@odata.context": "http://homologacao.cosmospro.com.br/api/v1/odata/Inquilino%20Padr%C3%A3o/$metadata#TableDataRows/$entity",
		"UniqueKeyId": 115,
		"TableId": 1,
		"Id": 115,
		"N_CampoTeste": 958787.56,
		"BI_CampoTeste": 1,
		"A_CampoTeste": "Teste",
		"DT_CampoTeste": "2017-07-24T18:05:59.977Z",
		"L_CampoTeste": true
	}
	```
---

> ### @icon-info-circle Informação
> O objeto JSON retornado pela operação POST possui um elemento com nome **UniqueKeyId**, esse elemento possui o valor da chave primaria gerada para os dados inseridos no armazenamento de dados do Cosmos Pro.

---

#### :pushpin: Alteração

---

#### :pushpin: Sobreposição

---

#### :pushpin: Leitura


API's que implementam o protocolo [OData](http://www.odata.org/) são [RestFull](https://en.wikipedia.org/wiki/Representational_state_transfer) por natureza, e por padrão, requisições que utilizam o método GET são destinadas 
a operações de leitura em recursos na API.Utilize método GET para receber dados de Entidades da Portal Cosmos Pro.

#### :arrow_forward: Recuperando uma Coleção de dados de uma Entidade.

Utilize este método para recuperar uma coleção de dados de uma tabela passada como parametro (Query String).Para refinar a consulta, utilize na url (query string), as funções suportadas pelo protocolo Odata.

##### :outbox_tray: Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows

- **Método** 

	Get

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/x-www-form-urlencoded | .
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	*Vazio.*

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Dados Retornados com Sucesso. |
	| 400 | Requisição não Processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON que representa um *array* com a coleção de registros da entidade é retornado no corpo da requisição.

	Exemplo:

	```JSON
	{
    "@odata.context": "http://pbswebserverhomolog.azurewebsites.net/odata/datastorage/Inquilino%20Padr%C3%A3o/Produ%C3%A7%C3%A3o/$metadata#TableDataRows",
    "value": [
        {
            "UniqueKeyId": 1,
            "TableId": 1,
            "Id": 1,
            "N_CampoTeste": 449.46,
            "BI_CampoTeste": 173253937333,
            "A_CampoTeste": "5588D74B",
            "DT_CampoTeste": "1934-12-25T00:00:00Z",
            "L_CampoTeste": true,
            "SecoesProdutosId": 2
        },
        {
            "UniqueKeyId": 2,
            "TableId": 1,
            "Id": 2,
            "N_CampoTeste": 114.74,
            "BI_CampoTeste": 1585325047,
            "A_CampoTeste": "75788538",
            "DT_CampoTeste": "2020-01-01T00:00:00Z",
            "L_CampoTeste": false,
            "SecoesProdutosId": 3
        },
        {
            "UniqueKeyId": 3,
            "TableId": 1,
            "Id": 3,
            "N_CampoTeste": 130.57,
            "BI_CampoTeste": 1340661892,
            "A_CampoTeste": "2A1230EC",
            "DT_CampoTeste": "2025-05-10T00:00:00Z",
            "L_CampoTeste": false,
            "SecoesProdutosId": 2
        },
        {
            "UniqueKeyId": 4,
            "TableId": 1,
            "Id": 4,
            "N_CampoTeste": 30.34,
            "BI_CampoTeste": 5681169041,
            "A_CampoTeste": "51CD4FD9",
            "DT_CampoTeste": "1949-12-15T00:00:00Z",
            "L_CampoTeste": false,
            "SecoesProdutosId": 2
        },
        {
            "UniqueKeyId": 5,
            "TableId": 1,
            "Id": 5,
            "N_CampoTeste": 236.67,
            "BI_CampoTeste": 1095547819,
            "A_CampoTeste": "66F723A2",
            "DT_CampoTeste": "2037-01-02T00:00:00Z",
            "L_CampoTeste": false,
            "SecoesProdutosId": 3
        }
    ]
	```

> ### @icon-info-circle Informação
>O objeto JSON retornado pela operação POST possui um elemento com nome **UniqueKeyId**, esse elemento possui o valor da chave primaria gerada para os dados inseridos no armazenamento de dados do Cosmos Pro.



#### :arrow_forward: Buscando dados com a Chave Primaria (UniqueKeyId e TableName).

A Cosmos Pro Web API suporta a recuperação de dados através da chave, o que fará com que a resposta da requisição retorne apenas uma linha da Entidade pesquisada.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows(UniqueKeyId=**100**, TableName=**'Produtos'**)*

> ### @icon-info-circle Informação
> Os Valores **"100"** e **"Produtos"**, fornecidos respectivamente para os parametros *UniqueKeyId* e *TableName* da URL base, são apenas exemplos.

- **Parametros URL Base**

    | Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| UniqueKeyId | long | Id unico do registro a ser pesquisado. 
	| TableName | string | Nome da Tabela para pesquisa. 

- **Método** 

	*Get*

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ |
	| Content-Type | application/x-www-form-urlencoded | Tipo de Conteúdo da requisição.
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	*Vazio.*

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Dados Retornados com Sucesso. |
	| 400 | Requisição não processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON que representa os dados inseridos na entidade são retornados no corpo da requisição do Tipo Post.

	Exemplo:

	```JSON
	{
		"@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/Inquilino%20Padr%C3%A3o/$metadata#TableDataRows/$entity",
		"UniqueKeyId": 115,
		"TableId": 1,
		"Id": 115,
		"N_CampoTeste": 958787.56,
		"BI_CampoTeste": 1,
		"A_CampoTeste": "Teste",
		"DT_CampoTeste": "2017-07-24T18:05:59.977Z",
		"L_CampoTeste": true
	}
	```

> ### @icon-info-circle Informação
> O objeto JSON retornado pela operação POST possui um elemento com nome **UniqueKeyId**, esse elemento possui o valor da chave primaria gerada para os dados inseridos no armazenamento de dados do Cosmos Pro.

---

#### :pushpin: Exclusão

Requisições que utilizam o método http *Delete* servem para a exclusão de recursos na API.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows(UniqueKeyId=100, TableName='Produtos')*

> ### @icon-info-circle Informação
> Os Valores **"100"** e **"Produtos"**, fornecidos respectivamente para os parametros *UniqueKeyId* e *TableName* da URL base, são apenas exemplos.

- **Parametros URL Base**

    | Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| UniqueKeyId | long | Id unico do registro a ser excluido. 
	| TableName | string | Nome da Tabela para operação de exclusão. 

- **Método** 

	*Delete*

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/x-www-form-urlencoded | .
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	*Vazio.*


> ### @icon-info-circle Informação
> Somente uma linha é excluida da entidade alvo a cada requisição enviada ao servidor.

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 204 | Dados Excluidos com Sucesso |
	| 404 | Registro não Eoncontrado |
	| 400 | Requisição não Processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

    *Vazio.*