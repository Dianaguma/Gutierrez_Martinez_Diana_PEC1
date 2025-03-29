# Gutierrez_Martinez_Diana_PEC1

# Análisis Exploratorio de Datos y Construcción del SummarizedExperiment
Diana Gutierrez Martínez
•	Fecha: 29/03/2025
•	UOC

# Introducción 

El análisis de datos ómicos se ha vuelto fundamental para entender los procesos biológicos detrás de diversas enfermedades y condiciones físicas. Dado que estos estudios involucran grandes cantidades de datos complejos, como los perfiles de metabolitos en diferentes contextos, es necesario utilizar estructuras de datos sofisticadas que permitan gestionar y analizar la información de manera efectiva. En este sentido, el rol del bioinformático es esencial. Este profesional no solo debe comprender a fondo los datos, sino también interpretar y analizar los metadatos asociados para obtener conclusiones significativas de los estudios. Gracias a su expertise, se pueden extraer resultados valiosos que ayuden a avanzar en el conocimiento de estos procesos biológicos.

Para ello he creado un archivo Rda  desde R-studio que he adjuntado a este proyecto llamado **Gutierrez_Martinez_Diana_PEC1** de la clase SummarizedExperiment. Este archivo llamado **SummarizedExperiment_Diana_Gutiérrez.rda** es una extensión moderna y poderosa de la clase ExpressionSet, que se usa para la biología computacional para poder manejar y analizar datos ómicos. SummarizedExperiment nos da datos de manera estructurada y nos ayuda a almacenar datos experimentales, metadatos de muestras (como IDs de pacientes, condiciones experimentales) y metadatos de características (como información sobre los metabolitos o genes estudiados). Y así nos es más comodo trabajar con paquetes como Bioconductor, como DESeq2 o edgeR, para análisis de datos de secuenciación de alto rendimiento, y en este caso, para el análisis de metabolitos. Como podemos ver en el archivo agregado llamado PEC1.Rmd en formato R Markdown. 

En este análisis, se está trabajando con un conjunto de datos de metabolómica que incluye mediciones de metabolitos en pacientes con cachexia, que consiste en una pérdida significativa de masa muscular entre otros síntomas. Los datos contienen tanto las concentraciones de diversos metabolitos como metadatos clínicos, la identificación del paciente y el estado de pérdida muscular. Por tanto he creado una estructura de datos SummarizedExperiment para organizar estos datos de manera que facilite su análisis, permitiendo explorar correlaciones entre los metabolitos y realizar análisis más profundos sobre su papel en la cachexia.

Para ello he tenido que preparar los datos, integrar metadatos, crear el objeto SummarizedExperiment, y hacer un análisis exploratorio inicial a través de una visualización de la correlación entre los metabolitos. Para así proporcionar una visión general sobre las interrelaciones entre los metabolitos y su posible vinculación con la pérdida muscular, todo dentro del marco estructurado y eficiente de la clase SummarizedExperiment.

# Objetivo del análisis.

Evaluar las concentraciones de diversos metabolitos para identificar posibles biomarcadores de condiciones clínicas y metabólicas en los pacientes.

# Selección y Justificación del Dataset 

El dataset proviene del repositorio nutrimetabolomics/metaboData en GitHub y contiene datos sobre concentraciones de metabolitos en pacientes, incluyendo información sobre la pérdida muscular (Muscle loss) y diversos metabolitos relacionados con el metabolismo energético y la función muscular. Las principales variables del dataset incluyen identificadores de pacientes (Patient ID), pérdida muscular y una serie de metabolitos que pueden proporcionar información sobre el estado metabólico de los individuos. Los metabolitos incluidos, como Anhydro-β-D-glucose, Methylnicotinamide, Aminobutyrate, entre otros, son relevantes porque están involucrados en vías metabólicas que afectan la síntesis de proteínas, el balance energético y el funcionamiento muscular. La medición de estos metabolitos puede ayudar a entender mejor los cambios metabólicos en la caquexia, una condición caracterizada por la pérdida de masa muscular y debilidad, a menudo observada en enfermedades crónicas como el cáncer y la insuficiencia cardíaca, proporcionando posibles biomarcadores de diagnóstico y objetivos terapéuticos.

# Incorporación de los Datos a SummarizedExperiment 

Para poder crear datos en formato SummarizedExpriment: 

  # Instalar y cargar librerías: 
  Primero, se instalan y cargan librerías necesarias, como usethis, BiocManager, SummarizedExperiment, y readr, así manejo el archivos CSV  llamado human_cachexia y creo un objeto de tipo SummarizedExperiment (adjunto en el proyecto llamado: SummarizedExperiment_Diana_Gutiérrez.rda.)

  # Leo el archivo CSV que contiene datos de pacientes, la pérdida muscular y las concentraciones de metabolitos.
    Los datos se separan en dos partes: Metadatos (como el ID del paciente y la pérdida muscular). Datos experimentales (mediciones de los metabolitos).

  # Limpieza de datos: 
    Elimino filas con valores faltantes (NA) en los metadatos y aseguro que las filas en los datos experimentales coincidan con los metadatos del paciente. 
    Además, elimino duplicados si los hay.
    
  # Alineación de los datos: 
  
  Miro que los datos de las filas de metadatos y las mediciones de metabolitos estén alineados correctamente, para ello uso las identificaciones de los pacientes.

  # Creación del objeto SummarizedExperiment:
  
    Utilizo la función **SummarizedExperiment()**. El conjunto de datos de metabolitos se almacena en el slot assays, bajo el nombre counts, y los metadatos del paciente en el slot colData.

  # Guardar el objeto:
  
  El objeto SummarizedExperiment se guarda en un archivo .rda para su posterior análisis (adjunto en Github): Gutierrez_Martinez_Diana_PEC1 

Los resultados que nos muestra el SummarizedExperiment son: 

        
        class: SummarizedExperiment 
        #dim: 63 63 
        #metadata(0):
        #assays(1): counts
        #rownames(63): PIF_178 PIF_087 ... NETCR_008_V1 NETCR_008_V2
        #rowData names(1): MuscleLoss
        #colnames(63): 1,6-Anhydro-beta-D-glucose 1-Methylnicotinamide ...
        #  pi-Methylhistidine tau-Methylhistidine
        #colData names(2): Patient ID Muscle loss

# Explicación detallada de los datos 

La **Clase** (class: SummarizedExperiment): Aqui veo que el objeto es de tipo SummarizedExperiment, clase estructurada en R diseñada para almacenar datos experimentales junto con metadatos a más de información relevante para análisis de datos omicos (como metabolómica, transcriptómica, etc.).

La **dimension de nuestro objeto** es de 63 filas y 63 columnas, lo que sugiere que: hay 63 muestras de pacientes y 63 columnas con mediciones de 63 metabolitos diferentes en esas muestras. 

Vemos que los **Metadatos (metadata(0))**: Significa qu no hay metadatos adicionales asociados a este objeto en este caso. No he almacenado informacion extra. 

**Asimetría de datos (assays(1): counts)**: El objeto tiene un solo conjunto de datos en el slot assays llamado counts, que es la matriz de mediciones de los metabolitos. Este es el conjunto de datos principal que contiene las concentraciones de los metabolitos en las muestras.

**(rownames(63))**: Las filas pertenecen a los pacientes, con identificadores como PIF_178, PIF_087, etc. IDs de los pacientes de la base de datos que se utilizaron en el análisis.

Datos de las filas (rowData names(1): MuscleLoss): La variable rowData tiene una sola columna, llamada MuscleLoss, que indica la pérdida de masa muscular en cada paciente.
Nombres de las columnas (colnames(63)): Las columnas corresponden a los **metabolitos medidos**, como 1,6-Anhydro-beta-D-glucose, 1-Methylnicotinamide, etc. Estas mediciones pueden ser importantes para entender cómo varía el metabolismo entre pacientes con diferente grado de pérdida muscular.

Datos de las columnas (colData names(2): Patient ID, Muscle loss): El **slot colData** contiene dos columnas: Patient ID: El identificador de cada paciente. Muscle loss: El grado de pérdida de masa muscular para cada paciente. Este es el factor principal en el estudio de la caquexia, por lo que este dato es esencial para cualquier análisis correlacionando los metabolitos con la severidad de la enfermedad.

# Análisis Exploratorio de los Datos (2-3 páginas)

•	Estadísticas descriptivas: análisis inicial para obtener una visión general del dataset.
•	Distribución de las variables:
o	Muscle loss: visualización de la distribución de pacientes según el grado de pérdida muscular.
o	Metabolitos: gráficas para identificar la variabilidad de los metabolitos entre pacientes.
•	Visualización de datos:
o	Gráficos de barras o boxplots que comparen los niveles de metabolitos entre pacientes con diferentes grados de caquexia.
o	Posible uso de PCA (análisis de componentes principales) para observar agrupamientos entre pacientes.
•  Interpretación de Resultados desde el Punto de Vista Biológico (2-3 páginas)
•	Resultados clave: relación entre los metabolitos y la pérdida de masa muscular (muscle loss).
•	Agrupamiento de pacientes: explicación de cómo las diferentes concentraciones de metabolitos pueden ser indicativas de la condición clínica de los pacientes.
•	Posibles implicaciones biológicas: cómo el análisis puede contribuir al entendimiento de la caquexia en humanos y el papel de los metabolitos en el proceso.
•  Conclusiones (0.5-1 página)
•	Resumen de los hallazgos más importantes.
•	Reflexiones sobre las limitaciones del análisis y posibles estudios futuros.
•  Anexos (opcional)
•	Fragmentos de código utilizados (si es necesario).

