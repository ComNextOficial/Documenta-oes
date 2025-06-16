Listar Criptomoedas | Documentação brapi.dev

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

Listar Criptomoedas
===================

Copiar Markdown[Ver Markdown](/docs/criptomoedas/available.mdx)

Endpoints focados na obtenção de dados sobre **Criptomoedas**.

Inclui consulta de cotações atuais em diversas moedas fiduciárias, dados
históricos e listagem de criptomoedas suportadas pela API.

[Listar Todas as Criptomoedas Disponíveis](#listar-todas-as-criptomoedas-disponíveis)
-------------------------------------------------------------------------------------

Obtenha a lista completa de todas as siglas (tickers) de criptomoedas que a API Brapi suporta para consulta no endpoint `/api/v2/crypto`.

### Funcionalidade:

* Retorna um array `coins` com as siglas.
* Pode ser filtrado usando o parâmetro `search`.

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Listar todas as criptomoedas disponíveis:**

```
curl -X GET "https://brapi.dev/api/v2/crypto/available?token=SEU_TOKEN"
```

**Buscar criptomoedas cujo ticker contenha 'DOGE':**

```
curl -X GET "https://brapi.dev/api/v2/crypto/available?search=DOGE&token=SEU_TOKEN"
```

### Resposta:

A resposta é um objeto JSON com a chave `coins`, contendo um array de strings com as siglas das criptomoedas (ex: `["BTC", "ETH", "LTC", "XRP"]`).

loading...

GET

/`api`/`v2`/`crypto`/`available`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`search`string

**Opcional.** Termo para filtrar a lista de siglas de criptomoedas (correspondência parcial, case-insensitive). Se omitido, retorna todas as siglas.

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200401404

Resposta do endpoint que lista todas as criptomoedas disponíveis.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`coins`array<string>

Lista de siglas (tickers) das criptomoedas disponíveis (ex: `BTC`, `ETH`, `LTC`).

Schema padrão para respostas de erro da API.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`error`Requiredboolean

Indica se a requisição resultou em erro. Sempre `true` para este schema.

`message`Requiredstring

Mensagem descritiva do erro ocorrido.

**Not Found.** Nenhuma criptomoeda encontrada correspondendo ao critério de busca (`search`) informado.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`message`string

cURLJavaScriptGoPython

```
curl -X GET "https://brapi.dev/api/v2/crypto/available?search=BTC" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/crypto/available?search=BTC", {
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
  url := "https://brapi.dev/api/v2/crypto/available?search=BTC"

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

url = "https://brapi.dev/api/v2/crypto/available?search=BTC"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200401404

```
{
  "coins": [
    "BTC",
    "ETH",
    "LTC"
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
  "message": "Coin not found"
}
```

[Cotação de CriptomoedasGET

Cotação de todas as criptomoedas disponíveis na brapi](/docs/criptomoedas)[Cotação de MoedasGET

Cotação de todas as moedas disponíveis na brapi](/docs/moedas)