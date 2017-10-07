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
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Compilación de aplicaciones de aprendizaje automático de Apache Spark en Azure HDInsight

Obtenga información acerca de cómo toobuild clúster de una aplicación de aprendizaje de máquina de Apache Spark utilizando un Spark en HDInsight. Este artículo muestra cómo toouse Hola Jupyter notebook disponible con hello clúster toobuild y probar esta aplicación. aplicación Hello usa datos de HVAC.csv de ejemplo de Hola que está disponibles en todos los clústeres de forma predeterminada.

**Requisitos previos:**

Debe disponer de hello siguiente:

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Comprender el conjunto de datos de Hola
Antes de empezar a compilar la aplicación hello, permítanos comprender la estructura de Hola de datos de hello para el que creamos aplicación hello y tipo de Hola de análisis que se realizará en los datos de Hola. 

En este artículo, se utiliza el ejemplo de Hola a **HVAC.csv** archivo de datos que está disponible en la cuenta de almacenamiento de Azure que se asocie con clúster de HDInsight de Hola Hola. Dentro de la cuenta de almacenamiento de hello, archivo hello es en **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Descargue y abra tooget de archivo CSV de hello una instantánea de datos de Hola.  

![Instantánea de datos usados para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Instantánea de datos usados para el ejemplo de aprendizaje automático de Spark")

datos de Hello muestran temperatura de destino de Hola y Hola la temperatura real de un edificio que tenga sistemas HVAC instalados. Supongamos que hello **System** columna representa el identificador de sistema de Hola y Hola **SystemAge** columna representa el número de Hola de sistema de hello HVAC ha estado en el lugar en la creación de hello de años.

Usamos esta toopredict de datos si un edificio será aun más o colder basándose en temperatura de destino de hello, dado un identificador de sistema y la edad del sistema.

## <a name="app"></a>Escritura de una aplicación de aprendizaje automático de Spark mediante Spark MLlib
En esta aplicación se utiliza un tooperform de canalización de aprendizaje automático de Spark una clasificación de documento. En la canalización de hello, se divide documento hello en palabras, convertir palabras hello en un vector de característica numéricos y finalmente crear un modelo de predicción mediante etiquetas y vectores de característica de Hola. Realizar Hola tras la aplicación de pasos toocreate Hola.

1. De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.   
2. En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.
   
   > [!NOTE]
   > También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Cree un nuevo notebook. Haga clic en **Nuevo** y, luego, en **PySpark**.
   
    ![Creación de un cuaderno de Jupyter Notebook para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Creación de un cuaderno de Jupyter Notebook para el ejemplo de aprendizaje automático de Spark")
4. Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.
   
    ![Proporcione un nombre de cuaderno para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Proporcione un nombre de cuaderno para el ejemplo de aprendizaje automático de Spark")
5. Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente. contextos de Spark y Hive Hola se crearán automáticamente automáticamente cuando se ejecuta la primera celda de código de hello. Puede iniciar mediante la importación de tipos de Hola que son necesarios para este escenario. Pegue Hola siguiente fragmento de código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR**. 
   
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
6. Ahora debe cargar los datos de hello (hvac.csv), analizarlo y usar modelos de hello tootrain. Para ello, se define una función que comprueba si la temperatura real de hello de la generación de hello es mayor que la temperatura de destino de Hola. Si temperatura real de hello es mayor, creación de hello está activa, indicado por el valor de hello **1.0**. Si la temperatura real de hello es menor, creación de hello está frío, indicado por el valor de hello **0,0**. 
   
    Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.

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


1. Configurar la canalización de aprendizaje automático de hello Spark que consta de tres fases: tokenizer, hashingTF y lr. Para más información sobre qué es una canalización y cómo funciona, vea <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Canalización de aprendizaje automático de Spark</a>.
   
    Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Documento de entrenamiento de hello ajuste canalización toohello. Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.
   
        model = pipeline.fit(training)
3. Comprobar el progreso con la aplicación hello de hello entrenamiento documento toocheckpoint. Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.
   
        training.show()
   
    Debería producir similar toohello siguiente de salida de hello:
   
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

    Volver atrás y comprobar la salida de hello en el archivo CSV sin procesar de hello. Por ejemplo, archivo de hello primera fila Hola CSV tiene estos datos:

    ![Instantánea de datos de salida para el ejemplo de aprendizaje automático de Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Instantánea de datos de salida para el ejemplo de aprendizaje automático de Spark")

    Observe cómo temperatura real de hello es menor que la temperatura de destino de hello sugiere la creación de hello está frío. Por lo tanto, en la salida de entrenamiento de hello, Hola valor para **etiqueta** Hola primera fila es **0,0**, lo que significa edificio hello no está activa.

1. Prepare un conjunto de datos toorun Hola entrenado en. toodo por lo tanto, se pasaría en un identificador del sistema y la edad de sistema (se denomina **SystemInfo** en la salida de entrenamiento de hello), y Hola modelo podría predecir si Hola compilar con dicha edad de identificador y el sistema de sistema podrían ser aun más (se indica con 1.0) o frío ( indica que esta 0.0).
   
   Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Por último, realizar predicciones en datos de prueba de saludo. Hola pegar siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Debería ver un siguiente toohello similar de salida:
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   Desde la primera fila de hello en la predicción de hello, puede ver que para un sistema HVAC con Id. de 20 y la edad de sistema de 25 años, creación de hello estará activa (**predicción = 1.0**). primer valor de Hola para DenseVector (0.49999) corresponde toohello predicción 0,0 y segundo valor de hello (0.5001) corresponde toohello predicción 1.0. En la salida de hello, aunque Hola segundo valor solo es ligeramente mayor, el modelo de hello muestra **predicción = 1.0**.
4. Una vez haya terminado de ejecutar la aplicación hello, debería recursos de hello toorelease de apagado Hola Bloc de notas. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**. Este se apagará y portátil de hello cerrar.

## <a name="anaconda"></a>Uso de la biblioteca scikit-learn de Anaconda para el aprendizaje automático de Spark
Los clústeres Apache Spark en HDInsight incluyen bibliotecas de Anaconda, Esto también incluye hello **scikit-aprender** biblioteca para el aprendizaje automático. biblioteca de Hello también incluye varios conjuntos de datos que puede utilizar aplicaciones de ejemplo de toobuild directamente desde Jupyter notebook. Para obtener ejemplos sobre el uso de Hola scikit: Obtenga información acerca de la biblioteca, consulte [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
