Cotação de Moedas | Documentação brapi.dev

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

Moedas

Cotação de Moedas
=================

Copiar Markdown[Ver Markdown](/docs/moedas.mdx)

Endpoints para consulta de **Moedas Fiduciárias**.

Atualmente, focado na listagem das moedas disponíveis para conversão ou consulta
de taxas de câmbio.

[Buscar Cotação de Pares de Moedas Fiduciárias](#buscar-cotação-de-pares-de-moedas-fiduciárias)
-----------------------------------------------------------------------------------------------

Obtenha cotações atualizadas para um ou mais pares de moedas fiduciárias (ex: USD-BRL, EUR-USD).

### Funcionalidades:

* **Cotação Múltipla:** Consulte vários pares de moedas em uma única requisição usando o parâmetro `currency`.
* **Dados Retornados:** Inclui nome do par, preços de compra (bid) e venda (ask), variação, máximas e mínimas, e timestamp da atualização.

### Parâmetros:

* **`currency` (Obrigatório):** Uma lista de pares de moedas separados por vírgula, no formato `MOEDA_ORIGEM-MOEDA_DESTINO` (ex: `USD-BRL`, `EUR-USD`). Consulte os pares disponíveis em [`/api/v2/currency/available`](#/Moedas/getAvailableCurrencies).
* **`token` (Obrigatório):** Seu token de autenticação.

### Autenticação:

Requer token de autenticação válido via `token` (query) ou `Authorization` (header).

loading...

GET

/`api`/`v2`/`currency`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`currency`Requiredstring

**Obrigatório.** Uma lista de um ou mais pares de moedas a serem consultados, separados por vírgula (`,`).

* **Formato:** `MOEDA_ORIGEM-MOEDA_DESTINO` (ex: `USD-BRL`).
* **Disponibilidade:** Consulte os pares válidos usando o endpoint [`/api/v2/currency/available`](#/Moedas/getAvailableCurrencies).
* **Exemplo:** `USD-BRL,EUR-BRL,BTC-BRL`

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200400401417

Estrutura da **resposta principal** do endpoint `GET /api/v2/currency`.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`currency`Requiredarray<object>

Array contendo os objetos `CurrencyQuote`, um para cada par de moeda válido solicitado no parâmetro `currency`.

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
curl -X GET "https://brapi.dev/api/v2/currency?currency=USD-BRL%2CEUR-USD" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/currency?currency=USD-BRL%2CEUR-USD", {
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
  url := "https://brapi.dev/api/v2/currency?currency=USD-BRL%2CEUR-USD"

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

url = "https://brapi.dev/api/v2/currency?currency=USD-BRL%2CEUR-USD"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200400401417

```
{
  "currency": [
    {
      "fromCurrency": "USD",
      "toCurrency": "BRL",
      "name": "Dólar Americano/Real Brasileiro",
      "high": "5.22",
      "low": "5.162",
      "bidVariation": "0.0454",
      "percentageChange": "0.88",
      "bidPrice": "5.2097",
      "askPrice": "5.2127",
      "updatedAtTimestamp": "1696601423",
      "updatedAtDate": "2023-10-06 11:10:23"
    }
  ]
}
```

```
{
  "error": true,
  "message": "Algo deu errado ao buscar essa moeda"
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
  "message": "Não foi possível encontrar o parâmetro obrigatório: 'currency', exemplo: https://brapi.dev/api/v2/currency?currency=USD-BRL"
}
```

[Listar CriptomoedasGET

Listar criptomoedas disponíveis na brapi com informações adicionais](/docs/criptomoedas/available)[Listar MoedasGET

Listar moedas disponíveis na brapi com informações adicionais](/docs/moedas/available)