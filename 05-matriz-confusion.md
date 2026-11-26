# Matriz de confusión (Naive Bayes, 20 observaciones al azar)

**Autor:** Alejandro del Jesus Diaz Lopez · Matrícula 191087

Se eligieron **20 observaciones de Iris al azar** y el clasificador Naive Bayes (gaussiano) se entrenó con las otras 130. Las filas son lo que dijo el clasificador y las columnas el valor real, como pide la actividad.

|               | setosa  | virginica | versicolor |
|:-------------:|:-------:|:---------:|:----------:|
| **setosa**    | 7 | 0 | 0 |
| **virginica** | 0 | 8 | 0 |
| **versicolor**| 0 | 0 | 5 |

**Aciertos:** 20 de 20.

## Las 20 observaciones

| # | fila de Iris | valor real | clasificador | acierta |
| - | ------------ | ---------- | ------------ | ------- |
| 1 | 127 | virginica | virginica | si |
| 2 | 97 | versicolor | versicolor | si |
| 3 | 101 | virginica | virginica | si |
| 4 | 112 | virginica | virginica | si |
| 5 | 113 | virginica | virginica | si |
| 6 | 4 | setosa | setosa | si |
| 7 | 45 | setosa | setosa | si |
| 8 | 118 | virginica | virginica | si |
| 9 | 52 | versicolor | versicolor | si |
| 10 | 11 | setosa | setosa | si |
| 11 | 64 | versicolor | versicolor | si |
| 12 | 24 | setosa | setosa | si |
| 13 | 105 | virginica | virginica | si |
| 14 | 90 | versicolor | versicolor | si |
| 15 | 140 | virginica | virginica | si |
| 16 | 50 | setosa | setosa | si |
| 17 | 26 | setosa | setosa | si |
| 18 | 131 | virginica | virginica | si |
| 19 | 15 | setosa | setosa | si |
| 20 | 86 | versicolor | versicolor | si |

## Nota

Esta matriz se calculó con Naive Bayes gaussiano en Python (cuaderno `iris-colab.ipynb`, sección 6, semilla 2026). La actividad pide probar el clasificador de la hoja de cálculo `naive-byes.iris.data.xls`; para entregar esa versión, se eligen 20 filas y se cuentan los resultados de esa hoja en la misma matriz.
