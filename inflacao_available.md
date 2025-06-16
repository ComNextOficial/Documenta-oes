Listar Países disponíveis | Documentação brapi.dev

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

Listar Países disponíveis
=========================

Copiar Markdown[Ver Markdown](/docs/inflacao/available.mdx)

Endpoints para acessar dados históricos de **Índices de Inflação**.

Permite consultar a inflação de diferentes países ao longo do tempo e listar os
países com dados disponíveis.

[Listar Países com Dados de Inflação Disponíveis](#listar-países-com-dados-de-inflação-disponíveis)
---------------------------------------------------------------------------------------------------

Obtenha a lista completa de todos os países para os quais a API Brapi possui dados de inflação disponíveis para consulta no endpoint `/api/v2/inflation`.

### Funcionalidade:

* Retorna um array `countries` com os nomes dos países (em minúsculas).
* Pode ser filtrado usando o parâmetro `search`.

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Listar todos os países com dados de inflação:**

```
curl -X GET "https://brapi.dev/api/v2/inflation/available?token=SEU_TOKEN"
```

**Buscar países cujo nome contenha 'arg':**

```
curl -X GET "https://brapi.dev/api/v2/inflation/available?search=arg&token=SEU_TOKEN"
```

### Resposta:

A resposta é um objeto JSON com a chave `countries`, contendo um array de strings com os nomes dos países (ex: `["brazil", "argentina", "usa"]`).

loading...

GET

/`api`/`v2`/`inflation`/`available`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`search`string

**Opcional.** Termo para filtrar a lista pelo nome do país (correspondência parcial, case-insensitive). Se omitido, retorna todos os países.

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200401404

Resposta do endpoint que lista os países com dados de inflação disponíveis.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`countries`array<string>

Lista de nomes de países (em minúsculas) para os quais há dados de inflação disponíveis (ex: `brazil`, `usa`, `argentina`).

Schema padrão para respostas de erro da API.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`error`Requiredboolean

Indica se a requisição resultou em erro. Sempre `true` para este schema.

`message`Requiredstring

Mensagem descritiva do erro ocorrido.

**Not Found.** Nenhum país encontrado correspondendo ao critério de busca (`search`) informado.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`message`string

cURLJavaScriptGoPython

```
curl -X GET "https://brapi.dev/api/v2/inflation/available?search=bra" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/inflation/available?search=bra", {
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
  url := "https://brapi.dev/api/v2/inflation/available?search=bra"

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

url = "https://brapi.dev/api/v2/inflation/available?search=bra"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200401404

```
{
  "countries": [
    "brazil"
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

[InflaçãoGET

Inflação Brasil com dados de IPCA, IGP-M e outros índices](/docs/inflacao)[Taxa SelicGET

Taxa básica de juros do Brasil com dados históricos e atuais](/docs/taxa-basica-de-juros)