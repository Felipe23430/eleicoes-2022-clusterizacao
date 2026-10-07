# Eleições Gerais 2022 — Segmentação do Perfil de Candidaturas com Machine Learning

## Sobre o projeto

Este projeto tem como objetivo identificar diferentes perfis de candidaturas a **Deputado Federal no estado de São Paulo nas Eleições Gerais de 2022**, utilizando dados públicos disponibilizados pelo **Tribunal Superior Eleitoral (TSE)**.

A análise utiliza técnicas de **Análise Exploratória de Dados (EDA)** e **Machine Learning não supervisionado**, aplicando o algoritmo **K-Means** para segmentar as candidaturas a partir de características financeiras, patrimoniais e demográficas.

Além da modelagem em Python, foi desenvolvido um dashboard no **Power BI** para facilitar a exploração e interpretação dos resultados.

---

## Pergunta de negócio

> Quais perfis de candidaturas a Deputado Federal em São Paulo podem ser identificados a partir de características financeiras e patrimoniais nas Eleições de 2022?

---

## Fonte dos dados

Os dados utilizados são provenientes dos conjuntos de dados públicos das **Eleições Gerais de 2022**, disponibilizados pelo Tribunal Superior Eleitoral (TSE).

Foram utilizadas informações relacionadas a:

- candidaturas;
- bens declarados;
- receitas de campanha;
- despesas contratadas;
- votação por candidato.

O projeto foi delimitado às candidaturas ao cargo de **Deputado Federal no estado de São Paulo**.

---

## Preparação dos dados

O processo de preparação envolveu:

- seleção das candidaturas de São Paulo;
- filtro para o cargo de Deputado Federal;
- seleção das variáveis relevantes;
- tratamento dos valores monetários;
- cálculo da idade das candidaturas;
- agregação do patrimônio declarado;
- agregação das receitas de campanha;
- agregação das despesas de campanha;
- agregação da quantidade de votos;
- integração das diferentes bases utilizando o identificador da candidatura;
- análise de valores ausentes;
- análise exploratória das variáveis.

Após o tratamento, a base principal utilizada na análise possui **1.540 candidaturas**.

---

## Análise exploratória

Durante a análise exploratória foi observada uma forte assimetria nas variáveis financeiras, com grande concentração de candidaturas em valores menores e algumas candidaturas apresentando valores significativamente superiores.

Também foi identificada uma correlação muito elevada entre **receita e despesa de campanha**, de aproximadamente **0,995**.

Para evitar redundância na formação dos clusters, a despesa não foi utilizada como variável de entrada do modelo.

---

## Variáveis utilizadas no K-Means

A segmentação foi construída utilizando:

- **Idade**
- **Patrimônio declarado**
- **Receita de campanha**

Como patrimônio e receita apresentavam distribuições muito assimétricas, foi aplicada a transformação:

`log1p(x)`

Posteriormente, as variáveis foram padronizadas utilizando **StandardScaler**.

A despesa de campanha, a quantidade de votos e o resultado eleitoral foram mantidos apenas para análises posteriores dos grupos.

---

## Escolha do número de clusters

Foram avaliadas diferentes quantidades de clusters utilizando:

- **Método do Cotovelo (Elbow Method)**
- **Silhouette Score**

O maior Silhouette Score entre as configurações analisadas ocorreu com:

**k = 3**

Silhouette Score aproximado:

**0,447**

A solução com três clusters também apresentou uma interpretação mais simples e coerente para o objetivo do projeto.

---

## Perfis identificados

O modelo identificou três grupos principais.

### Cluster 0 — Maior estrutura financeira

**975 candidaturas**

Características medianas:

- Idade: **50 anos**
- Patrimônio: aproximadamente **R$ 380 mil**
- Receita: aproximadamente **R$ 106 mil**
- Despesa: aproximadamente **R$ 100 mil**
- Votos: aproximadamente **2.575**

Representa cerca de **63% das candidaturas classificadas pelo modelo**.

---

### Cluster 1 — Baixa movimentação financeira

**137 candidaturas**

Características medianas:

- Idade: **51 anos**
- Patrimônio: **R$ 0**
- Receita: **R$ 0**
- Despesa: **R$ 0**
- Votos: aproximadamente **182**

Representa aproximadamente **9% das candidaturas classificadas**.

---

### Cluster 2 — Estrutura financeira intermediária

**427 candidaturas**

Características medianas:

- Idade: **48 anos**
- Patrimônio: **R$ 0**
- Receita: aproximadamente **R$ 25 mil**
- Despesa: aproximadamente **R$ 20 mil**
- Votos: aproximadamente **486**

Representa aproximadamente **28% das candidaturas classificadas**.

---

## Principais insights

A segmentação mostrou diferenças relevantes principalmente relacionadas à estrutura financeira das campanhas.

O grupo de **Maior estrutura financeira** concentra candidaturas com maiores valores medianos de patrimônio, receita e despesa.

O grupo de **Estrutura financeira intermediária** apresenta movimentação financeira de campanha, porém em níveis inferiores ao primeiro grupo.

Já o grupo de **Baixa movimentação financeira** apresenta valores medianos próximos ou iguais a zero para patrimônio, receita e despesa.

Também foram observadas diferenças na quantidade mediana de votos entre os grupos. Entretanto, **votos e resultado eleitoral não foram utilizados para formar os clusters**.

Portanto, os resultados devem ser interpretados como **associações observadas entre os perfis**, e não como evidência de que maior estrutura financeira cause melhor desempenho eleitoral.

---

## Dashboard Power BI

Para complementar a análise foi desenvolvido um dashboard interativo no Power BI dividido em quatro páginas:

### 1. Visão Geral

Apresenta os principais indicadores da base, distribuição das candidaturas por perfil, gênero, escolaridade e resultado eleitoral.

### 2. Análise dos Clusters

Compara os três perfis em relação a:

- receita;
- patrimônio;
- despesa;
- idade;
- quantidade de votos.

### 3. Perfil dos Clusters

Explora características das candidaturas dentro de cada grupo, incluindo:

- gênero;
- escolaridade;
- ocupação;
- resultado eleitoral.

### 4. Detalhamento das Candidaturas

Permite consultar individualmente as candidaturas e utilizar filtros por candidato, partido, perfil e resultado eleitoral.

---

## Dashboard

![Dashboard - Visão Geral](images/dashboard_visao_geral.png)

---

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- Power BI
- Machine Learning
- K-Means
- Git/GitHub

---

## Estrutura do projeto

```text
Projeto_GitHub/
│
├── data/
│   └── base_final_clusters.csv
│
├── notebooks/
│   └── eleição clusterização.ipynb
│
├── power_bi/
│   └── dashboard_eleicoes_2022_clusters.pbix
│
├── images/
│   └── dashboard_visao_geral.png
│
└── README.md
```

---

## Observações metodológicas

O algoritmo K-Means foi utilizado com finalidade **exploratória e descritiva**.

Os clusters não representam classificações oficiais do TSE e os nomes atribuídos aos grupos foram definidos após a análise das características predominantes de cada cluster.

O projeto não tem como objetivo prever resultados eleitorais ou estabelecer relações causais entre recursos financeiros e desempenho nas eleições.

---

## Autor

**Felipe Silva**

Projeto desenvolvido para estudo e portfólio nas áreas de **Análise de Dados, Business Intelligence e Machine Learning**.