# 1ACC0219-TP-TF-2026-01

## Clasificación de noticias falsas en español mediante técnicas de Data Science

Este repositorio contiene el desarrollo del Trabajo Final del curso **1ACC0219 - Aplicaciones de Data Science** de la **Universidad Peruana de Ciencias Aplicadas (UPC)**. El proyecto aplica técnicas de Procesamiento de Lenguaje Natural y aprendizaje automático para clasificar noticias en español como falsas o verdaderas.

## Objetivo

El objetivo del proyecto es desarrollar un modelo de clasificación automática capaz de identificar si una noticia en español es falsa o verdadera a partir de su contenido textual. Para ello, se realiza un proceso completo de Ciencia de Datos que incluye análisis exploratorio de datos, preprocesamiento textual, modelización, evaluación de resultados y análisis de explicabilidad.

El trabajo busca responder si las características lingüísticas, textuales y estilométricas de una noticia pueden aportar información útil para diferenciar contenido falso de contenido verdadero.

## Integrantes

| Código     | Integrante                       |
| ---------- | -------------------------------- |
| U202421876 | Gustavo Antonio Perez Rojas      |
| U20211B598 | Jesús Andrés Millones Espinoza   |
| U20231E612 | Jersson Aldair Aguilar Dominguez |

## Estructura del repositorio

```text
1ACC0219-TP-TF-2026-01/
│
├── code/
│   ├── EDA_AplicacionesDeDataScience.ipynb
│   └── ModelizacionAplicacionesDataScience.ipynb
│
├── data/
│   └── dataset utilizado o referencia al dataset original
│
├── README.md
└── LICENSE
```

## Dataset

El dataset utilizado corresponde al corpus **Fake News Corpus Spanish**, disponible en Hugging Face:

https://huggingface.co/datasets/mariagrandury/fake_news_corpus_spanish

El conjunto de datos contiene noticias en español clasificadas como falsas o verdaderas. Inicialmente cuenta con 572 registros y las siguientes variables principales:

| Variable   | Descripción                            |
| ---------- | -------------------------------------- |
| `ID`       | Identificador único de la noticia      |
| `CATEGORY` | Clase de la noticia: falsa o verdadera |
| `TOPICS`   | Tema principal de la noticia           |
| `SOURCE`   | Fuente o medio de origen               |
| `HEADLINE` | Titular de la noticia                  |
| `TEXT`     | Texto completo de la noticia           |
| `LINK`     | Enlace de referencia                   |

Para la modelización final se trabajó con los tres temas principales del dataset: **Covid-19**, **Sociedad** y **Política**, obteniendo un subconjunto de 539 noticias. Esta selección permitió concentrar el análisis en los temas con mayor cantidad de registros y reducir el ruido generado por categorías con muy pocos ejemplos.

## Técnicas utilizadas

Durante el desarrollo del proyecto se aplicaron las siguientes técnicas:

* Análisis Exploratorio de Datos (EDA).
* Limpieza y preprocesamiento textual.
* Procesamiento de Lenguaje Natural (NLP).
* Vectorización de textos mediante TF-IDF.
* Extracción de variables estilométricas.
* Clasificación binaria con Random Forest.
* Evaluación mediante métricas de clasificación.
* Matriz de confusión.
* Curva ROC y AUC ROC.
* Análisis de explicabilidad mediante importancia de características.

## Modelos evaluados

Se evaluaron diferentes configuraciones basadas en Random Forest y TF-IDF:

| Modelo                                        | Accuracy | Precision clase falsa | Recall clase falsa | AUC ROC |
| --------------------------------------------- | -------: | --------------------: | -----------------: | ------: |
| RF + TF-IDF | umbral 0.50                     |   0.6852 |                0.6282 |             0.9074 |  0.8057 |
| RF + TF-IDF | umbral 0.70                     |   0.6481 |                0.8333 |             0.3704 |  0.8057 |
| RF + TF-IDF + estilo | umbral 0.50            |   0.6667 |                0.6154 |             0.8889 |  0.8001 |
| RF + TF-IDF + stemming | umbral 0.50          |   0.6574 |                0.6049 |             0.9074 |  0.7985 |
| RF + TF-IDF optimizado | umbral 0.50          |   0.7407 |                0.7097 |             0.8148 |  0.8169 |
| RF + TF-IDF optimizado + estilo | umbral 0.50 |   0.7593 |                0.7333 |             0.8148 |  0.8234 |

El mejor modelo propio fue **Random Forest + TF-IDF optimizado + variables estilométricas**, con un **Accuracy de 0.7593** y un **AUC ROC de 0.8234**.

## Resultados principales

El modelo final logró clasificar correctamente una proporción importante de noticias falsas y verdaderas. En la matriz de confusión se obtuvo:

| Clase real | Predicha verdadera | Predicha falsa |
| ---------- | -----------------: | -------------: |
| Verdadera  |                 38 |             16 |
| Falsa      |                 10 |             44 |

Esto significa que el modelo clasificó correctamente **44 de 54 noticias falsas** y **38 de 54 noticias verdaderas**. Además, el AUC ROC de **0.8234** indica una buena capacidad de separación entre ambas clases.

## Comparación con trabajos previos

El modelo propio fue comparado con dos trabajos de referencia:

| Referencia                     | Modelo                          | Accuracy |
| ------------------------------ | ------------------------------- | -------: |
| Llaberia (2025)                | BETO + fine-tuning secuencial   |   0.8205 |
| Martínez-Gallego et al. (2021) | Random Forest + TF-IDF          |   0.8020 |
| Modelo propio final            | RF + TF-IDF optimizado + estilo |   0.7593 |

Aunque el modelo desarrollado no superó los resultados de los papers revisados, logró un rendimiento aceptable considerando que se utilizó un dataset filtrado de 539 noticias y un enfoque clásico basado en TF-IDF y Random Forest.

## Explicabilidad

Para interpretar el comportamiento del modelo se utilizó la importancia de características del Random Forest. Las variables más relevantes provinieron de dos fuentes:

1. Términos textuales generados mediante TF-IDF.
2. Variables estilométricas derivadas del texto.

Entre los términos relevantes se identificaron palabras asociadas a temas de salud, Covid-19, vacunación, sociedad y política. Además, las variables estilométricas como longitud del texto, signos de interrogación, exclamaciones, dígitos y proporción de mayúsculas aportaron información complementaria al modelo.

## Conclusiones

El proyecto permitió comprobar que las técnicas de Procesamiento de Lenguaje Natural y aprendizaje automático pueden aplicarse para clasificar noticias falsas y verdaderas en español. El mejor modelo propio fue **Random Forest + TF-IDF optimizado + variables estilométricas**, alcanzando un **Accuracy de 0.7593** y un **AUC ROC de 0.8234**.

Si bien el resultado no superó a los papers de referencia, esto puede explicarse por limitaciones como el tamaño reducido del dataset filtrado, el uso de un modelo clásico frente a modelos contextuales como BETO, la exclusión de variables como `SOURCE` para evitar fuga de información y el uso de una única partición train/test. Aun así, el modelo obtuvo un desempeño aceptable y mostró que las variables estilométricas pueden mejorar la clasificación.

Como trabajo futuro, se propone ampliar el dataset, aplicar validación cruzada, probar modelos basados en transformers como BETO o RoBERTa en español, optimizar hiperparámetros con técnicas más sistemáticas y utilizar métodos de explicabilidad más avanzados como SHAP o LIME.

## Licencia

Este proyecto se distribuye bajo la licencia **MIT**. Consulta el archivo `LICENSE` para más información.
