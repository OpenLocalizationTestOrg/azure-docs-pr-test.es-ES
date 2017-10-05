---
title: "Compilación de aplicaciones de aprendizaje automático de Apache Spark en Azure HDInsight | Microsoft Docs"
description: "En este artículo se muestran instrucciones paso a paso sobre cómo compilar aplicaciones de aprendizaje automático de Apache Spark en clústeres Spark de HDInsight utilizando Jupyter Notebook."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="e2461-103">Compilación de aplicaciones de aprendizaje automático de Apache Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2461-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="e2461-104">Obtenga información sobre cómo compilar una aplicación de aprendizaje automático con un clúster Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2461-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="e2461-105">En este artículo se muestra cómo usar el cuaderno de Jupyter Notebook disponible con el clúster para compilar y probar esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2461-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="e2461-106">La aplicación usa los datos de ejemplo de HVAC.csv, que está disponible en todos los clústeres de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e2461-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="e2461-107">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="e2461-107">**Prerequisites:**</span></span>

<span data-ttu-id="e2461-108">Debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2461-108">You must have the following:</span></span>

* <span data-ttu-id="e2461-109">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2461-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e2461-110">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e2461-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="e2461-111"><a name="data"></a>Comprensión del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="e2461-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="e2461-112">Antes de empezar a compilar la aplicación, trataremos de comprender la estructura de los datos para los que creamos la aplicación y el tipo de análisis que se realizará en ellos.</span><span class="sxs-lookup"><span data-stu-id="e2461-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="e2461-113">En este artículo, usamos el archivo de datos **HVAC.csv** de ejemplo que está disponible en la cuenta de Azure Storage que ha asociado con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2461-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="e2461-114">Dentro de la cuenta de almacenamiento, el archivo se encuentra en **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="e2461-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="e2461-115">Descargue y abra el archivo CSV para hacerse una idea de cuáles son los datos.</span><span class="sxs-lookup"><span data-stu-id="e2461-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="e2461-116">![Instantánea de datos usados para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Instantánea de datos usados para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="e2461-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="e2461-117">Los datos muestran la temperatura objetivo y la temperatura real de un edificio con sistemas HVAC instalados.</span><span class="sxs-lookup"><span data-stu-id="e2461-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="e2461-118">Supongamos que la columna **System** representa el identificador del sistema y la columna **SystemAge**, el número de años que lleva el sistema HVAC instalado en el edificio.</span><span class="sxs-lookup"><span data-stu-id="e2461-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="e2461-119">Estos datos se usarán para predecir si un edificio será más cálido o frío en función de la temperatura objetivo, dados un identificador del sistema y la antigüedad del sistema.</span><span class="sxs-lookup"><span data-stu-id="e2461-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="e2461-120"><a name="app"></a>Escritura de una aplicación de aprendizaje automático de Spark mediante Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="e2461-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="e2461-121">En esta aplicación se usa una canalización Spark ML para realizar una clasificación de documentos.</span><span class="sxs-lookup"><span data-stu-id="e2461-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="e2461-122">En la canalización, se divide el documento en palabras, se convierten las palabras en un vector numérico de característica y finalmente se genera un modelo de predicción que use los vectores de característica y las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="e2461-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="e2461-123">Realice los siguientes pasos para crear la aplicación:</span><span class="sxs-lookup"><span data-stu-id="e2461-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="e2461-124">Desde el [Portal de Azure](https://portal.azure.com/), en el panel de inicio, haga clic en el icono del clúster Spark (si lo ancló al panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="e2461-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="e2461-125">También puede navegar hasta el clúster en **Examinar todo** > **Clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e2461-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="e2461-126">En la hoja del clúster Spark, haga clic en **Panel de clúster** y, luego, en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="e2461-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="e2461-127">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="e2461-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e2461-128">También puede comunicarse con el equipo Jupyter Notebook en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="e2461-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="e2461-129">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="e2461-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="e2461-130">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="e2461-130">Create a new notebook.</span></span> <span data-ttu-id="e2461-131">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="e2461-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="e2461-132">![Creación de un cuaderno de Jupyter Notebook para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Creación de un cuaderno de Jupyter Notebook para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="e2461-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="e2461-133">Se crea y se abre un nuevo cuaderno con el nombre Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="e2461-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="e2461-134">Haga clic en el nombre del cuaderno en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="e2461-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="e2461-135">![Proporcione un nombre de cuaderno para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Proporcione un nombre de cuaderno para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="e2461-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="e2461-136">Dado que creó un cuaderno con el kernel PySpark, no necesitará crear ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="e2461-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="e2461-137">Los contextos Spark y Hive se crearán automáticamente al ejecutar la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="e2461-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="e2461-138">Puede empezar por importar los tipos que son necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="e2461-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="e2461-139">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="e2461-140">Ahora, debe cargar los datos (hvac.csv), analizarlos y usarlos para entrenar el modelo.</span><span class="sxs-lookup"><span data-stu-id="e2461-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="e2461-141">Para ello, se define una función que comprueba si la temperatura real del edificio es mayor que la temperatura objetivo.</span><span class="sxs-lookup"><span data-stu-id="e2461-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="e2461-142">Si la temperatura real es mayor, el edificio está cálido, lo que viene indicado por el valor **1.0**.</span><span class="sxs-lookup"><span data-stu-id="e2461-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="e2461-143">Si la temperatura real es menor, el edificio está frío, lo que se indica con el valor **0.0**.</span><span class="sxs-lookup"><span data-stu-id="e2461-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="e2461-144">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="e2461-145">Configure la canalización de aprendizaje automático de Spark, que consta de tres fases: tokenizer, hashingTF e lr.</span><span class="sxs-lookup"><span data-stu-id="e2461-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="e2461-146">Para más información sobre qué es una canalización y cómo funciona, vea <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Canalización de aprendizaje automático de Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="e2461-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="e2461-147">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="e2461-148">Ajuste la canalización al documento de formación.</span><span class="sxs-lookup"><span data-stu-id="e2461-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="e2461-149">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="e2461-150">Compruebe el documento de aprendizaje para controlar el progreso con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2461-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="e2461-151">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="e2461-152">Esto dará un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2461-152">This should give the output similar to the following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="e2461-153">Vuelva atrás y compruebe el resultado en el archivo CSV sin procesar.</span><span class="sxs-lookup"><span data-stu-id="e2461-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="e2461-154">Por ejemplo, la primera fila del archivo CSV tiene estos datos:</span><span class="sxs-lookup"><span data-stu-id="e2461-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="e2461-155">![Instantánea de datos de salida para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Instantánea de datos de salida para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="e2461-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="e2461-156">Observe que la temperatura real es menor que la temperatura objetivo, lo que indica que el edificio está frío.</span><span class="sxs-lookup"><span data-stu-id="e2461-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="e2461-157">Por lo tanto, en la salida de aprendizaje, el valor de **label** en la primera fila es **0.0**, lo que significa que la temperatura del edificio no es cálida.</span><span class="sxs-lookup"><span data-stu-id="e2461-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="e2461-158">Prepare un conjunto de datos con el que ejecutar el modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="e2461-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="e2461-159">Para ello, deberá pasar un identificador del sistema y la antigüedad del sistema (representados como **SystemInfo** en la salida de aprendizaje), y el modelo predirá si el edificio con ese identificador y esa antigüedad del sistema es más cálido (indicado por 1.0) o frío (indicado por 0.0).</span><span class="sxs-lookup"><span data-stu-id="e2461-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="e2461-160">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="e2461-161">Por último, realice predicciones basadas en los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="e2461-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="e2461-162">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e2461-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="e2461-163">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2461-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="e2461-164">En la primera fila de la predicción, puede ver que, en un sistema HVAC con el identificador 20 y una antigüedad de 25 años, el edificio tendrá una temperatura cálida (**prediction=1.0**).</span><span class="sxs-lookup"><span data-stu-id="e2461-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="e2461-165">El primer valor de DenseVector (0.49999) corresponde a la predicción 0.0 y el segundo, (0.5001), corresponde a la predicción 1.0.</span><span class="sxs-lookup"><span data-stu-id="e2461-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="e2461-166">En la salida, aunque el segundo valor solo es levemente superior, el modelo muestra **prediction=1.0**.</span><span class="sxs-lookup"><span data-stu-id="e2461-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="e2461-167">Cuando haya terminado de ejecutar la aplicación, debe cerrar el cuaderno para liberar los recursos.</span><span class="sxs-lookup"><span data-stu-id="e2461-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="e2461-168">Para ello, en el menú **Archivo** del cuaderno, haga clic en **Cerrar y detener**.</span><span class="sxs-lookup"><span data-stu-id="e2461-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="e2461-169">De esta manera se apagará y se cerrará el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="e2461-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="e2461-170"><a name="anaconda"></a>Uso de la biblioteca scikit-learn de Anaconda para el aprendizaje automático de Spark</span><span class="sxs-lookup"><span data-stu-id="e2461-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="e2461-171">Los clústeres Apache Spark en HDInsight incluyen bibliotecas de Anaconda,</span><span class="sxs-lookup"><span data-stu-id="e2461-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="e2461-172">Entre ellas, está la biblioteca **scikit-learn** para aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="e2461-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="e2461-173">La biblioteca también contiene diversos conjuntos de datos que puede usar para crear aplicaciones de ejemplo directamente a partir de un cuaderno de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e2461-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="e2461-174">Para ver ejemplos sobre el uso de la biblioteca scikit-learn, consulte [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="e2461-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="e2461-175"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e2461-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e2461-176">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e2461-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e2461-177">Escenarios</span><span class="sxs-lookup"><span data-stu-id="e2461-177">Scenarios</span></span>
* [<span data-ttu-id="e2461-178">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="e2461-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e2461-179">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="e2461-179">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e2461-180">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="e2461-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e2461-181">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2461-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e2461-182">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e2461-182">Create and run applications</span></span>
* [<span data-ttu-id="e2461-183">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="e2461-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e2461-184">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="e2461-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e2461-185">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="e2461-185">Tools and extensions</span></span>
* [<span data-ttu-id="e2461-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones Scala Spark)</span><span class="sxs-lookup"><span data-stu-id="e2461-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e2461-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="e2461-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e2461-188">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2461-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e2461-189">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2461-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e2461-190">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="e2461-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e2461-191">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e2461-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e2461-192">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="e2461-192">Manage resources</span></span>
* [<span data-ttu-id="e2461-193">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e2461-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e2461-194">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="e2461-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
