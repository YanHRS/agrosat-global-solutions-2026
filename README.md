# 🛰️ AgroSat — Monitoramento Agrícola com Dados de Satélite
> Global Solutions 2026 | FIAP — Tecnologia em Sistemas para Internet | 1º Ano

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://python.org)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)](https://pandas.pydata.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org)
[![FIAP](https://img.shields.io/badge/FIAP-Global%20Solutions%202026-red)](https://fiap.com.br)

---

## 📋 Sobre o Projeto

O **AgroSat** é uma plataforma de análise de dados de satélite voltada para apoiar pequenos e médios produtores rurais brasileiros na tomada de decisão agrícola e ambiental.

O Brasil é um dos maiores produtores agrícolas do mundo, mas **~77% dos estabelecimentos rurais** são de pequenos e médios produtores que tomam decisões sem acesso a dados climáticos e ambientais precisos. Queimadas descontroladas, secas e desmatamento afetam diretamente produtividade e meio ambiente.

**Problema central:** Como dados de satélite sobre focos de queimada, precipitação e índice de vegetação (NDVI) podem apoiar a tomada de decisão agrícola e ambiental no Brasil?

---

## 🎯 Alinhamento com ODS da ONU

| ODS | Contribuição |
|---|---|
| 🌾 **ODS 2** — Fome Zero e Agricultura Sustentável | Alertas preventivos ajudam a evitar perdas de lavoura por queimadas |
| 🌡️ **ODS 13** — Ação Contra a Mudança Global do Clima | Monitoramento ambiental contribui para mitigação climática |
| 🌿 **ODS 15** — Vida Terrestre | Proteção dos biomas por meio de dados e inteligência ambiental |

---

## 📊 Dados Utilizados

Três bases de dados com cobertura nacional de **2015 a 2024**, geradas com base na metodologia do **INPE/BDQueimadas** e **NASA EarthData**:

| Dataset | Registros | Descrição |
|---|---|---|
| `queimadas_brasil_2015_2024.csv` | ~2.400 | Focos de queimada por estado, bioma, mês e ano |
| `precipitacao_brasil_2015_2024.csv` | ~2.400 | Precipitação mensal (mm) por estado |
| `ndvi_brasil_2015_2024.csv` | ~960 | Índice de Vegetação por Diferença Normalizada (NDVI) por bioma |

---

## 🔬 Análises Realizadas

### 1. Limpeza e Tratamento de Dados
- Remoção de outliers extremos via método IQR (focos de queimada)
- Correção de valores negativos de precipitação
- Normalização do NDVI para o range `[0, 1]`
- Merge das 3 bases por chave `ano + mês + estado`

### 2. Estatística Descritiva
- Distribuição de focos por bioma (média, mediana, desvio padrão, assimetria e curtose)
- Identificação dos biomas com maior concentração histórica: **Amazônia** e **Cerrado**

### 3. Série Temporal
- Evolução anual de focos (2015–2024) com tendência de crescimento até 2021
- **Sazonalidade confirmada:** pico de queimadas entre **julho e outubro** (estação seca)
- Evolução por bioma ao longo do período

### 4. Análise de Correlação
- Correlação negativa significativa entre **precipitação e focos de queimada** (Pearson + Spearman)
- Quanto menor a chuva, maior o número de focos — base para o modelo de risco do AgroSat

### 5. Testes de Hipótese
- **Teste t** e **ANOVA** confirmando que a estação seca apresenta significativamente mais queimadas (p < 0,05)

### 6. Análise de NDVI
- NDVI médio por bioma: Amazônia com maior cobertura vegetal; Caatinga com maior vulnerabilidade
- Identificação de áreas com cobertura comprometida antes da percepção visual do agricultor

### 7. Taxa de Variação (Derivada Discreta)
- Identificação dos anos com maior aceleração no número de focos
- Picos positivos indicam anos críticos que demandam atenção redobrada

### 8. Focos Acumulados (Integral Discreta)
- Impacto cumulativo ao longo do período: reforça a urgência de monitoramento contínuo

### 9. Dashboard Executivo
- Painel visual completo com: série anual, sazonalidade, NDVI por bioma, correlação precipitação × focos e ranking dos 10 estados com mais queimadas

---

## 🧰 Stack Tecnológica

```python
import pandas as pd        # Manipulação e análise de dados
import numpy as np         # Operações numéricas
import matplotlib.pyplot   # Visualizações e dashboard
import seaborn as sns      # Gráficos estatísticos
from scipy import stats    # Testes de hipótese (t-test, ANOVA, Pearson, Spearman)
```

---

## 📈 Principais Resultados

| Análise | Resultado |
|---|---|
| Estatística Descritiva | Focos concentrados na Amazônia e Cerrado |
| Série Temporal | Pico sazonal Jul–Out; crescimento 2015–2021 |
| Correlação | Precipitação × focos: correlação negativa significativa |
| Teste de Hipótese | Estação seca com significativamente mais queimadas (p < 0,05) |
| NDVI | Amazônia com maior cobertura vegetal; Caatinga mais vulnerável |
| Taxa de Variação | Anos críticos identificados para ação preventiva |
| Focos Acumulados | Impacto cumulativo reforça urgência de monitoramento contínuo |

---

## 🛰️ Como a Análise Alimenta o AgroSat

1. **Alertas sazonais:** sazonalidade confirmada (Jul–Out) permite programar alertas preventivos com antecedência para produtores rurais
2. **Priorização geográfica:** estados e biomas com maior incidência histórica recebem monitoramento intensificado
3. **Modelo de risco:** correlação entre precipitação e focos embasa um modelo que cruza previsão climática com padrões históricos
4. **Índice de saúde vegetal:** NDVI permite identificar áreas comprometidas antes da percepção visual do agricultor
5. **Base de evidências:** dados fundamentam políticas públicas e decisões de cooperativas agrícolas

---

## 📁 Estrutura do Repositório

```
agrosat-global-solutions-2026/
│
├── README.md                              # Este arquivo
├── AgroSat_GlobalSolutions_2026.ipynb    # Notebook principal com toda a análise
│
├── data/
│   ├── queimadas_brasil_2015_2024.csv    # Focos de queimada 2015–2024
│   ├── precipitacao_brasil_2015_2024.csv # Precipitação mensal 2015–2024
│   └── ndvi_brasil_2015_2024.csv         # NDVI por bioma 2015–2024
│
└── docs/
    └── AgroSat_Pitch_GS2026.pdf          # Pitch deck do projeto
```

---

## 🎬 Apresentação em Vídeo

[![Assistir apresentação](https://img.shields.io/badge/YouTube-Assistir%20Apresenta%C3%A7%C3%A3o-red?logo=youtube)](https://youtu.be/iZXvOsfuGfs)

---

## 👥 Equipe — Grupo 28

| Nome | RM |
|---|---|
| Yan Reis | RM566698 |
| Giovanni Torres | RM566638 |
| Thierry Alves | RM567243 |

> **Instituição:** FIAP — Faculdade de Informática e Administração Paulista  
> **Curso:** Tecnologia em Sistemas para Internet — 1º Ano  
> **Evento:** Global Solutions 2026  
> **Tema:** Economia Espacial a serviço da Agricultura Brasileira

---

*Dados gerados com base na metodologia INPE/BDQueimadas e NASA EarthData para fins acadêmicos.*
