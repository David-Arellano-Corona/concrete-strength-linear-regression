# Concrete Strength — Linear Regression

Predicción de la resistencia a la compresión del concreto mediante regresión lineal múltiple y transformación de características.

## Objetivo

Construir, evaluar e interpretar un modelo capaz de estimar la resistencia a la compresión del concreto utilizando su composición y edad.

El proyecto compara el modelo contra un baseline, utiliza Cross-Validation, mantiene un conjunto Test aislado y analiza sus residuos, supuestos y limitaciones.

## Dataset

Se utilizó el dataset público [Concrete Compressive Strength](https://archive.ics.uci.edu/dataset/165/concrete+compressive+strength) del UCI Machine Learning Repository.

Contiene:

- 1,030 observaciones.
- 8 características numéricas.
- Una variable objetivo continua expresada en MPa.
- Sin valores faltantes.

### Características

- Cement
- Blast Furnace Slag
- Fly Ash
- Water
- Superplasticizer
- Coarse Aggregate
- Fine Aggregate
- Age

### Variable objetivo

- Concrete Compressive Strength (MPa)

## Metodología

1. Inspección inicial de los datos.
2. Separación 80/20 entre Train y Test.
3. Análisis exploratorio realizado únicamente sobre Train.
4. Construcción de un `DummyRegressor` como baseline.
5. Evaluación mediante 5-Fold Cross-Validation.
6. Entrenamiento de una regresión lineal múltiple.
7. Interpretación de coeficientes y análisis de residuos.
8. Identificación de una relación no lineal entre edad y resistencia.
9. Transformación de `Age` mediante `log(1 + Age)`.
10. Selección del modelo mediante Cross-Validation.
11. Evaluación final única sobre Test.

## Resultados de validación

| Modelo | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 13.580 MPa | 16.890 MPa | -0.012 |
| Regresión lineal | 8.422 MPa | 10.627 MPa | 0.597 |
| Regresión lineal + log(Age) | **5.612 MPa** | **7.352 MPa** | **0.807** |

La transformación logarítmica de la edad permitió representar mejor el crecimiento rápido de la resistencia durante los primeros días y su desaceleración posterior.

## Evaluación final en Test

| Métrica | Resultado |
|---|---:|
| MAE | 5.320 MPa |
| MSE | 44.576 MPa² |
| RMSE | 6.676 MPa |
| R² | 0.827 |

Los resultados de Test fueron consistentes con Cross-Validation, sin una degradación relevante ante datos aislados.

El mayor error absoluto observado en Test fue de 16.775 MPa. En ese caso, el modelo predijo 38.695 MPa para una resistencia real de 21.92 MPa.

## Principales hallazgos

- El cemento, el superplastificante y la edad presentaron relaciones positivas con la resistencia.
- El agua presentó una relación negativa.
- La edad no mostró una relación completamente lineal.
- Transformar la edad produjo la mejora más importante.
- Train y Validation obtuvieron resultados similares, sin señales fuertes de overfitting.
- El modelo tiende a subestimar algunos concretos de alta resistencia.
- Un buen resultado promedio puede coexistir con errores individuales importantes.

## Limitaciones

- El dataset contiene solamente 1,030 observaciones.
- El modelo asume efectos principalmente aditivos.
- Puede omitir interacciones complejas entre ingredientes.
- Algunas características están correlacionadas entre sí.
- Los coeficientes representan asociaciones, no causalidad.
- Las predicciones fuera de los rangos de entrenamiento pueden ser poco confiables.
- El modelo no sustituye pruebas físicas ni evaluación profesional en decisiones de seguridad estructural.

## Estructura

```text
concrete-strength-linear-regression/
├── README.md
├── requirements.txt
├── notebooks/
│   └── concrete_strength_regression.ipynb
└── .gitignore
```

## Instalación

```bash
git clone <URL_DEL_REPOSITORIO>
cd concrete-strength-linear-regression

python -m venv .venv
```

Activación en Windows:

```bash
.venv\Scripts\activate
```

Activación en macOS o Linux:

```bash
source .venv/bin/activate
```

Instalación de dependencias:

```bash
pip install -r requirements.txt
jupyter lab
```

Después, abre y ejecuta:

```text
notebooks/concrete_strength_regression.ipynb
```

## Tecnologías

- Python
- NumPy
- pandas
- Matplotlib
- Seaborn
- scikit-learn
- ucimlrepo
- Jupyter

## Autor

Built as part of my journey toward AI/NLP/LLM Engineering.  
— SM