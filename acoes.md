Cotação, Dividendos e Dados Financeiros | Documentação brapi.dev

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

Ações

Cotação, Dividendos e Dados Financeiros
=======================================

Copiar Markdown[Ver Markdown](/docs/acoes.mdx)

Endpoints para consulta de dados relacionados a ativos negociados na B3, como
**Ações**, **Fundos Imobiliários (FIIs)**, **BDRs**, **ETFs** e **Índices** (ex:
IBOVESPA).

Permite buscar cotações atuais, dados históricos, informações fundamentalistas
(via módulos) e listagens de ativos disponíveis.

[Buscar Cotação Detalhada de Ativos Financeiros](#buscar-cotação-detalhada-de-ativos-financeiros)
-------------------------------------------------------------------------------------------------

Este endpoint é a principal forma de obter informações detalhadas sobre um ou mais ativos financeiros (ações, FIIs, ETFs, BDRs, índices) listados na B3, identificados pelos seus respectivos **tickers**.

### Funcionalidades Principais:

* **Cotação Atual:** Retorna o preço mais recente, variação diária, máximas, mínimas, volume, etc.
* **Dados Históricos:** Permite solicitar séries históricas de preços usando os parâmetros `range` e `interval`.
* **Dados Fundamentalistas:** Opcionalmente, inclui dados fundamentalistas básicos (P/L, LPA) com o parâmetro `fundamental=true`.
* **Dividendos:** Opcionalmente, inclui histórico de dividendos e JCP com `dividends=true`.
* **Módulos Adicionais:** Permite requisitar conjuntos de dados financeiros mais aprofundados através do parâmetro `modules` (veja detalhes abaixo).

### Autenticação:

É **obrigatório** fornecer um token de autenticação válido, seja via query parameter `token` ou via header `Authorization: Bearer seu_token`.

### Exemplos de Requisição:

**1. Cotação simples de PETR4 e VALE3:**

```
curl -X GET "https://brapi.dev/api/quote/PETR4,VALE3?token=SEU_TOKEN"
```

**2. Cotação de MGLU3 com dados históricos do último mês (intervalo diário):**

```
curl -X GET "https://brapi.dev/api/quote/MGLU3?range=1mo&interval=1d&token=SEU_TOKEN"
```

**3. Cotação de ITSA4 incluindo dividendos e dados fundamentalistas básicos:**

```
curl -X GET "https://brapi.dev/api/quote/ITSA4?fundamental=true&dividends=true&token=SEU_TOKEN"
```

**4. Cotação de WEGE3 com Resumo da Empresa e Balanço Patrimonial Anual (via módulos):**

```
curl -X GET "https://brapi.dev/api/quote/WEGE3?modules=summaryProfile,balanceSheetHistory&token=SEU_TOKEN"
```

### Parâmetro `modules` (Detalhado):

O parâmetro `modules` é extremamente poderoso para enriquecer a resposta com dados financeiros detalhados. Você pode solicitar um ou mais módulos, separados por vírgula.

**Módulos Disponíveis:**

* `summaryProfile`: Informações cadastrais da empresa (endereço, setor, descrição do negócio, website, número de funcionários).
* `balanceSheetHistory`: Histórico **anual** do Balanço Patrimonial.
* `balanceSheetHistoryQuarterly`: Histórico **trimestral** do Balanço Patrimonial.
* `defaultKeyStatistics`: Principais estatísticas da empresa (Valor de Mercado, P/L, ROE, Dividend Yield, etc.) - **TTM (Trailing Twelve Months)**.
* `defaultKeyStatisticsHistory`: Histórico **anual** das Principais Estatísticas.
* `defaultKeyStatisticsHistoryQuarterly`: Histórico **trimestral** das Principais Estatísticas.
* `incomeStatementHistory`: Histórico **anual** da Demonstração do Resultado do Exercício (DRE).
* `incomeStatementHistoryQuarterly`: Histórico **trimestral** da Demonstração do Resultado do Exercício (DRE).
* `financialData`: Dados financeiros selecionados (Receita, Lucro Bruto, EBITDA, Dívida Líquida, Fluxo de Caixa Livre, Margens) - **TTM (Trailing Twelve Months)**.
* `financialDataHistory`: Histórico **anual** dos Dados Financeiros.
* `financialDataHistoryQuarterly`: Histórico **trimestral** dos Dados Financeiros.
* `valueAddedHistory`: Histórico **anual** da Demonstração do Valor Adicionado (DVA).
* `valueAddedHistoryQuarterly`: Histórico **trimestral** da Demonstração do Valor Adicionado (DVA).
* `cashflowHistory`: Histórico **anual** da Demonstração do Fluxo de Caixa (DFC).
* `cashflowHistoryQuarterly`: Histórico **trimestral** da Demonstração do Fluxo de Caixa (DFC).

**Exemplo de Uso do `modules`:**

Para obter a cotação de BBDC4 junto com seu DRE trimestral e Fluxo de Caixa anual:

```
curl -X GET "https://brapi.dev/api/quote/BBDC4?modules=incomeStatementHistoryQuarterly,cashflowHistory&token=SEU_TOKEN"
```

### Resposta:

A resposta é um objeto JSON contendo a chave `results`, que é um array. Cada elemento do array corresponde a um ticker solicitado e contém os dados da cotação e os módulos adicionais requisitados.

* **Sucesso (200 OK):** Retorna os dados conforme solicitado.
* **Bad Request (400 Bad Request):** Ocorre se um parâmetro for inválido (ex: `range=invalid`) ou se a formatação estiver incorreta.
* **Unauthorized (401 Unauthorized):** Token inválido ou ausente.
* **Payment Required (402 Payment Required):** Limite de requisições do plano atual excedido.
* **Not Found (404 Not Found):** Um ou mais tickers solicitados não foram encontrados.

loading...

GET

/`api`/`quote`/`{tickers}`

Send

Headers

Query

Path

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Path Parameters](#path-parameters)

`tickers`Requiredstring

**Obrigatório.** Um ou mais tickers de ativos financeiros (ações, FIIs, índices, etc.) que você deseja consultar.

* **Múltiplos Tickers:** Separe-os por vírgula (`,`).
* **Exemplos:** `PETR4`, `ITSA4,MGLU3`, `^BVSP` (para o índice Ibovespa).

### [Query Parameters](#query-parameters)

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

`range`string

**Opcional.** Define o período para os dados históricos de preço (`historicalDataPrice`). Se omitido, apenas a cotação mais recente é retornada (a menos que `interval` seja usado).

**Valores Possíveis:**

* `1d`: Último dia de pregão (intraday se `interval` for minutos/horas).
* `5d`: Últimos 5 dias.
* `1mo`: Último mês.
* `3mo`: Últimos 3 meses.
* `6mo`: Últimos 6 meses.
* `1y`: Último ano.
* `2y`: Últimos 2 anos.
* `5y`: Últimos 5 anos.
* `10y`: Últimos 10 anos.
* `ytd`: Desde o início do ano atual (Year-to-Date).
* `max`: Todo o período histórico disponível.

Value in: `"1d" | "5d" | "1mo" | "3mo" | "6mo" | "1y" | "2y" | "5y" | "10y" | "ytd" | "max"`

`interval`string

**Opcional.** Define a granularidade (intervalo) dos dados históricos de preço (`historicalDataPrice`). Requer que `range` também seja especificado.

**Valores Possíveis:**

* `1m`, `2m`, `5m`, `15m`, `30m`, `60m`, `90m`, `1h`: Intervalos intraday (minutos/horas). **Atenção:** Disponibilidade pode variar conforme o `range` e o ativo.
* `1d`: Diário (padrão se `range` for especificado e `interval` omitido).
* `5d`: 5 dias.
* `1wk`: Semanal.
* `1mo`: Mensal.
* `3mo`: Trimestral.

Value in: `"1m" | "2m" | "5m" | "15m" | "30m" | "60m" | "90m" | "1h" | "1d" | "5d" | "1wk" | "1mo" | "3mo"`

`fundamental`boolean

**Opcional.** Booleano (`true` ou `false`). Se `true`, inclui dados fundamentalistas básicos na resposta, como Preço/Lucro (P/L) e Lucro Por Ação (LPA).

**Nota:** Para dados fundamentalistas mais completos, utilize o parâmetro `modules`.

`dividends`boolean

**Opcional.** Booleano (`true` ou `false`). Se `true`, inclui informações sobre dividendos e JCP (Juros sobre Capital Próprio) pagos historicamente pelo ativo na chave `dividendsData`.

`modules`string

**Opcional.** Uma lista de módulos de dados adicionais, separados por vírgula (`,`), para incluir na resposta. Permite buscar dados financeiros detalhados.

**Exemplos:**

* `modules=summaryProfile` (retorna perfil da empresa)
* `modules=balanceSheetHistory,incomeStatementHistory` (retorna histórico anual do BP e DRE)

Veja a descrição principal do endpoint para a lista completa de módulos e seus conteúdos.

### [Response Body](#response-body)

200400401402404

Resposta principal do endpoint `/api/quote/{tickers}`.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`results`array<object>

Array contendo os resultados detalhados para cada ticker solicitado.

Show Attributes

`requestedAt`string

Timestamp indicando quando a requisição foi recebida pelo servidor. Formato ISO 8601.

Format: `"date-time"`

`took`string

Tempo aproximado que o servidor levou para processar a requisição, em formato de string (ex: `746ms`).

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
curl -X GET "https://brapi.dev/api/quote/PETR4,^BVSP?range=1d&interval=1m&fundamental=true&dividends=true&modules=summaryProfile%2CbalanceSheetHistory" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/quote/PETR4,^BVSP?range=1d&interval=1m&fundamental=true&dividends=true&modules=summaryProfile%2CbalanceSheetHistory", {
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
  url := "https://brapi.dev/api/quote/PETR4,^BVSP?range=1d&interval=1m&fundamental=true&dividends=true&modules=summaryProfile%2CbalanceSheetHistory"

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

url = "https://brapi.dev/api/quote/PETR4,^BVSP?range=1d&interval=1m&fundamental=true&dividends=true&modules=summaryProfile%2CbalanceSheetHistory"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200400401402404

```
{
  "results": [
    {
      "symbol": "PETR4",
      "currency": "BRL",
      "twoHundredDayAverage": 29.55485,
      "twoHundredDayAverageChange": 7.1551495,
      "twoHundredDayAverageChangePercent": 0.2420973,
      "marketCap": 497695817728,
      "shortName": "PETROBRAS   PN      N2",
      "longName": "Petróleo Brasileiro S.A. - Petrobras",
      "regularMarketChange": 1.1599998,
      "regularMarketChangePercent": 3.2630093,
      "regularMarketTime": "2023-11-17T21:07:47.000Z",
      "regularMarketPrice": 36.71,
      "regularMarketDayHigh": 36.82,
      "regularMarketDayRange": "35.51 - 36.82",
      "regularMarketDayLow": 35.51,
      "regularMarketVolume": 87666300,
      "regularMarketPreviousClose": 35.55,
      "regularMarketOpen": 35.83,
      "averageDailyVolume3Month": 49987483,
      "averageDailyVolume10Day": 54835377,
      "fiftyTwoWeekLowChange": 36.71,
      "fiftyTwoWeekRange": "32.21 - 38.86",
      "fiftyTwoWeekHighChange": -2.1500015,
      "fiftyTwoWeekHighChangePercent": -0.055326853,
      "fiftyTwoWeekLow": 32.21,
      "fiftyTwoWeekHigh": 38.86,
      "priceEarnings": 3.49722289,
      "earningsPerShare": 10.4968915,
      "logourl": "https://icons.brapi.dev/icons/PETR4.svg",
      "usedInterval": "1d",
      "usedRange": "5d",
      "historicalDataPrice": [
        {
          "date": 1699621200,
          "open": 34.66,
          "high": 35.06,
          "low": 34.51,
          "close": 34.72,
          "volume": 40004800,
          "adjustedClose": 34.72
        }
      ],
      "validRanges": [
        "1d",
        "5d",
        "7d",
        "1mo",
        "3mo",
        "6mo",
        "1y",
        "2y",
        "5y",
        "10y",
        "ytd",
        "max"
      ],
      "validIntervals": [
        "1m",
        "2m",
        "5m",
        "15m",
        "30m",
        "60m",
        "90m",
        "1h",
        "1d",
        "5d",
        "1wk",
        "1mo",
        "3mo"
      ],
      "balanceSheetHistory": [
        {
          "type": "yearly",
          "endDate": "2024-12-31",
          "cash": 20254000000,
          "shortTermInvestments": 26397000000,
          "netReceivables": 22080000000,
          "inventory": 41550000000,
          "otherCurrentAssets": 12756000000,
          "totalCurrentAssets": 135212000000,
          "longTermInvestments": 4081000000,
          "propertyPlantEquipment": 843917000000,
          "otherAssets": 989585000000,
          "totalAssets": 1124797000000,
          "accountsPayable": 37659000000,
          "shortLongTermDebt": 68783000000,
          "otherCurrentLiab": 4418000000,
          "longTermDebt": 304684000000,
          "otherLiab": 3284000000,
          "totalCurrentLiabilities": 194808000000,
          "totalLiab": 1124797000000,
          "commonStock": 205432000000,
          "retainedEarnings": null,
          "treasuryStock": null,
          "otherStockholderEquity": -2457000000,
          "totalStockholderEquity": 367514000000,
          "netTangibleAssets": null,
          "goodWill": null,
          "intangibleAssets": 13961000000,
          "deferredLongTermAssetCharges": null,
          "deferredLongTermLiab": 9100000000,
          "minorityInterest": 1508000000,
          "capitalSurplus": null
        }
      ],
      "dividendsData": {
        "cashDividends": [
          {
            "assetIssued": "BRPETRACNPR6",
            "paymentDate": "2023-11-22T13:00:00.000Z",
            "rate": 1.345348,
            "relatedTo": "4º Trimestre/2023",
            "approvedOn": "2023-11-22T13:00:00.000Z",
            "isinCode": "BRPETRACNPR6",
            "label": "DIVIDENDO",
            "lastDatePrior": "2023-11-22T13:00:00.000Z",
            "remarks": ""
          }
        ],
        "stockDividends": [],
        "subscriptions": []
      }
    },
    {
      "symbol": "^BVSP",
      "currency": "BRL",
      "twoHundredDayAverage": 111633.99,
      "twoHundredDayAverageChange": 3522.0781,
      "twoHundredDayAverageChangePercent": 0.03155023,
      "marketCap": null,
      "shortName": "IBOVESPA",
      "longName": "IBOVESPA",
      "regularMarketChange": 986.4375,
      "regularMarketChangePercent": 0.8640104,
      "regularMarketTime": "2023-10-09T20:19:00.000Z",
      "regularMarketPrice": 115156.07,
      "regularMarketDayHigh": 115218.65,
      "regularMarketDayRange": "113448.18 - 115218.65",
      "regularMarketDayLow": 113448.18,
      "regularMarketVolume": 0,
      "regularMarketPreviousClose": 114169.63,
      "regularMarketOpen": 114168.99,
      "averageDailyVolume3Month": 10704804,
      "averageDailyVolume10Day": 10880020,
      "fiftyTwoWeekLowChange": 18159.07,
      "fiftyTwoWeekLowChangePercent": 0.1872127,
      "fiftyTwoWeekRange": "96997.0 - 123010.0",
      "fiftyTwoWeekHighChange": -7853.9297,
      "fiftyTwoWeekHighChangePercent": -0.0638479,
      "fiftyTwoWeekLow": 96997,
      "fiftyTwoWeekHigh": 123010,
      "priceEarnings": null,
      "earningsPerShare": null,
      "logourl": "https://brapi.dev/favicon.svg",
      "updatedAt": "2023-10-10T00:45:08.312Z",
      "historicalDataPrice": [
        {
          "date": 1696338000,
          "open": 115055,
          "high": 115056,
          "low": 113151,
          "close": 113419,
          "volume": 11104800,
          "adjustedClose": 113419
        }
      ],
      "validRanges": [
        "1d",
        "5d",
        "1mo",
        "3mo",
        "6mo",
        "1y",
        "2y",
        "5y",
        "10y",
        "ytd",
        "max"
      ],
      "validIntervals": [
        "1m",
        "2m",
        "5m",
        "15m",
        "30m",
        "60m",
        "90m",
        "1h",
        "1d",
        "5d",
        "1wk",
        "1mo",
        "3mo"
      ],
      "dividendsData": {}
    }
  ],
  "requestedAt": "2023-11-19T23:55:24.958Z",
  "took": "746ms"
}
```

```
{
  "error": true,
  "message": "Campo 'range' inválido. Ranges válidos: 1d, 5d, 1mo, 3mo, 6mo, 1y, 2y, 5y, 10y, ytd, max"
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
  "message": "Você atingiu o limite de requisições para o seu plano. Por favor, considere fazer um upgrade para um plano melhor em brapi.dev/dashboard"
}
```

```
{
  "error": true,
  "message": "Não encontramos a ação G3X"
}
```

[Geral

Introdução à API da brapi](/docs)[Cotação de todas as açõesGET

Cotação de todas as ações disponíveis na brapi](/docs/acoes/list)