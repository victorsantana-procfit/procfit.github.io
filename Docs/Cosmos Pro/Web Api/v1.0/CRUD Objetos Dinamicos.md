## Operações CRUD em Objetos Dinamicos

A Cosmos Pro Web API permite a manipulação de dados de objetos criados através do módulo de formulários customizados que são desenvolvidos através do Portal Web do Cosmos Pro.

####  :pushpin: Inserção

Em API's do tipo [RestFull](https://en.wikipedia.org/wiki/Representational_state_transfer) , requisições que utilizam o método HTTP *Post* são destinadas a operações de inserção/criação de recursos. Utilize método HTTP Post para gravar dados em Entidades no Portal Cosmos Pro.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br/api/odata/v1/TableDataRows?TableName=**Produtos**
	
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

	No corpo da requisição HTTP deve-se enviar um objeto JSON com uma elemento para cada propriedade (Campo) que se deseja inserir na entidade alvo da requisição. O Nome dos elementos contidos no objeto JSON devem
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

A **Cosmos Pro Web API** possibilita a atualização de dados contidos nas entidades do módulo de Formulários Customizados através de requisições que utilizem os métodos http PUT ou PATCH, utilize PATCH para atualizar apenas algumas propriedades, ou Put para sobrepor todas as propriedades da linha desejada.

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
