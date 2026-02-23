# 🌊 Wave Energy Converters – Layout Optimization & Linear Regression

Projeto desenvolvido para análise geométrica e modelagem preditiva da
potência total gerada por fazendas de **Wave Energy Converters (WECs)**
a partir de suas coordenadas espaciais.

O projeto está dividido em duas etapas principais:

1. **Processamento e Engenharia de Features**
2. **Modelagem com Regressão Linear**

---

## 📁 Estrutura do Projeto
├── scripts/\
├── outputs/\
├── data/\
│ ├── raw/\
│ └── processed/\
├── ABNT/\
└── README.md

---

# 📊 1️⃣ Processamento dos Dados (`data_processing.ipynb`)

## 🔹 Objetivo

Transformar o dataset bruto contendo coordenadas e potências individuais
dos WECs em um dataset otimizado para modelagem preditiva.

---

## 🔹 Dataset

Cada observação contém:

- `X1` a `X16` → Coordenadas horizontais dos WECs  
- `Y1` a `Y16` → Coordenadas verticais dos WECs  
- `P1` a `P16` → Potências individuais  
- `Powerall` → Potência total gerada  
- `scenario` → Região (Adelaide, Tasmania, Sydney, Perth)

---

## 🔹 Etapas Realizadas

### ✅ 1. Remoção das potências individuais (`P1`–`P16`)

Motivos:
- Evitar vazamento de informação  
- Reduzir multicolinearidade  
- Simular cenário real de previsão  

---

### ✅ 2. Análise Exploratória

- Verificação de valores nulos  
- Estatísticas descritivas  
- Visualização da disposição espacial dos WECs  
- Análise de padrões geométricos  

---

### ✅ 3. Engenharia de Features

Foram criadas novas métricas geométricas:

- 📏 Distâncias entre pares de WECs  
- 📍 Centroide do arranjo  
- 📐 Distância média ao centroide  
- 📊 Métricas estatísticas das distâncias  

Cálculo do centroide:

$centroid_x = \frac{1}{N} \sum X_i$

$centroid_y = \frac{1}{N} \sum Y_i$

---

### ✅ 4. Correlação com a variável alvo

Foi gerado um heatmap de correlação com `Powerall`.

📌 **Insight principal:**

> A relação entre layout e potência total é fraca linearmente, sugerindo comportamento **não-linear**.

---

### ✅ 5. Exportação

O dataset tratado é salvo em:

data/processed/wec_all_processed.parquet


> ⚠️ Os arquivos de dados não estão incluídos no repositório devido ao limite de tamanho do GitHub.

---

# 🤖 2️⃣ Modelagem – Regressão Linear (`lr.ipynb`)

## 🔹 Objetivo

Prever `Powerall` utilizando apenas variáveis geométricas derivadas.

---

## 🔹 Pipeline do Modelo

Para cada cenário:

1. Separação por região  
2. Divisão treino/teste  
3. Padronização (`StandardScaler`)  
4. Treinamento com `LinearRegression`  
5. Avaliação com métricas:

- R²  
- MAE  
- MSE  
- RMSE  

---

## 📈 Resultados Obtidos

| Região    | Desempenho (R²) | Observação |
|-----------|-----------------|------------|
| Sydney    | ~0.89           | Forte relação linear |
| Adelaide  | Moderado        | Ajuste razoável |
| Perth     | Intermediário   | Dependência parcial |
| Tasmania  | ~0.49           | Indícios de não-linearidade |

---

## 🔎 Principais Conclusões

- O layout influencia a geração de energia.  
- A relação não é totalmente linear.  
- Features isoladas possuem baixo poder explicativo.  
- A combinação de métricas melhora o desempenho.  
- Cenários com maior energia marítima podem exigir modelos não-lineares.

---

# 🚀 Como Executar

## 1️⃣ Instalar dependências

```bash
!pip install pandas numpy scipy matplotlib seaborn scikit-learn fastparquet
```

## 2️⃣ Executar os notebooks

Execute data_processing.ipynb
Em seguida, execute lr.ipynb

# 🛠 Tecnologias Utilizadas

* Python
*Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Fastparquet

# 🔮 Próximos Passos

* Regressão Polinomial
* Random Forest
* Gradient Boosting
* XGBoost
* Redes Neurais

# 👨‍💻 Autor

Pedro Muniz Cherulli
Ciência de Dados

# 📌 Observação Final

Este projeto demonstra como engenharia geométrica de features
permite transformar coordenadas espaciais em variáveis preditivas
relevantes para sistemas físicos complexos, como fazendas de energia
das ondas.
