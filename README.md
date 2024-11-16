# Predição de Doença Cardíaca

Este repositório contém um projeto que utiliza aprendizado de máquina para prever a probabilidade de pacientes apresentarem doenças cardíacas. O sistema foi desenvolvido utilizando dados de saúde e métricas clínicas para fornecer uma análise preditiva confiável.

## 📜 Problema

Com o aumento do sedentarismo e consumo de alimentos não saudáveis, as doenças cardíacas estão se tornando cada vez mais comuns. Este projeto tem como objetivo prever quais pacientes podem ter doenças cardíacas, ajudando na detecção precoce e na prevenção.

## 🗂️ Dados Utilizados

O dataset utilizado foi obtido da [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php) e contém as seguintes variáveis:

- **Idade**
- **Sexo**
- **Tipo de Dor no Peito**
- **Pressão Arterial**
- **Colesterol**
- **Glicose em Jejum acima de 120**
- **Resultados de Eletrocardiograma (EKG)**
- **Frequência Cardíaca Máxima**
- **Angina Induzida por Exercício**
- **Depressão ST**
- **Inclinação de ST**
- **Número de Vasos Fluoroscópicos**
- **Talio**
- **Doença Cardíaca (variável alvo)**

## 📊 Metodologia

### 1. Pré-processamento de Dados
- O dataset já estava balanceado e sem valores nulos.
- Foi utilizada padronização com `StandardScaler` para normalizar variáveis contínuas.

### 2. Feature Engineering
- **Polynomial Features**: Geração de variáveis polinomiais de grau 3 para melhorar a capacidade preditiva dos modelos.
- **PCA**: Redução de dimensionalidade para 30 componentes.

### 3. Modelos Utilizados
Foram testados os seguintes algoritmos:
- Regressão Logística (`LogisticRegression`)
- Máquina de Vetores de Suporte (`SVC`)
- Floresta Aleatória (`RandomForestClassifier`)
- K-Nearest Neighbors (`KNN`)
- CatBoost

#### Melhor Modelo:
O modelo com melhor desempenho foi o **RandomForestClassifier** combinado com `PolynomialFeatures` e `StandardScaler`.

### 4. Avaliação
A métrica principal escolhida foi o **Recall**, visando minimizar falsos negativos e reduzir os riscos de diagnósticos tardios.

## 🚀 Deploy

O modelo final foi exportado no formato `pickle` e integrado em uma API desenvolvida com Flask. A API recebe os dados do paciente via requisição POST e retorna:

- **0**: Sem doença cardíaca.
- **1**: Com doença cardíaca.

### Exemplo de Requisição:
```json
# POST
[
  {
    "age": 70,
    "sex": 0,
    "chest_pain_type": 2,
    "bp": 145,
    "cholesterol": 533,
    "fbs_over_120": 0,
    "ekg_results": 0,
    "max_hr": 150,
    "exercise_angina": 0,
    "st_depression": 2.3,
    "slope_of_st": 3,
    "number_of_vessels_fluro": 0,
    "thallium": 7
  },
  {
    "age": 70,
    "sex": 0,
    "chest_pain_type": 1,
    "bp": 145,
    "cholesterol": 533,
    "fbs_over_120": 0,
    "ekg_results": 0,
    "max_hr": 150,
    "exercise_angina": 0,
    "st_depression": 2.3,
    "slope_of_st": 3,
    "number_of_vessels_fluro": 0,
    "thallium": 7
  }
]

# HTTP 200
{
  "predictions": [
    1,
    0
  ]
}


