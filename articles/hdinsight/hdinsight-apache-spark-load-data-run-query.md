---
title: "realizar consultas interactivas en un clúster de Azure HDInsight Spark aaaRun | Documentos de Microsoft"
description: "Inicio rápido de HDInsight Spark en forma de clúster toocreate un Apache Spark en HDInsight."
keywords: "inicio rápido para spark,spark interactivo,consulta interactiva,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="c6781-104">Ejecución de consultas interactivas en un clúster Spark de HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6781-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="c6781-105">En este artículo, use un Jupyter notebook toorun Spark SQL las consultas interactivas en un clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="c6781-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="c6781-106">Jupyter notebook es una aplicación basada en explorador que extiende Hola experiencia interactiva basada en consola toohello Web.</span><span class="sxs-lookup"><span data-stu-id="c6781-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="c6781-107">Para obtener más información, consulte [Bloc de notas de hello Jupyter](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="c6781-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="c6781-108">Para este tutorial, utilice hello **PySpark** kernel en hello Jupyter notebook toorun una consulta de Spark SQL interactiva.</span><span class="sxs-lookup"><span data-stu-id="c6781-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="c6781-109">Los notebooks de Jupyter en clústeres de HDInsight también admiten dos kernels: **PySpark3** y **Spark**.</span><span class="sxs-lookup"><span data-stu-id="c6781-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="c6781-110">Para obtener más información acerca de los kernels de Hola y Hola ventajas del uso de **PySpark**, consulte [clústeres de núcleos de Bloc de notas de uso Jupyter con Apache Spark en HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="c6781-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6781-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6781-111">Prerequisites</span></span>

* <span data-ttu-id="c6781-112">**Clúster Spark de Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c6781-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="c6781-113">Para obtener instrucciones, consulte [Creación de un clúster de Apache Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c6781-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="c6781-114">Crear Jupyter notebook toorun realizar consultas interactivas</span><span class="sxs-lookup"><span data-stu-id="c6781-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="c6781-115">consultas de toorun, utilizamos datos de ejemplo que está disponible en almacenamiento de hello asociada Hola clúster de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c6781-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="c6781-116">Sin embargo, primero debe cargar esos datos en Spark como una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="c6781-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="c6781-117">Una vez que tenga la trama de datos de hello, puede ejecutar consultas en ella con el Bloc de notas de hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c6781-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="c6781-118">En esta sección, puede aprender a:</span><span class="sxs-lookup"><span data-stu-id="c6781-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="c6781-119">Registrar un conjunto de datos de ejemplo como una trama de datos de Spark.</span><span class="sxs-lookup"><span data-stu-id="c6781-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="c6781-120">Ejecutar consultas en la trama de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6781-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="c6781-121">Abra hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c6781-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c6781-122">Si ha elegido el panel de toohello de toopin Hola clúster, haga clic en icono de clúster de Hola desde la hoja de clúster de hello panel toolaunch Hola.</span><span class="sxs-lookup"><span data-stu-id="c6781-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="c6781-123">Si no ancla panel Hola clúster toohello, desde el panel izquierdo de hello, haga clic en **clústeres de HDInsight**y, a continuación, haga clic en clúster de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="c6781-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="c6781-124">En **Quick links** (Vínculos rápidos), haga clic en **Cluster dashboards** (Paneles de clúster) y después en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="c6781-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="c6781-125">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="c6781-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="c6781-126">![Abrir Jupyter notebook toorun interactivo Spark SQL consulta](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "consultas Jupyter Abrir Bloc de notas toorun interactivo Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="c6781-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="c6781-127">También puede tener acceso a Jupyter notebook de hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="c6781-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c6781-128">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="c6781-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="c6781-129">Cree un cuaderno.</span><span class="sxs-lookup"><span data-stu-id="c6781-129">Create a notebook.</span></span> <span data-ttu-id="c6781-130">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="c6781-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="c6781-131">![Crear una consulta de Spark SQL interactiva de Jupyter notebook toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "crear una consulta Jupyter notebook toorun interactiva Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="c6781-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="c6781-132">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="c6781-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="c6781-133">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo si desea.</span><span class="sxs-lookup"><span data-stu-id="c6781-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="c6781-134">![Proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva de](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva desde")</span><span class="sxs-lookup"><span data-stu-id="c6781-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="c6781-135">Siguiente de Hola de pegar código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR** código de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="c6781-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="c6781-136">código de Hello importa tipos de hello necesarios en este escenario:</span><span class="sxs-lookup"><span data-stu-id="c6781-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="c6781-137">Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="c6781-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="c6781-138">contextos de Spark y Hive Hola se crean automáticamente cuando se ejecuta la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="c6781-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="c6781-139">![Estado de consulta Spark SQL interactiva](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Estado de consulta Spark SQL interactiva")</span><span class="sxs-lookup"><span data-stu-id="c6781-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="c6781-140">Cada vez que ejecute una consulta interactiva en Jupyter, el título de ventana de explorador web muestra un **(estado ocupado)** estado junto con el título de hello Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="c6781-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="c6781-141">También verá un toohello siguiente círculo sólido **PySpark** texto en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6781-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="c6781-142">Una vez completado el trabajo de hello, cambia el círculo hueco tooa.</span><span class="sxs-lookup"><span data-stu-id="c6781-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="c6781-143">Antes de cargar datos de hello en un clúster de Spark, nos permiten buscar una instantánea de él.</span><span class="sxs-lookup"><span data-stu-id="c6781-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="c6781-144">Hello datos de ejemplo utilizados en este tutorial están disponibles como un archivo CSV en todos los clústeres de HDInsight Spark en **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="c6781-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="c6781-145">datos de Hello captura las variaciones de temperatura de Hola de un edificio.</span><span class="sxs-lookup"><span data-stu-id="c6781-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="c6781-146">Presentamos hello en las primeras filas de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6781-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="c6781-147">![Instantánea de los datos de consulta SQL interactiva de Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Instantánea de los datos de consultas SQL interactivas de Spark")</span><span class="sxs-lookup"><span data-stu-id="c6781-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="c6781-148">Crear una trama de datos y una tabla temporal (**hvac**) ejecutando el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="c6781-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="c6781-149">Para este tutorial, no creamos todas las columnas de hello en tabla temporal de hello como toohello comparados columnas de datos sin procesar de CSV de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6781-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="c6781-150">Tras crea tabla hello, ejecutar consultas interactivas de datos de hello, utilice Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="c6781-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="c6781-151">Porque utiliza un núcleo de PySpark, ahora puede ejecutar directamente una consulta SQL interactiva en la tabla temporal de hello **hvac** que crean mediante hello `%%sql` magia.</span><span class="sxs-lookup"><span data-stu-id="c6781-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="c6781-152">Para obtener más información acerca de hello `%%sql` mágico y otros magics disponibles con kernel PySpark de hello, vea [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="c6781-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="c6781-153">Hola siguiendo la salida tabular se muestra de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c6781-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="c6781-154">![Tabla de salida de resultados de consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabla de salida de resultados de consultas Spark interactivas")</span><span class="sxs-lookup"><span data-stu-id="c6781-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="c6781-155">También puede ver los resultados de hello en otras visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c6781-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="c6781-156">Por ejemplo, un gráfico de áreas para hello misma salida sería Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="c6781-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="c6781-157">![Gráfico de área de resultados de consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gráfico de área de resultados de consultas Spark interactivas")</span><span class="sxs-lookup"><span data-stu-id="c6781-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="c6781-158">Apagar los recursos de clúster de hello Bloc de notas toorelease Hola después de que haya terminado de ejecutar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c6781-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="c6781-159">toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.</span><span class="sxs-lookup"><span data-stu-id="c6781-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="c6781-160">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c6781-160">Next step</span></span>

<span data-ttu-id="c6781-161">En este artículo se habrá aprendido cómo realizar consultas interactivas toorun en Spark con Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="c6781-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="c6781-162">Avanzar toohello siguiente artículo toosee cómo se pueden extraer datos de hello registrado en Spark en una herramienta de análisis de BI como Power BI y Tableau.</span><span class="sxs-lookup"><span data-stu-id="c6781-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="c6781-163">Spark BI mediante herramientas de visualización de datos con Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c6781-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




