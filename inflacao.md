Inflação | Documentação brapi.dev

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

Inflação

Inflação
========

Copiar Markdown[Ver Markdown](/docs/inflacao.mdx)

Endpoints para acessar dados históricos de **Índices de Inflação**.

Permite consultar a inflação de diferentes países ao longo do tempo e listar os
países com dados disponíveis.

[Buscar Dados Históricos de Inflação por País](#buscar-dados-históricos-de-inflação-por-país)
---------------------------------------------------------------------------------------------

Obtenha dados históricos sobre índices de inflação para um país específico.

### Funcionalidades:

* **Seleção de País:** Especifique o país desejado com o parâmetro `country` (padrão: `brazil`).
* **Filtragem por Período:** Defina um intervalo de datas com `start` e `end` (formato DD/MM/YYYY).
* **Inclusão de Histórico:** O parâmetro `historical` (booleano) parece controlar a inclusão de dados históricos (verificar comportamento exato, pode ser redundante com `start`/`end`).
* **Ordenação:** Ordene os resultados por data (`date`) ou valor (`value`) usando `sortBy` e `sortOrder`.

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Buscar dados de inflação do Brasil para o ano de 2022, ordenados por valor ascendente:**

```
curl -X GET "https://brapi.dev/api/v2/inflation?country=brazil&start=01/01/2022&end=31/12/2022&sortBy=value&sortOrder=asc&token=SEU_TOKEN"
```

**Buscar os dados mais recentes de inflação (sem período definido, ordenação padrão):**

```
curl -X GET "https://brapi.dev/api/v2/inflation?country=brazil&token=SEU_TOKEN"
```

### Resposta:

A resposta contém um array `inflation`, onde cada objeto representa um ponto de dado de inflação com sua `date` (DD/MM/YYYY), `value` (o índice de inflação como string) e `epochDate` (timestamp UNIX).

loading...

GET

/`api`/`v2`/`inflation`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`country`string

**Opcional.** Nome do país para o qual buscar os dados de inflação. Use nomes em minúsculas. O padrão é `brazil`. Consulte `/api/v2/inflation/available` para a lista de países suportados.

Default: `"brazil"`

`historical`boolean

**Opcional.** Booleano (`true` ou `false`). Define se dados históricos devem ser incluídos. O comportamento exato em conjunto com `start`/`end` deve ser verificado. Padrão: `false`.

Default: `false`

`start`string

**Opcional.** Data de início do período desejado para os dados históricos, no formato `DD/MM/YYYY`. Requerido se `end` for especificado.

Pattern: `"^\\d{2}/\\d{2}/\\d{4}$"`Format: `"date"`

`end`string

**Opcional.** Data final do período desejado para os dados históricos, no formato `DD/MM/YYYY`. Requerido se `start` for especificado.

Pattern: `"^\\d{2}/\\d{2}/\\d{4}$"`Format: `"date"`

`sortBy`string

**Opcional.** Campo pelo qual os resultados da inflação serão ordenados.

Default: `"date"`Value in: `"date" | "value"`

`sortOrder`string

**Opcional.** Direção da ordenação: `asc` (ascendente) ou `desc` (descendente). Padrão: `desc`. Requer que `sortBy` seja especificado.

Default: `"desc"`Value in: `"asc" | "desc"`

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200400401417

Resposta principal do endpoint `/api/v2/inflation`.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`inflation`array<object>

Array contendo os registros históricos de inflação para o país e período solicitados.

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
curl -X GET "https://brapi.dev/api/v2/inflation?country=brazil&historical=true&start=01%2F01%2F2020&end=31%2F12%2F2020&sortBy=value&sortOrder=asc" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/inflation?country=brazil&historical=true&start=01%2F01%2F2020&end=31%2F12%2F2020&sortBy=value&sortOrder=asc", {
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
  url := "https://brapi.dev/api/v2/inflation?country=brazil&historical=true&start=01%2F01%2F2020&end=31%2F12%2F2020&sortBy=value&sortOrder=asc"

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

url = "https://brapi.dev/api/v2/inflation?country=brazil&historical=true&start=01%2F01%2F2020&end=31%2F12%2F2020&sortBy=value&sortOrder=asc"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200400401417

```
{
  "inflation": [
    {
      "date": "01/01/2023",
      "value": "4.56",
      "epochDate": 1672531199
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

[Listar MoedasGET

Listar moedas disponíveis na brapi com informações adicionais](/docs/moedas/available)[Listar PaísesGET

Listar países disponíveis na brapi com informações adicionais](/docs/inflacao/available)