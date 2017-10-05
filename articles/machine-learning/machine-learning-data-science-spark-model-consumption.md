---
title: "Operacionalización de modelos de aprendizaje automático creados con Spark | Microsoft Docs"
description: "Cómo cargar y puntuar modelos de aprendizaje almacenados en Azure Blob Storage (WASB) con Python."
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
ms.openlocfilehash: 00fec675bed0137473f7e3c5ddfe9c3c0e8344c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="d073f-103">Operacionalización de modelos de aprendizaje automático creados con Spark</span><span class="sxs-lookup"><span data-stu-id="d073f-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="d073f-104">En este tema se muestra cómo operacionalizar un modelo de aprendizaje automático con Python en clústeres de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-104">This topic shows how to operationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="d073f-105">Se describe cómo cargar modelos de aprendizaje automático creados con Spark MLlib y almacenados en Azure Blob Storage (WASB), además de cómo puntuarlos con conjuntos de datos que también se han guardado en WASB.</span><span class="sxs-lookup"><span data-stu-id="d073f-105">It describes how to load machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how to score them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="d073f-106">Muestra cómo procesar previamente los datos de entrada, transformar las características mediante las funciones de indexación y codificación en el kit de herramientas MLlib, y cómo crear un objeto de datos de punto con etiqueta que se puede usar como entrada para la puntuación con los modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="d073f-106">It shows how to pre-process the input data, transform features using the indexing and encoding functions in the MLlib toolkit, and how to create a labeled point data object that can be used as input for scoring with the ML models.</span></span> <span data-ttu-id="d073f-107">Los modelos usados para la puntuación son regresión lineal, regresión logística, modelos de bosque aleatorio y modelos de árboles impulsados por gradiente.</span><span class="sxs-lookup"><span data-stu-id="d073f-107">The models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="d073f-108">Clústeres de Spark y cuadernos de Jupyter</span><span class="sxs-lookup"><span data-stu-id="d073f-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="d073f-109">En este tutorial se proporcionan los pasos de configuración y el código para operacionalizar un modelo de ML para usar un clúster de HDInsight Spark 1.6 y un clúster de Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d073f-109">Setup steps and the code to operationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="d073f-110">También se proporciona el código para estos procedimientos en los cuadernos de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d073f-110">The code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="d073f-111">Notebook para Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="d073f-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="d073f-112">En el cuaderno de Jupyter [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) se muestra cómo operacionalizar un modelo guardado con Python en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d073f-112">The [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how to operationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="d073f-113">Notebook para Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="d073f-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="d073f-114">Para modificar este cuaderno de Jupyter para Spark 1.6 para usarlo con un clúster de HDInsight Spark 2.0, reemplace el archivo de código Python por [este archivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="d073f-114">To modify the Jupyter notebook for Spark 1.6 to use with an HDInsight Spark 2.0 cluster, replace the Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="d073f-115">Este código muestra cómo utilizar los modelos creados en Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d073f-115">This code shows how to consume the models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d073f-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d073f-116">Prerequisites</span></span>

1. <span data-ttu-id="d073f-117">Necesita una cuenta de Azure y un clúster de Spark 1.6 o Spark 2.0 HDInsight para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d073f-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="d073f-118">Consulte el artículo [Información general sobre la ciencia de los datos con Spark en HDInsight de Azure](machine-learning-data-science-spark-overview.md) para obtener instrucciones sobre cómo satisfacer estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="d073f-118">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="d073f-119">Ese tema también contiene una descripción de los datos de taxis de Nueva York de 2013 que se usan aquí, además de instrucciones sobre cómo ejecutar el código de un cuaderno de Jupyter Notebook en el clúster Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-119">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 
2. <span data-ttu-id="d073f-120">También debe crear los modelos de aprendizaje automático que se puntuarán aquí; para ello, consulte el tema [Exploración y modelado de datos con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) relativo al clúster de Spark 1.6 o los cuadernos de Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d073f-120">You must also create the machine learning models to be scored here by working through the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for the Spark 1.6 cluster or the Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="d073f-121">Los cuadernos de Spark 2.0 usan un conjunto de datos adicional para la tarea de clasificación, el conocido conjunto de datos Airline On-time departure de 2011 y 2012.</span><span class="sxs-lookup"><span data-stu-id="d073f-121">The Spark 2.0 notebooks use an additional data set for the classification task, the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="d073f-122">Se proporciona una descripción de los cuadernos y de los vínculos a estos en el archivo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) del repositorio de GitHub que los contiene.</span><span class="sxs-lookup"><span data-stu-id="d073f-122">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="d073f-123">No obstante, este código y los cuadernos vinculados son genéricos y deberían funcionar en cualquier clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-123">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="d073f-124">Los pasos de configuración y administración del clúster pueden ser ligeramente diferentes de los que se muestran aquí si no está usando Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d073f-124">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="d073f-125">Configuración: Ubicaciones de almacenamiento, bibliotecas y el contexto de Spark preestablecido</span><span class="sxs-lookup"><span data-stu-id="d073f-125">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="d073f-126">Spark puede leer y escribir en un blob de Azure Storage (WASB),</span><span class="sxs-lookup"><span data-stu-id="d073f-126">Spark is able to read and write to an Azure Storage Blob (WASB).</span></span> <span data-ttu-id="d073f-127">por lo que cualquiera de los datos existentes almacenados allí pueden procesarse mediante Spark y volver a almacenarse en WASB.</span><span class="sxs-lookup"><span data-stu-id="d073f-127">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="d073f-128">Para guardar modelos o archivos en WASB, la ruta de acceso debe especificarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="d073f-128">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="d073f-129">Se puede hacer referencia al contenedor predeterminado asociado al clúster de Spark con un ruta que comience con *"wasb//"*.</span><span class="sxs-lookup"><span data-stu-id="d073f-129">The default container attached to the Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="d073f-130">El ejemplo de código siguiente especifica la ubicación de los datos que se van a leer y la ruta de acceso del directorio de almacenamiento del modelo donde se guardará la salida del modelo.</span><span class="sxs-lookup"><span data-stu-id="d073f-130">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="d073f-131">Establecimiento de rutas de directorio para las ubicaciones de almacenamiento de WASB</span><span class="sxs-lookup"><span data-stu-id="d073f-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="d073f-132">Los modelos se guardan en: "wasb:///user/remoteuser/NYCTaxi/Models".</span><span class="sxs-lookup"><span data-stu-id="d073f-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="d073f-133">Si esta ruta de acceso no está configurada correctamente, no se cargará los modelos para su puntuación.</span><span class="sxs-lookup"><span data-stu-id="d073f-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="d073f-134">Los resultados puntuados se guardan en: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="d073f-134">The scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="d073f-135">Si la ruta de acceso a la carpeta es incorrecta, los resultados no se guardarán en esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="d073f-135">If the path to folder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="d073f-136">La ruta de acceso a las ubicaciones de los archivos se puede copiar y pegar en los marcadores de posición en este código, en la salida de la última celda del Notebook **machine-learning-data-science-spark-data-exploration-modeling.ipynb** .</span><span class="sxs-lookup"><span data-stu-id="d073f-136">The file path locations can be copied and pasted into the placeholders in this code from the output of the last cell of the **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="d073f-137">Este es el código para establecer rutas de acceso de directorio:</span><span class="sxs-lookup"><span data-stu-id="d073f-137">Here is the code to set directory paths:</span></span> 

    # LOCATION OF DATA TO BE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR THE MODELS TO BE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="d073f-138">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-138">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="d073f-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="d073f-140">Importación de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="d073f-140">Import libraries</span></span>
<span data-ttu-id="d073f-141">Establezca el contexto de Spark e importe las bibliotecas necesarias con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d073f-141">Set spark context and import necessary libraries with the following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="d073f-142">Contexto de Spark preestablecido e instrucciones mágicas de PySpark</span><span class="sxs-lookup"><span data-stu-id="d073f-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="d073f-143">Los kernels de PySpark que se proporcionan con cuadernos de Jupyter Notebook tienen contextos preestablecidos.</span><span class="sxs-lookup"><span data-stu-id="d073f-143">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="d073f-144">No es necesario establecer explícitamente los contextos de Spark o Hive antes de empezar a trabajar con la aplicación que se esté desarrollando.</span><span class="sxs-lookup"><span data-stu-id="d073f-144">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="d073f-145">Estos contextos están disponibles de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d073f-145">These are available for you by default.</span></span> <span data-ttu-id="d073f-146">Estos contextos son:</span><span class="sxs-lookup"><span data-stu-id="d073f-146">These contexts are:</span></span>

* <span data-ttu-id="d073f-147">sc: Para Spark</span><span class="sxs-lookup"><span data-stu-id="d073f-147">sc - for Spark</span></span> 
* <span data-ttu-id="d073f-148">sqlContext: Para Hive</span><span class="sxs-lookup"><span data-stu-id="d073f-148">sqlContext - for Hive</span></span>

<span data-ttu-id="d073f-149">El kernel PySpark proporciona algunas “instrucciones mágicas” predefinidas, que son comandos especiales que se pueden llamar con %%.</span><span class="sxs-lookup"><span data-stu-id="d073f-149">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="d073f-150">Hay dos comandos de este tipo que se utilizan en estos ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="d073f-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="d073f-151">**%%local** Especifica que el código de las líneas siguientes se ejecutará localmente.</span><span class="sxs-lookup"><span data-stu-id="d073f-151">**%%local** Specified that the code in subsequent lines is executed locally.</span></span> <span data-ttu-id="d073f-152">El código debe ser un código de Python válido.</span><span class="sxs-lookup"><span data-stu-id="d073f-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="d073f-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="d073f-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="d073f-154">Ejecuta una consulta de Hive en el sqlContext.</span><span class="sxs-lookup"><span data-stu-id="d073f-154">Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="d073f-155">Si se pasa el parámetro -o, el resultado de la consulta se conserva en el contexto %%local de Python como trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="d073f-155">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="d073f-156">Para obtener más información sobre los kernels de cuadernos de Jupyter Notebook y las instrucciones mágicas predefinidas llamadas con %% (por ejemplo, %%local) que proporcionan, consulte [Kernels disponibles para cuadernos de Jupyter con clústeres de Spark en HDInsight basados en Linux en HDInsight (versión preliminar)](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="d073f-156">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="d073f-157">Inserción de datos y creación de una trama de datos limpia</span><span class="sxs-lookup"><span data-stu-id="d073f-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="d073f-158">Esta sección contiene el código de una serie de tareas necesarias para incorporar los datos que se van a puntuar.</span><span class="sxs-lookup"><span data-stu-id="d073f-158">This section contains the code for a series of tasks required to ingest the data to be scored.</span></span> <span data-ttu-id="d073f-159">Lee una muestra del 0,1 % combinado del archivo de tarifas y carreras de taxi (almacenado como un archivo .tsv), da formato a los datos y, después, crea un marco de datos limpio.</span><span class="sxs-lookup"><span data-stu-id="d073f-159">Read in a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file), format the data, and then creates a clean data frame.</span></span>

<span data-ttu-id="d073f-160">Los archivos de tarifas y carreras de taxi se combinaron según el procedimiento descrito en el tema [Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md) .</span><span class="sxs-lookup"><span data-stu-id="d073f-160">The taxi trip and fare files were joined based on the procedure provided in the: [The Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="d073f-161">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-161">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-162">Time taken to execute above cell: 46.37 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-162">Time taken to execute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="d073f-163">Preparación de los datos para la puntuación en Spark</span><span class="sxs-lookup"><span data-stu-id="d073f-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="d073f-164">En esta sección se explica cómo indexar, codificar y ajustar la escala de características categóricas para prepararlas para su uso en algoritmos de aprendizaje supervisado de MLlib para clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="d073f-164">This section shows how to index, encode, and scale categorical features to prepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="d073f-165">Transformación de características: indexación y codificación de características categóricas para su incorporación en modelos para puntuación</span><span class="sxs-lookup"><span data-stu-id="d073f-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="d073f-166">En esta sección se muestra cómo indexar datos de categorías mediante `StringIndexer` y cómo codificar características con la entrada de `OneHotEncoder` en los modelos.</span><span class="sxs-lookup"><span data-stu-id="d073f-166">This section shows how to index categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into the models.</span></span>

<span data-ttu-id="d073f-167">[StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica una columna de cadena de etiquetas en una columna de índices de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d073f-167">The [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels to a column of label indices.</span></span> <span data-ttu-id="d073f-168">Los índices se ordenan por frecuencias de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d073f-168">The indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="d073f-169">[OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) asigna una columna de índices de etiqueta a una columna de vectores binarios, con un solo valor como máximo.</span><span class="sxs-lookup"><span data-stu-id="d073f-169">The [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="d073f-170">Esta codificación permite aplicar algoritmos que esperan características con valores continuos, como la regresión logística, a características categóricas.</span><span class="sxs-lookup"><span data-stu-id="d073f-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, to be applied to categorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is the cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="d073f-171">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-171">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-172">Time taken to execute above cell: 5.37 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-172">Time taken to execute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="d073f-173">Creación de objetos RDD con matrices de características para su entrada en los modelos</span><span class="sxs-lookup"><span data-stu-id="d073f-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="d073f-174">Esta sección contiene código que muestra cómo indexar datos de texto categóricos como un objeto RDD y cómo codificarlos como “uno de n” para poder usarlos para entrenar y probar la regresión logística de MLlib y otros modelos basados en árboles.</span><span class="sxs-lookup"><span data-stu-id="d073f-174">This section contains code that shows how to index categorical text data as an RDD object and one-hot encode it so it can be used to train and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="d073f-175">Los datos indexados se almacenan en objetos de [conjunto de datos distribuido resistente (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) .</span><span class="sxs-lookup"><span data-stu-id="d073f-175">The indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="d073f-176">Esta es la abstracción básica en Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-176">These are the basic abstraction in Spark.</span></span> <span data-ttu-id="d073f-177">Un objeto RDD representa una colección inmutable con particiones de los elementos con los que se puede trabajar en paralelo con Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="d073f-178">También contiene código que muestra cómo escalar datos con el elemento `StandardScalar` que proporciona MLlib para usarse en la regresión lineal con descenso de gradiente estocástico (SGD), un popular algoritmo para entrenar una amplia variedad de modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="d073f-178">It also contains code that shows how to scale data with the `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="d073f-179">[StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) se usa para escalar las características a la varianza de la unidad.</span><span class="sxs-lookup"><span data-stu-id="d073f-179">The [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used to scale the features to unit variance.</span></span> <span data-ttu-id="d073f-180">El ajuste de la escala de las características, también conocido como normalización de los datos, garantiza que características con valores situados muy en los extremos no tengan un peso excesivo en la función objetivo.</span><span class="sxs-lookup"><span data-stu-id="d073f-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="d073f-181">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-181">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-182">Time taken to execute above cell: 11.72 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-182">Time taken to execute above cell: 11.72 seconds</span></span>

## <a name="score-with-the-logistic-regression-model-and-save-output-to-blob"></a><span data-ttu-id="d073f-183">Puntuación con el modelo de regresión logística y guardado de la salida en un blob</span><span class="sxs-lookup"><span data-stu-id="d073f-183">Score with the Logistic Regression Model and save output to blob</span></span>
<span data-ttu-id="d073f-184">El código de esta sección muestra cómo cargar un modelo de regresión logística guardado en Azure Blob Storage, y cómo usarlo para predecir si se dio o no una propina en una carrera de taxi, puntuarlo con métricas de clasificación estándar y, después, guardar y trazar los resultados en un almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d073f-184">The code in this section shows how to load a Logistic Regression Model that has been saved in Azure blob storage and use it to predict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot the results to blob storage.</span></span> <span data-ttu-id="d073f-185">Los resultados puntuados se almacenan en objetos RDD.</span><span class="sxs-lookup"><span data-stu-id="d073f-185">The scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) TO BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="d073f-186">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-186">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-187">Time taken to execute above cell: 19.22 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-187">Time taken to execute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="d073f-188">Puntuación de un modelo de regresión lineal</span><span class="sxs-lookup"><span data-stu-id="d073f-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="d073f-189">Usamos [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) para entrenar un modelo de regresión lineal que usa descenso de gradiente estocástico (SGD) para predecir los importes de las propinas de forma óptima.</span><span class="sxs-lookup"><span data-stu-id="d073f-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) to train a linear regression model using Stochastic Gradient Descent (SGD) for optimization to predict the amount of tip paid.</span></span> 

<span data-ttu-id="d073f-190">El código de esta sección muestra cómo cargar un modelo de regresión lineal desde Almacenamiento de blobs de Azure, puntuarlo mediante variables con ajuste de la escala y, después, guardar los resultados en el blob.</span><span class="sxs-lookup"><span data-stu-id="d073f-190">The code in this section shows how to load a Linear Regression Model from Azure blob storage, score using scaled variables, and then save the results back to the blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="d073f-191">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-191">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-192">Time taken to execute above cell: 16.63 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-192">Time taken to execute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="d073f-193">Puntuación de los modelos de bosque aleatorio de clasificación y regresión</span><span class="sxs-lookup"><span data-stu-id="d073f-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="d073f-194">El código de esta sección muestra cómo cargar los modelos de bosque aleatorio de clasificación y regresión guardados en Almacenamiento de blobs de Azure, puntuar su rendimiento con medidas estándar de clasificación y regresión y, después, guardar los resultados en Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d073f-194">The code in this section shows how to load the saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span>

<span data-ttu-id="d073f-195">[bosques aleatorios](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="d073f-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="d073f-196">Combinan varios árboles de decisión para reducir el riesgo de sobreajuste.</span><span class="sxs-lookup"><span data-stu-id="d073f-196">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="d073f-197">Los bosques aleatorios pueden controlar características categóricas, amplían la configuración de clasificación multiclase, no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características.</span><span class="sxs-lookup"><span data-stu-id="d073f-197">Random forests can handle categorical features, extend to the multiclass classification setting, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="d073f-198">Los bosques aleatorios son uno de los modelos de aprendizaje automático de más éxito para clasificación y regresión.</span><span class="sxs-lookup"><span data-stu-id="d073f-198">Random forests are one of the most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="d073f-199">[spark.mllib](http://spark.apache.org/mllib/) admite bosques aleatorios para realizar operaciones de clasificación binaria y multiclase, y de regresión; las dos emplean características de categorías y continuas.</span><span class="sxs-lookup"><span data-stu-id="d073f-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="d073f-200">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-200">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-201">Time taken to execute above cell: 31.07 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-201">Time taken to execute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="d073f-202">Puntuación de modelos de árboles impulsados por gradiente de clasificación y regresión</span><span class="sxs-lookup"><span data-stu-id="d073f-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="d073f-203">El código de esta sección muestra cómo cargar los modelos de árboles impulsados por gradiente de clasificación y regresión guardados en Almacenamiento de blobs de Azure, puntuar su rendimiento con medidas estándar de clasificación y regresión y, después, guardar los resultados en Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d073f-203">The code in this section shows how to load classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span> 

<span data-ttu-id="d073f-204">**spark.mllib** admite GBT para realizar operaciones de clasificación binaria y de regresión; las dos emplean características de categorías y continuas.</span><span class="sxs-lookup"><span data-stu-id="d073f-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="d073f-205">[árboles impulsados por gradiente](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) son conjuntos de árboles de decisión.</span><span class="sxs-lookup"><span data-stu-id="d073f-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="d073f-206">Los GBT entrenan árboles de decisión de forma iterativa para minimizar una función de pérdida.</span><span class="sxs-lookup"><span data-stu-id="d073f-206">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="d073f-207">Los GBT pueden controlar características categóricas, no requieren ajustar la escala de las características y pueden capturar errores de alineación e interacciones de las características.</span><span class="sxs-lookup"><span data-stu-id="d073f-207">GBTs can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="d073f-208">También se pueden usar en una configuración de clasificación multiclase.</span><span class="sxs-lookup"><span data-stu-id="d073f-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    #LOAD AND SCORE THE MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="d073f-209">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-209">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-210">Time taken to execute above cell: 14.6 seconds</span><span class="sxs-lookup"><span data-stu-id="d073f-210">Time taken to execute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="d073f-211">Limpieza de objetos de la memoria e impresión de las ubicaciones de los archivos puntuados</span><span class="sxs-lookup"><span data-stu-id="d073f-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH TO SCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="d073f-212">**SALIDA:**</span><span class="sxs-lookup"><span data-stu-id="d073f-212">**OUTPUT:**</span></span>

<span data-ttu-id="d073f-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="d073f-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="d073f-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="d073f-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="d073f-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="d073f-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="d073f-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="d073f-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="d073f-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="d073f-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="d073f-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="d073f-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="d073f-219">Uso de modelos de Spark mediante una interfaz web</span><span class="sxs-lookup"><span data-stu-id="d073f-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="d073f-220">Spark proporciona un mecanismo para el envío remoto de trabajos por lotes o consultas interactivas mediante una interfaz REST con un componente llamado Livy.</span><span class="sxs-lookup"><span data-stu-id="d073f-220">Spark provides a mechanism to remotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="d073f-221">Livy está habilitado de forma predeterminada en el clúster de Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d073f-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="d073f-222">Para más información, vea [Envío de trabajos de Spark de forma remota mediante Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="d073f-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="d073f-223">Puede usar Livy para enviar de forma remota un trabajo que puntúa por lotes un archivo almacenado en un blob de Azure y, después, escribe los resultados en otro blob.</span><span class="sxs-lookup"><span data-stu-id="d073f-223">You can use Livy to remotely submit a job that batch scores a file that is stored in an Azure blob and then writes the results to another blob.</span></span> <span data-ttu-id="d073f-224">Para ello, cargue el script de Python desde </span><span class="sxs-lookup"><span data-stu-id="d073f-224">To do this, you upload the Python script from</span></span>  
<span data-ttu-id="d073f-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) en el blob del clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) to the blob of the Spark cluster.</span></span> <span data-ttu-id="d073f-226">Puede usar una herramienta como el **Explorador de Microsoft Azure Storage** o **AzCopy** para copiar el script en el blob del clúster.</span><span class="sxs-lookup"><span data-stu-id="d073f-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** to copy the script to the cluster blob.</span></span> <span data-ttu-id="d073f-227">En este caso, se carga el script en ***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="d073f-227">In our case we uploaded the script to ***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="d073f-228">Las claves de acceso que necesita se encuentran en el portal de la cuenta de almacenamiento asociada con el clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-228">The access keys that you need can be found on the portal for the storage account associated with the Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="d073f-229">Una vez cargado en esta ubicación, el script se ejecutará dentro del clúster de Spark en un contexto distribuido.</span><span class="sxs-lookup"><span data-stu-id="d073f-229">Once uploaded to this location, this script runs within the Spark cluster in a distributed context.</span></span> <span data-ttu-id="d073f-230">Carga el modelo y ejecuta predicciones en los archivos de entrada basándose en el modelo.</span><span class="sxs-lookup"><span data-stu-id="d073f-230">It loads the model and runs predictions on input files based on the model.</span></span>  

<span data-ttu-id="d073f-231">Para invocar este script de forma remota con una sencilla solicitud HTTPS/REST en Livy.</span><span class="sxs-lookup"><span data-stu-id="d073f-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="d073f-232">Este es un comando de CURL para construir la solicitud HTTP para invocar el script de Python de forma remota.</span><span class="sxs-lookup"><span data-stu-id="d073f-232">Here is a curl command to construct the HTTP request to invoke the Python script remotely.</span></span> <span data-ttu-id="d073f-233">Reemplace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME por los valores adecuados para su clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="d073f-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with the appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND TO INVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="d073f-234">Puede usar cualquier lenguaje en el sistema remoto para invocar el trabajo de Spark a través de Livy con una sencilla llamada HTTPS con autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="d073f-234">You can use any language on the remote system to invoke the Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="d073f-235">Sería conveniente usar la biblioteca de solicitudes de Python para realizar esta llamada HTTP, pero actualmente no está instalada de forma predeterminada en Funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d073f-235">It would be convenient to use the Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="d073f-236">Por ese motivo se usan bibliotecas HTTP más antiguas.</span><span class="sxs-lookup"><span data-stu-id="d073f-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="d073f-237">Este es el código de Python para la llamada HTTP:</span><span class="sxs-lookup"><span data-stu-id="d073f-237">Here is the Python code for the HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF THE REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY THE PYTHON SCRIPT TO RUN ON THE SPARK CLUSTER
    # IN THE FILE PARAMETER OF THE JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="d073f-238">También puede agregar este código de Python a [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) para desencadenar el envío de un trabajo de Spark que puntúa un blob en función de diversos eventos, como un temporizador o la creación o actualización de un blob.</span><span class="sxs-lookup"><span data-stu-id="d073f-238">You can also add this Python code to [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) to trigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="d073f-239">Si prefiere usar un cliente sin código, use [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) para invocar la puntuación por lotes de Spark; para ello, defina una acción HTTP en el **Diseñador de Logic Apps** y establezca sus parámetros.</span><span class="sxs-lookup"><span data-stu-id="d073f-239">If you prefer a code free client experience, use the [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) to invoke the Spark batch scoring by defining an HTTP action on the **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="d073f-240">En Azure Portal, cree una nueva aplicación lógica seleccionando **+Nuevo** -> **Web y móvil** -> **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="d073f-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="d073f-241">Escriba el nombre de la aplicación lógica y del plan de App Service para que aparezca el **Diseñador de aplicaciones lógicas**.</span><span class="sxs-lookup"><span data-stu-id="d073f-241">To bring up the **Logic Apps Designer**, enter the name of the Logic App and App Service Plan.</span></span>
* <span data-ttu-id="d073f-242">Seleccione una acción HTTP y especifique los parámetros mostrados en la ilustración siguiente:</span><span class="sxs-lookup"><span data-stu-id="d073f-242">Select an HTTP action and enter the parameters shown in the following figure:</span></span>

![Diseñador de Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="d073f-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d073f-244">What's next?</span></span>
<span data-ttu-id="d073f-245">**Validación cruzada y barrido de hiperparámetros**: Consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.</span><span class="sxs-lookup"><span data-stu-id="d073f-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

