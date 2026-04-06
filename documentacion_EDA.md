# Fase 1. Exploración y limpieza de datos (EDA)

## 1. Objetivo de esta fase

En esta primera fase `se realizó un análisis exploratorio inicial de los dos conjuntos de datos proporcionados: "customer flight activity" y "customer loyalty history"`. El objetivo fue comprender la estructura de ambos archivos, detectar posibles problemas de calidad del dato y dejar preparado un único DataFrame limpio y coherente.

## 2. Exploración inicial de los datasets

En primer lugar, se cargaron ambos archivos .csv y se realizó una inspección general con funciones como `head(), shape(), info(), isna().sum() y decsribe()`. Esta exploración permitió conocer el número de filas y columnas de cada conjunto de datos, identificar los nombres de las variables, revisar sus tipos de datos y detectar la presencia de valores nulos.

Además, se analizó cada DataFrame por separado antes de unirlos, con el fin de entender mejor el papel de cada uno dentro del ejercicio:

- **"customer flight activity"**: Contiene información sobre la actividad de vuelos de los clientes, como el número de vuelos reservados, la distancia volada y los puntos acumulados o canjeados. Cuenta con: 324333 filas y 10 columnas.
- **"customer loyalty history"**: Recoge información del perfil del cliente, incluyendo ubicación, educación, salario, estado civil, tipo de tarjeta y datos relacionados con la inscripción y cancelación del programa de fidelización. Cuenta con: 16737 filas y 16 columnas.

Este análisis inicial permitió detectar desde el principio varios aspectos importantes: 

- La existencia de filas duplicadas en el dataset de "customer flight activity".
- La presencia de valores Nulos en el dataset de "customer loyalty history".
- La necesidad de usar una columna común para combinar ambos conjuntos de datos.
- Valores negativos en la columna numérica de "Salary".

## 3. Revisión de duplicados

Tras revisar los registros duplicados, se observó que el dataset "customer flight activity" contenía 1578 filas repetidas. Debido a que estas filas duplicadas podían afectar a los análisis posteriores, se eliminaron mediante `drop_duplicates()`.

En cambio, en "customer loyalty history" no se detectaron duplicados.

## 4. Revisión de Nulos

Después de estudiar los valores ausentes, se observó que las columnas con mayor presencia de nulos eran "Salary", "Cancellation Month" y "Cancellation Year".

- **Columna "Salary"** - 25.32%:

    - La variable "Salary" es una variable numérica, por lo que se valoró la posibilidad de imputar sus valores ausentes utilizando una medida de tendencia central. Antes de hacerlo, también se comprobó que la columna presentaba algunos valores negativos, lo cual no era coherente con el significado de la variable. Por ello, primero se corrigieron esos salarios negativos transformándolos a positivos mediante `abs()`.

    - Una vez corregida esa inconsistencia, los valores Nulos de "Salary" se sustituyeron por la mediana con `fillna().median()` de la propia columna. Esta decisión se tomó porque no se identificó una relación suficientemente clara con otras variables que permitiera imputar el salario de forma más específica y, al tratarse de una variable numérica, la mediana constituye una opción adecuada para representar el centro de los datos sin verse tan afectada por posibles valores extremos.

- **Columnas Cancellation Month y Cancellation Year** - 87.65% en ambos:

    - En el caso de "Cancellation Month" y "Cancellation Year", los valores Nulos no se interpretaron como un error del dato, sino como ausencia de cancelación.

    - Por ello, en lugar de imputar un mes o un año inventado, se optó por sustituir los Nulos por la etiqueta "Desconocido" con `fillna()`. De este modo, se evita mantener valores faltantes y, al mismo tiempo, se conserva una categoría que permite diferenciar entre clientes con cancelación registrada y clientes sin evidencia de cancelación. 

## 5. Unión de los dos datasets 

Una vez revisados ambos archivos, se unieron utilizando la columna "Loyalty Number", que actúa como identificador común del cliente en ambos conjuntos de datos. Para esta unión se utilizó `pd.merge()`, que es el método habitual para combinar DataFrames a partir de una clave compartida.

En este caso, se aplicó un `inner join`, de forma que el DataFrame final incluyera únicamente aquellos registros presentes en ambos conjuntos de datos. 

Tras la unión, se obtuvo un DataFrame combinado sobre el que se repitió la exploración inicial para comprobar su estructura, revisar de nuevo la presencia de Nulos y generar una visión general de las estadísticas descriptivas básicas.

## 6. Revisión de tipos de datos y consistencia

A lo largo de la limpieza también se revisaron los tipos de datos de las columnas tratadas para asegurar que fueran coherentes con el contenido de cada variable. En este caso, lo fueron y por lo tanto, no s ehicieron más cambios.

## 7. Resultado de la Fase 1

La fase de exploración y limpieza permitió transformar dos archivos independientes en una base de datos consolidada, consistente y apta para el análisis. Este paso fue fundamental para asegurar que las estadísticas, agrupaciones y visualizaciones de las fases posteriores se apoyaran en datos fiables y correctamente interpretados. En otras palabras, antes de analizar el comportamiento de los clientes, fue necesario garantizar que la información estuviera ordenada, sin duplicados relevantes y con un tratamiento razonado de las ausencias de información.