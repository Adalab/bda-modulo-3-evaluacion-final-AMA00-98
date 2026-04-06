# Análisis de Datos de Sector Aerolínea - Fidelización de Clientes 

## Contexto del Proyecto
Este proyecto forma parte de la **evaluación final del Módulo 3 (Análisis de Datos con Python)** del bootcamp de Data Analytics de Adalab. El objetivo principal es aplicar los conocimientos adquiridos en exploración, limpieza, análisis estadístico y visualización de datos sobre un conjunto de datos real de una aerolínea, centrado en la actividad de vuelo y el programa de fidelización de sus clientes.

## Descripción de los Datos
El proyecto trabaja con dos conjuntos de datos iniciales que se integran para obtener una visión completa del comportamiento del cliente:

1.  **Customer Flight Activity (`customer flight activity.csv`)**: Contiene registros detallados de la actividad de vuelo de los clientes, incluyendo:
    *   Número de vuelos reservados y totales.
    *   Distancia recorrida.
    *   Puntos de fidelidad acumulados y canjeados.
    *   Coste en dólares de los puntos canjeados.
2.  **Customer Loyalty History (`customer loyalty history.csv`)**: Proporciona información demográfica y de perfil de fidelización:
    *   Ubicación (país, provincia, ciudad).
    *   Perfil socioeconómico (género, nivel educativo, salario, estado civil).
    *   Datos del programa (tipo de tarjeta, CLV - Customer Loyalty Value, fechas de inscripción y cancelación).
3.  **Dataset Combinado (`combinado_limpio.csv`)**: Archivo generado tras la fase de limpieza que une ambas fuentes de información mediante el identificador único `Loyalty Number`.

## Fases del Proyecto
El proyecto se ha estructurado en tres fases diferenciadas, cada una documentada en su respectivo notebook:

### Fase 01: Exploración y Limpieza
En esta etapa se realizó el Análisis Exploratorio de Datos (EDA) inicial para garantizar la calidad de la información:
*   **Gestión de Duplicados**: Eliminación de registros repetidos en la actividad de vuelo.
*   **Tratamiento de Nulos**: 
    *   Imputación de la mediana en la variable `Salary` tras corregir valores negativos.
    *   Categorización como "Desconocido" para los datos de cancelación, interpretando el nulo como la ausencia de baja en el programa.
*   **Unión de Datasets**: Integración mediante un *inner join* para trabajar únicamente con clientes que tienen registro tanto de perfil como de actividad.

### Fase 02: Análisis Estadístico
Análisis descriptivo profundo de las variables para entender las tendencias de los datos:
*   **Variables Numéricas**: Cálculo de medidas de tendencia central y dispersión. Identificación de valores atípicos (*outliers*) en variables como `CLV`, `Salary` y `Distance`.
*   **Correlaciones**: Identificación de relaciones fuertes, destacando la correlación positiva entre distancia recorrida y puntos acumulados.
*   **Variables Categóricas**: Análisis de frecuencias para entender la distribución de niveles educativos, tipos de tarjeta y estados civiles.

### Fase 03: Visualización
Generación de gráficos interactivos y estáticos para responder a preguntas de negocio:
1.  **Estacionalidad**: Identificación de picos de reserva en los meses de verano (julio).
2.  **Relación Distancia-Puntos**: Confirmación visual de la tendencia positiva entre vuelo y recompensa.
3.  **Distribución Geográfica**: Localización de los principales mercados en Ontario, British Columbia y Quebec.
4.  **Perfil Económico**: Comparativa de salarios promedio según nivel educativo, confirmando mayores ingresos en clientes con Máster y Doctorado.
5.  **Fidelización**: Visualización de la cuota de mercado de cada tipo de tarjeta (Star, Nova, Aurora).

## Tecnologías Utilizadas
*   **Lenguaje**: Python 3.14.2.
*   **Librerías de Análisis**: Pandas, Numpy.
*   **Librerías de Visualización**: Matplotlib, Seaborn.
*   **Entorno**: Jupyter Notebook en VS Code.

## Conclusiones
*   La actividad de los clientes es altamente estacional, con una clara preferencia por los viajes en el tercer trimestre del año.
*   El programa de fidelización muestra una estructura clara donde la acumulación de beneficios está directamente ligada al uso intensivo del servicio (distancia).
*   Existe un nicho de clientes de alto valor (CLV) con niveles educativos superiores y salarios más altos que tienden a concentrarse en provincias específicas de Canadá.
*   La tarjeta "Star" es la opción de entrada o más común, mientras que las tarjetas "Nova" y "Aurora" representan segmentos más exclusivos que requieren estrategias de retención diferenciadas.
