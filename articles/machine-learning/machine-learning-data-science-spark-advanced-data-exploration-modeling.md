---
title: "aaaAdvanced una exploración de datos y modelado con Spark | Documentos de Microsoft"
description: "Utilice la exploración de datos de HDInsight Spark toodo y entrenar modelos de clasificación y regresión binarios con optimización para la validación cruzada y hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Exploración y modelado avanzados de datos con Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este tutorial usa HDInsight Spark toodo exploración y entrenar binaria clasificación de datos y modelos de regresión mediante la validación cruzada y optimización de hyperparameter en una muestra de Hola NYC taxi de ida y vuelta y resultados son el conjunto de datos de 2013. Le guiará por los pasos de Hola de hello [proceso de ciencia de datos](http://aka.ms/datascienceprocess), -to-end, con un HDInsight Spark de clúster para el procesamiento y modelos de datos y Hola Hola toostore de blobs de Azure. proceso de Hello explora y visualiza los datos agregados de un Blob de almacenamiento de Azure y, a continuación, prepara Hola datos toobuild modelos predictivos. Python ha sido toocode usado Hola solución y tooshow Hola relevantes trazados. Estos modelos son compilación con clasificación binaria del toodo Hola Spark MLlib Kit de herramientas y tareas de modelado de regresión. 

* Hola **clasificación binaria** tarea es toopredict haya o no una sugerencia se paga por los recorridos de Hola. 
* Hola **regresión** tarea es la cantidad de Hola de toopredict de sugerencia de hello en función de otras características de sugerencia. 

pasos de modelado de Hello también contienen código que muestra cómo tootrain, evaluar y guardar cada tipo de modelo. Hello tema trata algunos de hello mismo masa como hello [exploración de datos y el modelado con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tema. Pero es más "avanzado" ya que también utiliza la validación cruzada con hyperparameter barrido tootrain modelos de clasificación y regresión de forma óptima precisos. 

**Validación cruzada (CV)** es una técnica que evalúa la medida un modelo entrenado en un conjunto conocido de datos generaliza toopredicting Hola características de conjuntos de datos en el que no se está entrenada.  Una implementación común que se usa aquí es toodivide un conjunto de datos en subconjuntos de K y, a continuación, entrenar modelo de hello en un modo round-robin en todos excepto uno de los subconjuntos de Hola. se evalúa la capacidad de Hola de hello modelo tooprediction con precisión cuando prueba contra Hola conjunto de datos independientes en este modelo de subconjunto no utiliza tootrain Hola.

**Optimización de Hyperparameter** Hola problema de elegir un conjunto de hiperparámetros para un algoritmo de aprendizaje, normalmente con el objetivo de Hola de optimizar una medida de rendimiento del algoritmo de hello en un conjunto de datos independiente. **Hiperparámetros** son valores que deben especificarse fuera de procedimiento de entrenamiento del modelo de Hola. Suposiciones acerca de estos valores pueden afectar flexibilidad de Hola y precisión de los modelos de Hola. Árboles de decisión tienen hiperparámetros, por ejemplo, como Hola había deseado profundidad y el número de hojas de árbol de Hola. Las máquinas de vectores de soporte (SVM) requieren que se establezca un término de penalización para las clasificaciones incorrectas. 

Una optimización de hyperparameter de tooperform de forma común usada aquí es una búsqueda de la cuadrícula, o un **barrido de parámetros**. Esto se compone de realizar una búsqueda exhaustiva a través de los valores de hello un subconjunto específico de espacio de hello hyperparameter para un algoritmo de aprendizaje. La validación cruzada puede proporcionar un toosort de métrica de rendimiento out resultados óptimos Hola generado por el algoritmo de búsqueda de cuadrícula de Hola. CV utilizado con hyperparameter barrido ayuda a problemas de límite como sobreajuste una tootraining de datos de modelo para que el modelo hello conserva Hola capacidad tooapply toohello general conjunto de datos del que Hola se extrajeron los datos de entrenamiento.

los modelos de Hello que usamos incluyen regresión logística y lineal, los bosques aleatorios y los árboles impulsados degradados:

* [Regresión lineal con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) es un modelo de regresión lineal que usa un método de descenso de gradiente estocástico (SGD) y para la optimización y la característica de ajuste de escala en cantidades de sugerencia de hello toopredict pago. 
* [Regresión logística con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regresión "logit", es un modelo de regresión que puede usarse en la variable dependiente de hello es la clasificación de datos de categorías toodo. LBFGS es un algoritmo de optimización de Newton tipo que se aproxima al algoritmo de hello Broyden – Fletcher – Goldfarb – Shanno (BFGS) con una cantidad limitada de memoria del equipo y que se usa ampliamente en el aprendizaje automático.
* [bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.  Combina riesgo del Hola de tooreduce de árboles de muchos decisión de desbordamiento. Bosques aleatorios se utilizan para la clasificación y regresión, pueden controlar las características de categorías y se pueden ampliar Configuración de clasificación multiclase toohello. No se requieren característica ajuste de escala y se pueda toocapture no linealidades e interacciones de característica. Bosques aleatorios son uno de los modelos para la clasificación y regresión de aprendizaje de máquina más éxito Hola.
* [árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión. Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida. GBTs se usan para la clasificación y regresión y puede controlar las características de categorías, no requieren la característica escalado y no es capaz de toocapture linealidades y las interacciones de características. También se pueden usar en una configuración de clasificación multiclase.

Ver ejemplos de uso CV y Hyperparameter de modelado barrido se muestran para el problema de clasificación binaria de Hola. Ejemplos más simples (sin el parámetro sucias) se presentan en el tema principal de Hola para tareas de regresión. Pero, en el apéndice de hello, también se presenta con net elástico para la regresión lineal y CV con el uso de barrido de parámetros para la regresión de bosque aleatorio de validación. Hola **elásticas net** es un método de regresión regularizada para ajustar la regresión lineal de los modelos que linealmente combina las métricas de L1 y L2 hello como sanciones de hello [lazo](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) y [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) métodos.   

> [!NOTE]
> Aunque el Kit de herramientas de hello Spark MLlib es toowork diseñado en grandes conjuntos de datos, un ejemplo relativamente pequeño (con filas de 170K, aproximadamente 0,1% del conjunto de datos de Nueva York original Hola de ~ 30 Mb) se utiliza aquí por comodidad. ejercicio Hola aquí especificado se ejecuta eficazmente (en unos 10 minutos) en un clúster de HDInsight con 2 nodos de trabajador. Hello mismo código, con modificaciones menores, puede ser tooprocess usado más grandes conjuntos de datos, con las modificaciones apropiadas para almacenar en caché datos en la memoria y cambiar el tamaño de clúster de Hola.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Configuración: clústeres y cuadernos de Spark
Los pasos de instalación y el código proporcionado en este tutorial son para HDInsight Spark 1.6. Sin embargo, Jupyter Notebooks se proporciona para clústeres de HDInsight Spark 1.6 y Spark 2.0. Se proporciona una descripción de hello blocs de notas y vínculos toothem Hola [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para el repositorio de GitHub de Hola que los contienen. Además, código de hello aquí y en blocs de notas de hello vinculada genérica y debe funcionar en cualquier clúster de Spark. Si no utilizas HDInsight Spark, pasos de configuración y administración de clúster de hello pueden ser ligeramente diferentes de lo que se muestra aquí. Para mayor comodidad, estos son Hola vínculos toohello Jupyter blocs de notas para Spark 1.6 y toobe 2.0 ejecutar en el núcleo de pyspark Hola de servidor de Jupyter Notebook hello:

### <a name="spark-16-notebooks"></a>Cuadernos de Spark 1.6

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): incluye temas sobre el cuaderno 1 y sobre el desarrollo de modelos mediante el ajuste de hiperparámetros y la validación cruzada.

### <a name="spark-20-notebooks"></a>Cuadernos de Spark 2.0

[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este archivo proporciona información sobre cómo tooperform la exploración de datos, modelado y puntuación en Spark 2.0 clústeres.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>El programa de instalación: Hola, bibliotecas y ubicaciones de almacenamiento preestablecido contexto Spark
Spark es capaz de tooAzure tooread y escritura Blob de almacenamiento (también conocido como WASB). Por lo tanto, cualquiera de los datos existentes almacenados en ella se pueden procesar mediante Spark y Hola resultados almacenados en WASB.

modelos de toosave o archivos en WASB, ruta de acceso de hello debe toobe especificado correctamente. Hola de clúster predeterminado contenedor adjuntada toohello Spark puede hacer referencia mediante un ruta que comienza con: "wasb: / / /". Para hacer referencia a otras ubicaciones, se usa "wasb://".

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Establecimiento de rutas de directorio para las ubicaciones de almacenamiento de WASB
ejemplo de código siguiente Hello Especifica ubicación Hola de hello toobe de datos de lectura y se guarda la ruta de acceso de hello para la salida de hello modelo almacenamiento directory toowhich Hola modelo:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**SALIDA**

datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Importación de bibliotecas
Es necesario las bibliotecas de importación con hello siguiente código:

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a>Contexto de Spark preestablecido e instrucciones mágicas de PySpark
los kernels de Hello PySpark que se proporcionan con blocs de notas Jupyter tienen un contexto de valores preestablecido. Por lo que no es necesario tooset Hola Spark o subárbol contextos explícitamente antes de empezar a trabajar con la aplicación hello que está desarrollando. Estos contextos están disponibles de forma predeterminada. Estos contextos son:

* sc: Para Spark 
* sqlContext: Para Hive

Hello PySpark kernel proporciona algunos predefinidas "magics", que son comandos especiales que se pueden llamar con %%. Hay dos comandos de este tipo que se utilizan en estos ejemplos de código.

* **%% local** especifica que el código de hello en las líneas siguientes es toobe ejecutado de forma local. El código debe ser un código de Python válido.
* **%% sql -o <variable name>**  ejecuta una consulta de Hive en hello sqlContext. Si se pasa el parámetro -o de hello, resultado de hello de consulta de Hola se conserva en hello %% contexto Python local como una trama de datos de Pandas.

Para obtener más información sobre los kernels de Hola para hello predefinidos y blocs de notas de Jupyter "magics" que proporcionan, consulte [clústeres de núcleos disponibles para equipos portátiles Jupyter con Linux de HDInsight Spark en HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Ingesta de datos de blob público:
Hello primer paso en el proceso de ciencia de datos de hello es tooingest Hola datos toobe analizado desde orígenes que se encuentra en el entorno de exploración y el modelado de datos. Este entorno es Spark en este tutorial. Esta sección contiene código de hello toocomplete una serie de tareas:

* Introducción toobe de ejemplo de Hola datos modelada
* leer en el conjunto de datos de entrada hello (almacenado como un archivo .tsv)
* formato y Hola limpiar datos
* crear objetos en la memoria (RDD o tramas de datos) y almacenarlos en caché
* registrarlos como una tabla temporal en el contexto de SQL

Este es el código de hello para la recopilación de datos.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 276.62 segundos

## <a name="data-exploration--visualization"></a>Visualización y exploración de datos
Una vez introducidos los datos de hello en Spark, hello siguiente paso en el proceso de ciencia de datos de hello es toogain descripción más profunda de los datos de hello mediante exploración y visualización. En esta sección, se examinan datos de taxi hello mediante consultas SQL y las variables de destino de trazado hello y características posibles para la inspección visual. En concreto, se traza frecuencia Hola de recuentos de pasajeros en viajes taxi, la frecuencia de Hola de cantidades de sugerencia y cómo sugerencias varían según el tipo y la cantidad de pago.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Trazar un histograma de frecuencias de recuento de pasajeros en el ejemplo hello de viajes de taxi
Este código y fragmentos de código siguientes usan SQL tooquery mágico Hola datos de ejemplo y local tooplot mágico Hola.

* **Magia SQL (`%%sql`)** HDInsight PySpark kernel hello admite consultas de HiveQL en línea fácil contra Hola sqlContext. Hola (-o VARIABLE_NAME) argumento conserva la salida de hello de consulta SQL de hello como una trama de datos de Pandas en el servidor de Jupyter Hola. Esto significa que está disponible en modo local Hola.
* Hola  **`%%local` mágico** es código toorun los utiliza localmente en el servidor de Jupyter hello, que es el nodo principal de Hola Hola del clúster de HDInsight. Normalmente, se utiliza `%%local` mágico después hello `%%sql -o` mágico es toorun usa una consulta. parámetro de Hello -o podría conservar la salida de hello de consulta SQL Hola localmente. A continuación, Hola `%%local` desencadenadores mágicos Hola siguiente conjunto de toorun de fragmentos de código localmente en la salida de hello de consultas SQL de Hola que se ha guardado localmente. salida de Hello se visualiza automáticamente después de ejecutar código de hello.

Esta consulta recupera el recuento de pasajeros ciclos de ida y Hola. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Este código crea una trama de datos local de resultado de la consulta de Hola y representa los datos de Hola. Hola `%%local` mágico crea una trama de datos local, `sqlResults`, que se puede utilizar para trazar con matplotlib. 

> [!NOTE]
> Esta instrucción mágica de PySpark se utiliza varias veces en este tutorial. Si la cantidad de Hola de datos es grande, debe muestrear toocreate una trama de datos que cabe en la memoria local.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Aquí es viajes de hello código tooplot Hola pasajeros recuentos

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**SALIDA**

![Frecuencia de carreras por número de pasajeros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

Puede seleccionar entre los distintos tipos de visualizaciones (tabla, circular, línea, el área o barra) mediante el uso de hello **tipo** botones de menú en el Bloc de notas de Hola. aquí se muestra un gráfico de barras de Hola.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Trazado de un histograma de importes de propinas y de las variaciones en las propinas según número de pasajeros y tarifas.
Usar una consulta toosample datos de SQL...

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


Esta celda de código usa Hola SQL consulta toocreate tres traza Hola datos.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**SALIDA:** 

![Distribución del importe de las propinas](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Diseño, transformación y preparación de los datos para el modelado de características
En esta sección se describe y proporciona código de hello para conocer los procedimientos que utiliza datos tooprepare para su uso en el modelado de aprendizaje automático. Muestra cómo hello toodo siguientes tareas:

* Creación de una nueva característica mediante la partición de horas en intervalos de tiempo de tráfico
* Indexación y codificación "uno de n" de características categóricas
* Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático
* Crear un muestreo aleatorio dentro de los datos de Hola y dividir en entrenamiento y conjuntos de pruebas
* Ajuste de la escala de las características
* Almacenamiento de objetos en caché

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Creación de una nueva característica mediante la partición de tiempos de tráfico en intervalos
Este código muestra cómo toocreate una nueva característica dividiendo el tráfico de tiempo de espera en cubos y, a continuación, cómo toocache Hola resultante trama de datos en memoria. Almacenamiento en caché conduce tooimproved el tiempo de ejecución cuando se usan varias veces resistente distribuidas los conjuntos de datos (RDDs) y tramas de datos. Por lo tanto, almacenaremos en caché los RDD y las tramas de datos en varias fases del tutorial.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**SALIDA**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Indexación y codificación "uno de n" de características categóricas
Esta sección se muestra cómo tooindex o codificar las características de categorías para la entrada en hello las funciones de modelado. Hola de modelado y predecir las funciones de MLlib requieren que las características con los datos de entrada categorías estar codificadas o indizadas toouse anterior. 

Según el modelo de hello, necesita tooindex o codificarlos de maneras diferentes. Por ejemplo, los modelos de regresión lineal y logística requieren estrechamente con una codificación, donde, por ejemplo, se puede expandir una característica con tres categorías en tres columnas de característica, cada contenedor 0 o 1 según la categoría de Hola de una observación. Proporciona MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) función toodo estrechamente con una codificación. Este codificador asigna una columna de la columna de etiqueta índices tooa de vectores binarios, con al menos un solo uno valor. Esta codificación permite algoritmos que esperan las características con valores numéricas, como la regresión logística, toobe aplica toocategorical características.

Este es Hola código tooindex y codificar las características de categorías:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 3,14 segundos

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático
Esta sección contiene código que muestra cómo los tipos de datos de texto categorías tooindex como con la etiqueta de punto de datos y cómo tooencode lo. Esto prepara toobe utiliza tootrain y prueba MLlib la regresión logística y otros modelos de clasificación. Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada que necesita la mayoría de los algoritmos de aprendizaje automático de MLlib. Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.

Este es Hola código tooindex y codificar las características de texto para clasificación binaria.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Este es el código de hello tooencode e índice características de texto de categorías para el análisis de regresión lineal.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Crear un muestreo aleatorio dentro de los datos de Hola y dividir en entrenamiento y conjuntos de pruebas
Este código crea un muestreo aleatorio de datos de hello (25% se utiliza aquí). Aunque no es necesario para este ejemplo debido toohello tamaño del conjunto de datos de hello, mostramos cómo puede muestrear datos de hello aquí. Sabrá cómo toouse para su propio problema si es necesario. Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos. A continuación, dividiremos ejemplo hello en una parte de entrenamiento (aquí 75%) y una prueba toouse parte (aquí 25%) en la clasificación y el modelo de regresión.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 0,31 segundos

### <a name="feature-scaling"></a>Ajuste de la escala de las características
Ampliación de característica, también conocida como la normalización de datos, se garantiza que funciones con valores muy dispersos no se le otorgó excesivo sopesar en función del objetivo de hello. código para el escalado de la característica Hello usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza de tooscale Hola características toounit. MLlib lo proporciona para su uso en la regresión lineal con descenso de gradiente estocástico (SGD). SGD es un conocido algoritmo para entrenar una amplia variedad de otros modelos de aprendizaje automático tales como regresiones regularizadas o máquinas de vectores de soporte (SVM).   

> [!TIP]
> Hemos encontrado hello LinearRegressionWithSGD algoritmo toobe toofeature confidencial ajuste de escala.   
> 
> 

Aquí es tooscale variables de código de hello para su uso con un algoritmo SGD lineal Hola regularizado.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 11.67 segundos

### <a name="cache-objects-in-memory"></a>Almacenamiento de objetos en caché
tiempo Hola de entrenamiento y de prueba de algoritmos de aprendizaje automático puede reducirse mediante almacenamiento en caché de trama de datos de entrada de hello los objetos utilizados para la clasificación, la regresión y, características de escala.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA** 

Tiempo que tarda tooexecute encima de la celda: 0,13 segundos

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Predicción de si se dio propina o no con modelos de clasificación binaria
Esta sección muestra cómo usar tres modelos para la tarea de clasificación binaria de hello de predecir si no se le paga una sugerencia para un recorrido de taxi. modelos de Hello presentados son:

* Regresión logística 
* Bosque aleatorio
* Árboles impulsados por gradiente

Cada sección de código de generación del modelo se dividirá en pasos: 

1. **entrenamiento del modelo** con un conjunto de parámetros
2. **Evaluación del modelo** en un conjunto de datos de prueba con métricas
3. **Guardado del modelo** en un blob para utilizarse en el futuro

Le mostramos cómo toodo la validación cruzada (CV) con el parámetro barrido de dos maneras:

1. Usar **genérico** código personalizado que puede ser tooany aplicado el algoritmo de MLlib y tooany del parámetro se establece en un algoritmo. 
2. Con hello **pySpark función de la canalización de CrossValidator**. Tenga en cuenta que CrossValidator presenta algunas limitaciones para Spark 1.5.0: 
   
   * Los modelos de canalización no se pueden guardar ni conservar para usarlos en el futuro.
   * No se puede utilizar para todos los parámetros de un modelo.
   * No se puede usar para todos los algoritmos de MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Genérico cross barrido hyperparameter utilizado con el algoritmo de regresión logística de Hola para clasificación binaria y validación
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de regresión logística con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos dataset. modelo de Hola se entrena usando cross barrido hyperparameter implementado con código personalizado que puede ser tooany aplicada de hello algoritmos en MLlib de aprendizaje y validación (CV).   

> [!NOTE]
> ejecución de Hola de este código CV personalizado puede tardar varios minutos.
> 
> 

**Entrenar el modelo de regresión logística de hello mediante CV y barrido hyperparameter**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

Intercept: -0.0111216486893

Tiempo que tarda tooexecute encima de la celda: 14.43 segundos

**Evaluar el modelo de clasificación binaria de hello con métricas estándares**

código de Hello en esta sección muestra cómo tooevaluate una regresión logística modelo en una prueba de conjuntos de datos, incluyendo un gráfico de hello curva ROC.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

Area under PR = 0.985336538462

Area under ROC = 0.983383274312

Summary Stats

Precision = 0.984174341679

Recall = 0.984174341679

F1 Score = 0.984174341679

Tiempo que tarda tooexecute encima de la celda: 2,67 segundos

**Trazar la curva ROC Hola.**

Hola *predictionAndLabelsDF* está registrado como una tabla, *tmp_results*, en la celda anterior de Hola. *tmp_results* pueden toodo usado consultas y generar resultados en hello sqlResults-trama de datos para trazar. Este es el código de hello.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Aquí es predicciones de toomake de código de Hola y Hola trazado ROC curva.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**SALIDA**

![Curva ROC de regresión logística para el enfoque genérico](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Persistencia del modelo en un blob para su futuro consumo**

código de Hello en esta sección muestra cómo modelo de regresión logística de hello toosave para su uso.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 34.57 segundos

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Uso de la función de canalización CrossValidator de MLlib con el modelo de regresión logística (regresión elástica)
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de regresión logística con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos dataset. modelo de Hola se entrena usando la validación cruzada (CV) y barrido hyperparameter con hello MLlib CrossValidator canalización función implementada para CV con barrido de parámetros.   

> [!NOTE]
> ejecución de Hola de este código MLlib CV puede tardar varios minutos.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 107.98 segundos

**Trazar la curva ROC Hola.**

Hola *predictionAndLabelsDF* está registrado como una tabla, *tmp_results*, en la celda anterior de Hola. *tmp_results* pueden toodo usado consultas y generar resultados en hello sqlResults-trama de datos para trazar. Este es el código de hello.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Aquí es curva ROC de hello código tooplot Hola.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**SALIDA**

![Curva ROC de regresión logística con CrossValidator de MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Clasificación de bosque aleatorio
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar una regresión de bosque aleatorio que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos conjunto de datos.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

Area under ROC = 0.985336538462

Tiempo que tarda tooexecute encima de la celda: 26.72 segundos

### <a name="gradient-boosting-trees-classification"></a>Clasificación de árboles impulsados por gradiente
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de árboles de aumento de degradado que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos conjunto de datos.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA**

Area under ROC = 0.985336538462

Tiempo que tarda tooexecute encima de la celda: 28.13 segundos

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Predicción de propinas con modelos de regresión (sin VC)
Esta sección muestra cómo utilizar tres modelos para la tarea de regresión de hello: predecir Hola sugerencia tiempo pagado por una taxi de ida y vuelta en función de otras características de sugerencia. modelos de Hello presentados son:

* Regresión lineal regularizada
* Bosque aleatorio
* Árboles impulsados por gradiente

Estos modelos se describen en la introducción de Hola. Cada sección de código de generación del modelo se dividirá en pasos: 

1. **entrenamiento del modelo** con un conjunto de parámetros
2. **Evaluación del modelo** en un conjunto de datos de prueba con métricas
3. **Guardado del modelo** en un blob para utilizarse en el futuro   

> AZURE Nota: La validación cruzada no se utiliza con tres modelos de regresión hello en esta sección, ya que esto se muestra en detalle para los modelos de regresión logística de Hola. Un ejemplo que muestra cómo se proporciona toouse CV con Net elástico para la regresión lineal de hello apéndice de este tema.
> 
> AZURE Nota: En nuestra experiencia, puede haber problemas con la convergencia de los modelos de LinearRegressionWithSGD y parámetros necesitan toobe cambiado/optimizado cuidadosamente para obtener un modelo válido. El ajuste de la escala de las variables ayuda con la convergencia. Regresión de red elástica, que se muestra en el tema de toothis apéndice de hello, también puede usarse en lugar de LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>regresión lineal con SGD
Hello código en esta sección muestra cómo toouse escalarse características tootrain una regresión lineal que usa el descenso de gradiente estocástico (SGD) para la optimización, y cómo tooscore, evaluar y guardar el modelo de hello en el almacenamiento de blobs de Azure (WASB).

> [!TIP]
> En nuestra experiencia, puede haber problemas con la convergencia de Hola de modelos LinearRegressionWithSGD y parámetros necesitan toobe cambiado/optimizado cuidadosamente para obtener un modelo válido. El ajuste de la escala de las variables ayuda con la convergencia.
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA**

Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]

Intercept: 0.854507624459

RMSE = 1.23485131376

R-sqr = 0.597963951127

Tiempo que tarda tooexecute encima de la celda: 38.62 segundos

### <a name="random-forest-regression"></a>Regresión con bosque aleatorio
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de bosque aleatorio que predice la cantidad de sugerencia para datos de ida y vuelta de Nueva York taxi Hola.   

> [!NOTE]
> Se proporciona la validación cruzada con parámetro barrido usando código personalizado en el apéndice de hello.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA**

RMSE = 0.931981967875

R-sqr = 0.733445485802

Tiempo que tarda tooexecute encima de la celda: 25.98 segundos

### <a name="gradient-boosting-trees-regression"></a>Regresión con árboles impulsados por gradiente
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de árboles de aumento degradado que predice la cantidad de sugerencia para hello datos de Nueva York taxi de ida y vuelta.

**Entrenamiento y evaluación**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

RMSE = 0.928172197114

R-sqr = 0.732680354389

Tiempo que tarda tooexecute encima de la celda: 20,9 segundos

**Trazado**

*tmp_results* está registrado como una tabla de Hive en la celda anterior de Hola. Resultados de tabla Hola son salidas en hello *sqlResults* trama de datos para trazar. Este es el código de hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Aquí es Hola código tooplot Hola datos mediante servidor de Jupyter Hola.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Apéndice: Tareas de regresión adicionales mediante validación cruzada con barridos de parámetros
Este apéndice contiene que muestra de código cómo CV toodo con net elástico para la regresión lineal y cómo toodo CV con parámetro barrer usando código personalizado para la regresión de bosque aleatorio.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Validación cruzada con red elástica para la regresión lineal
código de Hello en esta sección muestra cómo toodo cross validación con net flexible para la regresión lineal y cómo tooevaluate Hola modelo con datos de prueba.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

Tiempo que tarda tooexecute encima de la celda: 161.21 segundos

**Evaluación con métrica R-SQR**

*tmp_results* está registrado como una tabla de Hive en la celda anterior de Hola. Resultados de tabla Hola son salidas en hello *sqlResults* trama de datos para trazar. Este es el código de hello

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Aquí es toocalculate de código de hello sqr R.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**SALIDA**

R-sqr = 0.619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Validación cruzada con barrido de parámetros mediante código personalizado para la regresión con bosque aleatorio
código de Hello en esta sección muestra cómo toodo validación cruzada con usando código personalizado para la regresión de bosque aleatorio de barrido de parámetros y cómo tooevaluate Hola modelo con datos de prueba.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA**

RMSE = 0.906972198262

R-sqr = 0.740751197012

Tiempo que tarda tooexecute encima de la celda: 69.17 segundos

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Limpieza de objetos de la memoria e impresión de las ubicaciones de los modelos
Use `unpersist()` objetos toodelete en la memoria caché.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**SALIDA**

PythonRDD[122] at RDD at PythonRDD.scala:43

** Copia impresa ruta de acceso toomodel archivos toobe utilizado en el Bloc de notas de hello consumo. ** tooconsume y puntuación una independiente de conjuntos de datos, necesita toocopy y pegue estos nombres de archivo en hello "Bloc de notas de consumo".

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**SALIDA**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>Pasos siguientes
Ahora que ha creado los modelos de regresión y de clasificación con hello Spark MlLib, cómo está listo toolearn tooscore y evaluar estos modelos.

**Consumo de modelo:** toolearn cómo tooscore y evaluar modelos de clasificación y regresión de hello creados en este tema, consulte [puntuación y evaluar modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md).

