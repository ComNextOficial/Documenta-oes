Taxa Básica de Juros | Documentação brapi.dev

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

Taxa Básica de Juros
====================

Copiar Markdown[Ver Markdown](/docs/taxa-basica-de-juros.mdx)

Endpoints para consulta de **Taxas Básicas de Juros (SELIC)** de diferentes
países.

Permite a obtenção de taxas atuais e séries históricas das taxas básicas de
juros, com personalização por país, período e opções de ordenação.

[Buscar Taxa Básica de Juros (SELIC) de um País por um Período Determinado](#buscar-taxa-básica-de-juros-selic-de-um-país-por-um-período-determinado)
-----------------------------------------------------------------------------------------------------------------------------------------------------

Obtenha informações atualizadas sobre a taxa básica de juros (SELIC) de um país por um período determinado.

### Funcionalidades:

* **Seleção por País:** Especifique o país desejado usando o parâmetro `country` (padrão: brazil).
* **Período Customizado:** Defina datas de início e fim com `start` e `end` para consultar um intervalo específico.
* **Ordenação:** Ordene os resultados por data ou valor com os parâmetros `sortBy` e `sortOrder`.
* **Dados Históricos:** Solicite o histórico completo ou apenas o valor mais recente com o parâmetro `historical`.

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Taxa de juros do Brasil entre dezembro/2021 e janeiro/2022:**

```
curl -X GET "https://brapi.dev/api/v2/prime-rate?country=brazil&start=01/12/2021&end=01/01/2022&sortBy=date&sortOrder=desc&token=SEU_TOKEN"
```

loading...

GET

/`api`/`v2`/`prime-rate`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`country`string

**Opcional.** O país do qual você deseja obter informações sobre a taxa básica de juros. Por padrão, o país é definido como brazil. Você pode consultar a lista de países disponíveis através do endpoint `/api/v2/prime-rate/available`.

Default: `"brazil"`

`historical`boolean

**Opcional.** Define se os dados históricos serão retornados. Se definido como `true`, retorna a série histórica completa. Se `false` (padrão) ou omitido, retorna apenas o valor mais recente.

Default: `false`

`start`string

**Opcional.** Data inicial do período para busca no formato DD/MM/YYYY. Útil quando `historical=true` para restringir o período da série histórica.

Format: `"date"`

`end`string

**Opcional.** Data final do período para busca no formato DD/MM/YYYY. Por padrão é a data atual. Útil quando `historical=true` para restringir o período da série histórica.

Format: `"date"`

`sortBy`string

**Opcional.** Campo pelo qual os resultados serão ordenados. Por padrão, ordena por `date` (data).

Default: `"date"`Value in: `"date" | "value"`

`sortOrder`string

**Opcional.** Define se a ordenação será crescente (`asc`) ou decrescente (`desc`). Por padrão, é `desc` (decrescente).

Default: `"desc"`Value in: `"asc" | "desc"`

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200400401417

Resposta principal do endpoint `/api/v2/prime-rate`.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`prime-rate`array<object>

Array contendo os registros históricos de taxa básica de juros (SELIC) para o país e período solicitados.

Show Attributes

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
curl -X GET "https://brapi.dev/api/v2/prime-rate?country=brazil&historical=true&start=01%2F12%2F2021&end=01%2F01%2F2022&sortBy=date&sortOrder=desc" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/prime-rate?country=brazil&historical=true&start=01%2F12%2F2021&end=01%2F01%2F2022&sortBy=date&sortOrder=desc", {
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
  url := "https://brapi.dev/api/v2/prime-rate?country=brazil&historical=true&start=01%2F12%2F2021&end=01%2F01%2F2022&sortBy=date&sortOrder=desc"

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

url = "https://brapi.dev/api/v2/prime-rate?country=brazil&historical=true&start=01%2F12%2F2021&end=01%2F01%2F2022&sortBy=date&sortOrder=desc"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200400401417

```
{
  "prime-rate": [
    {
      "date": "01/01/2022",
      "value": "9.25",
      "epochDate": 1640995200000
    }
  ]
}
```

```
{
  "error": true,
  "message": "Something went wrong while fetching the data"
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
  "error": true,
  "message": "this query value is not available, please use one of the following: asc,desc"
}
```

[Listar PaísesGET

Listar países disponíveis na brapi com informações adicionais](/docs/inflacao/available)[Listar PaísesGET

Listar países disponíveis na brapi com informações adicionais](/docs/taxa-basica-de-juros/available)