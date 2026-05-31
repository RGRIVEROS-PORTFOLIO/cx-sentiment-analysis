# CX Sentiment Analysis — Detección automática de clientes insatisfechos

**Autor:** Rodolfo Gabriel Riveros Lobos  
**Stack:** Python · pandas · NLTK · HuggingFace Transformers · scikit-learn  
**Dataset:** [Women's E-Commerce Clothing Reviews — Kaggle](https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews)

---

## El problema de negocio

Una cadena de tiendas necesita identificar automáticamente reseñas negativas
para activar recuperación proactiva de clientes antes de que abandonen la marca.

Hoy ese proceso es manual: alguien lee reseñas una por una.
Este proyecto lo automatiza.

---

## Qué hace este proyecto

1. Clasifica 22.632 reseñas reales como Positivo / Neutral / Negativo
2. Compara dos modelos NLP: VADER vs DistilBERT (HuggingFace)
3. Evalúa cuál es más útil para un sistema de alerta temprana en CX
4. Genera reporte de alertas exportable para el equipo de atención

---

## Resultados principales

| Modelo | Accuracy | Recall Negative | F1 Negative |
|---|---|---|---|
| VADER | 77.44% | 0.15 | 0.23 |
| DistilBERT | 72.35% | **0.93** | **0.43** |

**Conclusión:** El accuracy general es engañoso en datasets desbalanceados.
DistilBERT detecta 93 de cada 100 clientes insatisfechos reales
vs 15 de VADER — 6 veces más efectivo para sistemas de alerta CX.

---

## Estructura del proyecto
cx-sentiment-analysis/
├── notebooks/        # Análisis principal en Jupyter
├── outputs/          # Gráficos y reportes generados
├── docs/             # Conclusiones ejecutivas
└── data/             # Ver instrucciones de descarga abajo

---

## Cómo reproducir el análisis

**1. Clonar el repositorio**
```bash
git clone https://github.com/rgriveros/cx-sentiment-analysis.git
cd cx-sentiment-analysis
```

**2. Instalar dependencias**
```bash
pip install pandas numpy matplotlib seaborn nltk wordcloud
pip install transformers scikit-learn kagglehub
```

**3. Descargar el dataset**

El dataset no está incluido por licencia de Kaggle.
El notebook lo descarga automáticamente con `kagglehub` al ejecutar la Sección 2.
Requiere cuenta en Kaggle y token de API configurado.

**4. Ejecutar el notebook**
```bash
jupyter notebook notebooks/sentiment_analysis_cx.ipynb
```

---

## Contexto profesional

Este proyecto simula un caso real de **CX Analytics** aplicado a retail,
conectando análisis de texto con decisiones operativas concretas:
alertas automáticas, colas de atención priorizadas e inteligencia
para áreas de producto y logística.

Background del autor: +5 años en Customer Experience y Calidad ISO 9001,
con experiencia en gestión de NPS, reducción de TTR y auditorías en
concesionarias automotrices (Ford).

---

## Próximos pasos del proyecto

- [ ] Sistema de alertas automáticas con exportación a Excel
- [ ] Cola de atención priorizada por score + valor de cliente  

---

## Ver los notebooks

| Notebook | nbviewer |
|---|---|
| Análisis de sentimientos | [Ver](https://nbviewer.org/github/RGRIVEROS-PORTFOLIO/cx-sentiment-analysis/blob/main/notebooks/Woman_s_EcommerceClothingReviews.ipynb) |
| Sistema de alertas | [Ver](https://nbviewer.org/github/RGRIVEROS-PORTFOLIO/cx-sentiment-analysis/blob/main/notebooks/alert_system_cx.ipynb) |
| Cola priorizada | [Ver](https://nbviewer.org/github/RGRIVEROS-PORTFOLIO/cx-sentiment-analysis/blob/main/notebooks/priority_queue_cx.ipynb) |

---
