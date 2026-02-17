# 🛒 Previsão de Vendas em E-commerce com Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mgabrielamnts/previsao-vendas-ecommerce/blob/main/previsao-vendas-ecommerce.ipynb)
![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0+-orange.svg)

## 📌 Sobre o Projeto

Modelo de **classificação binária** desenvolvido para prever a ocorrência de pedidos em uma plataforma de e-commerce, visando otimizar o planejamento logístico e reduzir custos operacionais.

O projeto utiliza técnicas de **Machine Learning** e **Feature Engineering** customizado para identificar padrões de compra e antecipar demanda.

---

## 🎯 Objetivo

Estimar se haverá **pelo menos uma ordem de compra** para cada par `(cliente, data)` no futuro, possibilitando:

- ✅ Melhor alocação de recursos logísticos
- ✅ Redução de custos com preparação desnecessária
- ✅ Minimização de perdas por falta de estoque

---

## 📊 Dataset

O dataset contém histórico de transações com a seguinte estrutura:

| Campo | Descrição |
|-------|-----------|
| `account_id` | Identificador único do cliente |
| `order_date` | Data da transação |
| `total_amount` | Valor total das transações (R$) |
| `total_orders` | Quantidade de pedidos realizados |

**Período:** Julho/2022

---

## 🛠️ Tecnologias Utilizadas

### Linguagens e Bibliotecas
- **Python 3.8+**
- **Pandas** - Manipulação de dados
- **NumPy** - Computação numérica
- **Scikit-learn** - Machine Learning
- **Matplotlib / Seaborn** - Visualização de dados
- **Scipy** - Análises estatísticas

### Modelos de Machine Learning
- Regressão Logística
- Random Forest Classifier

---

## 🔄 Pipeline do Projeto

### 1️⃣ Análise Exploratória (EDA)
- Identificação de padrões temporais (sazonalidade semanal e mensal)
- Análise de distribuição de vendas por cliente
- Detecção de outliers e valores ausentes

### 2️⃣ Feature Engineering
- **Variáveis temporais:** dia da semana, dia do mês, fim de semana
- **Variáveis comportamentais:** probabilidades customizadas por dia da semana (odds)
- **Segmentação de clientes:** agrupamento por padrão de compra
- Criação de 7+ features derivadas

### 3️⃣ Modelagem
- **Split cronológico:** treino até 24/07, teste nos dias seguintes (evita data leakage)
- **Tratamento de desbalanceamento:** `class_weight='balanced'`
- **Otimização de threshold:** ajuste para 0.3 priorizando Recall
- **Pipeline completo:** preprocessamento + modelo

### 4️⃣ Avaliação
- Métricas: Accuracy, Precision, Recall, F1-Score, AUC-ROC
- Matriz de confusão
- Análise de importância de features
- Validação temporal

---

## 📈 Resultados

| Métrica | Valor | Interpretação |
|---------|-------|---------------|
| **Recall** | **82.3%** | Detecta 82.3% das vendas reais |
| **AUC-ROC** | **89.3%** | Excelente capacidade de distinção |
| **Precision** | - | Trade-off consciente priorizando Recall |

### 🎯 Trade-off Estratégico

O modelo foi configurado para **priorizar Recall** (minimizar Falsos Negativos), pois no contexto logístico:

> **Custo de NÃO atender um pedido real > Custo de preparação preventiva**

Isso resulta em mais Falsos Positivos (preparação sem venda), mas garante que **poucas vendas reais sejam perdidas**.

---

## 💡 Principais Insights

### 📊 Importância de Features

1. **Sazonalidade Semanal (`day_of_week`)** 🥇
   - Preditor mais forte
   - Negócio fortemente regido por rotina semanal
   - Dias úteis concentram vendas

2. **Ciclo Mensal (`day`)** 🥈
   - Comportamento oscila conforme calendário
   - Possivelmente ligado a ciclos de pagamento

3. **Comportamento Individual (`odds_sat`, `odds_fri`)** 🥉
   - Variação significativa entre clientes nos finais de semana
   - Permite personalização da predição

---

## 📁 Estrutura do Repositório

```
📦 previsao-vendas-ecommerce/
├── 📓 previsao-vendas-ecommerce.ipynb  # Notebook principal
├── 📄 README.md                         # Este arquivo
└── 📊 data/
    └── historical_orders.csv            # (não incluído - dados privados)
```

---

## 🚀 Como Executar

### Pré-requisitos

```bash
pip install pandas numpy scikit-learn matplotlib seaborn scipy
```

### Execução

**Opção 1: Google Colab** (Recomendado)
- Clique no badge "Open in Colab" no topo deste README
- Execute célula por célula

**Opção 2: Local**
```bash
# Clone o repositório
git clone https://github.com/mgabrielamnts/previsao-vendas-ecommerce.git

# Navegue até o diretório
cd previsao-vendas-ecommerce

# Abra o notebook
jupyter notebook previsao-vendas-ecommerce.ipynb
```

---

## 🔍 Metodologia

### Validação Temporal
- **Train:** Dados até 24/07/2022
- **Test:** Dias subsequentes
- Simula cenário real onde modelo só conhece o passado

### Tratamento de Desbalanceamento
- Maioria dos dias sem vendas (classe negativa predominante)
- Solução: `class_weight='balanced'` + ajuste de threshold
- Evita modelo enviesado para classe majoritária

### Prevenção de Data Leakage
- Split cronológico rigoroso
- Nenhuma informação do futuro usada no treino
- Features criadas apenas com dados históricos

---

## 📚 Aprendizados e Melhorias Futuras

### ✅ Principais Aprendizados
- Importância do **split cronológico** em problemas temporais
- **Trade-off entre métricas** conforme contexto de negócio
- **Feature engineering customizado** aumenta significativamente poder preditivo


---

## 📝 Contexto Acadêmico

Este projeto foi desenvolvido como trabalho final do curso **Introdução à Ciência de Dados e Métodos Quantitativos** (USP - 2026).

O desenvolvimento incluiu auxílio de LLMs para:
- Refinamento técnico da documentação
- Validação de pipeline e prevenção de data leakage
- Orientação em técnicas de modelagem

**Todo o código foi revisado, testado e compreendido integralmente.**

---

## 👩‍💻 Sobre a Autora

**Maria Gabriela Martins de Souza**

Profissional em transição para a área de Dados, com formação em Engenharia Química e experiência prática em análise de dados, automação e dashboards. Atualmente cursando Análise e Desenvolvimento de Sistemas (FATEC) e Google Data Analytics (Coursera).

### 🔗 Conecte-se comigo:

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/mgabrielamnts)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mgabrielamnts)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:mgabrielamnts@gmail.com)


## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar, modificar e distribuir.

---

## 🙏 Agradecimentos

- **USP** - Curso de Introdução à Ciência de Dados
- **Comunidade Python** - Bibliotecas open-source incríveis


