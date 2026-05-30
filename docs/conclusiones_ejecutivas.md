# Conclusiones Ejecutivas — CX Sentiment Analysis

**Proyecto:** Detección automática de clientes insatisfechos
**Analista:** Rodolfo Gabriel Riveros Lobos
**Período:** Mayo 2026
**Repositorio:** github.com/RGRIVEROS-PORTFOLIO/cx-sentiment-analysis

---

## Resumen ejecutivo del proyecto

Este proyecto construye un sistema completo de CX Intelligence
en tres fases: análisis de sentimientos, sistema de alertas
automáticas y cola de atención priorizada con aging queue.

El sistema procesa reseñas de clientes, identifica insatisfacción
de forma automática y entrega al equipo de CX una cola de atención
ordenada por urgencia real — lista para operar cada mañana.

---

## Fase 1 — Análisis de Sentimientos

**Archivo:** `notebooks/Woman_s_EcommerceClothingReviews.ipynb`

### Hallazgo principal

El accuracy general es una métrica engañosa en datasets desbalanceados.
Con 77% de reseñas positivas, cualquier modelo que prediga siempre
positivo obtiene 77% sin analizar nada.

La métrica correcta para CX es el Recall en la clase negativa.

### Resultados

| Modelo | Accuracy | Recall Negative | F1 Negative |
|---|---|---|---|
| VADER | 77.44% | 0.15 | 0.23 |
| DistilBERT | 72.35% | **0.93** | **0.43** |

### Conclusión

DistilBERT detecta 93 de cada 100 clientes insatisfechos reales
vs 15 de VADER. Es 6 veces más efectivo para sistemas de alerta CX
a pesar de tener menor accuracy general.

---

## Fase 2 — Sistema de Alertas Automáticas

**Archivo:** `notebooks/alert_system_cx.ipynb`

### Qué hace

Procesa reseñas nuevas del día con DistilBERT y genera
un reporte Excel con alertas clasificadas por nivel de urgencia.

### Resultados sobre 500 reseñas

| Prioridad | Casos | Acción |
|---|---|---|
| 🔴 CRÍTICO | 107 | Contactar en menos de 2 horas |
| 🟠 ALTO | 25 | Contactar antes del cierre del día |
| 🟡 MEDIO | 13 | Revisar y evaluar |
| ✅ OK | 355 | Sin acción requerida |

### Valor operativo

El equipo de CX recibe un Excel coloreado por urgencia cada mañana.
Sin leer una sola reseña manualmente. Sin criterio subjetivo.

---

## Fase 3 — Cola de Atención Priorizada

**Archivo:** `notebooks/priority_queue_cx.ipynb`

### Qué hace

Construye una cola de atención ordenada por score compuesto
que combina sentimiento, antigüedad y departamento.

### Lógica del score compuesto

| Factor | Peso | Justificación |
|---|---|---|
| Score de negatividad | 40% | Intensidad de la insatisfacción |
| Antigüedad sin gestión | 40% | Tiempo sin atención escala urgencia |
| Departamento | 20% | Impacto histórico en retención |

### Resultados sobre 145 alertas

| Prioridad | Casos |
|---|---|
| 🔴 CRÍTICO | 79 |
| 🟠 ALTO | 60 |
| 🟡 MEDIO | 6 |

Score compuesto promedio: **0.767**
Los 5 casos más urgentes acumulaban entre 137 y 142 horas sin gestión.

---

## Impacto del sistema completo

| Dimensión | Sin sistema | Con sistema |
|---|---|---|
| Tiempo de procesamiento | Horas | Menos de 3 minutos |
| Criterio de priorización | Subjetivo | Score compuesto objetivo |
| Casos no detectados | Frecuente | Cero |
| Escalada por antigüedad | Manual | Automática |

---

## Limitación identificada

DistilBERT genera falsos positivos en reseñas mixtas.
Reseñas que combinan aspectos positivos y negativos pueden
clasificarse como negativas por el tono del fragmento final.

Recomendación: revisión humana para casos con score de
sentimiento alto pero rating original 3 o 4.

---

## Conexión con experiencia real

Este sistema replica y automatiza el proceso implementado
manualmente en Goldstein Automotores (Ford) entre 2022 y 2025,
donde la gestión de alertas NPS se realizaba con Excel
y coordinación humana entre equipos.

Resultado manual obtenido:
- Reducción del TTR de 5 a 2 días
- NPS sostenido por encima del 85%
- Reducción de reclamos repetitivos en 30%

Este sistema elimina la fricción operativa que hacía
ese proceso dependiente de esfuerzo manual constante.