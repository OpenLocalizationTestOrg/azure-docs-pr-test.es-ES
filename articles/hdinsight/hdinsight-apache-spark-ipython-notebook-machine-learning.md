---
title: "máquina de Apache Spark aaaBuild aprendizaje aplicaciones en HDInsight de Azure | Documentos de Microsoft"
description: "Instrucciones paso a paso en la aplicación en HDInsight Spark de aprendizaje automático de Apache Spark de toobuild clústeres utilizando Jupyter notebook"
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
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="afdb3-103">Compilación de aplicaciones de aprendizaje automático de Apache Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="afdb3-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="afdb3-104">Obtenga información acerca de cómo toobuild clúster de una aplicación de aprendizaje de máquina de Apache Spark utilizando un Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="afdb3-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="afdb3-105">Este artículo muestra cómo toouse Hola Jupyter notebook disponible con hello clúster toobuild y probar esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="afdb3-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="afdb3-106">aplicación Hello usa datos de HVAC.csv de ejemplo de Hola que está disponibles en todos los clústeres de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="afdb3-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="afdb3-107">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="afdb3-107">**Prerequisites:**</span></span>

<span data-ttu-id="afdb3-108">Debe disponer de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="afdb3-108">You must have hello following:</span></span>

* <span data-ttu-id="afdb3-109">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="afdb3-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="afdb3-110">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="afdb3-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="afdb3-111"><a name="data"></a>Comprender el conjunto de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="afdb3-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="afdb3-112">Antes de empezar a compilar la aplicación hello, permítanos comprender la estructura de Hola de datos de hello para el que creamos aplicación hello y tipo de Hola de análisis que se realizará en los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="afdb3-113">En este artículo, se utiliza el ejemplo de Hola a **HVAC.csv** archivo de datos que está disponible en la cuenta de almacenamiento de Azure que se asocie con clúster de HDInsight de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="afdb3-114">Dentro de la cuenta de almacenamiento de hello, archivo hello es en **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="afdb3-115">Descargue y abra tooget de archivo CSV de hello una instantánea de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="afdb3-116">![Instantánea de datos usados para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Instantánea de datos usados para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="afdb3-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="afdb3-117">datos de Hello muestran temperatura de destino de Hola y Hola la temperatura real de un edificio que tenga sistemas HVAC instalados.</span><span class="sxs-lookup"><span data-stu-id="afdb3-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="afdb3-118">Supongamos que hello **System** columna representa el identificador de sistema de Hola y Hola **SystemAge** columna representa el número de Hola de sistema de hello HVAC ha estado en el lugar en la creación de hello de años.</span><span class="sxs-lookup"><span data-stu-id="afdb3-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="afdb3-119">Usamos esta toopredict de datos si un edificio será aun más o colder basándose en temperatura de destino de hello, dado un identificador de sistema y la edad del sistema.</span><span class="sxs-lookup"><span data-stu-id="afdb3-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="afdb3-120"><a name="app"></a>Escritura de una aplicación de aprendizaje automático de Spark mediante Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="afdb3-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="afdb3-121">En esta aplicación se utiliza un tooperform de canalización de aprendizaje automático de Spark una clasificación de documento.</span><span class="sxs-lookup"><span data-stu-id="afdb3-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="afdb3-122">En la canalización de hello, se divide documento hello en palabras, convertir palabras hello en un vector de característica numéricos y finalmente crear un modelo de predicción mediante etiquetas y vectores de característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="afdb3-123">Realizar Hola tras la aplicación de pasos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="afdb3-124">De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="afdb3-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="afdb3-125">También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="afdb3-126">En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="afdb3-127">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="afdb3-128">También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="afdb3-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="afdb3-129">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="afdb3-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="afdb3-130">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="afdb3-130">Create a new notebook.</span></span> <span data-ttu-id="afdb3-131">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="afdb3-132">![Creación de un cuaderno de Jupyter Notebook para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Creación de un cuaderno de Jupyter Notebook para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="afdb3-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="afdb3-133">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="afdb3-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="afdb3-134">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="afdb3-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="afdb3-135">![Proporcione un nombre de cuaderno para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Proporcione un nombre de cuaderno para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="afdb3-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="afdb3-136">Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="afdb3-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="afdb3-137">contextos de Spark y Hive Hola se crearán automáticamente automáticamente cuando se ejecuta la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="afdb3-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="afdb3-138">Puede iniciar mediante la importación de tipos de Hola que son necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="afdb3-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="afdb3-139">Pegue Hola siguiente fragmento de código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="afdb3-140">Ahora debe cargar los datos de hello (hvac.csv), analizarlo y usar modelos de hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="afdb3-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="afdb3-141">Para ello, se define una función que comprueba si la temperatura real de hello de la generación de hello es mayor que la temperatura de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="afdb3-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="afdb3-142">Si temperatura real de hello es mayor, creación de hello está activa, indicado por el valor de hello **1.0**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="afdb3-143">Si la temperatura real de hello es menor, creación de hello está frío, indicado por el valor de hello **0,0**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="afdb3-144">Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="afdb3-145">Configurar la canalización de aprendizaje automático de hello Spark que consta de tres fases: tokenizer, hashingTF y lr.</span><span class="sxs-lookup"><span data-stu-id="afdb3-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="afdb3-146">Para más información sobre qué es una canalización y cómo funciona, vea <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Canalización de aprendizaje automático de Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="afdb3-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="afdb3-147">Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="afdb3-148">Documento de entrenamiento de hello ajuste canalización toohello.</span><span class="sxs-lookup"><span data-stu-id="afdb3-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="afdb3-149">Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="afdb3-150">Comprobar el progreso con la aplicación hello de hello entrenamiento documento toocheckpoint.</span><span class="sxs-lookup"><span data-stu-id="afdb3-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="afdb3-151">Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="afdb3-152">Debería producir similar toohello siguiente de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="afdb3-152">This should give hello output similar toohello following:</span></span>
   
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

    <span data-ttu-id="afdb3-153">Volver atrás y comprobar la salida de hello en el archivo CSV sin procesar de hello.</span><span class="sxs-lookup"><span data-stu-id="afdb3-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="afdb3-154">Por ejemplo, archivo de hello primera fila Hola CSV tiene estos datos:</span><span class="sxs-lookup"><span data-stu-id="afdb3-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="afdb3-155">![Instantánea de datos de salida para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Instantánea de datos de salida para el ejemplo de aprendizaje automático de Spark")</span><span class="sxs-lookup"><span data-stu-id="afdb3-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="afdb3-156">Observe cómo temperatura real de hello es menor que la temperatura de destino de hello sugiere la creación de hello está frío.</span><span class="sxs-lookup"><span data-stu-id="afdb3-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="afdb3-157">Por lo tanto, en la salida de entrenamiento de hello, Hola valor para **etiqueta** Hola primera fila es **0,0**, lo que significa edificio hello no está activa.</span><span class="sxs-lookup"><span data-stu-id="afdb3-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="afdb3-158">Prepare un conjunto de datos toorun Hola entrenado en.</span><span class="sxs-lookup"><span data-stu-id="afdb3-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="afdb3-159">toodo por lo tanto, se pasaría en un identificador del sistema y la edad de sistema (se denomina **SystemInfo** en la salida de entrenamiento de hello), y Hola modelo podría predecir si Hola compilar con dicha edad de identificador y el sistema de sistema podrían ser aun más (se indica con 1.0) o frío ( indica que esta 0.0).</span><span class="sxs-lookup"><span data-stu-id="afdb3-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="afdb3-160">Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="afdb3-161">Por último, realizar predicciones en datos de prueba de saludo.</span><span class="sxs-lookup"><span data-stu-id="afdb3-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="afdb3-162">Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="afdb3-163">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="afdb3-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="afdb3-164">Desde la primera fila de hello en la predicción de hello, puede ver que para un sistema HVAC con Id. de 20 y la edad de sistema de 25 años, creación de hello estará activa (**predicción = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="afdb3-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="afdb3-165">primer valor de Hola para DenseVector (0.49999) corresponde toohello predicción 0,0 y segundo valor de hello (0.5001) corresponde toohello predicción 1.0.</span><span class="sxs-lookup"><span data-stu-id="afdb3-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="afdb3-166">En la salida de hello, aunque Hola segundo valor solo es ligeramente mayor, el modelo de hello muestra **predicción = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="afdb3-167">Una vez haya terminado de ejecutar la aplicación hello, debería recursos de hello toorelease de apagado Hola Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="afdb3-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="afdb3-168">toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.</span><span class="sxs-lookup"><span data-stu-id="afdb3-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="afdb3-169">Este se apagará y portátil de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="afdb3-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="afdb3-170"><a name="anaconda"></a>Uso de la biblioteca scikit-learn de Anaconda para el aprendizaje automático de Spark</span><span class="sxs-lookup"><span data-stu-id="afdb3-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="afdb3-171">Los clústeres Apache Spark en HDInsight incluyen bibliotecas de Anaconda,</span><span class="sxs-lookup"><span data-stu-id="afdb3-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="afdb3-172">Esto también incluye hello **scikit-aprender** biblioteca para el aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="afdb3-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="afdb3-173">biblioteca de Hello también incluye varios conjuntos de datos que puede utilizar aplicaciones de ejemplo de toobuild directamente desde Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="afdb3-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="afdb3-174">Para obtener ejemplos sobre el uso de Hola scikit: Obtenga información acerca de la biblioteca, consulte [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="afdb3-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="afdb3-175"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="afdb3-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="afdb3-176">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="afdb3-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="afdb3-177">Escenarios</span><span class="sxs-lookup"><span data-stu-id="afdb3-177">Scenarios</span></span>
* [<span data-ttu-id="afdb3-178">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="afdb3-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="afdb3-179">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="afdb3-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="afdb3-180">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="afdb3-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="afdb3-181">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="afdb3-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="afdb3-182">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="afdb3-182">Create and run applications</span></span>
* [<span data-ttu-id="afdb3-183">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="afdb3-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="afdb3-184">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="afdb3-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="afdb3-185">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="afdb3-185">Tools and extensions</span></span>
* [<span data-ttu-id="afdb3-186">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones</span><span class="sxs-lookup"><span data-stu-id="afdb3-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="afdb3-187">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="afdb3-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="afdb3-188">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="afdb3-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="afdb3-189">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="afdb3-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="afdb3-190">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="afdb3-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="afdb3-191">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="afdb3-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="afdb3-192">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="afdb3-192">Manage resources</span></span>
* [<span data-ttu-id="afdb3-193">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="afdb3-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="afdb3-194">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="afdb3-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
