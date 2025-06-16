Cotação de Criptomoedas | Documentação brapi.dev

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

Criptomoedas

Cotação de Criptomoedas
=======================

Copiar Markdown[Ver Markdown](/docs/criptomoedas.mdx)

Endpoints focados na obtenção de dados sobre **Criptomoedas**.

Inclui consulta de cotações atuais em diversas moedas fiduciárias, dados
históricos e listagem de criptomoedas suportadas pela API.

[Buscar Cotação Detalhada de Criptomoedas](#buscar-cotação-detalhada-de-criptomoedas)
-------------------------------------------------------------------------------------

Obtenha cotações atualizadas e dados históricos para uma ou mais criptomoedas.

### Funcionalidades:

* **Cotação Múltipla:** Consulte várias criptomoedas em uma única requisição usando o parâmetro `coin`.
* **Moeda de Referência:** Especifique a moeda fiduciária para a cotação com `currency` (padrão: BRL).
* **Dados Históricos:** Solicite séries históricas usando `range` e `interval` (similar ao endpoint de ações).

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Cotação de Bitcoin (BTC) e Ethereum (ETH) em Dólar Americano (USD):**

```
curl -X GET "https://brapi.dev/api/v2/crypto?coin=BTC,ETH&currency=USD&token=SEU_TOKEN"
```

**Cotação de Cardano (ADA) em Real (BRL) com histórico do último mês (intervalo diário):**

```
curl -X GET "https://brapi.dev/api/v2/crypto?coin=ADA&currency=BRL&range=1mo&interval=1d&token=SEU_TOKEN"
```

### Resposta:

A resposta contém um array `coins`, onde cada objeto representa uma criptomoeda solicitada, incluindo sua cotação atual, dados de mercado e, opcionalmente, a série histórica (`historicalDataPrice`).

loading...

GET

/`api`/`v2`/`crypto`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`coin`Requiredstring

**Obrigatório.** Uma ou mais siglas (tickers) de criptomoedas que você deseja consultar. Separe múltiplas siglas por vírgula (`,`).

* **Exemplos:** `BTC`, `ETH,ADA`, `SOL`.

`currency`string

**Opcional.** A sigla da moeda fiduciária na qual a cotação da(s) criptomoeda(s) deve ser retornada. Se omitido, o padrão é `BRL` (Real Brasileiro).

Default: `"BRL"`

`range`string

**Opcional.** Define o período para os dados históricos de preço (`historicalDataPrice`). Funciona de forma análoga ao endpoint de ações. Se omitido, apenas a cotação mais recente é retornada (a menos que `interval` seja usado).

* Valores: `1d`, `5d`, `1mo`, `3mo`, `6mo`, `1y`, `2y`, `5y`, `10y`, `ytd`, `max`.

Value in: `"1d" | "5d" | "1mo" | "3mo" | "6mo" | "1y" | "2y" | "5y" | "10y" | "ytd" | "max"`

`interval`string

**Opcional.** Define a granularidade (intervalo) dos dados históricos de preço (`historicalDataPrice`). Requer que `range` também seja especificado. Funciona de forma análoga ao endpoint de ações.

* Valores: `1m`, `2m`, `5m`, `15m`, `30m`, `60m`, `90m`, `1h`, `1d`, `5d`, `1wk`, `1mo`, `3mo`.

Value in: `"1m" | "2m" | "5m" | "15m" | "30m" | "60m" | "90m" | "1h" | "1d" | "5d" | "1wk" | "1mo" | "3mo"`

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200400401417

Resposta principal do endpoint `/api/v2/crypto`.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`coins`array<object>

Array contendo os resultados detalhados para cada criptomoeda solicitada.

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
curl -X GET "https://brapi.dev/api/v2/crypto?coin=BTC%2CETH&currency=USD&range=1mo&interval=1d" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/crypto?coin=BTC%2CETH&currency=USD&range=1mo&interval=1d", {
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
  url := "https://brapi.dev/api/v2/crypto?coin=BTC%2CETH&currency=USD&range=1mo&interval=1d"

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

url = "https://brapi.dev/api/v2/crypto?coin=BTC%2CETH&currency=USD&range=1mo&interval=1d"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200400401417

```
{
  "coins": [
    {
      "currency": "string",
      "currencyRateFromUSD": 0.1,
      "coinName": "string",
      "coin": "string",
      "regularMarketChange": 0.1,
      "regularMarketPrice": 0.1,
      "regularMarketChangePercent": 0.1,
      "regularMarketDayLow": 0.1,
      "regularMarketDayHigh": 0.1,
      "regularMarketDayRange": "string",
      "regularMarketVolume": 0,
      "marketCap": 0,
      "regularMarketTime": "2019-08-24T14:15:22Z",
      "coinImageUrl": "string",
      "usedInterval": "string",
      "usedRange": "string",
      "historicalDataPrice": [
        {
          "date": 0,
          "open": 0.1,
          "high": 0.1,
          "low": 0.1,
          "close": 0.1,
          "volume": 0,
          "adjustedClose": 0.1
        }
      ],
      "validRanges": [
        "string"
      ],
      "validIntervals": [
        "string"
      ]
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
  "message": "Missing required parameter: `coin`"
}
```

[Cotação de todas as açõesGET

Cotação de todas as ações disponíveis na brapi](/docs/acoes/list)[Listar CriptomoedasGET

Listar criptomoedas disponíveis na brapi com informações adicionais](/docs/criptomoedas/available)