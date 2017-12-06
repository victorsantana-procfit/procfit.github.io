
## Autenticação Cosmos Pro Web API

A autenticação da API Cosmos Pro se da através de envio de token de identificação no cabeçalho de todas as requisições enviadas ao endereço da API.
O token é obtido através do portal da requisição HTTP a URL de Login ou através do Portal Cosmos Pro Web, na seção de configurações de segurança.

##### :outbox_tray: Requisição


- **Url** 

	*http:// **[ambiente]**.cosmospro.com.br:**[porta]**/api/login/autenticar?api-version=1.0
	
    > ### :grey_exclamation: Informação
    > A porta HTTP padrão utilizada pela Cosmos Web API é 9090.
	
---

- **Parametros da Query String da URL:**

	| Nome | Tipo | Observação
	| ------ | ------ | ------ |
	| api-version | string | Versão da API (fixo 1.0).

---

- **Método** 

	*Post*
---

- **Cabeçalhos(Headers):**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| Content-Type | application/x-www-form-urlencoded |

---

- **Corpo**

	No corpo da requisição de Login, informações de usuário e senha devem ser enviadas com o formato x-www-form-urlencoded.

- **Campos do Body:**

	| Nome | Valor | Observação
	| ------ | ------ | ------ |
	| login | login do Portal Cosmos Pro Web |
	| senha | Senha do Portal Cosmos Pro Web |

##### :inbox_tray: Resposta

- **Códigos de Estado Possíveis**


	| HTTP Status Code | Motivo | Observação
	| ------ | ------ | ------ |
	| 200 | Autenticação Efetuada com Sucesso. |
	| 401 | Usuário e/ou Senha Incorreta|
---

- **Corpo**

	Um elemento JSON (não um Objeto) com o token gerado para a requisição de login.

	```JSON
	"d01b3a32-2148-4548-999b-b0dbdbe1b746"
	```


Esse token deve ser utilizado em todas as novas requisições HTTP enviadas ao Serviço da Cosmos pro Web API.
