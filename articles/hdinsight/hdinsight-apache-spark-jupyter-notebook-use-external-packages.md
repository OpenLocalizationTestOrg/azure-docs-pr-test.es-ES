---
title: Uso de paquetes personalizados de Maven con cuadernos de Jupyter Notebook en Spark en Azure HDInsight | Microsoft Docs
description: "Instrucciones detalladas sobre cómo configurar cuadernos de Jupyter Notebook disponibles con clústeres de HDInsight Spark para usar paquetes personalizados de Maven."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="8362e-103">Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8362e-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8362e-104">Uso de magic cell</span><span class="sxs-lookup"><span data-stu-id="8362e-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="8362e-105">Uso de acciones de script</span><span class="sxs-lookup"><span data-stu-id="8362e-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="8362e-106">Aprenda a configurar un cuaderno de Jupyter en clústeres de Apache Spark en HDInsight para usar paquetes **maven** externos aportados por la comunidad que no se incluyan listos para utilizarse en el clúster.</span><span class="sxs-lookup"><span data-stu-id="8362e-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="8362e-107">Puede buscar el [repositorio de Maven](http://search.maven.org/) para obtener una lista completa de los paquetes que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="8362e-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="8362e-108">También puede obtener una lista de paquetes disponibles de otras fuentes.</span><span class="sxs-lookup"><span data-stu-id="8362e-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="8362e-109">Por ejemplo, dispone de la lista completa de los paquetes externos aportados por la comunidad en [Spark Packages](http://spark-packages.org/)(Paquetes Spark).</span><span class="sxs-lookup"><span data-stu-id="8362e-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="8362e-110">En este artículo, aprenderá a utilizar el paquete [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) con el cuaderno de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="8362e-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="8362e-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8362e-111">Prerequisites</span></span>
<span data-ttu-id="8362e-112">Debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8362e-112">You must have the following:</span></span>

* <span data-ttu-id="8362e-113">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8362e-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8362e-114">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8362e-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="8362e-115">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="8362e-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="8362e-116">Desde el [Portal de Azure](https://portal.azure.com/), en el panel de inicio, haga clic en el icono del clúster Spark (si lo ancló al panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="8362e-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="8362e-117">También puede navegar hasta el clúster en **Examinar todo** > **Clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8362e-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="8362e-118">En la hoja del clúster Spark, haga clic en **Vínculos rápidos** y, luego, en la hoja **Panel de clúster**, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="8362e-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="8362e-119">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="8362e-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8362e-120">También puede comunicarse con el equipo Jupyter Notebook en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="8362e-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="8362e-121">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="8362e-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="8362e-122">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="8362e-122">Create a new notebook.</span></span> <span data-ttu-id="8362e-123">Haga clic en **Nuevo** y luego en **Spark**.</span><span class="sxs-lookup"><span data-stu-id="8362e-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="8362e-124">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="8362e-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="8362e-125">Se crea y se abre un nuevo cuaderno con el nombre Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="8362e-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="8362e-126">Haga clic en el nombre del cuaderno en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="8362e-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="8362e-127">![Proporcionar un nombre para el cuaderno](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Proporcionar un nombre para el cuaderno")</span><span class="sxs-lookup"><span data-stu-id="8362e-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="8362e-128">Utilizará la instrucción mágica `%%configure` para configurar el cuaderno para usar un paquete externo.</span><span class="sxs-lookup"><span data-stu-id="8362e-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="8362e-129">En los cuadernos que utilizan paquetes externos, asegúrese de invocar la instrucción mágica `%%configure` en la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="8362e-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="8362e-130">Esto garantiza que el kernel se configure para utilizar el paquete antes de iniciar la sesión.</span><span class="sxs-lookup"><span data-stu-id="8362e-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="8362e-131">Si se olvida de configurar el kernel en la primera celda, puede utilizar el parámetro `%%configure` con el parámetro `-f`, pero ello reiniciará la sesión y se perderá todo el trabajo.</span><span class="sxs-lookup"><span data-stu-id="8362e-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="8362e-132">Versión de HDInsight</span><span class="sxs-lookup"><span data-stu-id="8362e-132">HDInsight version</span></span> | <span data-ttu-id="8362e-133">Comando</span><span class="sxs-lookup"><span data-stu-id="8362e-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="8362e-134">Para HDInsight 3.3 y HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="8362e-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="8362e-135">Para HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="8362e-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="8362e-136">En el fragmento de código anterior, se esperan las coordenadas de Maven correspondientes al paquete externo de Maven Central Repository.</span><span class="sxs-lookup"><span data-stu-id="8362e-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="8362e-137">En este fragmento de código, `com.databricks:spark-csv_2.10:1.4.0` es la coordenada de Maven para el paquete **spark-csv** .</span><span class="sxs-lookup"><span data-stu-id="8362e-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="8362e-138">Le mostramos cómo crear las coordenadas de un paquete.</span><span class="sxs-lookup"><span data-stu-id="8362e-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="8362e-139">a.</span><span class="sxs-lookup"><span data-stu-id="8362e-139">a.</span></span> <span data-ttu-id="8362e-140">Busque el paquete en el repositorio de Maven.</span><span class="sxs-lookup"><span data-stu-id="8362e-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="8362e-141">En este tutorial, utilizamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="8362e-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="8362e-142">b.</span><span class="sxs-lookup"><span data-stu-id="8362e-142">b.</span></span> <span data-ttu-id="8362e-143">En el repositorio, recopile los valores de **GroupId**, **ArtifactId** y **Version**.</span><span class="sxs-lookup"><span data-stu-id="8362e-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="8362e-144">Asegúrese de que los valores recopilados coincidan con el clúster.</span><span class="sxs-lookup"><span data-stu-id="8362e-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="8362e-145">En este caso, estamos usando un paquete de Scala 2.10 y Spark 1.4.0, pero quizás tenga que seleccionar versiones diferentes para la versión de Scala o Spark concreta del clúster.</span><span class="sxs-lookup"><span data-stu-id="8362e-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="8362e-146">Puede averiguar la versión de Scala del clúster mediante la ejecución de `scala.util.Properties.versionString` en el kernel de Spark Jupyter o en el envío de Spark.</span><span class="sxs-lookup"><span data-stu-id="8362e-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="8362e-147">Puede averiguar la versión de Spark del clúster mediante la ejecución de `sc.version` en Jupyter Notebooks.</span><span class="sxs-lookup"><span data-stu-id="8362e-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="8362e-148">![Uso de paquetes externos con cuadernos de Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Uso de paquetes externos con cuadernos de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="8362e-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="8362e-149">c.</span><span class="sxs-lookup"><span data-stu-id="8362e-149">c.</span></span> <span data-ttu-id="8362e-150">Concatene los tres valores separados por dos puntos (**:**).</span><span class="sxs-lookup"><span data-stu-id="8362e-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="8362e-151">Ejecute la celda de código con la instrucción mágica `%%configure` .</span><span class="sxs-lookup"><span data-stu-id="8362e-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="8362e-152">De esta forma, se configurará la sesión de Livy subyacente para utilizar el paquete que facilitó.</span><span class="sxs-lookup"><span data-stu-id="8362e-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="8362e-153">En las siguientes celdas del cuaderno, ya podrá usar el paquete como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="8362e-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="8362e-154">A continuación, podrá ejecutar los fragmentos de código como se muestra seguidamente para ver los datos de la trama de datos que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8362e-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="8362e-155"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8362e-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8362e-156">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8362e-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8362e-157">Escenarios</span><span class="sxs-lookup"><span data-stu-id="8362e-157">Scenarios</span></span>
* [<span data-ttu-id="8362e-158">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="8362e-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8362e-159">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8362e-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8362e-160">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="8362e-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8362e-161">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="8362e-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8362e-162">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8362e-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8362e-163">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8362e-163">Create and run applications</span></span>
* [<span data-ttu-id="8362e-164">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="8362e-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8362e-165">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="8362e-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8362e-166">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="8362e-166">Tools and extensions</span></span>

* [<span data-ttu-id="8362e-167">Uso de paquetes externos de Python con cuadernos de Jupyter Notebook en clústeres de Apache Spark en HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="8362e-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="8362e-168">Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="8362e-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8362e-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="8362e-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8362e-170">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8362e-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8362e-171">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="8362e-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8362e-172">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8362e-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8362e-173">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="8362e-173">Manage resources</span></span>
* [<span data-ttu-id="8362e-174">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8362e-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8362e-175">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8362e-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

