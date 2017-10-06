---
title: "modelos de aprendizaje de automático integrado Spark aaaOperationalize | Documentos de Microsoft"
description: "Cómo se almacena en el almacenamiento de blobs de Azure (WASB) con Python tooload y puntuación de aprendizaje de los modelos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a>Operacionalización de modelos de aprendizaje automático creados con Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este tema muestra cómo toooperationalize un modelo de aprendizaje de máquina guardada (ML) con Python en HDInsight Spark clústeres. Describe cómo tooload máquina modelos de aprendizaje que se han creado mediante Spark MLlib y almacenado en el almacenamiento de blobs de Azure (WASB) y cómo tooscore con conjuntos de datos que también han sido almacenados en WASB. Muestra datos de entrada de proceso de toopre cómo hello, características de transformación con Hola funciones de indización y codificación en el Kit de herramientas de hello MLlib y cómo toocreate un objeto de datos con la etiqueta de punto que se puede usar como entrada para puntuar con modelos de aprendizaje automático de Hola. los modelos de Hello usados para puntuar incluyen regresión lineal, regresión logística, modelos de bosque aleatorio y modelos de árboles de impulso degradado.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Clústeres de Spark y cuadernos de Jupyter
Pasos de configuración y Hola código toooperationalize un modelo de aprendizaje automático se proporcionan en este tutorial para usar un clúster de HDInsight Spark 1.6, así como un clúster de Spark 2.0. También se proporciona código de Hello para estos procedimientos en blocs de notas de Jupyter.

### <a name="notebook-for-spark-16"></a>Notebook para Spark 1.6
Hola [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook muestra cómo toooperationalize un modelo guardado con Python en HDInsight de clústeres. 

### <a name="notebook-for-spark-20"></a>Notebook para Spark 2.0
Bloc de notas de toomodify hello Jupyter para toouse 1.6 Spark con un clúster de HDInsight Spark 2.0, reemplace el archivo de código Python de hello con [este archivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Este código muestra cómo se crean modelos de hello tooconsume en Spark 2.0.


## <a name="prerequisites"></a>Requisitos previos

1. Se necesita una cuenta de Azure y un Spark 1.6 (o 2.0 de Spark) clúster de HDInsight toocomplete en este tutorial. Vea hello [información general de ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) para obtener instrucciones sobre cómo toosatisfy estos requisitos. Este tema también contiene una descripción de hello datos NYC 2013 Taxi emplear e instrucciones sobre cómo tooexecute código de Jupyter notebook en clúster de Spark Hola. 
2. Hola también se debe crear modelos de aprendizaje automático toobe con puntuación aquí por trabajar a través de hello [exploración de datos y el modelado con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tema para clúster Hola Spark 1.6 o blocs de notas de hello Spark 2.0. 
3. blocs de notas de Hello Spark 2.0 utiliza un conjunto de datos adicional para la tarea de clasificación de hello, Hola conocido Airline a la hora de salida dataset desde 2011 y 2012. Se proporciona una descripción de hello blocs de notas y vínculos toothem Hola [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para el repositorio de GitHub de Hola que los contienen. Además, código de hello aquí y en blocs de notas de hello vinculada genérica y debe funcionar en cualquier clúster de Spark. Si no utilizas HDInsight Spark, pasos de configuración y administración de clúster de hello pueden ser ligeramente diferentes de lo que se muestra aquí. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>El programa de instalación: Hola, bibliotecas y ubicaciones de almacenamiento preestablecido contexto Spark
Spark es capaz de tooan tooread y escritura Blob de almacenamiento de Azure (WASB). Por lo tanto, cualquiera de los datos existentes almacenados en ella se pueden procesar mediante Spark y Hola resultados almacenados en WASB.

modelos de toosave o archivos en WASB, ruta de acceso de hello debe toobe especificado correctamente. Hola de clúster predeterminado contenedor adjuntada toohello Spark puede hacer referencia mediante un ruta que comienza con: *"wasb / /"*. ejemplo de código siguiente Hello Especifica ubicación Hola de hello toobe de datos de lectura y se guarda la ruta de acceso de hello para la salida de hello modelo almacenamiento directory toowhich Hola modelo. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Establecimiento de rutas de directorio para las ubicaciones de almacenamiento de WASB
Los modelos se guardan en: "wasb:///user/remoteuser/NYCTaxi/Models". Si esta ruta de acceso no está configurada correctamente, no se cargará los modelos para su puntuación.

Hello resultados puntuados se han guardado en: "wasb: / / / usuario/remoteuser/NYCTaxi/ScoredResults". Si hello toofolder de ruta de acceso es incorrecta, no se guardan los resultados en esa carpeta.   

> [!NOTE]
> ubicaciones de ruta de acceso del archivo de Hello pueden copiarse y pegarse en marcadores de posición de hello en este código de salida de hello de la última celda de Hola de hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** Bloc de notas.   
> 
> 

Le mostramos las rutas de acceso de directorio de hello código tooset: 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

**SALIDA:**

datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Importación de bibliotecas
Establecer contexto de spark y bibliotecas necesarias de importación con el siguiente código de hello

    #IMPORT LIBRARIES
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

* **%% local** especifica que el código de hello en las líneas siguientes se ejecuta localmente. El código debe ser un código de Python válido.
* **%%sql -o <variable name>** 
* Ejecuta una consulta de Hive en hello sqlContext. Si se pasa el parámetro -o de hello, resultado de hello de consulta de Hola se conserva en hello %% contexto Python local como una trama de datos de Pandas.

Para obtener más información sobre los kernels de Hola para hello predefinidos y blocs de notas de Jupyter "magics" que proporcionan, consulte [clústeres de núcleos disponibles para equipos portátiles Jupyter con Linux de HDInsight Spark en HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Inserción de datos y creación de una trama de datos limpia
Esta sección contiene código de hello para una serie de tareas requiere tooingest Hola datos toobe con puntuación. Leer de un ejemplo de 0,1% combinadas de hello taxi de ida y vuelta y tarifa del archivo (almacenado como un archivo .tsv), dar formato a datos hello y, a continuación, crea una trama de datos limpia.

archivos de ida y vuelta y tarifa taxi Hola se unieron basándose en el procedimiento de hello proporcionado en el: [Hola proceso de ciencia de datos de equipo en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md) tema.

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
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

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 46.37 segundos

## <a name="prepare-data-for-scoring-in-spark"></a>Preparación de los datos para la puntuación en Spark
Esta sección muestra cómo codificar tooindex y escalar tooprepare de las características de categorías para su uso en algoritmos de aprendizaje MLlib supervisado para la clasificación y regresión.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Transformación de características: indexación y codificación de características categóricas para su incorporación en modelos para puntuación
Esta sección se muestra cómo tooindex datos de categorías mediante un `StringIndexer` y codificar características con `OneHotEncoder` de entrada en los modelos de Hola.

Hola [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica una columna de cadena de la columna de etiquetas de tooa de índices de la etiqueta. índices de Hola se ordenan por frecuencias de etiqueta. 

Hola [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) asigna una columna de la columna de etiqueta índices tooa de vectores binarios, con al menos un solo uno valor. Esta codificación permite algoritmos que esperan las características con valores continuas, como la regresión logística, toobe aplica toocategorical características.

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
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

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 5.37 segundos

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Creación de objetos RDD con matrices de características para su entrada en los modelos
Esta sección contiene código que muestre cómo tooindex datos de texto por categorías como un diseño dirigido por responsabilidades de objeto y activa uno codifican por lo que puede ser usado tootrain y prueba MLlib la regresión logística y los modelos basados en árbol. los datos indizados Hello se almacenan una en [resistente distribuidas conjunto de datos (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objetos. Se trata de abstracción básica de hello en Spark. Un objeto RDD representa una colección inmutable con particiones de los elementos con los que se puede trabajar en paralelo con Spark.

También contiene el código que muestra cómo Hola tooscale datos con `StandardScalar` proporcionada por MLlib para su uso en la regresión lineal con estocástico degradado descenso (SGD), un algoritmo popular para entrenar una amplia variedad de modelos de aprendizaje automático. Hola [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) es tooscale usado Hola características toounit varianza. Ampliación de característica, también conocida como la normalización de datos, se garantiza que funciones con valores muy dispersos no se le otorgó excesivo sopesar en función del objetivo de hello. 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 11.72 segundos

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Puntuación con hello modelo de regresión logística y guardar tooblob de salida
código de Hello en esta sección se muestra cómo tooload un modelo de regresión logística que se ha guardado en Azure almacenamiento de blobs usar toopredict o no se le paga una sugerencia durante un viaje taxi puntuar con métricas de clasificación estándar y, a continuación, guarde y trazar Hola resultados tooblob almacenamiento de información. Hola resultados puntuado se almacenan en objetos de diseño dirigido por responsabilidades. 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 19.22 segundos

## <a name="score-a-linear-regression-model"></a>Puntuación de un modelo de regresión lineal
Utilizamos [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain un modelo de regresión lineal con descenso de gradiente estocástico (SGD) de cantidad de hello toopredict de optimización de sugerencia de pago. 

código de Hello en esta sección muestra cómo tooload un modelo de regresión lineal desde el almacenamiento de blobs de Azure, puntuación mediante variables de escaladas y, a continuación, guarde el blob de hello resultados toohello back.

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 16.63 segundos

## <a name="score-classification-and-regression-random-forest-models"></a>Puntuación de los modelos de bosque aleatorio de clasificación y regresión
código de Hello en esta sección muestra cómo hello tooload guarda clasificación y modelos de bosque aleatorio de regresión que guarda en el almacenamiento de blobs de Azure, puntuación su rendimiento con clasificador estándar y las medidas de regresión y, a continuación, guarde Hola resultados tooblob atrás almacenamiento.

[bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.  Combina riesgo del Hola de tooreduce de árboles de muchos decisión de desbordamiento. Bosques aleatorios pueden controlar las características de categorías, ampliar la configuración de clasificación multiclase toohello, no requieren escalado de características y no es capaz de toocapture linealidades y las interacciones de características. Bosques aleatorios son uno de los modelos para la clasificación y regresión de aprendizaje de máquina más éxito Hola.

[spark.mllib](http://spark.apache.org/mllib/) admite bosques aleatorios para realizar operaciones de clasificación binaria y multiclase, y de regresión; las dos emplean características de categorías y continuas. 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 31.07 segundos

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Puntuación de modelos de árboles impulsados por gradiente de clasificación y regresión
código de Hello en esta sección muestra cómo clasificación tooload regresión modelos de árboles de impulso degradado desde el almacenamiento de blobs de Azure, puntuación su rendimiento con clasificador estándar y las medidas de regresión y, a continuación, guardar Hola resultados tooblob back-almacenamiento. 

**spark.mllib** admite GBT para realizar operaciones de clasificación binaria y de regresión; las dos emplean características de categorías y continuas. 

[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión. Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida. GBTs puede controlar las características de categorías, no requieren escalado de características y no es capaz de toocapture linealidades y las interacciones de características. También se pueden usar en una configuración de clasificación multiclase.

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SALIDA:**

Tiempo que tarda tooexecute encima de la celda: 14.6 segundos

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Limpieza de objetos de la memoria e impresión de las ubicaciones de los archivos puntuados
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


**SALIDA:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Uso de modelos de Spark mediante una interfaz web
Spark proporciona un mecanismo de trabajos por lotes de envío de tooremotely o realizar consultas interactivas a través de un resto de la interfaz con un componente denominado a Livio. Livy está habilitado de forma predeterminada en el clúster de Spark en HDInsight. Para más información, vea [Envío de trabajos de Spark de forma remota mediante Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

Puede usar a Livio tooremotely enviar un trabajo que procesar por lotes puntuaciones de un archivo que se almacena en un blob de Azure y, a continuación, escribe el blob de hello resultados tooanother. toodo, cargar el script de Python Hola desde  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob de clúster de Spark Hola. Puede usar una herramienta como **Microsoft Azure Storage Explorer** o **AzCopy** blob de clúster de toocopy Hola script toohello. En nuestro caso se carga el script de Hola demasiado***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Hola teclas de acceso que necesitan puede encontrarse en el portal de Hola Hola cuenta de almacenamiento asociada con el clúster de Spark Hola. 
> 
> 

Una vez cargado toothis ubicación, esta secuencia de comandos se ejecuta en el clúster de Spark hello en un contexto distribuido. Se carga el modelo de Hola y se ejecuta predicciones en archivos de entrada basados en modelo Hola.  

Para invocar este script de forma remota con una sencilla solicitud HTTPS/REST en Livy.  Aquí es un curl comando tooconstruct Hola HTTP solicitud tooinvoke hello script de Python remotamente. Reemplace CLUSTERLOGIN, CLUSTERPASSWORD, nombre del clúster con los valores adecuados para su clúster Spark Hola.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

Puede utilizar cualquier lenguaje en el trabajo Hola sistema remoto tooinvoke Hola Spark a través de Livio realizando una llamada simple de HTTPS con autenticación básica.   

> [!NOTE]
> Sería biblioteca de Python solicitudes de hello toouse cómoda cuando se realiza esta llamada HTTP, pero actualmente no está instalado de forma predeterminada en las funciones de Azure. Por ese motivo se usan bibliotecas HTTP más antiguas.   
> 
> 

Este es el código de Python de Hola para llamada Hola HTTP:

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


También puede agregar este código de Python[funciones de Azure](https://azure.microsoft.com/documentation/services/functions/) tootrigger un envío de trabajos de Spark que puntúa un blob en función de diversos eventos como un temporizador, creación o actualización de un blob. 

Si prefiere una experiencia de cliente gratuito de código, usar hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke Hola Spark proceso por lotes de puntuación mediante la definición de una acción HTTP en hello **el Diseñador de aplicaciones de la lógica de** y establecer sus parámetros. 

* En Azure Portal, cree una nueva aplicación lógica seleccionando **+Nuevo** -> **Web y móvil** -> **Aplicación lógica**. 
* toobring seguridad hello **el Diseñador de aplicaciones de la lógica de**, escriba nombre de Hola de hello aplicación lógica y Plan de servicio de aplicaciones.
* Seleccione una acción HTTP y escriba los parámetros de Hola que se muestra en hello figura siguiente:

![Diseñador de Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Pasos siguientes
**Validación cruzada y barrido de hiperparámetros**: Consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.

