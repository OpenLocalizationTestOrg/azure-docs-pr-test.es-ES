---
title: "exploración de aaaData y modelado con Spark | Documentos de Microsoft"
description: "Exhibe Hola funciones del Kit de herramientas de hello MLlib Spark en Azure de modelado y exploración de datos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Exploración y modelado de datos con Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

En este tutorial usa exploración de datos de HDInsight Spark toodo y clasificación binaria y regresión tareas de modelado en una muestra de Hola NYC taxi de ida y vuelta y resultados son el conjunto de datos de 2013.  Le guiará por los pasos de Hola de hello [proceso de ciencia de datos](http://aka.ms/datascienceprocess), -to-end, con un HDInsight Spark de clúster para el procesamiento y modelos de datos y Hola Hola toostore de blobs de Azure. proceso de Hello explora y visualiza los datos agregados de un Blob de almacenamiento de Azure y, a continuación, prepara Hola datos toobuild modelos predictivos. Estos modelos son compilación con clasificación binaria del toodo Hola Spark MLlib Kit de herramientas y tareas de modelado de regresión.

* Hola **clasificación binaria** tarea es toopredict haya o no una sugerencia se paga por los recorridos de Hola. 
* Hola **regresión** tarea es la cantidad de Hola de toopredict de sugerencia de hello en función de otras características de sugerencia. 

los modelos de Hello que usamos incluyen regresión logística y lineal, los bosques aleatorios y los árboles impulsados degradados:

* [Regresión lineal con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) es un modelo de regresión lineal que usa un método de descenso de gradiente estocástico (SGD) y para la optimización y la característica de ajuste de escala en cantidades de sugerencia de hello toopredict pago. 
* [Regresión logística con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regresión "logit", es un modelo de regresión que puede usarse en la variable dependiente de hello es la clasificación de datos de categorías toodo. LBFGS es un algoritmo de optimización de Newton tipo que se aproxima al algoritmo de hello Broyden – Fletcher – Goldfarb – Shanno (BFGS) con una cantidad limitada de memoria del equipo y que se usa ampliamente en el aprendizaje automático.
* [bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.  Combina riesgo del Hola de tooreduce de árboles de muchos decisión de desbordamiento. Bosques aleatorios se utilizan para la clasificación y regresión, pueden controlar las características de categorías y se pueden ampliar Configuración de clasificación multiclase toohello. No se requieren característica ajuste de escala y se pueda toocapture no linealidades e interacciones de característica. Bosques aleatorios son uno de los modelos para la clasificación y regresión de aprendizaje de máquina más éxito Hola.
* [árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión. Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida. GBTs se usan para la clasificación y regresión y puede controlar las características de categorías, no requieren la característica escalado y no es capaz de toocapture linealidades y las interacciones de características. También se pueden usar en una configuración de clasificación multiclase.

pasos de modelado de Hello también contienen código que muestra cómo tootrain, evaluar y guardar cada tipo de modelo. Python ha sido toocode usado Hola solución y tooshow Hola relevantes trazados.   

> [!NOTE]
> Aunque el Kit de herramientas de hello Spark MLlib es toowork diseñado en grandes conjuntos de datos, un ejemplo relativamente pequeño (con filas de 170K, aproximadamente 0,1% del conjunto de datos de Nueva York original Hola de ~ 30 Mb) se utiliza aquí por comodidad. ejercicio Hola aquí especificado se ejecuta eficazmente (en unos 10 minutos) en un clúster de HDInsight con 2 nodos de trabajador. Hello mismo código, con modificaciones menores, puede ser tooprocess usado más grandes conjuntos de datos, con las modificaciones apropiadas para almacenar en caché datos en la memoria y cambiar el tamaño de clúster de Hola.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Se necesita una cuenta de Azure y un Spark 1.6 (o 2.0 de Spark) clúster de HDInsight toocomplete en este tutorial. Vea hello [información general de ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) para obtener instrucciones sobre cómo toosatisfy estos requisitos. Este tema también contiene una descripción de hello datos NYC 2013 Taxi emplear e instrucciones sobre cómo tooexecute código de Jupyter notebook en clúster de Spark Hola. 

## <a name="spark-clusters-and-notebooks"></a>Clústeres y cuadernos de Spark
Los pasos de instalación y el código proporcionado en este tutorial son para HDInsight Spark 1.6. Sin embargo, Jupyter Notebooks se proporciona para clústeres de HDInsight Spark 1.6 y Spark 2.0. Se proporciona una descripción de hello blocs de notas y vínculos toothem Hola [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para el repositorio de GitHub de Hola que los contienen. Además, código de hello aquí y en blocs de notas de hello vinculada genérica y debe funcionar en cualquier clúster de Spark. Si no utilizas HDInsight Spark, pasos de configuración y administración de clúster de hello pueden ser ligeramente diferentes de lo que se muestra aquí. Para mayor comodidad, estos son Hola vínculos toohello Jupyter portátiles con Spark 1.6 (toobe ejecutar en el núcleo de pySpark Hola de hello servidor de Jupyter Notebook) y Spark 2.0 (se ejecuta en el núcleo de pySpark3 Hola de servidor de Jupyter Notebook hello toobe):

### <a name="spark-16-notebooks"></a>Cuadernos de Spark 1.6

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): proporciona información acerca de cómo tooperform la exploración de datos, modelado y puntuación con varios algoritmos.

### <a name="spark-20-notebooks"></a>Cuadernos de Spark 2.0
tareas de clasificación y regresión de Hola que se implementan mediante un clúster de Spark 2.0 son en blocs de notas independientes y portátil de clasificación de hello utiliza otro conjunto de datos:

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este archivo proporciona información sobre cómo tooperform la exploración de datos, modelado y puntuación en Spark 2.0 clústeres utilizando Hola recorridos Taxi de Nueva York y se describe de conjunto de datos tarifa [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Este bloc de notas puede ser un buen punto de partida para analizar rápidamente el código de hello que se proporcionan para Spark 2.0. Para un bloc de notas más detallada analiza Hola datos Taxi de Nueva York, consulte Bloc de notas siguiente hello en esta lista. Vea las notas de hello después de la lista que comparan estos blocs de notas. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): este archivo muestra cómo tooperform datos problemas con (Spark SQL y trama de datos de operaciones), la exploración, modelado y puntuación mediante Hola tarifas conjunto de datos se describe y recorridos de Nueva York Taxi [ aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): este archivo muestra cómo tooperform datos problemas con (Spark SQL y trama de datos de operaciones), la exploración, modelado y puntuación mediante Hola conocido salida en el momento de Airline conjunto de datos de 2011 y 2012. El conjunto de datos de hello airline se habían integrado con hello aeropuerto tiempo datos (por ejemplo, velocidad del viento, temperatura, altitud, etc.) anteriores toomodeling para que estas características de tiempo pueden incluirse en el modelo de Hola.

<!-- -->

> [!NOTE]
> el conjunto de datos de Hello airline agregó blocs de notas toohello Spark 2.0 toobetter ilustran el uso de Hola de algoritmos de clasificación. Vea Hola siguientes vínculos para obtener información sobre el conjunto de datos de salida en el momento de airline y conjunto de datos de tiempo:

>- Datos de salida puntuales de líneas aéreas: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Datos climatológicos del aeropuerto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
blocs de notas de Hello Spark 2.0 en hello taxi de Nueva York y airline vuelo retraso conjuntos de datos pueden tardar 10 minutos o más toorun (según el tamaño de Hola de su clúster HDI). Hello primer portátil Hola por encima de la lista muestra muchos aspectos Hola de exploración de datos, visualización y aprendizaje automático del modelo de entrenamiento en un portátil que toma menos toorun de tiempo con muestrear abajo NYC conjunto de datos, en qué Hola taxi y tarifa que se hayan archivos previamente combinados: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) este bloc de notas toma una cantidad menor tiempo toofinish (2-3 minutos) y puede ser un buen punto de partida para analizar rápidamente el código de hello tenemos se proporcionan para Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
las descripciones de Hola a continuación están relacionado toousing Spark 1.6. En las versiones 2.0 Spark, use blocs de notas de Hola se describe e indicados anteriormente. 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Importación de bibliotecas
Para la configuración también es necesario importar las bibliotecas necesarias. Establecer contexto de spark e importar bibliotecas necesarias con hello siguiente código:

    # IMPORT LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>Ingesta de datos de blob público
Hola primer paso en el proceso de ciencia de datos de hello es tooingest Hola datos toobe analizado de orígenes donde es reside en el entorno de exploración y el modelado de datos. entorno de Hello es Spark en este tutorial. Esta sección contiene código de hello toocomplete una serie de tareas:

* Introducción toobe de ejemplo de Hola datos modelada
* leer en el conjunto de datos de entrada hello (almacenado como un archivo .tsv)
* formato y Hola limpiar datos
* crear objetos en la memoria (RDD o tramas de datos) y almacenarlos en caché
* registrarlos como una tabla temporal en el contexto de SQL

Este es el código de hello para la recopilación de datos.

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 51.72 segundos

## <a name="data-exploration--visualization"></a>Visualización y exploración de datos
Una vez introducidos los datos de hello en Spark, hello siguiente paso en el proceso de ciencia de datos de hello es toogain descripción más profunda de los datos de hello mediante exploración y visualización. En esta sección, se examinan datos de taxi hello mediante consultas SQL y las variables de destino de trazado hello y características posibles para la inspección visual. En concreto, se traza frecuencia Hola de recuentos de pasajeros en viajes taxi, la frecuencia de Hola de cantidades de sugerencia y cómo sugerencias varían según el tipo y la cantidad de pago.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Trazar un histograma de frecuencias de recuento de pasajeros en el ejemplo hello de viajes de taxi
Este código y fragmentos de código siguientes usan SQL tooquery mágico Hola datos de ejemplo y local tooplot mágico Hola.

* **Magia SQL (`%%sql`)** HDInsight PySpark kernel hello admite consultas de HiveQL en línea fácil contra Hola sqlContext. Hola (-o VARIABLE_NAME) argumento conserva la salida de hello de consulta SQL de hello como una trama de datos de Pandas en el servidor de Jupyter Hola. Esto significa que está disponible en modo local Hola.
* Hola  **`%%local` mágico** es código toorun los utiliza localmente en el servidor de Jupyter hello, que es el nodo principal de Hola Hola del clúster de HDInsight. Normalmente, se utiliza `%%local` mágico junto con hello `%%sql` mágico con el parámetro -o. parámetro de Hello -o podría conservar la salida de hello de consulta SQL Hola localmente y, a continuación, %% magia local desencadenaría conjunto siguiente de Hola de toorun de fragmento de código localmente en la salida de hello de consultas SQL de Hola que se guarda localmente

salida de Hello se visualiza automáticamente después de ejecutar código de hello.

Esta consulta recupera el recuento de pasajeros ciclos de ida y Hola. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Este código crea una trama de datos local de resultado de la consulta de Hola y representa los datos de Hola. Hola `%%local` mágico crea una trama de datos local, `sqlResults`, que se puede utilizar para trazar con matplotlib. 

> [!NOTE]
> Esta instrucción mágica de PySpark se utiliza varias veces en este tutorial. Si la cantidad de Hola de datos es grande, debe muestrear toocreate una trama de datos que cabe en la memoria local.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Aquí es viajes de hello código tooplot Hola pasajeros recuentos

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**SALIDA:**

![Frecuencia de las carreras por número de pasajeros](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

Puede seleccionar entre los distintos tipos de visualizaciones (tabla, circular, línea, el área o barra) mediante el uso de hello **tipo** botones de menú en el Bloc de notas de Hola. aquí se muestra un gráfico de barras de Hola.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Trazado de un histograma de importes de propinas y de las variaciones en las propinas según número de pasajeros y tarifas.
Utilice una consulta toosample datos de SQL.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**SALIDA:** 

![Distribución del importe de las propinas](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Importe de las propinas por número de pasajeros](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importe de las propinas por importe de la tarifa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Diseño, transformación y preparación de los datos para el modelado de características
En esta sección se describe y proporciona código de hello para conocer los procedimientos que utiliza datos tooprepare para su uso en el modelado de aprendizaje automático. Muestra cómo hello toodo siguientes tareas:

* Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico
* Indexación y codificación de características categóricas
* Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático
* Crear un muestreo aleatorio dentro de los datos de Hola y dividir en entrenamiento y conjuntos de pruebas
* Ajuste de la escala de las características
* Almacenamiento de objetos en caché

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Creación de una nueva característica mediante la discretización de horas en cubos de tiempo de tráfico
Este código muestra cómo los depósitos de toocreate una nueva característica discretizando horas en vez de tráfico y, a continuación, cómo toocache Hola resultante trama de datos en memoria. Cuando se utilicen repetidamente resistente distribuidas los conjuntos de datos (RDDs) y tramas de datos, el almacenamiento en caché conduce tooimproved los tiempos de ejecución. En consecuencia, se almacenará en caché RDDs y tramas de datos en varias fases de tutorial Hola. 

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

**SALIDA:** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Indexación y codificación de características categóricas para la entrada en funciones de modelado
Esta sección se muestra cómo tooindex o codificar las características de categorías para la entrada en hello las funciones de modelado. Hola modelado y predecir las funciones de MLlib requieren características con los datos de entrada categorías toobe la indización o codifican toouse anterior. Según el modelo de hello, necesita tooindex o codificarlos de maneras diferentes:  

* **Modelado basados en árbol** requiere toobe categorías codificado como valores numéricos (por ejemplo, una función con tres categorías puede codificarse con 0, 1, 2). Esto lo proporciona la función [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) de MLlib. Esta función codifica una columna de cadena de la columna de etiquetas de tooa de índices de etiqueta que se ordenan por frecuencias de etiqueta. Aunque indizada con valores numéricos de entrada y manipulación de datos, algoritmos de hello basados en árbol pueden ser tootreat especificado correctamente como categorías. 
* **Modelos de regresión lineal y logística** requieren estrechamente con una codificación, donde, por ejemplo, una función con tres categorías se puede expandir en tres columnas de característica, cada contenedor 0 o 1 según la categoría de Hola de una observación. Proporciona MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) función toodo estrechamente con una codificación. Este codificador asigna una columna de la columna de etiqueta índices tooa de vectores binarios, con al menos un solo uno valor. Esta codificación permite algoritmos que esperan las características con valores numéricas, como la regresión logística, toobe aplica toocategorical características.

Este es Hola código tooindex y codificar las características de categorías:

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 1,28 segundos

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Creación de objetos de punto con etiqueta para la entrada en funciones de aprendizaje automático
Esta sección contiene código que muestra cómo tipo de datos de texto de categorías de tooindex como datos de un punto con la etiqueta y codifican, por lo que puede ser usado tootrain y prueba MLlib la regresión logística y otros modelos de clasificación. Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) con el formato de datos de entrada que necesita la mayoría de los algoritmos de aprendizaje automático de MLlib. Un [punto con etiqueta](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) es un vector local, denso o disperso, asociado con una etiqueta o respuesta.  

Esta sección contiene código que muestra cómo tooindex datos de texto por categorías como un [con la etiqueta punto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) tipo de datos y codificar, por lo que puede ser usado tootrain y prueba MLlib la regresión logística y otros modelos de clasificación. Los objetos de punto con etiqueta son conjuntos de datos distribuidos resistentes (RDD) que constan de una etiqueta (variable destino/respuesta) y un vector de característica. Muchos algoritmos de aprendizaje automático de MLlib necesitan este formato de entrada.

Este es Hola código tooindex y codificar las características de texto para clasificación binaria.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
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
Este código crea un muestreo aleatorio de datos de hello (25% se utiliza aquí). Aunque no es necesario para este ejemplo debido toohello tamaño del conjunto de datos de hello, demostraremos cómo puede muestrear aquí para saber cómo toouse para su propio problema cuando sea necesario. Cuando las muestras son grandes, esto puede ahorrar mucho tiempo al entrenar modelos. A continuación, dividiremos ejemplo hello en una parte de entrenamiento (aquí 75%) y una prueba toouse parte (aquí 25%) en la clasificación y el modelo de regresión.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 0,24 segundos

### <a name="feature-scaling"></a>Ajuste de la escala de las características
Ampliación de característica, también conocida como la normalización de datos, se garantiza que funciones con valores muy dispersos no se le otorgó excesivo sopesar en función del objetivo de hello. código para el escalado de la característica Hello usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza de tooscale Hola características toounit. MLlib lo proporciona para su uso en la regresión lineal con descenso de gradiente estocástico (SGD), un popular algoritmo para entrenar una amplia variedad de otros modelos de aprendizaje automático tales como regresiones regularizadas o máquinas de vectores de soporte (SVM).

> [!NOTE]
> Hemos encontrado hello LinearRegressionWithSGD algoritmo toobe toofeature confidencial ajuste de escala.
> 
> 

Aquí es tooscale variables de código de hello para su uso con un algoritmo SGD lineal Hola regularizado.

    # FEATURE SCALING

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

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 13.17 segundos

### <a name="cache-objects-in-memory"></a>Almacenamiento de objetos en caché
tiempo Hola para entrenamiento y prueba de algoritmos de aprendizaje automático pueden reducirse mediante objetos de marco de hello datos de entrada utilizados para la clasificación de regresión, el almacenamiento en caché y escalar características.

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

**SALIDA:** 

Tiempo que tarda tooexecute encima de la celda: 0,15 segundos

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Predicción de si se dio propina o no con modelos de clasificación binaria
Esta sección muestra cómo usar tres modelos para la tarea de clasificación binaria de hello de predecir si no se le paga una sugerencia para un recorrido de taxi. modelos de Hello presentados son:

* Regresión logística regularizada 
* Modelo de bosque aleatorio
* Árboles impulsados por gradiente

Cada sección de código de generación del modelo se dividirá en pasos: 

1. **entrenamiento del modelo** con un conjunto de parámetros
2. **Evaluación del modelo** en un conjunto de datos de prueba con métricas
3. **Guardado del modelo** en un blob para utilizarse en el futuro

### <a name="classification-using-logistic-regression"></a>Clasificación mediante regresión logística
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de regresión logística con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos dataset.

**Entrenar el modelo de regresión logística de hello mediante CV y barrido hyperparameter**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA:** 

Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

Intercept: -0.0111216486893

Tiempo que tarda tooexecute encima de la celda: 14.43 segundos

**Evaluar el modelo de clasificación binaria de hello con métricas estándares**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SALIDA:** 

Area under PR = 0.985297691373

Area under ROC = 0.983714670256

Summary Stats

Precision = 0.984304060189

Recall = 0.984304060189

F1 Score = 0.984304060189

Tiempo que tarda tooexecute encima de la celda: 57.61 segundos

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

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


**SALIDA:**

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Clasificación de bosque aleatorio
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de bosque aleatorio que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos conjunto de datos.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

**SALIDA:**

Area under ROC = 0.985297691373

Tiempo que tarda tooexecute encima de la celda: 31.09 segundos

### <a name="gradient-boosting-trees-classification"></a>Clasificación de árboles impulsados por gradiente
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de árboles de aumento de degradado que predice si no se le paga una sugerencia para un recorrido en hello NYC taxi tarifas y recorridos conjunto de datos.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


**SALIDA:**

Area under ROC = 0.985297691373

Tiempo que tarda tooexecute encima de la celda: 19.76 segundos

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Predicción de los importes de las propinas en las carreras de taxi con modelos de regresión
Esta sección muestra cómo utilizar tres modelos para la tarea de regresión de hello de predecir la cantidad de Hola de sugerencia de hello pagado por una taxi de ida y vuelta en función de otras características de sugerencia. modelos de Hello presentados son:

* Regresión lineal regularizada
* Bosque aleatorio
* Árboles impulsados por gradiente

Estos modelos se describen en la introducción de Hola. Cada sección de código de generación del modelo se dividirá en pasos: 

1. **entrenamiento del modelo** con un conjunto de parámetros
2. **Evaluación del modelo** en un conjunto de datos de prueba con métricas
3. **Guardado del modelo** en un blob para utilizarse en el futuro

### <a name="linear-regression-with-sgd"></a>regresión lineal con SGD
Hello código en esta sección muestra cómo toouse escalarse características tootrain una regresión lineal que usa el descenso de gradiente estocástico (SGD) para la optimización, y cómo tooscore, evaluar y guardar el modelo de hello en el almacenamiento de blobs de Azure (WASB).

> [!TIP]
> En nuestra experiencia, puede haber problemas con la convergencia de Hola de modelos LinearRegressionWithSGD y parámetros necesitan toobe cambiado/optimizado cuidadosamente para obtener un modelo válido. El ajuste de la escala de las variables ayuda con la convergencia. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA:**

Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]

Intercept: 0.853872718283

RMSE = 1.24190115863

R-sqr = 0.608017146081

Tiempo que tarda tooexecute encima de la celda: 58,42 segundos

### <a name="random-forest-regression"></a>Regresión con bosque aleatorio
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar una regresión de bosque aleatorio que predice la cantidad de sugerencia para hello datos de Nueva York taxi de ida y vuelta.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

**SALIDA:**

RMSE = 0.891209218139

R-sqr = 0.759661334921

Tiempo que tarda tooexecute encima de la celda: 49.21 segundos

### <a name="gradient-boosting-trees-regression"></a>Regresión con árboles impulsados por gradiente
código de Hello en esta sección muestra cómo tootrain, evaluar y guardar un modelo de árboles de aumento degradado que predice la cantidad de sugerencia para hello datos de Nueva York taxi de ida y vuelta.

**Entrenamiento y evaluación**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA:**

RMSE = 0.908473148639

R-sqr = 0.753835096681

Tiempo que tarda tooexecute encima de la celda: 34.52 segundos

**Trazado**

*tmp_results* está registrado como una tabla de Hive en la celda anterior de Hola. Resultados de tabla Hola son salidas en hello *sqlResults* trama de datos para trazar. Este es el código de hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Aquí es Hola código tooplot Hola datos mediante servidor de Jupyter Hola.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**SALIDA:**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Limpieza de objetos de la memoria
Use `unpersist()` objetos toodelete en la memoria caché.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Ubicaciones de almacenamiento de registro de los modelos de hello para el consumo y la puntuación
tooconsume y puntuación de un conjunto de datos independiente descrito en hello [puntuación y evalúe los modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md) tema, deberá toocopy y pegar estos archivos nombres que contienen modelos de hello guarda creados aquí en hello Bloc de notas de Jupyter de consumo. Aquí es tooprint de código de hello los archivos toomodel hello las rutas de acceso que necesita no existe.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**SALIDA**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>Pasos siguientes
Ahora que ha creado los modelos de regresión y de clasificación con hello Spark MlLib, cómo está listo toolearn tooscore y evaluar estos modelos. Hola avanzada de exploración de datos y modelado más profunda, profundiza Bloc de notas en incluida la validación cruzada, parámetro de hyper-barrido y el modelo de evaluación. 

**Consumo de modelo:** toolearn cómo tooscore y evaluar modelos de clasificación y regresión de hello creados en este tema, consulte [puntuación y evaluar modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md).

**Validación cruzada y barrido de hiperparámetros**: consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.

