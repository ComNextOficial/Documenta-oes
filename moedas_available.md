Listar Moedas | Documentação brapi.dev

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

Listar Moedas
=============

Copiar Markdown[Ver Markdown](/docs/moedas/available.mdx)

Endpoints para consulta de **Moedas Fiduciárias**.

Atualmente, focado na listagem das moedas disponíveis para conversão ou consulta
de taxas de câmbio (embora o endpoint de cotação de moedas não esteja detalhado
aqui, a listagem está disponível).

[Listar Todas as Moedas Fiduciárias Disponíveis](#listar-todas-as-moedas-fiduciárias-disponíveis)
-------------------------------------------------------------------------------------------------

Obtenha a lista completa de todas as moedas fiduciárias suportadas pela API, geralmente utilizadas no parâmetro `currency` de outros endpoints (como o de criptomoedas) ou para futuras funcionalidades de conversão.

### Funcionalidade:

* Retorna um array `currencies` com os nomes das moedas.
* Pode ser filtrado usando o parâmetro `search`.

### Autenticação:

Requer token de autenticação via `token` (query) ou `Authorization` (header).

### Exemplo de Requisição:

**Listar todas as moedas disponíveis:**

```
curl -X GET "https://brapi.dev/api/v2/currency/available?token=SEU_TOKEN"
```

**Buscar moedas cujo nome contenha 'Euro':**

```
curl -X GET "https://brapi.dev/api/v2/currency/available?search=Euro&token=SEU_TOKEN"
```

### Resposta:

A resposta é um objeto JSON com a chave `currencies`, contendo um array de objetos. Cada objeto possui uma chave `currency` com o nome completo da moeda (ex: `"Dólar Americano/Real Brasileiro"`). **Nota:** O formato do nome pode indicar um par de moedas, dependendo do contexto interno da API.

loading...

GET

/`api`/`v2`/`currency`/`available`

Send

Headers

Query

### [Authorization](#authorization)

`Authorization`RequiredBearer <token>

Autenticação via header HTTP `Authorization`. Use o formato `Authorization: Bearer SEU_TOKEN`. [Obtenha seu token](https://brapi.dev/dashboard).

In: `header`

### [Query Parameters](#query-parameters)

`search`string

**Opcional.** Termo para filtrar a lista pelo nome da moeda (correspondência parcial, case-insensitive).

`token`string

**Obrigatório caso não esteja adicionado como header "Authorization".** Seu token de autenticação pessoal da API Brapi.

**Formas de Envio:**

1. **Query Parameter:** Adicione `?token=SEU_TOKEN` ao final da URL.
2. **HTTP Header:** Inclua o header `Authorization: Bearer SEU_TOKEN` na sua requisição.

Ambos os métodos são aceitos, mas pelo menos um deles deve ser utilizado. Obtenha seu token em [brapi.dev/dashboard](https://brapi.dev/dashboard).

### [Response Body](#response-body)

200401404

Resposta do endpoint que lista todas as moedas fiduciárias disponíveis.

TypeScript Definitions

Use the response body type in TypeScript.

Copy

`currencies`array<object>

Lista de objetos, cada um contendo o nome de uma moeda fiduciária ou par suportado pela API.

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

cURLJavaScriptGoPython

```
curl -X GET "https://brapi.dev/api/v2/currency/available?search=Real" \
  -H "Authorization: Bearer <token>"
```

```
fetch("https://brapi.dev/api/v2/currency/available?search=Real", {
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
  url := "https://brapi.dev/api/v2/currency/available?search=Real"

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

url = "https://brapi.dev/api/v2/currency/available?search=Real"

response = requests.request("GET", url, headers = {
  "Authorization": "Bearer <token>"
})

print(response.text)
```

200401404

```
{
  "currencies": [
    {
      "name": "USD-BRL",
      "currency": "Dólar Americano/Real Brasileiro"
    },
    {
      "name": "EUR-BRL",
      "currency": "Euro/Real Brasileiro"
    }
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
  "error": true,
  "message": "Currency not found"
}
```

[Cotação de MoedasGET

Cotação de todas as moedas disponíveis na brapi](/docs/moedas)[InflaçãoGET

Inflação Brasil com dados de IPCA, IGP-M e outros índices](/docs/inflacao)