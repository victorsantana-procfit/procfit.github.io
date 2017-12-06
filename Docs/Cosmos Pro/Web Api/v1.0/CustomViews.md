## Consumindo Consultas Customizadas

Quando a necessidade exige que o formato dos dados retornados pela consulta (requisição HTTP) não necessáriamente remeta ao formato de qualquer entidade do modelo de dados do Portal Cosmos Pro, porem ainda é necessário a utilização de suporte a funções avançadas de consultas do lado server da API como Paginação e Ordenação dos resultados da consulta, utilize o endpoint OData *CustomViews* da Cosmos Pro Web API, esse endpoint possui capacidade de execução de Consultas Customizadas previamente desenvolvidas através do portal Web do Portal Cosmos Pro.

Não é possível alterar dados através da execução de Comsultas Customizadas do Portal Cosmos Pro.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br:**[porta]**/odata/CustomViews(Name=**'ProdutosEmPromocao'**,EmpresaId=**1**)/ExecuteAndReceive()?api-version=1.0*
	
    > ### :grey_exclamation: Informação
    > Os valor **"ProdutosEmPromocao"** fornecido para o parametro *Name* da ação *ExecuteAndReceive* e o valor **1** fornecido para o parametro *EmpresaId* da URL base da requisição são apenas exemplos.
	
---

- **Parametros URL Base**

    | Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| Name | String | Nome da CustomView a ser acionada. 
	| EmpresaId | Int | Código da Empresa usuária do Cosmos Pro.

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
	| 200 | Query Executada com Sucesso. |
	| 400 | Requisição não processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto JSON que representa um *array* com a coleção de registros retornados pela execução da CustomView é anexado ao corpo da resposta HTTP.

	Exemplo:

	```JSON
    {
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
