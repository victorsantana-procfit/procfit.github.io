# Introdução a 'Cosmos Pro Web API' (V1)

## Sobre a API


1. **Restfull**  
A **Cosmos Pro Web API** é desenvolvida no padrão [RestFull](https://en.wikipedia.org/wiki/Representational_state_transfer).
2. **OData**  
A **Cosmos Pro Web API** é compatível com a versão 4 do protocolo [OData](http://www.odata.org/documentation/).
3. **Propósito**  
A **Cosmos Pro Web API** possui funcionalidades que proveem acesso a dados do módulo de Formulários Customizados do Portal Cosmos Pro, as requisições devem ser direcionadas ao endpoint *TableDataRows* da API, esse recurso OData possui a inteligencia de efetivar as operações CRUD em objetos do módulo de Formulários Customizados do portal Cosmos Pro de acordo com os parametros fornecidos para a API.


## Autenticação

A autenticação da API Cosmos Pro se da através de envio de token de identificação no cabeçalho de todas as requisições enviadas ao endereço da API.
O token é obtido através do portal Cosmos Pro Web, na seção de configurações de segurança.


## Ambientes

* Produção
* Homologação


## Tenant (inquilino)

Para consumir a API de maneira adequada, na composição url de destino da requisição HTTP será necessário a utilização do nome do *tenant* do portal Cosmos Pro.Caso não possua o nome do *tenant* fornecido no momento da aquisição de acesso ao portal Cosmos Pro, contate o administrador de sua organização.


## Operações CRUD

####  :pushpin: Inserção

Em API's do tipo [RestFull](https://en.wikipedia.org/wiki/Representational_state_transfer) , requisições que utilizam o método HTTP *Post* são destinadas a operações de inserção/criação de recursos.Utilize método HTTP Post para gravar dados em Entidades no Portal Cosmos Pro.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows?TableName=**Produtos**
	
    > ### :grey_exclamation: Informação
    > O texto **"Produtos"**, fornecido para o parametro *TableName* da query string da URL, é apenas um exemplo.
	
---

- **Parametros da Query String da URL:**

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

	No corpo da requisição HTTP deve-se enviar um objeto JSON com uma elemento para cada propriedade (Campo) que se deseja inserir na entidade alvo da requisição.O Nome dos elementos contidos no objeto JSON devem
	corresponder aos nomes das propriedades existentes na entidade alvo da inserção.

	Exemplo:

	```JSON
	{
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

	Um objeto JSON que representa a linha inserida na entidade é retornado no corpo da resposta HTTP correspondente a requisição HTTP do Tipo Post recem transmitida.

	Exemplo:

	```JSON
	{
		"@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/Inquilino%20Padr%C3%A3o/$metadata#TableDataRows/$entity",
		"UniqueKeyId": 115,
		"TableId": 1,
		"TableName": "Produtos",
		"Id": 115,
		"N_CampoTeste": 958787.56,
		"BI_CampoTeste": 1,
		"A_CampoTeste": "Teste",
		"DT_CampoTeste": "2017-07-24T18:05:59.977Z",
		"L_CampoTeste": true
	}
	```
---

> ### :grey_exclamation: Informação
> O objeto JSON retornado pela operação POST possui um elemento com nome **UniqueKeyId**, esse elemento possui o valor da chave primaria gerada para a nova linha inserida no armazenamento de dados do Cosmos Pro.

---

#### :pushpin: Alteração

A **Cosmos Pro Web API** possibilita a atualização de dados contidos nas entidades do módulo de Formularios Customizados através de requisições que utilizem os métodos http PUT ou PATCH, utilize PATCH para atualizar apenas algumas propriedades, ou Put para sobrepor todas as propriedades da linha desejada.

> ### :grey_exclamation: Informação
> Somente uma linha é atualizada na entidade alvo a cada requisição enviada ao servidor, para atualizar mais de um registro de uma entidade ou mais entidades com apenas uma requisição HTTP utilize a operação do tipo Batch.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows(UniqueKeyId=**100**, TableName=**'Produtos'**)*

> ### :grey_exclamation: Informação
> Os Valores **"100"** e **"Produtos"**, fornecidos respectivamente para os parametros *UniqueKeyId* e *TableName* da URL base, são apenas exemplos.

- **Parametros URL Base**

    | Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| UniqueKeyId | long | Id unico do registro a ser pesquisado. 
	| TableName | string | Nome da Tabela para pesquisa. 

- **Método** 

	*Put ou Patch*

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ |------ |
	| Content-Type | application/json | Tipo de Conteúdo da requisição.
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro
    | Prefer | return=representation | **Opcional** , caso seja fornecido, o objeto JSON representando a linha inserida será retornada no corpo da resposta.

- **Corpo**

    No corpo da requisição deve-se enviar um objeto JSON com um nó para cada propriedade que se deseja atualizar na entidade alvo da requisição.O Nome do elemento JSON deve
	corresponder ao nome da propriedade existente na entidade alvo da atualização.

	Exemplo:

	```JSON
	{
            "UniqueKeyId": 6,
            "TableId": 1,
            "N_CampoTeste": 958787.56,
            "A_CampoTeste": "Teste U",
            "DT_CampoTeste": "2017-07-24T18:05:59.977",
            "L_CampoTeste": true,
            "BI_CampoTeste": 6
    }
	```

##### :outbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Dados Atualizados com Sucesso. |
	| 400 | Requisição não processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON que representa os dados do registro logo após a atualização.

	Exemplo:

	```JSON
    {
        "@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/Inquilino%20Padr%C3%A3o/$metadata#TableDataRows/$entity",
        "UniqueKeyId": 6,
        "TableId": 1,
        "TableName": "Produtos",
        "Id": 6,
        "N_CampoTeste": 958787.56,
        "BI_CampoTeste": 6,
        "A_CampoTeste": "Teste U",
        "DT_CampoTeste": "2017-07-24T18:05:59.977Z",
        "L_CampoTeste": true,
        "SecoesProdutosId": 2
    }
	```

> ### :grey_exclamation: Informação
> O objeto JSON com a linha atualizada somente será adicionada ao corpo da resposta http caso no momento da requisição http, o cabeçalho *Prefer* tenha sido fornecido com o valor *return=representation*.

---

#### :pushpin: Leitura


Utilize este método para recuperar uma coleção de dados de uma entidade passada como parametro (Query String).

Para refinar a consulta, utilize na url (query string), as [funções suportadas pelo protocolo Odata](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part2-url-conventions/odata-v4.0-errata03-os-part2-url-conventions-complete.html#_Toc453752357).

#### :arrow_forward: Recuperando uma Coleção de dados de uma Entidade.

Utilize este método para recuperar uma coleção de dados de uma entidade passada como parametro (Query String).Para refinar a consulta, utilize na url (query string), as funções suportadas pelo protocolo Odata.

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

#### :arrow_forward: Buscando dados com a Chave Primaria (UniqueKeyId e TableName).

A Cosmos Pro Web API suporta a recuperação de dados através da chave, o que fará com que a resposta da requisição retorne apenas uma linha da Entidade pesquisada.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows(UniqueKeyId=**100**, TableName=**'Produtos'**)*

> ### :grey_exclamation: Informação
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
	| ------ | ------ |------ |
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

> ### :grey_exclamation: Informação
> O objeto JSON retornado pela operação POST possui um elemento com nome **UniqueKeyId**, esse elemento possui o valor da chave primaria gerada para os dados inseridos no armazenamento de dados do Cosmos Pro.

---

#### :pushpin: Exclusão

Requisições que utilizam o método http *Delete* servem para a exclusão de recursos na API.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/TableDataRows(UniqueKeyId=100, TableName='Produtos')*

> ### :grey_exclamation: Informação
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


> ### :grey_exclamation: Informação
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
    
#### :pushpin: Batch

A Comos Pro Web API tambem possui suporte a operações do tipo *Batch*, operações desse tipo permitem que os consumidores da API possam "empacotar" mais de uma operação em uma unica requisição HTTP e a enviem ao serviço, e com isso recebam apenas uma unico retorno contendo todas as respostas HTTP para todas as requisições transmitidas.Desse jeito, consumidores da API podem otimizar chamadas ao serviço e melhorar a escalabilidade.


## Consumindo Consultas Customizadas

Quando a necessidade exige que o formato dos dados retornados pela consulta não necessáriamente remeta a qualquer entidade do modelo de dados do Portal Cosmos Pro, porem ainda é necessário a utilização de suporte a Paginação e ordenação dos resultados da consulta, utilize o endpoint Odata *CustomViews* da Cosmos Pro Web API, esse endpoint possui capacidade de execução de Consultas Customizadas previamente desenvolvidas através do portal Web do Portal Cosmos Pro.

Não é possível alterar dados através da execução de Comsultas Customizadas do Portal Cosmos Pro.


#### :arrow_forward: Acionando a Execução da Consulta.

Para utilizar esse recurso, o Cliente Consumidor da API deve efetuar ao menos duas requisições HTTP com destino ao recurso "CustomViews" da API, sendo que a primeira requisição tem proposito apenas de disparo da execução da consulta por parte do servidor da API, um identificador unico da execução será retornado para o consumidor como resposta HTTP.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/CustomViews('ProdutosEmPromocao')/Execute()*
	
    > ### :grey_exclamation: Informação
    > O texto **"ProdutosEmPromocao"**, fornecido para o parametro da ação *Execute* URL base é apenas um exemplo.
	
---

- **Parametros URL Base**

    | Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| CustomViewName | String | Nome da CustomView a ser acionada. 

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

	No corpo da requisição HTTP deve-se enviar um objeto JSON com uma elemento para cada parametro necessário para execução da CustomView.

	Exemplo:

	```JSON
	{
        "Parameters":{
	    "DataInicial":"2017-07-24T00:00:00.000",
	    "DataFinal":"2017-07-25T00:00:00.000"
        }
    }
	```

##### :outbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Processamento Executado com Sucesso. |
	| 400 | Requisição não processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON contendo o ExecutionId.

	Exemplo:

	```JSON
    {
        "@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/Inquilino%20Padr%C3%A3o/$metadata#Edm.Guid",
        "value": "97ae1270-115d-46ca-a76e-ec752971ad26"
    }
	```


#### :arrow_forward: Executando e Recebendo os dados em apenas uma Requisição.

Com esse recurso é possível com apenas uma requisição, que o consumidor da API execute e receba os dados da Consulta Customizada da Cosmos Pro Web API.

##### :outbox_tray: Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/CustomViews('ProdutosEmPromocao')/ExecuteAndReceiveData()
	
> ### :grey_exclamation: Informação
> O método ExecuteAndReceiveData prove suporte as covenções de url do protocolo OData.

- **Método** 

	Post

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/json | .
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	No corpo da requisição HTTP deve-se enviar um objeto JSON com uma elemento para cada parametro necessário para execução da CustomView.

	Exemplo:

	```JSON
	{
        "Parameters":{
	    "DataInicial":"2017-07-24T00:00:00.000",
	    "DataFinal":"2017-07-25T00:00:00.000"
        }
    }
	```

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Dados Retornados com Sucesso. |
	| 400 | Requisição não Processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON que representa um *array* com a coleção de registros da CustomView é retornado no corpo da requisição.

	Exemplo:

	```JSON
    {
    "@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/dictionary/Inquilino%20Padr%C3%A3o/Produ%C3%A7%C3%A3o/$metadata#CustomViewDataRows(name,Var,object_id)",
    "@odata.count": 10,
    "value": [
        {
            "name": "CustomActionAllowedRequestContentTypes",
            "Var": "valor vari",
            "object_id": 565577053
        },
        {
            "name": "CustomActionAllowedResponseContentTypes",
            "Var": "valor vari",
            "object_id": 757577737
        },
        {
            "name": "CustomActionContentTypes",
            "Var": "valor vari",
            "object_id": 629577281
        }
    ]
}
	```
	

##### :outbox_tray: Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/CustomViews('ProdutosEmPromocao')/ReceiveData(ExecutionId=97ae1270-115d-46ca-a76e-ec752971ad26)
	
> ### :grey_exclamation: Informação
> O método ReceiveData prove suporte as covenções de url do protocolo OData.

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

	Um objeto JSON que representa um *array* com a coleção de registros da CustomView é retornado no corpo da requisição.

	Exemplo:

	```JSON
    {
        "@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/Inquilino%20Padr%C3%A3o/$metadata#CustomViewDataRows",
        "value": [
            {
                "InResultId": 1,
                "CampoTeste1": "ValorTeste1",
                "CampoTeste2": "ValorTeste2"
            },
            {
                "InResultId": 2,
                "CampoTeste1": "ValorTeste12333",
                "CampoTeste2": "ValorTeste24545454"
            }
        ]
    }
	```
	

## Acionando Ações Customizadas

Como dito anteriormente, Consultas Costumizadas não oferecem suporte a efetuar requisões que alterem dados do Cosmos Pro, essa limitação existe para que os recursos como Armazenamento de Cache do Resultado da Consulta, Paginação, Filtros e etc sejam possiveis.Porem em certas ocasiões, as operações CRUD da Cosmos Pro Web API (que são baseadas no Modelo de Dados) não atendem a necessidade da integração.

Utilize Ações Customizadas para acionar tarefas previamente desenvolvidas através do Portal Web do Cosmos Pro.

##### :outbox_tray: Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/**[tenant]**/CustomViews('ProdutosEmPromocao')/ReceiveData(ExecutionId=97ae1270-115d-46ca-a76e-ec752971ad26)
	
> ### :grey_exclamation: Informação
> O método ReceiveData prove suporte as covenções de url do protocolo OData.

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

	Um objeto JSON que representa um *array* com a coleção de registros da CustomView é retornado no corpo da requisição.

	Exemplo:

	```JSON
    {
        "@odata.context": "http://homologacao.cosmospro.com.br/api/odata/v1/Inquilino%20Padr%C3%A3o/$metadata#CustomViewDataRows",
        "value": [
            {
                "InResultId": 1,
                "CampoTeste1": "ValorTeste1",
                "CampoTeste2": "ValorTeste2"
            },
            {
                "InResultId": 2,
                "CampoTeste1": "ValorTeste12333",
                "CampoTeste2": "ValorTeste24545454"
            }
        ]
    }
	```
