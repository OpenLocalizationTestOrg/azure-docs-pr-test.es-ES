---
title: "Análisis de registros de sitios web mediante bibliotecas Python en Spark - Azure | Microsoft Docs"
description: "En este cuaderno se muestra cómo analizar los datos de registro mediante una biblioteca personalizada con Spark en Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2a028beb1e9eae89d32238e61b6f67c4c059a94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="f9fc7-103">Análisis de registros de sitios web mediante una biblioteca Python personalizada con un clúster Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fc7-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="f9fc7-104">En este cuaderno se muestra cómo analizar los datos de registro mediante una biblioteca personalizada con Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="f9fc7-105">La biblioteca personalizada que usamos es una biblioteca de Python llamada **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="f9fc7-106">Este tutorial también está disponible como un cuaderno de Jupyter en un clúster Spark (Linux) que se crea en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="f9fc7-107">La experiencia del cuaderno le permite ejecutar los fragmentos de código de Python desde el propio Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="f9fc7-108">Para realizar el tutorial desde un cuaderno, cree un clúster Spark, inicie un cuaderno de Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`) y luego ejecute el cuaderno **Analyze logs with Spark using a custom library.ipynb** (Análisis de registros con Spark mediante una biblioteca personalizada.ipynb) en la carpeta **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="f9fc7-109">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="f9fc7-109">**Prerequisites:**</span></span>

<span data-ttu-id="f9fc7-110">Debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-110">You must have the following:</span></span>

* <span data-ttu-id="f9fc7-111">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-111">An Azure subscription.</span></span> <span data-ttu-id="f9fc7-112">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f9fc7-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f9fc7-113">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f9fc7-114">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f9fc7-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="f9fc7-115">Almacenamiento de datos sin procesar como RDD</span><span class="sxs-lookup"><span data-stu-id="f9fc7-115">Save raw data as an RDD</span></span>
<span data-ttu-id="f9fc7-116">En esta sección, usamos el cuaderno de [Jupyter](https://jupyter.org) asociado con un clúster Apache Spark en HDInsight para ejecutar trabajos que procesan los datos de ejemplo sin procesar y los guardan como una tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="f9fc7-117">Los datos de ejemplo corresponden a un archivo .csv (hvac.csv) que está disponible en todos los clústeres de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="f9fc7-118">Una vez que los datos se guardan como tabla de Hive, en la sección siguiente, nos conectaremos a la tabla de Hive mediante herramientas de BI como Power BI y Tableau.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="f9fc7-119">Desde [Azure Portal](https://portal.azure.com/), en el panel de inicio, haga clic en el icono del clúster Spark (si lo ancló al panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="f9fc7-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="f9fc7-120">También puede navegar hasta el clúster en **Examinar todo** > **Clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="f9fc7-121">En la hoja del clúster Spark, haga clic en **Panel de clúster** y, luego, en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="f9fc7-122">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f9fc7-123">También puede comunicarse con el equipo Jupyter Notebook en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="f9fc7-124">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="f9fc7-125">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-125">Create a new notebook.</span></span> <span data-ttu-id="f9fc7-126">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="f9fc7-127">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="f9fc7-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="f9fc7-128">Se crea y se abre un nuevo cuaderno con el nombre Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="f9fc7-129">Haga clic en el nombre del cuaderno en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="f9fc7-130">![Proporcionar un nombre para el cuaderno](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Proporcionar un nombre para el cuaderno")</span><span class="sxs-lookup"><span data-stu-id="f9fc7-130">![Provide a name for the notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="f9fc7-131">Dado que creó un cuaderno con el kernel PySpark, no necesitará crear ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="f9fc7-132">Los contextos Spark y Hive se crearán automáticamente al ejecutar la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="f9fc7-133">Puede empezar por importar los tipos que son necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="f9fc7-134">Pegue el siguiente fragmento de código en una celda vacía y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="f9fc7-135">Crear un RDD con los datos de registro de ejemplo ya disponibles en el clúster.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="f9fc7-136">Puede acceder a los datos de la cuenta de almacenamiento predeterminada asociada al clúster en **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="f9fc7-137">Recupere un registro de ejemplo establecido para comprobar que el paso anterior se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="f9fc7-138">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="f9fc7-139">Análisis de datos de registro mediante una biblioteca personalizada de Python</span><span class="sxs-lookup"><span data-stu-id="f9fc7-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="f9fc7-140">En la salida anterior, las primeras líneas del par incluyen la información de encabezado y cada línea restante coincide con el esquema descrito en ese encabezado.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="f9fc7-141">Analizar dichos registros podría ser complicado.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="f9fc7-142">Por lo tanto, utilizamos una biblioteca personalizada de Python (**iislogparser.py**) que ayuda a analizar estos registros de manera más fácil.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="f9fc7-143">De forma predeterminada, esta biblioteca se incluye con el clúster Spark en HDInsight en **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="f9fc7-144">Sin embargo, esta biblioteca no está en `PYTHONPATH`, por lo que no podemos usarla mediante una instrucción de importación como `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="f9fc7-145">Para usar esta biblioteca, debemos distribuirla a todos los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="f9fc7-146">Ejecute el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-146">Run the following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="f9fc7-147">`iislogparser` proporciona una función `parse_log_line` que devuelve `None` si una línea de registro es una fila de encabezado y devuelve una instancia de la clase `LogLine` si encuentra una línea de registro.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="f9fc7-148">Utilice la clase `LogLine` para extraer solo las líneas de registro desde el RDD:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="f9fc7-149">Recupere un par de líneas de registro extraídas para comprobar que el paso se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="f9fc7-150">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="f9fc7-151">La clase `LogLine`, a su vez, tiene algunos métodos útiles, como `is_error()`, que indica si una entrada de registro tiene un código de error.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="f9fc7-152">Use esto para calcular el número de errores en las líneas de registro extraídas y luego inicie todos los errores en un archivo diferente.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="f9fc7-153">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="f9fc7-154">También puede usar **Matplotlib** para generar una visualización de los datos.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="f9fc7-155">Por ejemplo, si desea aislar la causa de las solicitudes que se ejecutan durante mucho tiempo, puede encontrar los archivos que, como promedio, tarden más tiempo en atenderse.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="f9fc7-156">El fragmento de código siguiente recupera los 25 recursos principales que tardaron más tiempo en atender una solicitud.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="f9fc7-157">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-157">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="f9fc7-158">También puede presentar esta información en forma de gráfico.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="f9fc7-159">Como primer paso para crear un trazado, permítanos crear primero una tabla temporal **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="f9fc7-160">La tabla agrupa los registros por tiempo para ver si se produjeron picos de latencia inusuales en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="f9fc7-161">A continuación, puede ejecutar la siguiente consulta SQL para ubicar todos los registros en la tabla **AverageTime** .</span><span class="sxs-lookup"><span data-stu-id="f9fc7-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="f9fc7-162">La instrucción mágica `%%sql` seguida de `-o averagetime` garantiza que el resultado de la consulta persista localmente en el servidor de Jupyter (normalmente, el nodo principal del clúster).</span><span class="sxs-lookup"><span data-stu-id="f9fc7-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="f9fc7-163">El resultado se conserva como una trama de datos [Pandas](http://pandas.pydata.org/) con el nombre especificado **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="f9fc7-164">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-164">You should see an output like the following:</span></span>

   <span data-ttu-id="f9fc7-165">![Salida de la consulta SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Salida de la consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="f9fc7-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="f9fc7-166">Para obtener más información sobre la instrucción mágica `%%sql`, vea [Parámetros compatibles con la instrucción mágica %%sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="f9fc7-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="f9fc7-167">Ahora puede usar Matplotlib, una biblioteca que se usa para construir la visualización de datos, para crear un gráfico.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="f9fc7-168">Dado que el gráfico se debe crear a partir de la trama de datos **averagetime** persistente localmente, el fragmento de código debe comenzar con la función mágica `%%local`.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="f9fc7-169">Esto garantiza que el código se ejecuta localmente en el servidor de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="f9fc7-170">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9fc7-170">You should see an output like the following:</span></span>

   <span data-ttu-id="f9fc7-171">![Salida de Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Salida de Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="f9fc7-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="f9fc7-172">Cuando haya terminado de ejecutar la aplicación, debe cerrar el cuaderno para liberar los recursos.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="f9fc7-173">Para ello, en el menú **Archivo** del cuaderno, haga clic en **Cerrar y detener**.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="f9fc7-174">De esta manera se apagará y se cerrará el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="f9fc7-174">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="f9fc7-175"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f9fc7-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f9fc7-176">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f9fc7-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f9fc7-177">Escenarios</span><span class="sxs-lookup"><span data-stu-id="f9fc7-177">Scenarios</span></span>
* [<span data-ttu-id="f9fc7-178">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="f9fc7-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f9fc7-179">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f9fc7-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f9fc7-180">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="f9fc7-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f9fc7-181">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="f9fc7-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f9fc7-182">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f9fc7-182">Create and run applications</span></span>
* [<span data-ttu-id="f9fc7-183">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="f9fc7-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f9fc7-184">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="f9fc7-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f9fc7-185">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="f9fc7-185">Tools and extensions</span></span>
* [<span data-ttu-id="f9fc7-186">Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="f9fc7-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f9fc7-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="f9fc7-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f9fc7-188">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fc7-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f9fc7-189">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9fc7-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f9fc7-190">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="f9fc7-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f9fc7-191">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f9fc7-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f9fc7-192">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="f9fc7-192">Manage resources</span></span>
* [<span data-ttu-id="f9fc7-193">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="f9fc7-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f9fc7-194">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f9fc7-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
