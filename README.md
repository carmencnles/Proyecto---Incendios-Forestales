# 📊 Análisis de la Matriz de Confusión en la Clasificación de Incendios Forestales

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit_learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

Este repositorio contiene el trabajo de investigación centrado en la **clasificación multiclase de la intensidad de incendios forestales** (Low, Moderate, High, Extreme). El proyecto evalúa críticamente el comportamiento de los modelos meteorológicos preventivos mediante el análisis profundo de la **Matriz de Confusión**, el tratamiento del desbalanceo de clases y el control de la fuga de datos (*Data Leakage*).

---

## 🗂️ Estructura del Proyecto

El repositorio se encuentra estructurado de forma limpia según los siguientes módulos técnicos:
* 📁 `matriz/`: Almacena los recursos gráficos y visualizaciones de las matrices de confusión generadas.
* 📁 `notebooks/`: Contiene el desarrollo experimental en Jupyter Notebook (`Trabajo_Carmen.ipynb`) y el archivo de respaldo Markdown (`Trabajo.md`).
* 📁 `pdf/`: Documento final y memoria de investigación lista para su lectura (`TrabajoMatriz_MCC.pdf`).

---

## 🚀 Resumen del Enfoque Técnico

### 1. Control de Fuga de Datos (*Data Leakage*)
Para medir el impacto de la integridad de las variables, se diseñaron tres escenarios predictivos:
* **Escenario 1 (Base):** Modelo inicial basado exclusivamente en variables climáticas esenciales (`temp_max`, `humidity`, `precip`).
* **Escenario 2 (Leakage):** Modelo con un **0.99 de Accuracy** artificial. Se identificó una fuga crítica al incluir `frp_mw` (potencia radiativa) y `brightness_k` (temperatura de brillo), variables que registran el incendio cuando ya está activo.
* **Escenario 3 (Modelo Predictivo Real):** Modelo honesto basado en 26 variables meteorológicas puras, obteniendo un **0.43 de Accuracy**, reflejando la complejidad real de la prevención climática.

### 2. Tratamiento del Desbalanceo de Clases
Debido a la naturaleza del problema, el conjunto de datos sufría un sesgo masivo hacia eventos `Moderate`. Para evitar un modelo trivial que ignorara las clases críticas (`High` y `Extreme`), se aplicó la penalización matemática:
```python
class_weight='balanced'
