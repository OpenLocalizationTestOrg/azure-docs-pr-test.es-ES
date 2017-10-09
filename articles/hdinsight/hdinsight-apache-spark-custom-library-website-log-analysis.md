---
title: registros del sitio Web de aaaAnalyze con bibliotecas de Python en Spark - Azure | Documentos de Microsoft
description: "Este bloc de notas, muestra cómo tooanalyze registrar datos de uso de una biblioteca personalizada con Spark en HDInsight de Azure."
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
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="4b582-103">Análisis de registros de sitios web mediante una biblioteca Python personalizada con un clúster Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b582-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="4b582-104">Este bloc de notas, muestra cómo tooanalyze registrar datos de uso de una biblioteca personalizada con Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b582-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="4b582-105">se utiliza la biblioteca personalizada Hello es una biblioteca de Python llama **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="4b582-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="4b582-106">Este tutorial también está disponible como un cuaderno de Jupyter en un clúster Spark (Linux) que se crea en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b582-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="4b582-107">experiencia de Bloc de notas de Hello le permite ejecutar fragmentos de código de Python Hola desde Bloc de notas de hello propio.</span><span class="sxs-lookup"><span data-stu-id="4b582-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="4b582-108">tutorial de hello tooperform desde dentro de un bloc de notas, cree un clúster de Spark, inicie Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), y, a continuación, ejecutar el Bloc de notas de hello **analizar registros con Spark mediante un library.ipynb personalizado** en hello  **PySpark** carpeta.</span><span class="sxs-lookup"><span data-stu-id="4b582-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="4b582-109">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="4b582-109">**Prerequisites:**</span></span>

<span data-ttu-id="4b582-110">Debe disponer de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b582-110">You must have hello following:</span></span>

* <span data-ttu-id="4b582-111">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b582-111">An Azure subscription.</span></span> <span data-ttu-id="4b582-112">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4b582-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="4b582-113">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b582-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4b582-114">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4b582-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="4b582-115">Almacenamiento de datos sin procesar como RDD</span><span class="sxs-lookup"><span data-stu-id="4b582-115">Save raw data as an RDD</span></span>
<span data-ttu-id="4b582-116">En esta sección, se utiliza hello [Jupyter](https://jupyter.org) Bloc de notas asociada a un clúster de Apache Spark en HDInsight toorun trabajos que procesan los datos de ejemplo sin formato y guardarla como una tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="4b582-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="4b582-117">datos de ejemplo de Hola están un archivo .csv (hvac.csv) disponible en todos los clústeres de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4b582-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="4b582-118">Una vez que los datos se guardan como una tabla de Hive, en la sección siguiente Hola se conectará toohello tabla de Hive con herramientas de BI como Power BI y Tableau.</span><span class="sxs-lookup"><span data-stu-id="4b582-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="4b582-119">De hello [portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="4b582-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="4b582-120">También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4b582-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="4b582-121">En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="4b582-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="4b582-122">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="4b582-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b582-123">También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="4b582-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="4b582-124">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="4b582-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="4b582-125">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="4b582-125">Create a new notebook.</span></span> <span data-ttu-id="4b582-126">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="4b582-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="4b582-127">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="4b582-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="4b582-128">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="4b582-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="4b582-129">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="4b582-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="4b582-130">![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "proporcione un nombre para el Bloc de notas de Hola")</span><span class="sxs-lookup"><span data-stu-id="4b582-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="4b582-131">Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="4b582-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="4b582-132">contextos de Spark y Hive Hola se crearán automáticamente automáticamente cuando se ejecuta la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="4b582-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="4b582-133">Puede iniciar mediante la importación de tipos de Hola que son necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="4b582-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="4b582-134">Pegue Hola siguiente fragmento de código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="4b582-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="4b582-135">Crear un diseño dirigido por responsabilidades mediante datos de registro de ejemplo de Hola ya están disponibles en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b582-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="4b582-136">Puede tener acceso a datos de hello en hello cuenta de almacenamiento predeterminado asociado con el clúster de hello en **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="4b582-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="4b582-137">Recuperar un tooverify de conjunto de registros de ejemplo que Hola paso anterior que se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4b582-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="4b582-138">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="4b582-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="4b582-139">Análisis de datos de registro mediante una biblioteca personalizada de Python</span><span class="sxs-lookup"><span data-stu-id="4b582-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="4b582-140">En la salida de hello anterior, primeras líneas del par Hola incluyen información de encabezado de Hola y cada línea restante coincide con esquema de hello descrito en ese encabezado.</span><span class="sxs-lookup"><span data-stu-id="4b582-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="4b582-141">Analizar dichos registros podría ser complicado.</span><span class="sxs-lookup"><span data-stu-id="4b582-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="4b582-142">Por lo tanto, utilizamos una biblioteca personalizada de Python (**iislogparser.py**) que ayuda a analizar estos registros de manera más fácil.</span><span class="sxs-lookup"><span data-stu-id="4b582-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="4b582-143">De forma predeterminada, esta biblioteca se incluye con el clúster Spark en HDInsight en **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="4b582-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="4b582-144">Sin embargo, esta biblioteca no está en hello `PYTHONPATH` por lo que no podemos usar mediante una instrucción de importación como `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="4b582-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="4b582-145">toouse esta biblioteca, debemos distribuirla nodos de trabajador de tooall Hola.</span><span class="sxs-lookup"><span data-stu-id="4b582-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="4b582-146">Ejecute hello siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="4b582-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="4b582-147">`iislogparser`Proporciona una función `parse_log_line` que devuelve `None` si una línea de registro es una fila de encabezado y devuelve una instancia de hello `LogLine` clase si encuentra una línea de registro.</span><span class="sxs-lookup"><span data-stu-id="4b582-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="4b582-148">Hola de uso `LogLine` clase tooextract Hola solo líneas de registro de hello RDD:</span><span class="sxs-lookup"><span data-stu-id="4b582-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="4b582-149">Recuperar un par de líneas de registro extraídos tooverify que Hola paso se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4b582-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="4b582-150">salida de Hello debe ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="4b582-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="4b582-151">Hola `LogLine` (clase), a su vez, tiene algunos métodos útiles, como `is_error()`, que se devuelve si una entrada del registro tiene un código de error.</span><span class="sxs-lookup"><span data-stu-id="4b582-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="4b582-152">Usar este número de hello toocompute de errores en las líneas de registro de hello extraído y, a continuación, todos los Hola errores tooa otro archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="4b582-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="4b582-153">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b582-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="4b582-154">También puede usar **Matplotlib** tooconstruct una visualización de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b582-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="4b582-155">Por ejemplo, si desea que la causa de hello tooisolate de solicitudes que se ejecutan durante mucho tiempo, podría desea toofind Hola archivos que toman Hola mayoría tooserve de tiempo promedio.</span><span class="sxs-lookup"><span data-stu-id="4b582-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="4b582-156">siguiente fragmento de Hello recupera Hola top 25 recursos que realizó una solicitud de mayoría tooserve de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4b582-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="4b582-157">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b582-157">You should see an output like hello following:</span></span>

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
5. <span data-ttu-id="4b582-158">También se puede presentar esta información en forma de Hola de trazado.</span><span class="sxs-lookup"><span data-stu-id="4b582-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="4b582-159">Como un primer paso toocreate un trazado, permítanos primero crea una tabla temporal **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="4b582-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="4b582-160">Hola Hola de grupos de tabla se registra por tiempo toosee si hubiera los picos de latencia inusuales en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="4b582-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="4b582-161">A continuación, puede ejecutar todos los registros de Hola de Hola después tooget de consultas SQL en Hola **AverageTime** tabla.</span><span class="sxs-lookup"><span data-stu-id="4b582-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="4b582-162">Hola `%%sql` mágico seguido `-o averagetime` garantiza que la salida de hello de consulta de Hola se conserva localmente en el servidor de Jupyter Hola (normalmente Hola nodo principal del clúster de hello).</span><span class="sxs-lookup"><span data-stu-id="4b582-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="4b582-163">salida de Hello se almacena como un [Pandas](http://pandas.pydata.org/) trama de datos con hello especificado nombre **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="4b582-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="4b582-164">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b582-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="4b582-165">![Salida de la consulta SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Salida de la consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="4b582-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="4b582-166">Para obtener más información acerca de hello `%%sql` mágico, vea [admiten parámetros con hello %% magia sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="4b582-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="4b582-167">Ahora puede usar Matplotlib, una biblioteca usa tooconstruct visualización de datos, toocreate un gráfico.</span><span class="sxs-lookup"><span data-stu-id="4b582-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="4b582-168">Porque se debe crear trazado de Hola de hello localmente conservan **averagetime** trama de datos, el fragmento de código de hello debe comienzan con hello `%%local` magia.</span><span class="sxs-lookup"><span data-stu-id="4b582-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="4b582-169">Esto garantiza que el código de hello se ejecuta localmente en el servidor de Jupyter Hola.</span><span class="sxs-lookup"><span data-stu-id="4b582-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="4b582-170">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b582-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="4b582-171">![Salida de Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Salida de Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="4b582-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="4b582-172">Una vez haya terminado de ejecutar la aplicación hello, debería recursos de hello toorelease de apagado Hola Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="4b582-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="4b582-173">toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.</span><span class="sxs-lookup"><span data-stu-id="4b582-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="4b582-174">Este se apagará y portátil de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="4b582-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="4b582-175"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="4b582-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4b582-176">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4b582-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4b582-177">Escenarios</span><span class="sxs-lookup"><span data-stu-id="4b582-177">Scenarios</span></span>
* [<span data-ttu-id="4b582-178">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="4b582-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4b582-179">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4b582-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4b582-180">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="4b582-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4b582-181">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="4b582-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4b582-182">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b582-182">Create and run applications</span></span>
* [<span data-ttu-id="4b582-183">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="4b582-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4b582-184">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="4b582-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4b582-185">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="4b582-185">Tools and extensions</span></span>
* [<span data-ttu-id="4b582-186">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="4b582-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4b582-187">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="4b582-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4b582-188">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b582-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4b582-189">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b582-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4b582-190">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="4b582-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4b582-191">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="4b582-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4b582-192">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="4b582-192">Manage resources</span></span>
* [<span data-ttu-id="4b582-193">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="4b582-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4b582-194">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="4b582-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
