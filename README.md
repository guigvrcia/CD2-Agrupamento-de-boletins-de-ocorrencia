# Agrupamento de Boletins de Ocorrência (MG) com Clusterização

Projeto da disciplina **Ciência de Dados II (UFU)** para análise de padrões temporais, contextuais e tipológicos da criminalidade em Minas Gerais, utilizando dados agregados de boletins de ocorrência e técnicas de clusterização.

## Integrantes

- Arthur Aquino Guardieiro  
- Guilherme Antonio Garcia do Nascimento  
- Rodrigo Martins de Souza

## Objetivo Geral

Identificar padrões temporais e estruturais da criminalidade no estado de Minas Gerais por meio de:

- análise exploratória dos registros;
- construção de variáveis derivadas;
- testes estatísticos de associação;
- clusterização não supervisionada de tipos de crime.

## Objetivos Específicos

- Detectar padrões por **dia da semana** e **faixa horária**.
- Verificar concentração de ocorrências com **arma de fogo** por contexto temporal e regional (RISP).
- Avaliar associação entre **tipo de local** e **crime violento**.
- Agrupar tipos de crime por **perfil temporal** com K-Means.

## Base de Dados

Dados obtidos do **Portal de Dados Abertos de Minas Gerais**, em múltiplos CSVs agregados por `qtde ocorrencias`.

### Variáveis centrais utilizadas

- `natureza_principal_completa`
- `dia_semana_fato`
- `horario fato` (convertida para `faixa_horaria`)
- `descricao local imediato`
- `descricao_longa_meio_utilizado`
- `municipio`
- `risp`
- `qtde ocorrencias` (peso das análises)

### Variáveis derivadas

- `crime_violento`: classificação binária por padrão textual (ex.: homicídio, roubo, estupro, lesão, sequestro, extorsão).
- `usa_arma_fogo`: classificação binária por presença de “ARMA DE FOGO” no meio utilizado.
- `faixa_horaria`: Madrugada, Manhã, Tarde, Noite.

## Metodologia

Pipeline implementado no notebook `AGRUPAMENTO-BOs-CD2.ipynb`:

1. Leitura e unificação dos CSVs.
2. Padronização de colunas e limpeza de dados (incluindo datas e nulos).
3. Criação de variáveis derivadas (`crime_violento`, `usa_arma_fogo`, `faixa_horaria`).
4. Análise exploratória (distribuições, boxplots e heatmaps).
5. Testes estatísticos (Qui-quadrado e V de Cramér).
6. Clusterização de tipos de crime por perfil temporal com K-Means.

Também há comparações auxiliares de qualidade com métricas de clusterização e avaliação adicional com DBSCAN/hierárquico.

## Principais Resultados

### Padrões temporais

- Crimes em geral apresentam padrão temporal consistente, com maior incidência na **tarde em dias úteis**.
- Há aumento relativo de ocorrências **à noite nos finais de semana**.

### Crimes violentos

- Proporção geral ponderada de crimes violentos: **0.2858838770332108**.
- Crimes violentos apresentam concentração mais forte no **período noturno**.

### Arma de fogo

- Proporção geral ponderada de ocorrências com arma de fogo: **0.002689689041462455**.
- Maiores proporções por faixa horária:
  - Noite: **0.004686**
  - Madrugada: **0.002202**
  - Tarde: **0.002016**
  - Manhã: **0.001473**
- Há diferença estatisticamente significativa por faixa horária (`p-valor ponderado = 0.0`).

### Tipo de local × crime violento

- Teste Qui-quadrado: **635668.3859635122**
- `p-value`: **0.0**
- V de Cramér: **0.2712567965789548**

Interpretação: existe associação estatística relevante entre contexto de local e ocorrência de crimes violentos.

### Clusterização de tipos de crime

- Modelo final: **K-Means com K = 3**
- Silhouette final: **0.3327**

Perfis temporais médios dos clusters:

- **Cluster 0**: perfil mais equilibrado, com maior participação noturna. Exemplos representativos: *Sequestro e Cárcere Privado*, *Estupro Tentado*, *Estupro de Vulnerável*.
- **Cluster 1**: maior concentração na **tarde**. Exemplos representativos: *Furto Consumado*, *Extorsão Consumada*, *Lesão Corporal*.
- **Cluster 2**: forte concentração na **noite**. Exemplos representativos: *Roubo Tentado*, *Roubo Consumado*, *Homicídio Tentado*.

Arquivo de saída gerado no fluxo final:

- `clusters_tipos_crime.csv`

## Estrutura do Projeto

- `AGRUPAMENTO-BOs-CD2.ipynb`: notebook principal do trabalho.
- `Agrupamento_de_BOs_relatório.pdf`: relatório escrito.
- `Agrupamento-de-Boletins-de-Ocorrencia-Utilizando-Algoritmos-de-Clusterizacao.pptx`: apresentação.
- `*.csv`: bases de entrada e arquivos intermediários/finais.
- `clusters_tipos_crime.csv`: saída da etapa final de clusterização por tipo de crime.

## Como Executar

1. Instale as dependências:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
```

2. Garanta que os CSVs estejam no mesmo diretório do notebook. Faça seu download aqui: https://drive.google.com/drive/folders/1Zhyb4lo8BMxzKt3JZtivw_5AjAt4j2JW?usp=sharing
3. Abra e execute, em ordem, o `AGRUPAMENTO-BOs-CD2.ipynb`.
4. Ao final, será gerado o arquivo `clusters_tipos_crime.csv`.

## Limitações

- Dados agregados (não há granularidade individual por ocorrência).
- Variáveis derivadas dependem de classificação textual.
- Possíveis inconsistências administrativas de preenchimento na base original.

## Observações de Reprodutibilidade

- O projeto usa `qtde ocorrencias` como **peso** nas métricas de proporção.
- Parte das análises depende da limpeza de datas/horários e da normalização de colunas.
- Resultados de clusterização podem variar levemente com alterações de versão de biblioteca e parâmetros.
