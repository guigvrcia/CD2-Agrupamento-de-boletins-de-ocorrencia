# Agrupamento de Boletins de Ocorrência

Este repositório apresenta uma análise exploratória e estatística de registros agregados de boletins de ocorrência do estado de Minas Gerais, com foco em padrões **temporais**, **espaciais** e **tipológicos** da criminalidade.

## 📌 Objetivo

Investigar como os crimes se distribuem ao longo do tempo (dia da semana e faixa horária), no território (municípios e RISP) e por características do evento (crime violento, uso de arma de fogo e tipo de local).

## 🗂️ Fonte de dados

- **Origem:** Portal de Dados Abertos do Estado de Minas Gerais
- **Unidade de análise:** registros agregados
- **Variável de peso:** `qtde ocorrencias` (frequência real de eventos por combinação de atributos)

## 🧪 Metodologia

A análise foi estruturada em quatro blocos:

1. **Pré-processamento**
   - Integração de múltiplos CSV em `dataset_combinado`
   - Padronização de colunas com `mapa_colunas`
   - Remoção de variáveis com `colunas_remover`
   - Tratamento de nulos e padronização de `data_fato`
   - Criação de `faixa_horaria` (Madrugada, Manhã, Tarde, Noite)

2. **Engenharia de variáveis**
   - `usa_arma_fogo`: derivada de `descricao_longa_meio_utilizado`
   - `crime_violento`: derivada de `natureza_principal_completa`

3. **Análise exploratória (EDA)**
   - Tabelas e heatmaps absolutos e proporcionais
   - Distribuições por `dia_semana_fato`, `faixa_horaria`, `municipio`, `risp`, `tipo_local`
   - Métricas ponderadas por `qtde ocorrencias`

4. **Modelagem e validação**
   - Clusterização com **K-Means** por perfil temporal de municípios
   - Escolha de `k` por **Método do Cotovelo** e **Silhouette Score**
   - Testes de independência com `chi2_contingency`
   - Magnitude de associação com **V de Cramér**
   - Concentração/diversidade regional com **entropia**

## 📊 Principais variáveis utilizadas

- `natureza_principal_completa`
- `qtde ocorrencias`
- `logradouro ocorrencia - tipo`
- `municipio`
- `risp`
- `data_fato`
- `faixa_horaria`
- `descricao_longa_meio_utilizado`
- `alvo`
- `causa_presumida`

## 🧰 Tecnologias e bibliotecas

- Python 3
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- scipy
- re (biblioteca padrão)

## ▶️ Como executar

1. Clone este repositório.
2. Instale as dependências:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
```

3. Abra o notebook `Trablho_de_CD2 (2) (1).ipynb` no VS Code/Jupyter.
4. Ajuste o caminho dos arquivos CSV na variável `caminho` (célula de leitura dos dados).
5. Execute as células em ordem, de cima para baixo.

## 📁 Estrutura sugerida do repositório

```text
.
├── Trablho_de_CD2 (2) (1).ipynb
├── clusters_municipios_perfil_temporal.csv   # gerado durante a execução
└── README.md
```

## ✅ Resultados esperados

- Heatmaps de distribuição criminal por dia e faixa horária
- Indicadores de crimes violentos e uso de arma de fogo
- Perfis temporais de municípios por cluster
- Evidências estatísticas de associação entre variáveis categóricas

## 👤 Autor


- **Nome:** Arthur Guardieiro, Guilherme Nascimento, Rodrigo Martins
- **Curso/Disciplina:** Sistemas de Informação - Ciencias de Dados II
- **Instituição:** Universidade Federal de Uberlândia


