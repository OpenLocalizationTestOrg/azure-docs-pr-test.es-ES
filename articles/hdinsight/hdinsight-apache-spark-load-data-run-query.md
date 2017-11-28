---
title: "Ejecución de consultas interactivas en un clúster de Azure HDInsight Spark | Microsoft Docs"
description: "Tutorial de inicio rápido para HDInsight Spark sobre cómo crear un clúster de Apache Spark en HDInsight."
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
ms.openlocfilehash: ada1c3d1482c68834dbbf5eabbd045a7e0c01f9f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="eb14c-104">Ejecución de consultas interactivas en un clúster Spark de HDInsight</span><span class="sxs-lookup"><span data-stu-id="eb14c-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="eb14c-105">En este artículo, utilice un notebook de Jupyter para ejecutar consultas SQL de Spark interactivas en un clúster Spark.</span><span class="sxs-lookup"><span data-stu-id="eb14c-105">In this article, you use a Jupyter notebook to run interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="eb14c-106">Notebook de Jupyter es una aplicación basada en explorador que extiende a la web la experiencia interactiva basada en la consola.</span><span class="sxs-lookup"><span data-stu-id="eb14c-106">Jupyter notebook is a browser-based application that extends the console-based interactive experience to the Web.</span></span> <span data-ttu-id="eb14c-107">Para más información, consulte [Notebook de Jupyter](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="eb14c-107">For more information, see [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="eb14c-108">En este tutorial, use el kernel **PySpark** en el notebook de Jupyter para ejecutar una consulta SQL de Spark interactiva.</span><span class="sxs-lookup"><span data-stu-id="eb14c-108">For this tutorial, you use the **PySpark** kernel in the Jupyter notebook to run an interactive Spark SQL query.</span></span> <span data-ttu-id="eb14c-109">Los notebooks de Jupyter en clústeres de HDInsight también admiten dos kernels: **PySpark3** y **Spark**.</span><span class="sxs-lookup"><span data-stu-id="eb14c-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="eb14c-110">Para más información sobre los kernels y las ventanas del uso de **PySpark**, consulte [Kernels para Jupyter Notebook en clústeres Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="eb14c-110">For more information about the kernels, and the benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb14c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eb14c-111">Prerequisites</span></span>

* <span data-ttu-id="eb14c-112">**Clúster Spark de Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eb14c-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="eb14c-113">Para obtener instrucciones, consulte [Creación de un clúster de Apache Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="eb14c-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a><span data-ttu-id="eb14c-114">Creación de un notebook de Jupyter para ejecutar consultas interactivas</span><span class="sxs-lookup"><span data-stu-id="eb14c-114">Create a Jupyter notebook to run interactive queries</span></span>

<span data-ttu-id="eb14c-115">Para ejecutar consultas, utilizamos los datos de ejemplo que están disponibles de forma predeterminada en el almacenamiento asociado al clúster.</span><span class="sxs-lookup"><span data-stu-id="eb14c-115">To run queries, we use sample data that is by default available in the storage associated with the cluster.</span></span> <span data-ttu-id="eb14c-116">Sin embargo, primero debe cargar esos datos en Spark como una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="eb14c-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="eb14c-117">Una vez que tenga la trama de datos, puede ejecutar consultas con ella usando el notebook de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eb14c-117">Once you have the dataframe, you can run queries on it using the Jupyter notebook.</span></span> <span data-ttu-id="eb14c-118">En esta sección, puede aprender a:</span><span class="sxs-lookup"><span data-stu-id="eb14c-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="eb14c-119">Registrar un conjunto de datos de ejemplo como una trama de datos de Spark.</span><span class="sxs-lookup"><span data-stu-id="eb14c-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="eb14c-120">Ejecutar consultas en la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="eb14c-120">Run queries on the dataframe.</span></span>

1. <span data-ttu-id="eb14c-121">Abra el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eb14c-121">Open the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="eb14c-122">Si ha elegido anclar el clúster al panel, haga clic en el icono de clúster desde el panel para abrir la hoja del clúster.</span><span class="sxs-lookup"><span data-stu-id="eb14c-122">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="eb14c-123">Si no ancló el clúster al panel, en el panel izquierdo, haga clic en **Clústeres de HDInsight** y luego haga clic en el clúster que ha creado.</span><span class="sxs-lookup"><span data-stu-id="eb14c-123">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="eb14c-124">En **Quick links** (Vínculos rápidos), haga clic en **Cluster dashboards** (Paneles de clúster) y después en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="eb14c-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="eb14c-125">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="eb14c-125">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="eb14c-126">![Abrir un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Abrir un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas")</span><span class="sxs-lookup"><span data-stu-id="eb14c-126">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="eb14c-127">También puede acceder al cuaderno de Jupyter en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="eb14c-127">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="eb14c-128">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="eb14c-128">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="eb14c-129">Cree un cuaderno.</span><span class="sxs-lookup"><span data-stu-id="eb14c-129">Create a notebook.</span></span> <span data-ttu-id="eb14c-130">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="eb14c-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="eb14c-131">![Crear un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Crear un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas")</span><span class="sxs-lookup"><span data-stu-id="eb14c-131">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="eb14c-132">Se crea y se abre un nuevo Notebook con el nombre Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="eb14c-132">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="eb14c-133">Haga clic en el nombre del Notebook en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="eb14c-133">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="eb14c-134">![Proporcionar un nombre para el cuaderno de Jupyter para ejecutar consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Proporcionar un nombre para el cuaderno de Jupyter ejecutar consultas Spark interactivas")</span><span class="sxs-lookup"><span data-stu-id="eb14c-134">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5. <span data-ttu-id="eb14c-135">Pegue el código siguiente en una celda vacía y presione **MAYÚS + ENTRAR** para ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="eb14c-135">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="eb14c-136">El código importa los tipos necesarios para este escenario:</span><span class="sxs-lookup"><span data-stu-id="eb14c-136">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="eb14c-137">Dado que creó un cuaderno con el kernel PySpark, no necesitará crear ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="eb14c-137">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="eb14c-138">Los contextos de Spark y Hive se crean automáticamente al ejecutar la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="eb14c-138">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="eb14c-139">![Estado de consulta Spark SQL interactiva](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Estado de consulta Spark SQL interactiva")</span><span class="sxs-lookup"><span data-stu-id="eb14c-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="eb14c-140">Cada vez que se ejecuta una consulta interactiva en Jupyter, el título de la ventana del explorador web muestra el estado **(Busy)** (Ocupado) junto con el título del cuaderno.</span><span class="sxs-lookup"><span data-stu-id="eb14c-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="eb14c-141">También verá un círculo sólido junto al texto **PySpark** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="eb14c-141">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="eb14c-142">Cuando finaliza el trabajo, cambia a un círculo vacío.</span><span class="sxs-lookup"><span data-stu-id="eb14c-142">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="eb14c-143">Antes de cargar los datos en un clúster de Spark, echemos un vistazo a una instantánea del mismo.</span><span class="sxs-lookup"><span data-stu-id="eb14c-143">Before you load the data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="eb14c-144">Los datos de ejemplo utilizados en este tutorial están disponibles como un archivo CSV en todos los clústeres Spark de HDInsight en **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="eb14c-144">The sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="eb14c-145">Los datos capturan las variaciones de temperatura de un edificio.</span><span class="sxs-lookup"><span data-stu-id="eb14c-145">The data captures the temperature variations of a building.</span></span> <span data-ttu-id="eb14c-146">Aquí están las primeras filas de los datos.</span><span class="sxs-lookup"><span data-stu-id="eb14c-146">Here are the first few rows of the data.</span></span>

    <span data-ttu-id="eb14c-147">![Instantánea de los datos de consulta SQL interactiva de Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Instantánea de los datos de consultas SQL interactivas de Spark")</span><span class="sxs-lookup"><span data-stu-id="eb14c-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="eb14c-148">Ejecute el código siguiente para crear una trama de datos y una tabla temporal (**hvac**).</span><span class="sxs-lookup"><span data-stu-id="eb14c-148">Create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> <span data-ttu-id="eb14c-149">En este tutorial, no creamos todas las columnas en la tabla temporal en comparación con las columnas de los datos CSV sin procesar.</span><span class="sxs-lookup"><span data-stu-id="eb14c-149">For this tutorial, we do not create all the columns in the temporary table as compared to the columns in the raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="eb14c-150">Una vez creada la tabla, ejecute la consulta interactiva en los datos con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="eb14c-150">Once the table is created, run interactive query on the data, use the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="eb14c-151">Como va a usar un kernel de PySpark, ahora puede ejecutar directamente una consulta SQL interactiva en la tabla temporal **hvac** que creó con la instrucción mágica `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="eb14c-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="eb14c-152">Para más información sobre la instrucción mágica `%%sql`, así como otras instrucciones mágicas disponibles con el kernel de PySpark, consulte [Kernels disponibles en Jupyter Notebook con clústeres de Spark en HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="eb14c-152">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="eb14c-153">De forma predeterminada, se muestra la siguiente salida tabular.</span><span class="sxs-lookup"><span data-stu-id="eb14c-153">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="eb14c-154">![Tabla de salida de resultados de consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabla de salida de resultados de consultas Spark interactivas")</span><span class="sxs-lookup"><span data-stu-id="eb14c-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="eb14c-155">También puede ver la salida en otras visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="eb14c-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="eb14c-156">Por ejemplo, un gráfico de área con la misma salida tendría el siguiente aspecto.</span><span class="sxs-lookup"><span data-stu-id="eb14c-156">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="eb14c-157">![Gráfico de área de resultados de consultas Spark interactivas](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gráfico de área de resultados de consultas Spark interactivas")</span><span class="sxs-lookup"><span data-stu-id="eb14c-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="eb14c-158">Cuando haya terminado de ejecutar la aplicación, cierre el Notebook para liberar los recursos del clúster.</span><span class="sxs-lookup"><span data-stu-id="eb14c-158">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="eb14c-159">Para ello, en el menú **Archivo** del cuaderno, haga clic en **Cerrar y detener**.</span><span class="sxs-lookup"><span data-stu-id="eb14c-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="eb14c-160">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="eb14c-160">Next step</span></span>

<span data-ttu-id="eb14c-161">En este artículo aprendió a ejecutar consultas interactivas en Spark con un notebook de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eb14c-161">In this article you learned how to run interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="eb14c-162">Continúe con el siguiente artículo para ver cómo se pueden extraer los datos registrados en Spark en una herramienta de análisis de BI, como Power BI y Tableau.</span><span class="sxs-lookup"><span data-stu-id="eb14c-162">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="eb14c-163">Spark BI mediante herramientas de visualización de datos con Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="eb14c-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




