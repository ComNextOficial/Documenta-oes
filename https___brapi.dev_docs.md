Documentação | brapi.dev

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

Geral

Comece a Usar a API da brapi.dev
================================

Copiar Markdown[Ver Markdown](/docs.mdx)

Bem-vindo à documentação da **brapi.dev**. Nossa API foi projetada para ser
**simples, robusta e confiável**, permitindo que você integre dados financeiros
do mercado brasileiro em suas aplicações com o mínimo de esforço.

Este guia vai te mostrar como fazer sua primeira requisição em minutos.

#### [1. Obtenha sua Chave de API (Token)](#1-obtenha-sua-chave-de-api-token)

Primeiro, você precisa de uma chave de API (token). Crie sua conta em nosso dashboard para gerar seu token gratuito.

Onde encontrar seu token?

Seu token estará disponível na seção "Chaves de API" do seu **[Dashboard](/dashboard)** após o login.

#### [2. Faça sua Primeira Requisição](#2-faça-sua-primeira-requisição)

Com o token em mãos, você já pode consultar a API. Vamos pegar a cotação da PETR4 como exemplo. Copie o comando abaixo, substitua `SEU_TOKEN` pelo seu token real e execute no seu terminal.

Terminal (cURL)

```
curl --request GET \
  --url 'https://brapi.dev/api/quote/PETR4' \
  --header 'Authorization: Bearer SEU_TOKEN'
```

#### [3. Receba os Dados](#3-receba-os-dados)

Pronto! Você receberá uma resposta em formato JSON, estruturada e pronta para ser utilizada.

Resposta da API (JSON)

```
{
  "results": [
    {
      "symbol": "PETR4",
      "shortName": "PETROBRAS PN",
      "longName": "Petróleo Brasileiro S.A. - Petrobras",
      "currency": "BRL",
      "regularMarketPrice": 38.50,
      "regularMarketDayHigh": 39.00,
      "regularMarketDayLow": 38.20,
      "regularMarketChange": 0.30,
      "regularMarketChangePercent": 0.78,
      "regularMarketTime": "2024-10-26T17:08:00.000Z",
      "marketCap": 503100000000,
      "regularMarketVolume": 45678901,
      "logourl": "https://icons.brapi.dev/logos/PETR4.png",
    }
  ]
}
```

[Autenticação](#autenticação)
-----------------------------

Todas as requisições à API devem ser autenticadas. Recomendamos enviar seu token
através do header `Authorization` por ser mais seguro.

Header (Recomendado)Query Param

`Authorization: Bearer SEU_TOKEN`

`?token=SEU_TOKEN`

Atenção

Nunca exponha seu token no código do lado do cliente (frontend). Em aplicações
web, faça as chamadas para a API da brapi.dev a partir do seu backend.

[Principais Conceitos](#principais-conceitos)
---------------------------------------------

* **URL Base:** Todas as requisições usam a URL base `https://brapi.dev/api`.
* **Múltiplos Ativos:** A maioria dos endpoints permite a consulta de múltiplos
  ativos em uma única requisição, separando os tickers por vírgula. Ex:
  `PETR4,VALE3,MGLU3`.
* **Módulos Adicionais:** Use o parâmetro `modules` para enriquecer suas
  respostas com dados fundamentalistas e mais (disponível conforme seu plano).

[Explore Nossos Endpoints](#explore-nossos-endpoints)
-----------------------------------------------------

Navegue pelas seções para descobrir todos os dados que você pode acessar.

[### Ações e Fundos

Obtenha cotações, dados históricos, dividendos e fundamentos de Ações, FIIs, ETFs e BDRs.](/docs/acoes)[### Criptomoedas

Acesse cotações e informações das principais criptomoedas do mercado.](/docs/criptomoedas)[### Moedas (Câmbio)

Consulte taxas de câmbio atualizadas para mais de 50 pares de moedas.](/docs/moedas)[### Inflação

Acesse séries históricas de indicadores de inflação como IPCA e IGP-M.](/docs/inflacao)[### Taxa SELIC

Consulte a série histórica da taxa básica de juros do Brasil.](/docs/taxa-basica-de-juros)[### Exemplos

Veja exemplos práticos de como usar a API em diferentes cenários e linguagens.](/docs/examples)

[Exemplos Práticos](#exemplos-práticos)
---------------------------------------

Veja como é fácil buscar dados em diferentes linguagens.

cURLPythonJavaScript

```
curl -H "Authorization: Bearer SEU_TOKEN" \
  "https://brapi.dev/api/quote/ITUB4,BBDC4?range=1mo&interval=1d"
```

```
import requests

token = "SEU_TOKEN"
tickers = "ITUB4,BBDC4"
url = f"https://brapi.dev/api/quote/{tickers}"

response = requests.get(
    url,
    headers={"Authorization": f"Bearer {token}"},
    params={"range": "1mo", "interval": "1d"}
)

if response.status_code == 200:
    data = response.json()
    print(data['results'])
else:
    print(f"Erro: {response.status_code}")
```

```
const token = 'SEU_TOKEN';
const tickers = 'ITUB4,BBDC4';
const url = `https://brapi.dev/api/quote/${tickers}?range=1mo&interval=1d`;

async function fetchQuotes() {
  try {
    const response = await fetch(url, {
      headers: {
        'Authorization': `Bearer ${token}`
      }
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    console.log(data.results);
  } catch (error) {
    console.error('Falha ao buscar cotações:', error);
  }
}

fetchQuotes();
```

[Próximos Passos](#próximos-passos)
-----------------------------------

Agora que você já entendeu o básico, o que acha de explorar mais a fundo?

* **[Explore os endpoints de Ações](/docs/acoes):** A seção mais completa, com
  dados fundamentalistas e dividendos.
* **[Veja todos os exemplos](/docs/examples):** Descubra como aplicar a API em
  casos de uso mais complexos.

[Cotação, Dividendos e Dados FinanceirosGET

Ações disponíveis na brapi](/docs/acoes)

### On this page

[1. Obtenha sua Chave de API (Token)](#1-obtenha-sua-chave-de-api-token)[2. Faça sua Primeira Requisição](#2-faça-sua-primeira-requisição)[3. Receba os Dados](#3-receba-os-dados)[Autenticação](#autenticação)[Principais Conceitos](#principais-conceitos)[Explore Nossos Endpoints](#explore-nossos-endpoints)[Exemplos Práticos](#exemplos-práticos)[Próximos Passos](#próximos-passos)