Cotação de todas as ações | Documentação brapi.dev

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

Cotação de todas as ações
=========================

Copiar Markdown[Ver Markdown](/docs/acoes/list.mdx)

Endpoints para consulta de dados relacionados a ativos negociados na B3, como
**Ações**, **Fundos Imobiliários (FIIs)**, **BDRs**, **ETFs** e **Índices** (ex:
IBOVESPA).

Permite buscar cotações atuais, dados históricos, informações fundamentalistas
(via módulos) e listagens de ativos disponíveis.

[Listar e Filtrar Cotações de Ativos](#listar-e-filtrar-cotações-de-ativos)
---------------------------------------------------------------------------

Obtenha uma lista paginada de cotações de diversos ativos (ações, FIIs, BDRs) negociados na B3, com opções avançadas de busca, filtragem e ordenação.

### Funcionalidades:

* **Busca por Ticker:** Filtre por parte do ticker usando `search`.
* **Filtragem por Tipo:** Restrinja a lista a `stock`, `fund` (FII) ou `bdr` com o parâmetro `type`.
* **Filtragem por Setor:** Selecione ativos de um setor específico usando `sector`.
* **Ordenação:** Ordene os resultados por diversos campos (preço, variação, volume, etc.) usando `sortBy` e `sortOrder`.
* **Paginação:** Controle o número de resultados por página (`limit`) e a página desejada (`page`).

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Listar as 10 ações do setor Financeiro com maior volume, ordenadas de forma decrescente:**

```
curl -X GET "https://brapi.dev/api/quote/list?sector=Finance&sortBy=volume&sortOrder=desc&limit=10&page=1&token=SEU_TOKEN"
```

**Buscar por ativos cujo ticker contenha 'ITUB' e ordenar por nome ascendente:**

```
curl -X GET "https://brapi.dev/api/quote/list?search=ITUB&sortBy=name&sortOrder=asc&token=SEU_TOKEN"
```

### Resposta:

A resposta contém a lista de `stocks` (e `indexes` relevantes), informações sobre os filtros aplicados, detalhes da paginação (`currentPage`, `totalPages`, `itemsPerPage`, `totalCount`, `hasNextPage`) e listas de setores (`availableSectors`) e tipos (`availableStockTypes`) disponíveis para filtragem.

loading...

GET

/`api`/`quote`/`list`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`search`string

**Opcional.** Termo para buscar ativos por ticker (correspondência parcial). Ex: `PETR` encontrará `PETR4`, `PETR3`.

`sortBy`string

**Opcional.** Campo pelo qual os resultados serão ordenados.

Value in: `"name" | "close" | "change" | "change_abs" | "volume" | "market_cap_basic" | "sector"`

`sortOrder`string

**Opcional.** Direção da ordenação: `asc` (ascendente) ou `desc` (descendente). Requer que `sortBy` seja especificado.

Value in: `"asc" | "desc"`

`limit`integer

**Opcional.** Número máximo de ativos a serem retornados por página. O valor padrão pode variar.

Minimum: `1`

`page`integer

**Opcional.** Número da página dos resultados a ser retornada, considerando o `limit` especificado. Começa em 1.

Minimum: `1`

`type`string

**Opcional.** Filtra os resultados por tipo de ativo.

Value in: `"stock" | "fund" | "bdr"`

`sector`string

**Opcional.** Filtra os resultados por setor de atuação da empresa. Utilize um dos valores retornados em `availableSectors`.

Value in: `"Retail Trade" | "Energy Minerals" | "Health Services" | "Utilities" | "Finance" | "Consumer Services" | "Consumer Non-Durables" | "Non-Energy Minerals" | "Commercial Services" | "Distribution Services" | "Transportation" | "Technology Services" | "Process Industries" | "Communications" | "Producer Manufacturing" | "Miscellaneous" | "Electronic Technology" | "Industrial Services" | "Health Technology" | "Consumer Durables"`

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200401417

Resposta do endpoint de listagem de cotações (`/api/quote/list`).

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`indexes`array<object>

Lista resumida de índices relevantes (geralmente inclui IBOVESPA).

Show Attributes

`stocks`array<object>

Lista paginada e filtrada dos ativos solicitados.

Show Attributes

`availableSectors`array<string>

Lista de todos os setores disponíveis que podem ser usados no parâmetro de filtro `sector`.

`availableStockTypes`array<string>

Lista dos tipos de ativos (`stock`, `fund`, `bdr`) disponíveis que podem ser usados no parâmetro de filtro `type`.

`currentPage`integer

Número da página atual retornada nos resultados.

`totalPages`integer

Número total de páginas existentes para a consulta/filtros aplicados.

`itemsPerPage`integer

Número de itens (ativos) retornados por página (conforme `limit` ou padrão).

`totalCount`integer

Número total de ativos encontrados que correspondem aos filtros aplicados (sem considerar a paginação).

`hasNextPage`boolean

Indica se existe uma próxima página de resultados (`true`) ou se esta é a última página (`false`).

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
curl -X GET "https://brapi.dev/api/quote/list?search=PETR&sortBy=close&sortOrder=desc&limit=10&page=1&type=stock&sector=Energy+Minerals" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/quote/list?search=PETR&sortBy=close&sortOrder=desc&limit=10&page=1&type=stock&sector=Energy+Minerals", {
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
  url := "https://brapi.dev/api/quote/list?search=PETR&sortBy=close&sortOrder=desc&limit=10&page=1&type=stock&sector=Energy+Minerals"

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

url = "https://brapi.dev/api/quote/list?search=PETR&sortBy=close&sortOrder=desc&limit=10&page=1&type=stock&sector=Energy+Minerals"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200401417

### Example success

```
{
  "indexes": [
    {
      "stock": "^BVSP",
      "name": "IBOVESPA"
    }
  ],
  "stocks": [
    {
      "stock": "PETR4",
      "name": "PETROBRAS PN",
      "close": 36.71,
      "change": 3.26,
      "volume": 87666300,
      "market_cap": 497695817728,
      "logo": "https://icons.brapi.dev/icons/PETR4.svg",
      "sector": "Energy Minerals",
      "type": "stock"
    }
  ],
  "availableSectors": [
    "Energy Minerals",
    "Finance",
    "..."
  ],
  "availableStockTypes": [
    "stock",
    "fund",
    "bdr"
  ],
  "currentPage": 1,
  "totalPages": 5,
  "itemsPerPage": 10,
  "totalCount": 45,
  "hasNextPage": true
}
```

### Nenhum ativo encontrado com os filtros aplicados

```
{
  "error": true,
  "message": "O seu token é inválido, por favor, verifique o seu token em brapi.dev/dashboard"
}
```

```
{
  "error": true,
  "message": "Campo 'sortBy' inválido. sortBy válidos: name, close, change, change_abs, volume, market_cap_basic, sector"
}
```

[Cotação, Dividendos e Dados FinanceirosGET

Ações disponíveis na brapi](/docs/acoes)[Cotação de CriptomoedasGET

Cotação de todas as criptomoedas disponíveis na brapi](/docs/criptomoedas)