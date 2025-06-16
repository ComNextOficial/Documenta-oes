Exemplos de Integração | Documentação brapi.dev

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

Exemplos

Exemplos de Integração
======================

Copiar Markdown[Ver Markdown](/docs/examples.mdx)

A API da brapi.dev é uma API REST, o que significa que ela pode ser integrada
com praticamente qualquer plataforma ou linguagem de programação. Esta página
apresenta exemplos concretos de como integrar nossa API em diferentes ambientes.

[Linguagens de Programação](#linguagens-de-programação)
-------------------------------------------------------

### [TypeScript / JavaScript](#typescript--javascript)

```
// Usando fetch nativo
const fetchData = async () => {
  const token = 'SEU_TOKEN';
  const ticker = 'PETR4';
  const response = await fetch(
    `https://brapi.dev/api/quote/${ticker}?token=${token}`,
  );
  const data = await response.json();
  console.log(data);
};

// Usando Axios
import axios from 'axios';

const token = 'SEU_TOKEN';
const ticker = 'PETR4';
const url = `https://brapi.dev/api/quote/${ticker}?token=${token}`;

async function fetchQuote() {
  try {
    const response = await axios.get(url);
    console.log(response.data);
  } catch (error) {
    console.error('Erro ao buscar cotação', error);
  }
}
```

### [Python](#python)

```
# Usando requests
import requests

token = 'SEU_TOKEN'
ticker = 'PETR4'
url = f'https://brapi.dev/api/quote/{ticker}?token={token}'

response = requests.get(url)
data = response.json()
print(data)
```

### [PHP](#php)

```
<?php
// Usando cURL
$token = 'SEU_TOKEN';
$ticker = 'PETR4';
$url = "https://brapi.dev/api/quote/{$ticker}?token={$token}";

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($curl);
curl_close($curl);

$data = json_decode($response, true);
print_r($data);
?>
```

### [Java](#java)

```
// Usando HttpClient (Java 11+)
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class BrapiExample {
    public static void main(String[] args) throws Exception {
        String token = "SEU_TOKEN";
        String ticker = "PETR4";
        String url = "https://brapi.dev/api/quote/" + ticker + "?token=" + token;

        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create(url))
            .build();

        HttpResponse<String> response = client.send(request,
            HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

### [C#](#c)

```
// Usando HttpClient
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        string token = "SEU_TOKEN";
        string ticker = "PETR4";
        string url = $"https://brapi.dev/api/quote/{ticker}?token={token}";

        using HttpClient client = new HttpClient();
        string response = await client.GetStringAsync(url);
        Console.WriteLine(response);
    }
}
```

[Planilhas e Ferramentas Sem Código](#planilhas-e-ferramentas-sem-código)
-------------------------------------------------------------------------

### [Google Sheets](#google-sheets)

```
=IMPORTJSON("https://brapi.dev/api/quote/PETR4?token=SEU_TOKEN")
```

Observação: O Google Sheets não possui uma função IMPORTJSON nativa. Você
precisará instalar uma extensão ou usar Apps Script para adicionar esta
funcionalidade.

### [Microsoft Excel](#microsoft-excel)

No Excel, você pode usar o Power Query para importar dados JSON:

1. Vá para a guia "Dados" e selecione "Obter Dados" > "De Outras Fontes" > "Da
   Web"
2. Insira a URL `https://brapi.dev/api/quote/PETR4?token=SEU_TOKEN`
3. Siga o assistente para transformar os dados JSON

### [WordPress](#wordpress)

Usando um snippet de código PHP no arquivo `functions.php` do seu tema ou em um
plugin personalizado:

```
function brapi_stock_price_shortcode($atts) {
    $atts = shortcode_atts(array(
        'ticker' => 'PETR4',
    ), $atts);

    $token = 'SEU_TOKEN';
    $ticker = $atts['ticker'];
    $url = "https://brapi.dev/api/quote/{$ticker}?token={$token}";

    $response = wp_remote_get($url);
    if (is_wp_error($response)) {
        return "Erro ao buscar dados";
    }

    $body = wp_remote_retrieve_body($response);
    $data = json_decode($body, true);

    if (isset($data['results'][0]['regularMarketPrice'])) {
        return "R$ " . number_format($data['results'][0]['regularMarketPrice'], 2, ',', '.');
    } else {
        return "Cotação indisponível";
    }
}
add_shortcode('brapi_cotacao', 'brapi_stock_price_shortcode');
```

Uso no WordPress: `[brapi_cotacao ticker="PETR4"]`

[Aplicações Mobile](#aplicações-mobile)
---------------------------------------

### [React Native](#react-native)

```
import React, { useState, useEffect } from 'react';
import { View, Text, StyleSheet } from 'react-native';

const StockPrice = ({ ticker }) => {
  const [price, setPrice] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const token = 'SEU_TOKEN';
    const fetchPrice = async () => {
      try {
        const response = await fetch(
          `https://brapi.dev/api/quote/${ticker}?token=${token}`,
        );
        const data = await response.json();
        setPrice(data.results[0].regularMarketPrice);
      } catch (error) {
        console.error(error);
      } finally {
        setLoading(false);
      }
    };

    fetchPrice();
  }, [ticker]);

  if (loading) return <Text>Carregando...</Text>;

  return (
    <View style={styles.container}>
      <Text style={styles.ticker}>{ticker}</Text>
      <Text style={styles.price}>R$ {price.toFixed(2)}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    padding: 16,
    backgroundColor: '#f5f5f5',
    borderRadius: 8,
  },
  ticker: {
    fontSize: 16,
    fontWeight: 'bold',
  },
  price: {
    fontSize: 20,
    marginTop: 8,
  },
});

export default StockPrice;
```

[Conclusão](#conclusão)
-----------------------

Como uma API REST, a brapi.dev pode ser integrada em praticamente qualquer
ambiente de desenvolvimento, desde aplicações web e mobile tradicionais até
planilhas e sistemas de gerenciamento de conteúdo. A flexibilidade do formato
JSON e o uso do protocolo HTTP padrão garantem compatibilidade universal.

Para sugestões de integração com outras plataformas ou linguagens, entre em
contato com nossa equipe de suporte.

[Listar PaísesGET

Listar países disponíveis na brapi com informações adicionais](/docs/taxa-basica-de-juros/available)

### On this page

[Linguagens de Programação](#linguagens-de-programação)[TypeScript / JavaScript](#typescript--javascript)[Python](#python)[PHP](#php)[Java](#java)[C#](#c)[Planilhas e Ferramentas Sem Código](#planilhas-e-ferramentas-sem-código)[Google Sheets](#google-sheets)[Microsoft Excel](#microsoft-excel)[WordPress](#wordpress)[Aplicações Mobile](#aplicações-mobile)[React Native](#react-native)[Conclusão](#conclusão)