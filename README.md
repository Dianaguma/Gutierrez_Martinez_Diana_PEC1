# Gutierrez-Martinez-Diana-PEC1

# Análisis Exploratorio de Datos y Construcción del SummarizedExperiment
Diana Gutierrez Martínez
- Archivo: human_cachexia : (https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/human_cachexia.csv)
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

El dataset proviene del repositorio nutrimetabolomics/metaboData en GitHub y contiene datos sobre concentraciones de metabolitos en 77 pacientes, 47 con cachexia y 30 controles , incluyendo información sobre la pérdida muscular (Muscle loss) y diversos metabolitos relacionados con el metabolismo energético y la función muscular. Las principales variables del dataset incluyen identificadores de pacientes (Patient ID), pérdida muscular y una serie de metabolitos que pueden proporcionar información sobre el estado metabólico de los individuos. 

Los metabolitos incluidos, como Anhydro-β-D-glucose, Methylnicotinamide, Aminobutyrate, entre otros, son relevantes porque están involucrados en vías metabólicas que afectan la síntesis de proteínas, el balance energético y el funcionamiento muscular. La medición de estos metabolitos puede ayudar a entender mejor los cambios metabólicos en la caquexia, una condición caracterizada por la pérdida de masa muscular y debilidad, a menudo observada en enfermedades crónicas como el cáncer y la insuficiencia cardíaca, proporcionando posibles biomarcadores de diagnóstico y objetivos terapéuticos.

# Incorporación de los Datos a SummarizedExperiment 

Primero, se instalan y cargan librerías necesarias, como usethis, BiocManager, SummarizedExperiment, y readr, así manejo el archivos CSV  llamado human_cachexia y creo un objeto de tipo SummarizedExperiment (adjunto en el proyecto llamado: SummarizedExperiment_Diana_Gutiérrez.rda.)

Leo el archivo CSV que contiene datos de pacientes, la pérdida muscular y las concentraciones de metabolitos. Los datos se separan en dos partes: Metadatos (como el ID del paciente y la pérdida muscular). Datos experimentales (mediciones de los metabolitos).

Elimino filas con valores faltantes (NA) en los metadatos y aseguro que las filas en los datos experimentales coincidan con los metadatos del paciente.  Además, elimino duplicados si los hay. Miro que los datos de las filas de metadatos y las mediciones de metabolitos estén alineados correctamente, para ello uso las identificaciones de los pacientes.

# Creación del objeto SummarizedExperiment:
  
Utilizo la función **SummarizedExperiment()**. El conjunto de datos de metabolitos se almacena en el slot assays, bajo el nombre counts, y los metadatos del paciente en el slot colData. El objeto SummarizedExperiment se guarda en un archivo .rda para su posterior análisis (adjunto en Github): Gutierrez_Martinez_Diana_PEC1 

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
colData(se) # Vemos que efectivamente estan las dos variables Patient ID y Muscle loss y nos sale los metabolitos relacionados a la cachexia y a este proyecto. Han separado 2 grupos: los controles y pacientes con cachexia. 

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

# Ver la distribución de las categorías de "Muscle.loss"G

Genero una tabla de frecuencias de la variable Muscle.loss y luego creo un gráfico de barras para visualizar cómo se distribuyen los valores de esa variable. Efectivamente **no hay distribución homogenea**. 

          table(sample_data$Muscle.loss)
          
          library(ggplot2)
          
          ggplot(sample_data, aes(x = Muscle.loss)) +
            geom_bar(fill = "skyblue", color = "black") +
            labs(title = "Distribución de muestras por grupo", x = "Grupo", y = "Frecuencia") +
            theme_minimal()



# Me enfoco en mirar las estadisticas descriptivas: 

Al hacer un  **summary(assays(se)$counts)** Si nos enfocamos en los resultados de los metabolitos obtengo en general una gran variabilidad en sus concentraciones. Si nos enfocamos en el citrato y la creatinina, vemos que estan mucho más elevados en comparación con otros. Estos valores son importantes en el análisis de condiciones fisiológicas y pueden ser claves en estudios relacionados con el metabolismo y patologías como la cachexia. En la tabla de los resúmenes estadísticos, las estadísticas clave incluyen el valor mínimo, primer cuartil (Q1), mediana (Q2), media, tercer cuartil (Q3) y valor máximo para cada metabolito. En el caso de **1,6-Anhydro-beta-D-glucose** , los valores muestran una gran variabilidad, con un rango muy amplio entre el mínimo y el máximo, el minimo es 4.71 y el máximo es 685.40. Esto ocurre tambien con **1-Methylnicotinamide** con un mínimo de 6.42 y un maximo de 1032.77, mostrando una variablidad con un máximo mucho más alta. 
Si nos fijamos en algunos metabolitos tienen valores máximos extremadamente altos en comparación con la media, esto puede indicar la aparicion de **outliers** o un pequeño número de muestras con concentraciones mucho más altas de esos metabolitos. Se puede utilizar para identificar patrones anómalos en los datos. 

# Calculo la corrección entre los metabolitos 

El analisis de correlación podría proporcionar más información sobre las relaciones entre ellos. Y ayudar a identificar metabolitos que coexisten en concentraciones más altas o más bajas, para intentar entender más el contexto de la cachexia. 

Observo que los ácidos como el **succinato** y el **oxoglutarato** tienen fuertes correlaciones entre ellos. Se que están involucrados en las rutas metabólicas relacionadas con el ciclo de Krebs, lo que indica una estrecha relación en la producción de energía.  La correlación con **X2.Oxoglutarate** es **0.5909**, siendo una correlación positiva moderada. Por tanto, cuando el oxoglutarato aumenta, el succinato también tiende a aumentar en cierta medida, lo que tiene sentido, ya que ambos forman parte del ciclo de Krebs. **2-oxoglutarato deshidrogenasa** se trata de un complejo multienzimático que forma parte del ciclo de Krebs. Se encarga de transformar el 2-oxoglutarato en succinil-coenzima A (1). Este succinil-coA sale del succinato y la coenzima A. Por eso vemos fuertes correlaciones entre los dos compuestos. 

En cambio la **acetona**, también está correlacionada con **X2.Oxoglutarate** con 0.0375, lo que indica una correlación muy débil, casi nula. El  **Acetate** y **Acetone** también están bien correlacionados entre sí (0.4516), lo que podría indicar una relación entre estos compuestos en términos de ciclos de reducción-oxidación.  

La **alanina** tiene una fuerte correlación con el **Acetate** (0.7415) y también se correlaciona moderadamente con **Acetone** (0.6707). El aumento de alanina en la caquexia podría reflejar una respuesta a la degradación muscular y el uso de aminoácidos para la producción de energía. Relacionado con el uso de aminoacidos para producir energia estan la **leucina**, la **serina** y la **valina** que fijandonos en la correlacion entre ellas tienen relaciones moderadas entre sí, son importantes para el metabolismo celular y en la síntesis de proteínas. La **serina y valina**: La correlación es 0.6072, que es bastante fuerte, lo que sugiere que estos dos aminoácidos podrían estar más estrechamente relacionados en sus procesos metabólicos. En cambio la **Leucina y Serina**: La correlación es 0.2907, tienen relación moderada entre estos dos aminoácidos. Esto puede reflejar que, aunque ambos están involucrados en el metabolismo de proteínas, no tienen una relación directa muy fuerte.

el **ácido acético**, y el **ácido adipato** tienen correlaciones positivas moderadas **0.3169**, sabemos que se relacionan entre si porque son metabolitos conectados con la utilización de grasas o la producción de cuerpos cetónicos, cuando estamos en ayuno o metabolismo alterado. 


El **ácido pantoténico**, el **acetato** y el **nicotinamida** son coenzimas esenciales en las vías metabólicas, sobretodo en la producción de energía. **Ácido Pantoténico** tiene una correlación baja a moderada con el acetato (0.2597) y con la nicotinamida (0.2613), lo que sugiere que alteraciones en estas rutas metabólicas (como la producción de CoA y NAD+) podrían influir en el desarrollo o progresión de la cachexia. **Acetato** tiene una correlación moderada con **nicotinamida** **0.4041**, indicando que las rutas metabólicas de acetato y NAD+ podrían estar conectadas, y las alteraciones en ambas pueden estar relacionadas con el metabolismo alterado que se observa en la cachexia.

Finalmente, el **ácido fenilacético** y el **indoxilsulfato** muestran correlaciones entre sí moderadas **0.5959**, creo que están involucrados en procesos antioxidantes y de detoxificación. Y son importantes en el metabolismo de los fenoles.

**Glucose** es un indicador importante del metabolismo energético. Su concentración más baja podría reflejar cambios en el uso de energía o el metabolismo de carbohidratos en pacientes con cachexia.

¡[Matriz correlacion](https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/correlation_matrix.csv)

# Calculo la media de los metabolitos. 

Los metabolitos relacionados con la cachexia suelen estar involucrados en alteraciones del **metabolismo energético**, la **inflamación** y el **catabolismo de proteínas**. Encontramos casos como glutamina, alanina, acetato, citrato, y creatinina, metabolitos estrechamente relacionados con procesos catabólicos y metabólicos que ocurren en la cachexia. 

La **Glutamina** tiene una media de **337.10** y una mediana de **284.29**, podría estar relacionada con un estado de catabolismo muscular, común en la cachexia. Este aminoácido juega un papel importante para la síntesis de proteínas y el metabolismo muscular. En el caso de la cachexia, se a visto en pacientes una alteración en el metabolismo de la glutamina, porque el cuerpo comienza a descomponer las proteínas musculares para liberar aminoácidos como la glutamina. En el caso de la **alanina** la media es **303.18** con una mediana de **237.46**, y se a visto que los valores de alanina en cachexia suelen estar elevados debido al proceso catabólico muscular. 


Miro tambien la media de cada metabolito y observo que la **Creatinine** tiene el valor más alto de concentración entre los metabolitos estudiados, con **9521.7754**, seguido por Hippurate **2614.1479** y Citrate tiene una media de **2423.47** y una mediana de **2079.74**. La creatinina podría ser uno de los metabolitos más presentes en las muestras que estás analizando. Este es un subproducto del metabolismo muscular, y ver valores elevados se han visto relacionados con la función renal y el estado muscular. Como el análisis parece estar centrado en la cachexia, la creatinina podría ser relevante para evaluar el daño muscular y la degradación proteica. El  **pi-Methylhistidine** es un marcador de degradación muscular y está presente en niveles moderados **391.5184**, es importante analizar este marcador porque es relevante en pacientes cachexicos, ya que la degradación muscular es un proceso clave en esta condición. 


# Hago mapa de calor de la correlación entre metabolitos

Instalo el paquete igraph y cargo el paquete. Estableces un umbral (threshold) de 0.7. Este valor se usará para filtrar las correlaciones. Hago una copia de la matriz de correlación original (cor_matrix) y la asigno a una nueva variable llamada cor_matrix_filtered. Modifico **cor_matrix_filtered** estableciendo a cero todas las correlaciones cuya magnitud sea menor que 0.7. Por tanto las correlaciones débiles se eliminan, dejando solo aquellas con correlaciones fuertes (mayores o iguales a 0.7 o menores o iguales a -0.7). Creo un mapa de correlación y guardo ese gráfico en un archivo PNG en mi escritorio. 

                    ggplot(cor_data, aes(Var1, Var2, fill = value)) +
                      geom_tile() +
                      scale_fill_gradient2(low = "blue", high = "red", mid = "white", 
                                           midpoint = 0, limit = c(-1, 1), space = "Lab", 
                                           name = "Correlación") +
                      theme_minimal() +
                      theme(axis.text.x = element_text(angle = 45, vjust = 1, 
                                                       hjust = 1)) +
                      labs(title = "Mapa de calor de la correlación entre metabolitos",
                           x = "Metabolito", 
                           y = "Metabolito")


![Mapa de calor](https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/heatmap.png)

En este mapa de calor los colores reflejan la fuerza de las correlaciones, donde los valores cercanos a 1 (tonalidades rojas) indican una fuerte correlación positiva, y los valores cercanos a -1 indican una correlación negativa (tonalidad azul). Ver archivo png en Github.  Este tipo de visualización es útil para identificar las relaciones más fuertes entre los metabolitos, lo cual es crucial al estudiar la cachexia y su impacto en el metabolismo energético y muscular. 


![Gráfico de correlación](https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/grafico_correlacion.png)

En el gráfico de correlación, el citrato y la glutamina están cerca el uno del otro, conectados, lo que indica que están relacionados. El citrato es un compuesto clave en el ciclo de Krebs, que es el proceso que las células usan para obtener energía; en situaciones como la caquexia, que es una pérdida de peso extrema y debilidad muscular, el metabolismo energético del cuerpo se ve alterado. Esto puede hacer que los niveles de citrato cambien, ya que el cuerpo intenta producir más energía de lo normal para compensar el desequilibrio. La glutamina es un aminoácido muy importante para mantener el funcionamiento energético de las células y para la síntesis de proteínas, como las que forman los músculos. En la caquexia, el cuerpo descompone rápidamente las proteínas, lo que provoca una disminución de la glutamina; además, la glutamina ayuda al sistema inmunológico, que también puede verse afectado durante la enfermedad. Cuando en tu gráfico el citrato y la glutamina están muy cerca y correlacionados positivamente, es decir, tienden a aumentar o disminuir juntos, esto podría sugerir que ambos están siendo influenciados por el mismo proceso metabólico en la caquexia. En otras palabras, cuando el cuerpo necesita más energía, lo que puede suceder cuando hay un estado catabólico o de descomposición de tejidos, el citrato y la glutamina están trabajando juntos para tratar de mantener el equilibrio energético y protegen el cuerpo de los efectos del catabolismo acelerado. Por lo tanto, la correlación positiva entre citrato y glutamina en este contexto indica que ambos están involucrados en una respuesta metabólica similar cuando el cuerpo enfrenta un déficit de energía o una pérdida de masa muscular.

# Analisis de PCA

El procedimiento es el siguiente: 

El primer paso que hago es estandarizar los datos, así cada variable tiene media 0 y desviación estándar 1. Cálculo de la matriz de covarianza o correlación y calculo los vectores propios y los valores propios de la matriz de covarianza. Proyecto datos sobre los componentes principales. Y tengo en cuenta los primeros dos componentes (PC1 y PC2) porque son los más relevantes para la visualización, ya que explican la mayor parte de la variabilidad en los datos.
        pca_result <- prcomp(t(assays(se)$counts), scale = TRUE)
        
        # t(assays(se)$counts): Se realiza una transposición de la matriz de conteos. Porque en el análisis de componentes principales (PCA), cada fila es en este caso, un gen, y cada columna una muestra.
        #prcomp: función de R que realiza el análisis de componentes principales (PCA), descompone la matriz de datos utilizando el método de descomposición en valores singulares. 
        
        pca_scores <- pca_result$x 

      # https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/pca_scores.csv Aquí estan los scores de pca. 

Puedo concluir que PC1 tiene una desviación estándar significativamente mayor (7.488), por tanto esto indica que representa una gran parte de la variabilidad en los datos. Esto es consistente con la proporción de varianza de 0.890, lo que significa que el PC1 explica el 89% de la variabilidad en los datos.  PC2 tiene una desviación estándar mucho menor (1.6894) y una proporción de varianza de 0.0453, explicando solo el 4.53% de la variabilidad en los datos. La **proporción acumulada** muestra que después de las primeras 10 componentes principales (PC), ya se ha explicado más del 99% de la variabilidad. Por tanto, esto indica que para la mayoría de los análisis, podrías trabajar con solo las primeras 2-3 componentes y aún así capturar casi toda la variabilidad en los datos.


![Scores PCA](https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/pca_scores.csv)

Finalmente genero un gráfico de dispersión de los primeros dos componentes principales (PC1 vs. PC2), lo que permite identificar patrones, agrupaciones o posibles anomalías en los datos. Los puntos en el gráfico representan las muestras y su distribución puede revelar patrones biológicos interesantes, como agrupaciones de muestras similares.

![PCA plot](https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/pca_plot.png)

# Conclusiones 

En conclusión, los metabolitos analizados, como la **creatinina**, **pi-Methylhistidine**, **oxoglutarato**, **succinato**, **acetato**, y los **aminoácidos** (alanina, glutamina, leucina, y valina) ofrecen una visión integral del complejo estado metabólico presente en la caquexia. Creatinina y pi-Methylhistidine reflejan la descomposición muscular, un proceso central en la caquexia, que se caracteriza por la pérdida acelerada de masa muscular. Niveles elevados de estos metabolitos indican un catabolismo de proteínas aumentado, lo cual es un claro indicador de daño y pérdida de tejido muscular, como hemos visto en los resultados del calculo la media de los metabolitos la  **Creatinina** y **pi-Methylhistidine** hemos vistoo valores de **9521.7754** y **391.5184** de media.  **Oxoglutarato**, **succinato** y **acetato** están involucrados en la producción de energía, especialmente a través del ciclo de Krebs. Por esta razon hemos visto fuertes correlaciones entre ellos. Ya que alteraciones en estos metabolitos sugieren una disfunción metabólica, donde el cuerpo intenta compensar la falta de energía utilizando vías alternativas, como la oxidación de ácidos grasos, lo que refleja un cambio en el metabolismo energético típico de la caquexia. Finalmente, los aminoácidos como **alanina, glutamina, leucina**, y **valina** están estrechamente relacionados con la degradación y síntesis de proteínas musculares. La presencia elevada de estos aminoácidos es indicativa de un estado catabólico donde el cuerpo busca compensar la pérdida muscular mediante la movilización de reservas de aminoácidos. Además, estos metabolitos ayudan a mantener funciones críticas como la respuesta inmune y la regulación de la síntesis proteica, aunque su efectividad es limitada debido a las condiciones catabólicas.

# Bibliografia 
- (1)(https://chemevol.web.uah.es/wp/la-enzima-de-las-mil-caras-el-complejo-2-oxoglutarato-deshidrogenasa/?print=print)
- (2)Ciclo de Krebs (https://www.studocu.com/latam/document/universidad-tecnologica-de-santiago/bioquimica-i/cap-16-ciclo-de-krebs-harpers-bioquimica-ilustrada-30a-edicion/8335805)

  # Anexos
  
- Resumen de ruta metabolica (https://github.com/Dianaguma/Gutierrez_Martinez_Diana_PEC1/blob/main/Captura%20de%20pantalla.png)


