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
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="d4702-103">Operacionalización de modelos de aprendizaje automático creados con Spark</span><span class="sxs-lookup"><span data-stu-id="d4702-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="d4702-104">Este tema muestra cómo toooperationalize un modelo de aprendizaje de máquina guardada (ML) con Python en HDInsight Spark clústeres.</span><span class="sxs-lookup"><span data-stu-id="d4702-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="d4702-105">Describe cómo tooload máquina modelos de aprendizaje que se han creado mediante Spark MLlib y almacenado en el almacenamiento de blobs de Azure (WASB) y cómo tooscore con conjuntos de datos que también han sido almacenados en WASB.</span><span class="sxs-lookup"><span data-stu-id="d4702-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="d4702-106">Muestra datos de entrada de proceso de toopre cómo hello, características de transformación con Hola funciones de indización y codificación en el Kit de herramientas de hello MLlib y cómo toocreate un objeto de datos con la etiqueta de punto que se puede usar como entrada para puntuar con modelos de aprendizaje automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="d4702-107">los modelos de Hello usados para puntuar incluyen regresión lineal, regresión logística, modelos de bosque aleatorio y modelos de árboles de impulso degradado.</span><span class="sxs-lookup"><span data-stu-id="d4702-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="d4702-108">Clústeres de Spark y cuadernos de Jupyter</span><span class="sxs-lookup"><span data-stu-id="d4702-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="d4702-109">Pasos de configuración y Hola código toooperationalize un modelo de aprendizaje automático se proporcionan en este tutorial para usar un clúster de HDInsight Spark 1.6, así como un clúster de Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d4702-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="d4702-110">También se proporciona código de Hello para estos procedimientos en blocs de notas de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d4702-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="d4702-111">Notebook para Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="d4702-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="d4702-112">Hola [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook muestra cómo toooperationalize un modelo guardado con Python en HDInsight de clústeres.</span><span class="sxs-lookup"><span data-stu-id="d4702-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="d4702-113">Notebook para Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="d4702-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="d4702-114">Bloc de notas de toomodify hello Jupyter para toouse 1.6 Spark con un clúster de HDInsight Spark 2.0, reemplace el archivo de código Python de hello con [este archivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="d4702-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="d4702-115">Este código muestra cómo se crean modelos de hello tooconsume en Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d4702-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d4702-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d4702-116">Prerequisites</span></span>

1. <span data-ttu-id="d4702-117">Se necesita una cuenta de Azure y un Spark 1.6 (o 2.0 de Spark) clúster de HDInsight toocomplete en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d4702-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="d4702-118">Vea hello [información general de ciencia de datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) para obtener instrucciones sobre cómo toosatisfy estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="d4702-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="d4702-119">Este tema también contiene una descripción de hello datos NYC 2013 Taxi emplear e instrucciones sobre cómo tooexecute código de Jupyter notebook en clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="d4702-120">Hola también se debe crear modelos de aprendizaje automático toobe con puntuación aquí por trabajar a través de hello [exploración de datos y el modelado con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tema para clúster Hola Spark 1.6 o blocs de notas de hello Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d4702-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="d4702-121">blocs de notas de Hello Spark 2.0 utiliza un conjunto de datos adicional para la tarea de clasificación de hello, Hola conocido Airline a la hora de salida dataset desde 2011 y 2012.</span><span class="sxs-lookup"><span data-stu-id="d4702-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="d4702-122">Se proporciona una descripción de hello blocs de notas y vínculos toothem Hola [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para el repositorio de GitHub de Hola que los contienen.</span><span class="sxs-lookup"><span data-stu-id="d4702-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="d4702-123">Además, código de hello aquí y en blocs de notas de hello vinculada genérica y debe funcionar en cualquier clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="d4702-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="d4702-124">Si no utilizas HDInsight Spark, pasos de configuración y administración de clúster de hello pueden ser ligeramente diferentes de lo que se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="d4702-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="d4702-125">El programa de instalación: Hola, bibliotecas y ubicaciones de almacenamiento preestablecido contexto Spark</span><span class="sxs-lookup"><span data-stu-id="d4702-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="d4702-126">Spark es capaz de tooan tooread y escritura Blob de almacenamiento de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="d4702-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="d4702-127">Por lo tanto, cualquiera de los datos existentes almacenados en ella se pueden procesar mediante Spark y Hola resultados almacenados en WASB.</span><span class="sxs-lookup"><span data-stu-id="d4702-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="d4702-128">modelos de toosave o archivos en WASB, ruta de acceso de hello debe toobe especificado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d4702-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="d4702-129">Hola de clúster predeterminado contenedor adjuntada toohello Spark puede hacer referencia mediante un ruta que comienza con: *"wasb / /"*.</span><span class="sxs-lookup"><span data-stu-id="d4702-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="d4702-130">ejemplo de código siguiente Hello Especifica ubicación Hola de hello toobe de datos de lectura y se guarda la ruta de acceso de hello para la salida de hello modelo almacenamiento directory toowhich Hola modelo.</span><span class="sxs-lookup"><span data-stu-id="d4702-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="d4702-131">Establecimiento de rutas de directorio para las ubicaciones de almacenamiento de WASB</span><span class="sxs-lookup"><span data-stu-id="d4702-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="d4702-132">Los modelos se guardan en: "wasb:///user/remoteuser/NYCTaxi/Models".</span><span class="sxs-lookup"><span data-stu-id="d4702-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="d4702-133">Si esta ruta de acceso no está configurada correctamente, no se cargará los modelos para su puntuación.</span><span class="sxs-lookup"><span data-stu-id="d4702-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="d4702-134">Hello resultados puntuados se han guardado en: "wasb: / / / usuario/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="d4702-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="d4702-135">Si hello toofolder de ruta de acceso es incorrecta, no se guardan los resultados en esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="d4702-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="d4702-136">ubicaciones de ruta de acceso del archivo de Hello pueden copiarse y pegarse en marcadores de posición de hello en este código de salida de hello de la última celda de Hola de hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="d4702-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="d4702-137">Le mostramos las rutas de acceso de directorio de hello código tooset:</span><span class="sxs-lookup"><span data-stu-id="d4702-137">Here is hello code tooset directory paths:</span></span> 

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

<span data-ttu-id="d4702-138">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-138">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="d4702-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="d4702-140">Importación de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="d4702-140">Import libraries</span></span>
<span data-ttu-id="d4702-141">Establecer contexto de spark y bibliotecas necesarias de importación con el siguiente código de hello</span><span class="sxs-lookup"><span data-stu-id="d4702-141">Set spark context and import necessary libraries with hello following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="d4702-142">Contexto de Spark preestablecido e instrucciones mágicas de PySpark</span><span class="sxs-lookup"><span data-stu-id="d4702-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="d4702-143">los kernels de Hello PySpark que se proporcionan con blocs de notas Jupyter tienen un contexto de valores preestablecido.</span><span class="sxs-lookup"><span data-stu-id="d4702-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="d4702-144">Por lo que no es necesario tooset Hola Spark o subárbol contextos explícitamente antes de empezar a trabajar con la aplicación hello que está desarrollando.</span><span class="sxs-lookup"><span data-stu-id="d4702-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="d4702-145">Estos contextos están disponibles de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d4702-145">These are available for you by default.</span></span> <span data-ttu-id="d4702-146">Estos contextos son:</span><span class="sxs-lookup"><span data-stu-id="d4702-146">These contexts are:</span></span>

* <span data-ttu-id="d4702-147">sc: Para Spark</span><span class="sxs-lookup"><span data-stu-id="d4702-147">sc - for Spark</span></span> 
* <span data-ttu-id="d4702-148">sqlContext: Para Hive</span><span class="sxs-lookup"><span data-stu-id="d4702-148">sqlContext - for Hive</span></span>

<span data-ttu-id="d4702-149">Hello PySpark kernel proporciona algunos predefinidas "magics", que son comandos especiales que se pueden llamar con %%.</span><span class="sxs-lookup"><span data-stu-id="d4702-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="d4702-150">Hay dos comandos de este tipo que se utilizan en estos ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="d4702-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="d4702-151">**%% local** especifica que el código de hello en las líneas siguientes se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="d4702-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="d4702-152">El código debe ser un código de Python válido.</span><span class="sxs-lookup"><span data-stu-id="d4702-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="d4702-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="d4702-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="d4702-154">Ejecuta una consulta de Hive en hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="d4702-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="d4702-155">Si se pasa el parámetro -o de hello, resultado de hello de consulta de Hola se conserva en hello %% contexto Python local como una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="d4702-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="d4702-156">Para obtener más información sobre los kernels de Hola para hello predefinidos y blocs de notas de Jupyter "magics" que proporcionan, consulte [clústeres de núcleos disponibles para equipos portátiles Jupyter con Linux de HDInsight Spark en HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="d4702-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="d4702-157">Inserción de datos y creación de una trama de datos limpia</span><span class="sxs-lookup"><span data-stu-id="d4702-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="d4702-158">Esta sección contiene código de hello para una serie de tareas requiere tooingest Hola datos toobe con puntuación.</span><span class="sxs-lookup"><span data-stu-id="d4702-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="d4702-159">Leer de un ejemplo de 0,1% combinadas de hello taxi de ida y vuelta y tarifa del archivo (almacenado como un archivo .tsv), dar formato a datos hello y, a continuación, crea una trama de datos limpia.</span><span class="sxs-lookup"><span data-stu-id="d4702-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="d4702-160">archivos de ida y vuelta y tarifa taxi Hola se unieron basándose en el procedimiento de hello proporcionado en el: [Hola proceso de ciencia de datos de equipo en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md) tema.</span><span class="sxs-lookup"><span data-stu-id="d4702-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

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

<span data-ttu-id="d4702-161">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-161">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-162">Tiempo que tarda tooexecute encima de la celda: 46.37 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="d4702-163">Preparación de los datos para la puntuación en Spark</span><span class="sxs-lookup"><span data-stu-id="d4702-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="d4702-164">Esta sección muestra cómo codificar tooindex y escalar tooprepare de las características de categorías para su uso en algoritmos de aprendizaje MLlib supervisado para la clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="d4702-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="d4702-165">Transformación de características: indexación y codificación de características categóricas para su incorporación en modelos para puntuación</span><span class="sxs-lookup"><span data-stu-id="d4702-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="d4702-166">Esta sección se muestra cómo tooindex datos de categorías mediante un `StringIndexer` y codificar características con `OneHotEncoder` de entrada en los modelos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="d4702-167">Hola [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica una columna de cadena de la columna de etiquetas de tooa de índices de la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d4702-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="d4702-168">índices de Hola se ordenan por frecuencias de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d4702-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="d4702-169">Hola [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) asigna una columna de la columna de etiqueta índices tooa de vectores binarios, con al menos un solo uno valor.</span><span class="sxs-lookup"><span data-stu-id="d4702-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="d4702-170">Esta codificación permite algoritmos que esperan las características con valores continuas, como la regresión logística, toobe aplica toocategorical características.</span><span class="sxs-lookup"><span data-stu-id="d4702-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

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

<span data-ttu-id="d4702-171">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-171">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-172">Tiempo que tarda tooexecute encima de la celda: 5.37 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="d4702-173">Creación de objetos RDD con matrices de características para su entrada en los modelos</span><span class="sxs-lookup"><span data-stu-id="d4702-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="d4702-174">Esta sección contiene código que muestre cómo tooindex datos de texto por categorías como un diseño dirigido por responsabilidades de objeto y activa uno codifican por lo que puede ser usado tootrain y prueba MLlib la regresión logística y los modelos basados en árbol.</span><span class="sxs-lookup"><span data-stu-id="d4702-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="d4702-175">los datos indizados Hello se almacenan una en [resistente distribuidas conjunto de datos (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objetos.</span><span class="sxs-lookup"><span data-stu-id="d4702-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="d4702-176">Se trata de abstracción básica de hello en Spark.</span><span class="sxs-lookup"><span data-stu-id="d4702-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="d4702-177">Un objeto RDD representa una colección inmutable con particiones de los elementos con los que se puede trabajar en paralelo con Spark.</span><span class="sxs-lookup"><span data-stu-id="d4702-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="d4702-178">También contiene el código que muestra cómo Hola tooscale datos con `StandardScalar` proporcionada por MLlib para su uso en la regresión lineal con estocástico degradado descenso (SGD), un algoritmo popular para entrenar una amplia variedad de modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="d4702-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="d4702-179">Hola [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) es tooscale usado Hola características toounit varianza.</span><span class="sxs-lookup"><span data-stu-id="d4702-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="d4702-180">Ampliación de característica, también conocida como la normalización de datos, se garantiza que funciones con valores muy dispersos no se le otorgó excesivo sopesar en función del objetivo de hello.</span><span class="sxs-lookup"><span data-stu-id="d4702-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

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

<span data-ttu-id="d4702-181">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-181">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-182">Tiempo que tarda tooexecute encima de la celda: 11.72 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="d4702-183">Puntuación con hello modelo de regresión logística y guardar tooblob de salida</span><span class="sxs-lookup"><span data-stu-id="d4702-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="d4702-184">código de Hello en esta sección se muestra cómo tooload un modelo de regresión logística que se ha guardado en Azure almacenamiento de blobs usar toopredict o no se le paga una sugerencia durante un viaje taxi puntuar con métricas de clasificación estándar y, a continuación, guarde y trazar Hola resultados tooblob almacenamiento de información.</span><span class="sxs-lookup"><span data-stu-id="d4702-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="d4702-185">Hola resultados puntuado se almacenan en objetos de diseño dirigido por responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="d4702-185">hello scored results are stored in RDD objects.</span></span> 

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

<span data-ttu-id="d4702-186">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-186">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-187">Tiempo que tarda tooexecute encima de la celda: 19.22 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="d4702-188">Puntuación de un modelo de regresión lineal</span><span class="sxs-lookup"><span data-stu-id="d4702-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="d4702-189">Utilizamos [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain un modelo de regresión lineal con descenso de gradiente estocástico (SGD) de cantidad de hello toopredict de optimización de sugerencia de pago.</span><span class="sxs-lookup"><span data-stu-id="d4702-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="d4702-190">código de Hello en esta sección muestra cómo tooload un modelo de regresión lineal desde el almacenamiento de blobs de Azure, puntuación mediante variables de escaladas y, a continuación, guarde el blob de hello resultados toohello back.</span><span class="sxs-lookup"><span data-stu-id="d4702-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

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


<span data-ttu-id="d4702-191">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-191">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-192">Tiempo que tarda tooexecute encima de la celda: 16.63 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="d4702-193">Puntuación de los modelos de bosque aleatorio de clasificación y regresión</span><span class="sxs-lookup"><span data-stu-id="d4702-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="d4702-194">código de Hello en esta sección muestra cómo hello tooload guarda clasificación y modelos de bosque aleatorio de regresión que guarda en el almacenamiento de blobs de Azure, puntuación su rendimiento con clasificador estándar y las medidas de regresión y, a continuación, guarde Hola resultados tooblob atrás almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d4702-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="d4702-195">[bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="d4702-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="d4702-196">Combina riesgo del Hola de tooreduce de árboles de muchos decisión de desbordamiento.</span><span class="sxs-lookup"><span data-stu-id="d4702-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="d4702-197">Bosques aleatorios pueden controlar las características de categorías, ampliar la configuración de clasificación multiclase toohello, no requieren escalado de características y no es capaz de toocapture linealidades y las interacciones de características.</span><span class="sxs-lookup"><span data-stu-id="d4702-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="d4702-198">Bosques aleatorios son uno de los modelos para la clasificación y regresión de aprendizaje de máquina más éxito Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="d4702-199">[spark.mllib](http://spark.apache.org/mllib/) admite bosques aleatorios para realizar operaciones de clasificación binaria y multiclase, y de regresión; las dos emplean características de categorías y continuas.</span><span class="sxs-lookup"><span data-stu-id="d4702-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

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

<span data-ttu-id="d4702-200">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-200">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-201">Tiempo que tarda tooexecute encima de la celda: 31.07 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="d4702-202">Puntuación de modelos de árboles impulsados por gradiente de clasificación y regresión</span><span class="sxs-lookup"><span data-stu-id="d4702-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="d4702-203">código de Hello en esta sección muestra cómo clasificación tooload regresión modelos de árboles de impulso degradado desde el almacenamiento de blobs de Azure, puntuación su rendimiento con clasificador estándar y las medidas de regresión y, a continuación, guardar Hola resultados tooblob back-almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d4702-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="d4702-204">**spark.mllib** admite GBT para realizar operaciones de clasificación binaria y de regresión; las dos emplean características de categorías y continuas.</span><span class="sxs-lookup"><span data-stu-id="d4702-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="d4702-205">[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="d4702-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="d4702-206">Árboles de decisión de entrenamiento de GBTs forma iterativa toominimize una función de pérdida.</span><span class="sxs-lookup"><span data-stu-id="d4702-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="d4702-207">GBTs puede controlar las características de categorías, no requieren escalado de características y no es capaz de toocapture linealidades y las interacciones de características.</span><span class="sxs-lookup"><span data-stu-id="d4702-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="d4702-208">También se pueden usar en una configuración de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="d4702-208">They can also be used in a multiclass-classification setting.</span></span>

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

<span data-ttu-id="d4702-209">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-209">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-210">Tiempo que tarda tooexecute encima de la celda: 14.6 segundos</span><span class="sxs-lookup"><span data-stu-id="d4702-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="d4702-211">Limpieza de objetos de la memoria e impresión de las ubicaciones de los archivos puntuados</span><span class="sxs-lookup"><span data-stu-id="d4702-211">Clean up objects from memory and print scored file locations</span></span>
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


<span data-ttu-id="d4702-212">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d4702-212">**OUTPUT:**</span></span>

<span data-ttu-id="d4702-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="d4702-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="d4702-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="d4702-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="d4702-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="d4702-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="d4702-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="d4702-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="d4702-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="d4702-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="d4702-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="d4702-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="d4702-219">Uso de modelos de Spark mediante una interfaz web</span><span class="sxs-lookup"><span data-stu-id="d4702-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="d4702-220">Spark proporciona un mecanismo de trabajos por lotes de envío de tooremotely o realizar consultas interactivas a través de un resto de la interfaz con un componente denominado a Livio.</span><span class="sxs-lookup"><span data-stu-id="d4702-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="d4702-221">Livy está habilitado de forma predeterminada en el clúster de Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4702-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="d4702-222">Para más información, vea [Envío de trabajos de Spark de forma remota mediante Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="d4702-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="d4702-223">Puede usar a Livio tooremotely enviar un trabajo que procesar por lotes puntuaciones de un archivo que se almacena en un blob de Azure y, a continuación, escribe el blob de hello resultados tooanother.</span><span class="sxs-lookup"><span data-stu-id="d4702-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="d4702-224">toodo, cargar el script de Python Hola desde</span><span class="sxs-lookup"><span data-stu-id="d4702-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="d4702-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob de clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="d4702-226">Puede usar una herramienta como **Microsoft Azure Storage Explorer** o **AzCopy** blob de clúster de toocopy Hola script toohello.</span><span class="sxs-lookup"><span data-stu-id="d4702-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="d4702-227">En nuestro caso se carga el script de Hola demasiado***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="d4702-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="d4702-228">Hola teclas de acceso que necesitan puede encontrarse en el portal de Hola Hola cuenta de almacenamiento asociada con el clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="d4702-229">Una vez cargado toothis ubicación, esta secuencia de comandos se ejecuta en el clúster de Spark hello en un contexto distribuido.</span><span class="sxs-lookup"><span data-stu-id="d4702-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="d4702-230">Se carga el modelo de Hola y se ejecuta predicciones en archivos de entrada basados en modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="d4702-231">Para invocar este script de forma remota con una sencilla solicitud HTTPS/REST en Livy.</span><span class="sxs-lookup"><span data-stu-id="d4702-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="d4702-232">Aquí es un curl comando tooconstruct Hola HTTP solicitud tooinvoke hello script de Python remotamente.</span><span class="sxs-lookup"><span data-stu-id="d4702-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="d4702-233">Reemplace CLUSTERLOGIN, CLUSTERPASSWORD, nombre del clúster con los valores adecuados para su clúster Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="d4702-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="d4702-234">Puede utilizar cualquier lenguaje en el trabajo Hola sistema remoto tooinvoke Hola Spark a través de Livio realizando una llamada simple de HTTPS con autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="d4702-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="d4702-235">Sería biblioteca de Python solicitudes de hello toouse cómoda cuando se realiza esta llamada HTTP, pero actualmente no está instalado de forma predeterminada en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4702-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="d4702-236">Por ese motivo se usan bibliotecas HTTP más antiguas.</span><span class="sxs-lookup"><span data-stu-id="d4702-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="d4702-237">Este es el código de Python de Hola para llamada Hola HTTP:</span><span class="sxs-lookup"><span data-stu-id="d4702-237">Here is hello Python code for hello HTTP call:</span></span>

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


<span data-ttu-id="d4702-238">También puede agregar este código de Python[funciones de Azure](https://azure.microsoft.com/documentation/services/functions/) tootrigger un envío de trabajos de Spark que puntúa un blob en función de diversos eventos como un temporizador, creación o actualización de un blob.</span><span class="sxs-lookup"><span data-stu-id="d4702-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="d4702-239">Si prefiere una experiencia de cliente gratuito de código, usar hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke Hola Spark proceso por lotes de puntuación mediante la definición de una acción HTTP en hello **el Diseñador de aplicaciones de la lógica de** y establecer sus parámetros.</span><span class="sxs-lookup"><span data-stu-id="d4702-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="d4702-240">En Azure Portal, cree una nueva aplicación lógica seleccionando **+Nuevo** -> **Web y móvil** -> **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="d4702-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="d4702-241">toobring seguridad hello **el Diseñador de aplicaciones de la lógica de**, escriba nombre de Hola de hello aplicación lógica y Plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d4702-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="d4702-242">Seleccione una acción HTTP y escriba los parámetros de Hola que se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4702-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Diseñador de Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="d4702-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4702-244">What's next?</span></span>
<span data-ttu-id="d4702-245">**Validación cruzada y barrido de hiperparámetros**: Consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.</span><span class="sxs-lookup"><span data-stu-id="d4702-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

