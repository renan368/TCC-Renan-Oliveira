# TCC - Análise e Predição de Resultados em League of Legends

## 📋 Sobre o Projeto

Este projeto é um trabalho de conclusão de curso (TCC) que utiliza técnicas de **Machine Learning** para analisar e prever resultados de partidas de **League of Legends** em diferentes ligas profissionais. O projeto processa dados históricos de partidas, treina modelos de classificação e compara o desempenho desses modelos entre diferentes ligas e períodos temporais.

### Objetivos

- Processar dados brutos de partidas de League of Legends de múltiplas ligas profissionais
- Treinar e avaliar diferentes algoritmos de Machine Learning para predição de resultados
- Comparar o desempenho dos modelos entre diferentes ligas (CBLOL, LEC, LCS, LCK)
- Analisar a importância das features usando SHAP (SHapley Additive exPlanations)
- Gerar visualizações e métricas de desempenho dos modelos

## 🎮 Ligas Analisadas

O projeto analisa dados de quatro ligas profissionais de League of Legends:

- **CBLOL** - Campeonato Brasileiro de League of Legends
- **LEC** - League of Legends European Championship
- **LCS** - League of Legends Championship Series (América do Norte)
- **LCK** - League of Legends Champions Korea

## 📊 Fonte de Dados

Os dados são obtidos do **Oracle's Elixir**, uma fonte confiável de dados estatísticos de e-sports. O projeto utiliza dados das temporadas de 2022, 2023 e 2024.

## 🏗️ Estrutura do Projeto

```
project/
├── data/                                    # Dados brutos do Oracle's Elixir
│   ├── 2022_LoL_esports_match_data_from_OraclesElixir.csv
│   ├── 2023_LoL_esports_match_data_from_OraclesElixir.csv
│   ├── 2024_LoL_esports_match_data_from_OraclesElixir.csv
│   └── organized_matches.csv
│
├── src/
│   ├── repository/                          # Dados processados por liga
│   │   ├── cblol/
│   │   │   ├── CBLOL_matches_2.csv         # 1 temporada
│   │   │   └── CBLOL_matches_4.csv         # 2 temporadas
│   │   ├── lck/
│   │   ├── lcs/
│   │   └── lec/
│   │
│   └── service/                             # Notebooks de análise
│       ├── oracle_elixir/
│       │   └── oracle_elixir.ipynb          # Processamento dos dados brutos
│       ├── cblol/
│       │   ├── CBLOL2.ipynb                # Análise com 1 temporada
│       │   ├── CBLOL4.ipynb                # Análise com 2 temporadas
│       │   └── CBLOL*_results.json         # Resultados dos modelos
│       ├── lck/
│       ├── lcs/
│       ├── lec/
│       └── general_comparison/
│           └── general_comparison.ipynb      # Comparação geral dos modelos
│
├── requirements.txt                         # Dependências do projeto
└── README.md
```

## 🔧 Tecnologias Utilizadas

- **Python 3**
- **Pandas** - Manipulação e análise de dados
- **Scikit-learn** - Algoritmos de Machine Learning
- **SHAP** - Explicabilidade dos modelos
- **Matplotlib/Seaborn** - Visualizações
- **Jupyter Notebook** - Ambiente de desenvolvimento e análise

## 📦 Instalação

### Pré-requisitos

- Python 3.7 ou superior
- pip (gerenciador de pacotes Python)

### Passos para Instalação

1. **Clone o repositório** (ou baixe os arquivos do projeto)

2. **Instale as dependências:**

```bash
pip install -r requirements.txt
```

As dependências incluem:
- `pandas`
- `scikit-learn`
- `shap`
- `matplotlib`
- `seaborn`
- `jupyter`

## 🚀 Como Usar

### 1. Processamento dos Dados

Primeiro, é necessário processar os dados brutos do Oracle's Elixir:

1. Abra o notebook `src/service/oracle_elixir/oracle_elixir.ipynb`
2. Execute todas as células para processar os dados
3. Os arquivos CSV organizados serão gerados em `src/repository/` para cada liga

**Nota:** O notebook processa os dados para:
- **Período 2**: 1 temporada (2023)
- **Período 4**: 2 temporadas (2022 + 2023)

### 2. Análise por Liga

Para analisar uma liga específica:

1. Navegue até a pasta da liga desejada (ex: `src/service/cblol/`)
2. Abra o notebook correspondente:
   - `CBLOL2.ipynb` - Análise com 1 temporada
   - `CBLOL4.ipynb` - Análise com 2 temporadas
3. Execute todas as células do notebook

Cada notebook realiza:
- Carregamento e limpeza dos dados
- Análise exploratória inicial
- Treinamento de 4 modelos de ML:
  - **Naive Bayes**
  - **Regressão Logística**
  - **SVM (Support Vector Machine)**
  - **Árvore de Decisão**
- Avaliação com métricas (Acurácia e F1-Score)
- Análise de importância das features com SHAP
- Geração de matriz de confusão
- Salvamento dos resultados em JSON

### 3. Comparação Geral

Para comparar o desempenho dos modelos entre todas as ligas:

1. Abra o notebook `src/service/general_comparison/general_comparison.ipynb`
2. Execute todas as células
3. O notebook gerará visualizações comparativas dos modelos

## 📈 Features Utilizadas

Os modelos utilizam as seguintes features para predição:

- `team_1_encoded` - Time 1 (codificado)
- `team_2_encoded` - Time 2 (codificado)
- `league_encoded` - Liga (codificada)
- `gamelength` - Duração da partida (em segundos)
- `firsttower_team_encoded` - Time que obteve a primeira torre
- `firstblood_team_encoded` - Time que obteve o primeiro abate
- `firstdragon_team_encoded` - Time que obteve o primeiro dragão

**Target:** Vencedor da partida (0 = Time 2, 1 = Time 1)

## 📊 Divisão dos Dados

Os dados são divididos em três conjuntos:

- **Treino**: 80% dos dados
- **Teste**: 10% dos dados
- **Previsão**: 10% dos dados

A divisão é feita mantendo a ordem cronológica das partidas para preservar a informação temporal.

## 📝 Resultados

Os resultados de cada análise são salvos em arquivos JSON no formato:

```json
{
  "LIGA_PERIODO": {
    "Naive Bayes": 0.50,
    "Regressao Logistica": 0.54,
    "SVM": 0.54,
    "Arvore de Decisao": 0.62
  }
}
```

## 🔍 Explicabilidade dos Modelos

O projeto utiliza **SHAP (SHapley Additive exPlanations)** para explicar as predições dos modelos:

- Valores positivos de SHAP indicam que uma feature está aumentando a probabilidade de vitória do Time 1
- Valores negativos indicam que uma feature está diminuindo essa probabilidade
- Os gráficos SHAP ajudam a entender quais features são mais importantes para cada modelo

## 📌 Observações Importantes

1. **Dados Temporais**: Os dados são ordenados cronologicamente antes da divisão para manter a ordem temporal
2. **Normalização**: As features são normalizadas usando `MinMaxScaler` antes do treinamento
3. **Codificação**: Nomes de times e ligas são codificados usando `LabelEncoder`
4. **Valores Ausentes**: Linhas com valores nulos são removidas durante o pré-processamento

## 🤝 Contribuindo

Este é um projeto de TCC. Para sugestões ou melhorias, sinta-se à vontade para abrir uma issue ou fazer um fork do projeto.

## 📄 Licença

Este projeto é parte de um trabalho acadêmico (TCC).

## 👤 Autor

Renan Oliveira

---

**Nota:** Certifique-se de ter os dados do Oracle's Elixir na pasta `data/` antes de executar os notebooks de processamento.
