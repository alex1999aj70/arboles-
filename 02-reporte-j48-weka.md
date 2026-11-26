# Reporte: algoritmo J48 aplicado a Iris en Weka

**Autor:** Alejandro del Jesus Diaz Lopez · Matrícula 191087
**Materia:** Programación avanzada (IA) · FCI UNACAR · Profesor: Jesús Alejandro Flores Hernández

> **Nota para ti (bórrala antes de entregar):** los resultados de este reporte salieron de ejecutar J48 de Weka con sus valores por defecto (`-C 0.25 -M 2`) por línea de comandos, con la versión 3.6.14 de Weka y los datos de Iris de Fisher. Abre Weka en tu computadora, repite los pasos de la sección 2 y compara: el árbol y los números deben salir iguales o casi iguales. Reemplaza las capturas marcadas con las de tu pantalla.

## 1. Objetivo

Aplicar el algoritmo J48 (la implementación en Weka de C4.5, una versión mejorada de ID3) al conjunto de datos Iris y contrastar el árbol obtenido con el que se construyó con ID3 (ver `01-id3-iris.pdf`).

## 2. Procedimiento

1. Instalar Weka desde https://waikato.github.io/weka-wiki/downloading_weka/.
2. Abrir Weka y hacer clic en **Explorer**.
3. En la pestaña **Preprocess**, abrir el archivo `iris.arff` (carpeta `data` de la instalación, por ejemplo `C:\Program Files\Weka-3-8-6\data`).
4. En la pestaña **Classify**, elegir como atributo de clase `class` (la especie).
5. Elegir el clasificador **trees → J48** con los parámetros por defecto (factor de confianza 0.25, mínimo de 2 instancias por hoja).
6. En **Test options**, elegir **Cross-validation, 10 folds** y hacer clic en **Start**.
7. Clic derecho sobre el resultado en la lista y **Visualize tree**.

**Captura 1:** pantalla de Weka con `iris.arff` cargado (Preprocess).
`[inserta aquí tu captura]`

## 3. Resultados

**Captura 2:** salida del clasificador (Classifier output).
`[inserta aquí tu captura]`

| Dato | Con el conjunto de entrenamiento | Con validación cruzada de 10 pliegues |
| ---- | -------------------------------- | ------------------------------------- |
| Instancias clasificadas correctamente | 147 (98 %) | 144 (96 %) |
| Instancias clasificadas incorrectamente | 3 (2 %) | 6 (4 %) |
| Estadístico Kappa | 0.97 | 0.94 |
| Número de hojas | 5 | 5 |
| Tamaño del árbol | 9 | 9 |

### Árbol de decisión

**Captura 3:** árbol (Visualize tree).
`[inserta aquí tu captura]`

Árbol podado que muestra Weka (entre paréntesis: flores que llegan a la hoja / flores mal clasificadas):

```
petalwidth <= 0.6: Iris-setosa (50.0)
petalwidth > 0.6
|   petalwidth <= 1.7
|   |   petallength <= 4.9: Iris-versicolor (48.0/1.0)
|   |   petallength > 4.9
|   |   |   petalwidth <= 1.5: Iris-virginica (3.0)
|   |   |   petalwidth > 1.5: Iris-versicolor (3.0/1.0)
|   petalwidth > 1.7: Iris-virginica (46.0/1.0)
```

En palabras: si el ancho del pétalo es menor o igual a 0.6 cm, es setosa. Si es mayor a 1.7 cm, es virginica. En el rango intermedio se decide con el largo del pétalo (hasta 4.9 cm, versicolor) y, si es mayor, con el ancho del pétalo otra vez.

### Matriz de confusión

Con el conjunto de entrenamiento (150 flores):

```
  a  b  c   <-- classified as
 50  0  0 |  a = Iris-setosa
  0 49  1 |  b = Iris-versicolor
  0  2 48 |  c = Iris-virginica
```

Con validación cruzada de 10 pliegues:

```
  a  b  c   <-- classified as
 49  1  0 |  a = Iris-setosa
  0 47  3 |  b = Iris-versicolor
  0  2 48 |  c = Iris-virginica
```

## 4. Contraste con el árbol de ID3

| Aspecto | ID3 (hecho a mano / en Python) | J48 (Weka) |
| ------- | ------------------------------ | ---------- |
| Atributo en la raíz | `petal_width` | `petalwidth` |
| Manejo de atributos numéricos | Se discretizan antes en 3 intervalos de igual ancho (bajo, medio, alto) | Elige cortes del tipo `atributo <= valor` (0.6, 1.7, 4.9, 1.5) |
| Poda | No | Sí (árbol podado) |
| Número de hojas | 17 hojas (8 sin ninguna flor; 9 con flores) | 5 hojas |
| Exactitud | 98 % (147/150, con los mismos datos de entrenamiento) | 98 % con el conjunto de entrenamiento; 96 % con validación cruzada |

## 5. Conclusiones

- En los dos árboles el atributo más importante es el **ancho del pétalo** (`petal_width`), que queda en la raíz; el largo del pétalo es el segundo.
- J48 genera un árbol mucho más pequeño (5 hojas contra 17 de ID3). Esto se debe a que no necesita discretizar los atributos numéricos y a que **poda** el árbol: elige cortes numéricos directamente y no deja ramas sin ejemplos.
- Con los mismos datos de entrenamiento ambos aciertan 147 de 150 flores (98 %). Con validación cruzada de 10 pliegues, J48 baja a 96 %, que es una estimación más confiable de cómo clasificaría flores nuevas.
- En ambos casos, los errores son entre *versicolor* y *virginica*; *setosa* se separa sin errores con una sola pregunta.
- ID3 es más simple de seguir paso a paso y sirve para entender la entropía y la ganancia, pero J48 es más práctico porque maneja atributos numéricos y evita árboles demasiado grandes.
