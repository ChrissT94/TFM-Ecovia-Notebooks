---
title: TFM Ecovía — Notebooks
---

# Comparación de modelos de aprendizaje automático para predecir el tiempo de llegada entre paradas en el sistema BRT Ecovía de Quito utilizando registros históricos de GPS

## Trabajo de Fin de Máster
**Universidad Internacional del Ecuador (UIDE)**  
**Maestría en Inteligencia Artificial Aplicada**  
**2026**

## Autores
- Ortega Campus Jhon Henry
- Ramos Mayorga Oscar Andrés
- Torres Chango Christian Damian

## Descripción
Este repositorio contiene los notebooks de desarrollo del TFM que compara seis modelos de aprendizaje automático para predecir el tiempo de llegada entre paradas del sistema BRT Ecovía de Quito, utilizando registros históricos de GPS proporcionados por Mivilsoft S.A. mediante el sistema SAE.

## Orden de ejecución

| Notebook | Descripción |
|---|---|
| `01_TFMEcovia_AnalisisExploratorio.ipynb` | Análisis exploratorio del dataset histórico |
| `02_TFMEcovia_ProcesamientoDatos.ipynb` | Limpieza y transformación del dataset |
| `03_TFMEcovia_Modelos_MinMaxScaler.ipynb` | Entrenamiento con normalización MinMaxScaler |
| `04_TFMEcovia_Modelos_StandardScaler.ipynb` | Entrenamiento con normalización StandardScaler |

## Modelos evaluados

| Modelo | Tipo | MAE promedio (seg) |
|---|---|---|
| XGBoost | Ensemble | 19.0 (Recomendado) |
| Gradient Boosting | Ensemble | 19.1 |
| GRU | Red neuronal recurrente | 20.6 |
| LSTM | Red neuronal recurrente | 20.9 |
| Regresión lineal | Baseline | 28.2 |
| Promedio histórico | Baseline | 48.3 |

## Resultados por ruta - XGBoost (MAE en segundos)

| Ruta | MAE (seg) | Ventana LSTM/GRU |
|---|---|---|
| E1 | 19.3 | 7 |
| E1M | 20.7 | 5 |
| E2_NS | 21.9 | 5 |
| E2_SN | 10.4 | 10 |
| E3_NS | 19.8 | 10 |
| E3_SN | 18.0 | 7 |
| E4 | 22.6 | 7 |

## Hallazgos principales

1. **XGBoost supera a LSTM y GRU** en todas las rutas con MAE promedio de 19.0 segundos
2. **StandardScaler mejora los modelos RNN** - LSTM mejora 1.6 seg y GRU mejora 1.2 seg respecto a MinMaxScaler
3. **La ruta E2_SN** tiene los mejores resultados con MAE=10.4 seg
4. **La ruta E4** tiene los peores resultados con MAE=22.6 seg
5. **El horario programado no predice** la operación real (correlación < 0.06)

## Dataset

- **Fuente:** Mivilsoft S.A. - Sistema SAE
- **Período:** 15/09/2025 - 15/03/2026
- **Registros originales:** 28,011,776
- **Registros limpios:** 24,308,817 (86.78% conservado)
- **Rutas:** E1, E1M, E2_NS, E2_SN, E3_NS, E3_SN, E4

> **Nota:** El dataset no está disponible en este repositorio por acuerdo de confidencialidad con Mivilsoft S.A.

## Prototipo web

El prototipo de predicción en tiempo real está disponible en:  
🚌 [Sistema ETA Ecovía - Panel de Operaciones](https://huggingface.co/spaces/ChrissHF/Dev-ML)

## Requisitos

```bash
pip install -r requirements.txt
```

## Tecnologías utilizadas

- Python 3.11
- TensorFlow 2.21 / Keras 3.15
- XGBoost 3.2
- Scikit-learn 1.9
- Pandas 3.0
- NumPy 2.4