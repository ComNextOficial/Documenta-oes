Taxa Básica de Juros - Países Disponíveis | Documentação brapi.dev

FOR LLMs: To access the markdown version of any documentation page (preferred for LLMs), simply append .mdx to the end of the URL. For example, instead of /docs/acoes, use /docs/acoes.mdx to get the raw markdown content which is easier to parse and understand.

Toggle Menu[![brapi logo](/favicon.svg)brapi](/)

[Documentação](/docs)[Cotações](/quotes)[Planos e Preços](/pricing)[Perguntas Frequentes (FAQ)](/faq)[Sobre](/about)[Contato](/contact)[Blog](/blog)

[Obter Chave de API](/dashboard)Alterar tema

[Geral](/docs)

Ações

[Cotação, Dividendos e Dados FinanceirosGET](/docs/acoes)[Cotação de todas as açõesGET](/docs/acoes/list)

Criptomoedas

[Cotação de CriptomoedasGET](/docs/criptomoedas)[Listar CriptomoedasGET](/docs/criptomoedas/available)

Moedas

[Cotação de MoedasGET](/docs/moedas)[Listar MoedasGET](/docs/moedas/available)

Inflação

[InflaçãoGET](/docs/inflacao)[Listar PaísesGET](/docs/inflacao/available)

Taxa Básica de Juros (SELIC)

[Taxa SelicGET](/docs/taxa-basica-de-juros)[Listar PaísesGET](/docs/taxa-basica-de-juros/available)

[Exemplos](/docs/examples)

Taxa Básica de Juros (SELIC)

Taxa Básica de Juros - Países Disponíveis
=========================================

Copiar Markdown[Ver Markdown](/docs/taxa-basica-de-juros/available.mdx)

Endpoint para listar todos os **países com dados de Taxa Básica de Juros
(SELIC)** disponíveis na API.

Facilita a descoberta de quais países possuem dados disponíveis e permite a
implementação de recursos de busca e autocomplete em interfaces de usuário.

[Listar Todos Os Possíveis Países com Taxa Básica de Juros (SELIC) Suportados](#listar-todos-os-possíveis-países-com-taxa-básica-de-juros-selic-suportados)
-----------------------------------------------------------------------------------------------------------------------------------------------------------

Liste todos os países disponíveis com dados de taxa básica de juros (SELIC) na API brapi. Este endpoint facilita a descoberta de quais países possuem dados disponíveis para consulta através do endpoint principal `/api/v2/prime-rate`.

### Funcionalidades:

* **Busca Filtrada:** Utilize o parâmetro `search` para filtrar países por nome ou parte do nome.
* **Ideal para Autocomplete:** Perfeito para implementar campos de busca com autocompletar em interfaces de usuário.

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Listar países que contenham "BR" no nome:**

```
curl -X GET "https://brapi.dev/api/v2/prime-rate/available?search=BR&token=SEU_TOKEN"
```

loading...

GET

/`api`/`v2`/`prime-rate`/`available`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`search`string

**Opcional.** Termo para filtrar a lista de países por nome. Retorna países cujos nomes contenham o termo especificado (case insensitive).

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200401404

Resposta do endpoint `/api/v2/prime-rate/available` que lista os países disponíveis para consulta de taxa básica de juros (SELIC).

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`countries`array<string>

Lista de países com dados de taxa básica de juros (SELIC) disponíveis para consulta.

Schema padrão para respostas de erro da API.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`error`Requiredboolean

Indica se a requisição resultou em erro. Sempre `true` para este schema.

`message`Requiredstring

Mensagem descritiva do erro ocorrido.

Schema padrão para respostas de erro da API.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`error`Requiredboolean

Indica se a requisição resultou em erro. Sempre `true` para este schema.

`message`Requiredstring

Mensagem descritiva do erro ocorrido.

cURLJavaScriptGoPython

```
curl -X GET "https://brapi.dev/api/v2/prime-rate/available?search=BR" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/prime-rate/available?search=BR", {
  headers: {
    "Authorization": "Bearer <token>"
  }
})
```

```
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {
  url := "https://brapi.dev/api/v2/prime-rate/available?search=BR"

  req, _ := http.NewRequest("GET", url, nil)
  req.Header.Add("Authorization", "Bearer <token>")
  res, _ := http.DefaultClient.Do(req)
  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))
}
```

```
import requests

url = "https://brapi.dev/api/v2/prime-rate/available?search=BR"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200401404

```
{
  "countries": [
    "brazil",
    "united states",
    "european union"
  ]
}
```

```
{
  "error": true,
  "message": "O seu token é inválido, por favor, verifique o seu token em brapi.dev/dashboard"
}
```

```
{
  "message": "Country not found"
}
```

[Taxa SelicGET

Taxa básica de juros do Brasil com dados históricos e atuais](/docs/taxa-basica-de-juros)[Exemplos

Exemplos de uso da brapi](/docs/examples)