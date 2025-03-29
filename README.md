# Gutierrez-Martinez-Diana-PEC1

# Análisis Exploratorio de Datos y Construcción del SummarizedExperiment
Diana Gutierrez Martínez
•	Fecha: 29/03/2025
•	UOC

\textcolor{red}{Introducción }

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
Nombres de las columnas (colnames(63)): Las columnas corresponden a los **metabolitos medidos**, como 1,6-Anhydro-beta-D-glucose, 1-Methylnicotinamide, etc. Estas mediciones pueden ser importantes para entender cómo varía el metabolismo entre pacientes con diferente grado de pérdida muscular. Datos de las columnas (colData names(2): Patient ID, Muscle loss): El **slot colData** contiene dos columnas: Patient ID: El identificador de cada paciente. Muscle loss: El grado de pérdida de masa muscular para cada paciente. Este es el factor principal en el estudio de la caquexia, por lo que este dato es esencial para cualquier análisis correlacionando los metabolitos con la severidad de la enfermedad.

# Análisis Exploratorio de los Datos 

**Estadísticas descriptivas: análisis inicial para obtener una visión general del dataset.**
Podemos hacer un analisis inicial para poder ver una vision general de los datos entrando directamente al archivo rda. Y con el codigo: 
colData(se) # Vemos que efectivamente estan las dos variables Patient ID y Muscle loss y nos sale los metabolitos relacionados a la cachexia y a este proyecto. 
                    DataFrame with 63 rows and 2 columns
                                                 Patient ID Muscle loss
                                                <character>    <factor>
                    1,6-Anhydro-beta-D-glucose      PIF_178    cachexic
                    1-Methylnicotinamide            PIF_087    cachexic
                    2-Aminobutyrate                 PIF_090    cachexic
                    2-Hydroxyisobutyrate        NETL_005_V1    cachexic
                    2-Oxoglutarate                  PIF_115    cachexic
                    ...                                 ...         ...
                    cis-Aconitate              NETCR_005_V1     control
                    myo-Inositol                    PIF_111     control
                    trans-Aconitate                 PIF_171     control
                    pi-Methylhistidine         NETCR_008_V1     control
                    tau-Methylhistidine        NETCR_008_V2     control
Podemos ver el resumen de metadatos en columna
colnames(assays(se)$counts)
[1] "1,6-Anhydro-beta-D-glucose" "1-Methylnicotinamide"       "2-Aminobutyrate"           
 [4] "2-Hydroxyisobutyrate"       "2-Oxoglutarate"             "3-Aminoisobutyrate"        
 [7] "3-Hydroxybutyrate"          "3-Hydroxyisovalerate"       "3-Indoxylsulfate"          
[10] "4-Hydroxyphenylacetate"     "Acetate"                    "Acetone"                   
[13] "Adipate"                    "Alanine"                    "Asparagine"                
[16] "Betaine"                    "Carnitine"                  "Citrate"                   
[19] "Creatine"                   "Creatinine"                 "Dimethylamine"             
[22] "Ethanolamine"               "Formate"                    "Fucose"                    
[25] "Fumarate"                   "Glucose"                    "Glutamine"                 
[28] "Glycine"                    "Glycolate"                  "Guanidoacetate"            
[31] "Hippurate"                  "Histidine"                  "Hypoxanthine"              
[34] "Isoleucine"                 "Lactate"                    "Leucine"                   
[37] "Lysine"                     "Methylamine"                "Methylguanidine"           
[40] "N,N-Dimethylglycine"        "O-Acetylcarnitine"          "Pantothenate"              
[43] "Pyroglutamate"              "Pyruvate"                   "Quinolinate"               
[46] "Serine"                     "Succinate"                  "Sucrose"                   
[49] "Tartrate"                   "Taurine"                    "Threonine"                 
[52] "Trigonelline"               "Trimethylamine N-oxide"     "Tryptophan"                
[55] "Tyrosine"                   "Uracil"                     "Valine"                    
[58] "Xylose"                     "cis-Aconitate"              "myo-Inositol"              
[61] "trans-Aconitate"            "pi-Methylhistidine"         "tau-Methylhistidine"   

Miramos las condiciones de cada paciente relacionadas a la massa muscular : 
 
           se$`Muscle loss`
           [1] cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic
          [11] cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic
          [21] cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic
          [31] cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic cachexic
          [41] cachexic cachexic cachexic cachexic cachexic cachexic cachexic control  control  control 
          [51] control  control  control  control  control  control  control  control  control  control 
          [61] control  control  control 
          Levels: cachexic control

# Me enfoco en mirar las estadisticas descriptivas: 

Al hacer un  **summary(assays(se)$counts)** Si nos enfocamos en los resultados de los metabolitos obtengo en general una gran variabilidad en sus concentraciones. Si nos enfocamos en el citrato y la creatinina, vemos que estan mucho más elevados en comparación con otros. Estos valores son importantes en el análisis de condiciones fisiológicas y pueden ser claves en estudios relacionados con el metabolismo y patologías como la cachexia.

# Primero calculo la corrección entre los metabolitos 

Observo que los ácidos como el **succinato**, el **oxoglutarato** y el **ácido acético** tienen fuertes correlaciones entre ellos. Se que están involucrados en las rutas metabólicas relacionadas con el ciclo de Krebs, lo que indica una estrecha relación en la producción de energía.

En cambio la **acetona**, el **ácido acético**, y el **ácido adipato** tienen correlaciones significativas, sabemos que se relacionan entre si porque son metabolitos conectados con la utilización de grasas o la producción de cuerpos cetónicos, cuando estamos en ayuno o metabolismo alterado. 

La **glutamina**, la **alanina**, la **leucina**, la **serina** y la **valina** tienen relaciones entre sí, son importantes para el metabolismo celular y en la síntesis de proteínas. La **Glutamina** también es relevante en el metabolismo muscular y la respuesta inmunológica. Una menor concentración de glutamina (337.0968) podría estar relacionada con un estado de catabolismo muscular, común en la cachexia.

El **ácido pantoténico**, el **acetato** y el **nicotinamida** son coenzimas esenciales en las vías metabólicas, sobretodo en la producción de energía. 

Finalmente, el **ácido fenilacético** y el **indoxilsulfato** muestran correlaciones entre sí, creo que están involucrados en procesos antioxidantes y de detoxificación. Y son importantes en el metabolismo de los fenoles.

**Glucose** es un indicador importante del metabolismo energético. Su concentración más baja podría reflejar cambios en el uso de energía o el metabolismo de carbohidratos en pacientes con cachexia.

# Calculo la media de los metabolitos. 

Miro tambien la media de cada metabolito y observo que la **Creatinine** tiene el valor más alto de concentración entre los metabolitos estudiados, con **9521.7754**, seguido por Hippurate **2614.1479** y Citrate **2423.4689**. La creatinina podría ser uno de los metabolitos más presentes en las muestras que estás analizando. Este es un subproducto del metabolismo muscular, y ver valores elevados se han visto relacionados con la función renal y el estado muscular. Como el análisis parece estar centrado en la cachexia, la creatinina podría ser relevante para evaluar el daño muscular y la degradación proteica. El  **pi-Methylhistidine** es un marcador de degradación muscular y está presente en niveles moderados (391.5184), es importante analizar este marcador porque es relevante en pacientes cachexicos, ya que la degradación muscular es un proceso clave en esta condición. 


# Hago mapa de calor de la correlación entre metabolitos

Instalo el paquete igraph y cargo el paquete. Estableces un umbral (threshold) de 0.7. Este valor se usará para filtrar las correlaciones. Hago una copia de la matriz de correlación original (cor_matrix) y la asigno a una nueva variable llamada cor_matrix_filtered. Modifico **cor_matrix_filtered** estableciendo a cero todas las correlaciones cuya magnitud sea menor que 0.7. Por tanto las correlaciones débiles se eliminan, dejando solo aquellas con correlaciones fuertes (mayores o iguales a 0.7 o menores o iguales a -0.7). Creo un mapa de correlación y guardo ese gráfico en un archivo PNG en mi escritorio. 

# Analisis de PCA
PC1 tiene una desviación estándar significativamente mayor (7.488), por tanto esto indica que representa una gran parte de la variabilidad en los datos. Esto es consistente con la proporción de varianza de 0.890, lo que significa que el PC1 explica el 89% de la variabilidad en los datos.  PC2 tiene una desviación estándar mucho menor (1.6894) y una proporción de varianza de 0.0453, explicando solo el 4.53% de la variabilidad en los datos. La **proporción acumulada** muestra que después de las primeras 10 componentes principales (PC), ya se ha explicado más del 99% de la variabilidad. Por tanto, esto indica que para la mayoría de los análisis, podrías trabajar con solo las primeras 2-3 componentes y aún así capturar casi toda la variabilidad en los datos.


# Conclusiones 

Los resultados de las correlaciones metabólicas sugieren varias formas en las que el síndrome de caquexia puede estar relacionado con alteraciones en el metabolismo energético, la descomposición de proteínas, la inflamación sistémica y la disfunción de las vías de señalización celular. Los metabolitos observados en este análisis están directamente involucrados en las vías que se alteran en la caquexia, lo que indica que los cambios metabólicos descritos podrían ser indicativos de los procesos subyacentes a la pérdida de masa muscular, la fatiga, la alteración de los procesos energéticos y el aumento de la inflamación crónica.

El entendimiento de cómo estos metabolitos interactúan entre sí podría ayudar en el diseño de estrategias terapéuticas para tratar o mitigar los efectos de la caquexia en pacientes con enfermedades crónicas.

El **Oxoglutarato**, **succinato**, y **acetato**: Son metabolitos involucrados en el ciclo de Krebs, importantes en la producción de energía a nivel celular. Sabemos que en la caquexia, se observa una disfunción del metabolismo energético, alterando la utilización de energía y la producción de ATP. Por tanto si vemos niveles elevados o alterados de estos metabolitos nos puede indicar que el cuerpo está intentando adaptarse a un estado de energía reducido. Esto ocurre en la caquexia, debido a la desregulación en el metabolismo de los carbohidratos, las grasas y las proteínas.

la **acetona**: En situaciones de caquexia, puede haber una mayor utilización de los cuerpos cetónicos para la producción de energía debido a la disminución de los carbohidratos disponibles, y la acetona es uno de esos productos. La acumulación de cetonas podría reflejar un cambio hacia la utilización de las grasas para obtener energía y esto es lo que ocurre en la caquexia.

Aminoácidos como la alanina, glutamina, leucina y valina: En la caquexia, la pérdida de masa muscular se asocia con un catabolismo aumentado de las proteínas, lo que libera aminoácidos. La glutamina juega un papel fundamental en el metabolismo celular y en el mantenimiento de la función inmune, pero también es un indicador de la degradación muscular. La correlación de la glutamina con otros metabolitos podría reflejar un intento del cuerpo de compensar la pérdida muscular y la alteración del metabolismo energético. La alanina es un aminoácido que se produce durante la glucólisis y tiene un papel crucial en el transporte de energía entre los músculos y el hígado, y sus niveles elevados en condiciones de caquexia podrían reflejar un metabolismo alterado de proteínas y glucosa. La leucina es un aminoácido esencial que está involucrado en la síntesis de proteínas musculares, y su correlación con otros metabolitos podría estar indicando intentos del cuerpo por estimular la síntesis proteica para contrarrestar la pérdida de masa muscular.

# Reflexiones sobre las limitaciones del análisis y posibles estudios futuros.



