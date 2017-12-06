

## Acionando Ações Customizadas

Como dito anteriormente, Consultas Costumizadas não oferecem suporte a efetuar requisões que alterem dados do Cosmos Pro, essa limitação existe para que os recursos como Armazenamento de Cache do Resultado da Consulta, Paginação, Filtros , Ordenação e etc sejam possiveis.Porem em certas ocasiões, as operações CRUD da Cosmos Pro Web API (que são baseadas no Modelo de Dados) também não atendem a necessidade da integração.

Utilize Ações Customizadas para acionar tarefas previamente desenvolvidas através do Portal Web do Cosmos Pro.

##### :outbox_tray: Requisição


- **Url** 

	http:// **[ambiente]**.cosmospro.com.br:**[porta]**/api/ExecuteCustomAction/ExecuteAction?ActionName=DRE&empresa=2&api-version=1.0
	
- **Método** 

	Post

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/xml, application/json ou text/plain | Especifica o tipo de dados do corpo da requição HTTP.
    | Accept | application/xml, application/json ou text/plain | Especifica o tipo de dados do corpo da resposta HTTP.
	| Authorization | Bearer [Token] | Token de Autenticação obtido junto ao Administrador do Inquilino Cosmos Pro


- **Corpo**

	Objeto a ser enviado ao Cosmos Pro, respeitando o formato especificado no header "Content-Type" da requisição HTTP.

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Dados Processadps com Sucesso. |
	| 400 | Requisição não Processada | O elemento **message** do objeto JSON retornado possui mais detalhes sobre a resposta.


- **Corpo**

	Um objeto que representa a resposta do processamento da ação customizada no formato correspondente ao solicitado no herader "Accept" da requisição.
