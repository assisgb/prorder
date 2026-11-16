# prorder

Previsão de atraso na entrega de pedidos de e-commerce com dados da Olist.
Resultado principal: [uma frase com seu número, ex.: "LightGBM atinge PR-AUC de X contra Y do baseline, em teste temporal"].

## Problema e momento de uso

O modelo estima a probabilidade de um pedido chegar depois da data estimada informada ao cliente.
Momento de uso assumido: [compra / aprovação do pagamento / envio à transportadora] (decisão D1).
Ação de negócio que ele permitiria: [ex.: avisar o cliente ou priorizar o pedido].

## Dados e definição do alvo

- Fonte: [Brazilian E-Commerce Public Dataset by Olist, no Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). Os dados brutos não estão neste repositório. Confira a licença na página do dataset.
- Universo: pedidos com status [..] e data de entrega preenchida, num total de [N] pedidos entre [data] e [data].
- Alvo: atraso = [definição exata, ex.: entrega real posterior à data estimada] (decisão D3).
- Proporção de atrasos: [x%] no treino, [x%] na validação e [x%] no teste.
- Granularidade: uma linha por pedido. Tabelas de itens foram agregadas por [agregações usadas] (decisão D2).

## Divisão temporal e cuidados contra vazamento

| Conjunto | Período | Pedidos | Atrasos |
| --- | --- | --- | --- |
| Treino | [..] | [..] | [..] |
| Validação | [..] | [..] | [..] |
| Teste | [..] | [..] | [..] |

- Cortes escolhidos porque [justificativa] (decisão D5).
- Variáveis excluídas por só existirem depois do momento de previsão: [lista] (decisão D4).
- Todo pré-processamento é ajustado apenas no treino, dentro de um Pipeline.
- O teste foi avaliado uma única vez, ao final.

## Baseline e métrica

- Métrica principal: [ex.: PR-AUC], porque [justificativa] (decisão D6).
- Limiar: [valor], escolhido na validação com custo assumido de [..] (decisão D7).
- Baselines: classificador de classe majoritária, regressão logística [com/sem pesos de classe].

## Resultados

| Modelo | Métrica principal | Métrica secundária | Tempo de treino |
| --- | --- | --- | --- |
| Classe majoritária | [..] | [..] | [..] |
| Regressão logística | [..] | [..] | [..] |
| Random forest | [..] | [..] | [..] |
| LightGBM | [..] | [..] | [..] |

Validação cruzada temporal: [média ± desvio] para o modelo final.
Resultado final no teste: [valor, com intervalo].

![Curva precision-recall](reports/pr_curve.png)

## Análise de erros

- Onde o modelo vai pior: [fatias, com o tamanho de cada uma].
- Categorias de erro encontradas lendo exemplos: [3 a 5 categorias].
- Importância por permutação: [variáveis mais relevantes e o que se pode e não se pode concluir].
- Calibração: [resumo da curva e do Brier score].

![Desempenho por fatia](reports/slices.png)

## Limitações e riscos

- O dataset cobre [período] e [região/marketplace]. Não há garantia de validade fora dele.
- Só pedidos entregues entram no treino, o que introduz viés de seleção.
- Fatores que o dado não contém: [ex.: clima, greves, estoque do vendedor].
- Importância de variável não implica causalidade.
- [Outras limitações específicas do seu projeto.]

## Como reproduzir

```bash
git clone https://github.com/assisgb/prorder.git
cd prorder
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
# baixe o dataset do Kaggle para data/raw/
python -m src.train
pytest
```

Os resultados e gráficos são gerados em `reports/`. A semente fixa é [valor].

## Estrutura do repositório

```text
prorder/
├── README.md
├── LICENSE
├── requirements.txt
├── data/            # raw/ e processed/ ficam fora do Git
├── notebooks/       # exploração
├── src/             # dados, variáveis, divisão, treino, avaliação
├── tests/
└── reports/
```

## Decisões e alternativas descartadas

- **[D5] Corte temporal:** escolhi [..] em vez de [..] porque [evidência].
- **[D6] Métrica:** escolhi [..] em vez de [..] porque [evidência].
- **[D9] Desbalanceamento:** escolhi [..] em vez de [..] porque [evidência].

## Autor

Gabriel Assis da Silva, [@assisgb](https://github.com/assisgb)

## Licença

Distribuído sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para os detalhes.
O dataset da Olist não faz parte deste repositório e segue os termos da página dele no Kaggle.