# Comece a Usar a API da brapi.dev
URL: /docs.mdx
Guia completo para começar a usar a API da brapi.dev. Aprenda sobre autenticação, endpoints principais e veja exemplos práticos para integrar dados financeiros do Brasil em suas aplicações.
\*\*\*
title: 'Comece a Usar a API da brapi.dev'
description:
'Guia completo para começar a usar a API da brapi.dev. Aprenda sobre
autenticação, endpoints principais e veja exemplos práticos para integrar
dados financeiros do Brasil em suas aplicações.'
------------------------------------------------
import { Callout } from 'fumadocs-ui/components/callout';
import { Card, Cards } from 'fumadocs-ui/components/card';
import { Step, Steps } from 'fumadocs-ui/components/steps';
import { Tab, Tabs } from 'fumadocs-ui/components/tabs';
Bem-vindo à documentação da \*\*brapi.dev\*\*. Nossa API foi projetada para ser
\*\*simples, robusta e confiável\*\*, permitindo que você integre dados financeiros
do mercado brasileiro em suas aplicações com o mínimo de esforço.
Este guia vai te mostrar como fazer sua primeira requisição em minutos.

#### 1. Obtenha sua Chave de API (Token)
Primeiro, você precisa de uma chave de API (token). Crie sua conta em nosso dashboard para gerar seu token gratuito.
Seu token estará disponível na seção "Chaves de API" do seu \*\*[Dashboard](/dashboard)\*\* após o login.

#### 2. Faça sua Primeira Requisição
Com o token em mãos, você já pode consultar a API. Vamos pegar a cotação da PETR4 como exemplo. Copie o comando abaixo, substitua `SEU\_TOKEN` pelo seu token real e execute no seu terminal.
```bash title="Terminal (cURL)"
curl --request GET \
--url 'https://brapi.dev/api/quote/PETR4' \
--header 'Authorization: Bearer SEU\_TOKEN'
```

#### 3. Receba os Dados
Pronto! Você receberá uma resposta em formato JSON, estruturada e pronta para ser utilizada.
```jsonc title="Resposta da API (JSON)"
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
## Autenticação
Todas as requisições à API devem ser autenticadas. Recomendamos enviar seu token
através do header `Authorization` por ser mais seguro.
`Authorization: Bearer SEU\_TOKEN `
`?token=SEU\_TOKEN`

Nunca exponha seu token no código do lado do cliente (frontend). Em aplicações
web, faça as chamadas para a API da brapi.dev a partir do seu backend.
## Principais Conceitos
\* \*\*URL Base:\*\* Todas as requisições usam a URL base `https://brapi.dev/api`.
\* \*\*Múltiplos Ativos:\*\* A maioria dos endpoints permite a consulta de múltiplos
ativos em uma única requisição, separando os tickers por vírgula. Ex:
`PETR4,VALE3,MGLU3`.
\* \*\*Módulos Adicionais:\*\* Use o parâmetro `modules` para enriquecer suas
respostas com dados fundamentalistas e mais (disponível conforme seu plano).
## Explore Nossos Endpoints
Navegue pelas seções para descobrir todos os dados que você pode acessar.


## Exemplos Práticos
Veja como é fácil buscar dados em diferentes linguagens.

```bash
curl -H "Authorization: Bearer SEU\_TOKEN" \
"https://brapi.dev/api/quote/ITUB4,BBDC4?range=1mo&interval=1d"
```

```python
import requests
token = "SEU\_TOKEN"
tickers = "ITUB4,BBDC4"
url = f"https://brapi.dev/api/quote/{tickers}"
response = requests.get(
url,
headers={"Authorization": f"Bearer {token}"},
params={"range": "1mo", "interval": "1d"}
)
if response.status\_code == 200:
data = response.json()
print(data['results'])
else:
print(f"Erro: {response.status\_code}")
```

```javascript
const token = 'SEU\_TOKEN';
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
## Próximos Passos
Agora que você já entendeu o básico, o que acha de explorar mais a fundo?
\* \*\*[Explore os endpoints de Ações](/docs/acoes):\*\* A seção mais completa, com
dados fundamentalistas e dividendos.
\* \*\*[Veja todos os exemplos](/docs/examples):\*\* Descubra como aplicar a API em
casos de uso mais complexos.