# Reto Ternium 2026

Proyecto de análisis y optimización del proceso de armado de tarimas, 
desarrollado en colaboración entre el ITESM y Ternium (enero–junio 2026).
El objetivo es derivar reglas de armado desde el histórico de despachos 
y proponer un algoritmo que minimice los desarmes de tarimas.

## Requisito previo

Para poder correr los notebooks es necesario incluir manualmente el archivo
`ultimos13a7meses.xlsx` en la carpeta `/data`. Este archivo no está en el 
repositorio para evitar filtrar datos confidenciales de Ternium a personas 
no autorizadas. Por la misma razón, la carpeta `/outputs` se encuentra vacía 
— el `.gitignore` impide que los archivos generados se suban al repositorio.

## Flujo de trabajo

Los notebooks deben correrse en el siguiente orden:

1. `01_limpieza` — Limpieza de datos: eliminación de valores nulos y 
   selección de variables relevantes para el análisis.
2. `02_vista_tarimas` — Agrupación de cintas por tarima y creación de 
   variables para los modelos.
3. `Modelado_01` — Modelos de machine learning para identificar los factores 
   asociados al desarme de tarimas.
4. `Script_definir_maximos_reglas` — Derivación de las reglas de armado 
   (peso máximo y número máximo de cintas por tarima) a partir de consultas 
   SQL sobre el histórico. Este archivo se trabajo aparte del repositorio y unicamente se adjunta en el mismo como evidencia del trabajo. Se adjunta el output de este código con otro nombre, "num_parte_hijo_consignatario.csv" a la carpeta de /data para correr el algoritmo heuristico.
5. `heuristicaCodigo` — Algoritmo heurístico greedy para el armado óptimo 
   de tarimas respetando todas las restricciones operativas.

Las consultas SQL utilizadas para derivar las reglas de armado están 
documentadas en `notebooks/Consultas_sql.txt`.

## Estructura del repositorio

### `/data`
Carpeta de datos de entrada. Es necesario colocar aquí el archivo 
`ultimos13a7meses.xlsx` antes de correr cualquier notebook.

### `/notebooks`
Contiene todos los notebooks y scripts del proyecto. Ver el flujo de 
trabajo descrito arriba para el orden de ejecución.

### `/outputs`
Carpeta donde se guardan los archivos generados por cada notebook, 
los cuales son utilizados como input por los notebooks siguientes. 
El archivo `heuristica_tarimas.csv` contiene el armado de tarimas 
propuesto por el algoritmo en base a las reglas derivadas.
