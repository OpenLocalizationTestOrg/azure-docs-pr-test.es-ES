---
title: aaaUse paquetes personalizados de Maven con Jupyter de Spark en HDInsight de Azure | Documentos de Microsoft
description: "Instrucciones paso a paso sobre cómo tooconfigure Jupyter portátiles disponibles con HDInsight Spark clústeres toouse paquetes de Maven personalizados."
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
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="898f8-103">Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="898f8-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="898f8-104">Uso de magic cell</span><span class="sxs-lookup"><span data-stu-id="898f8-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="898f8-105">Uso de acciones de script</span><span class="sxs-lookup"><span data-stu-id="898f8-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="898f8-106">Obtenga información acerca de cómo tooconfigure Jupyter notebook en clústeres de Apache Spark en HDInsight toouse externa, Comunidad proporcionado **maven** paquetes que no están incluyen de cuadro en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="898f8-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="898f8-107">Puede buscar hello [repositorio Maven](http://search.maven.org/) para la lista completa de Hola de paquetes que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="898f8-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="898f8-108">También puede obtener una lista de paquetes disponibles de otras fuentes.</span><span class="sxs-lookup"><span data-stu-id="898f8-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="898f8-109">Por ejemplo, dispone de la lista completa de los paquetes externos aportados por la comunidad en [Spark Packages](http://spark-packages.org/)(Paquetes Spark).</span><span class="sxs-lookup"><span data-stu-id="898f8-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="898f8-110">En este artículo, aprenderá cómo hello toouse [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paquete con el Bloc de notas de hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="898f8-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="898f8-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="898f8-111">Prerequisites</span></span>
<span data-ttu-id="898f8-112">Debe disponer de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="898f8-112">You must have hello following:</span></span>

* <span data-ttu-id="898f8-113">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="898f8-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="898f8-114">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="898f8-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="898f8-115">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="898f8-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="898f8-116">De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="898f8-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="898f8-117">También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="898f8-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="898f8-118">En la hoja de clúster de Spark hello, haga clic en **vínculos rápidos**y, a continuación, desde hello **panel clúster** hoja, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="898f8-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="898f8-119">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="898f8-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="898f8-120">También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="898f8-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="898f8-121">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="898f8-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="898f8-122">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="898f8-122">Create a new notebook.</span></span> <span data-ttu-id="898f8-123">Haga clic en **Nuevo** y luego en **Spark**.</span><span class="sxs-lookup"><span data-stu-id="898f8-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="898f8-124">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="898f8-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="898f8-125">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="898f8-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="898f8-126">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="898f8-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="898f8-127">![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "proporcione un nombre para el Bloc de notas de Hola")</span><span class="sxs-lookup"><span data-stu-id="898f8-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="898f8-128">Va a usar hello `%%configure` tooconfigure mágico Hola Bloc de notas toouse un paquete externo.</span><span class="sxs-lookup"><span data-stu-id="898f8-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="898f8-129">En los equipos portátiles que utilizan los paquetes externos, asegúrese de que se llama a hello `%%configure` mágico en la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="898f8-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="898f8-130">Esto garantiza que kernel Hola paquete de hello toouse configurado antes de inicia sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="898f8-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="898f8-131">Si olvida tooconfigure kernel de hello en la primera celda de hello, puede usar hello `%%configure` con hello `-f` parámetro, pero que se reiniciará la sesión de Hola y se perderá todos los progreso.</span><span class="sxs-lookup"><span data-stu-id="898f8-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="898f8-132">Versión de HDInsight</span><span class="sxs-lookup"><span data-stu-id="898f8-132">HDInsight version</span></span> | <span data-ttu-id="898f8-133">Comando</span><span class="sxs-lookup"><span data-stu-id="898f8-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="898f8-134">Para HDInsight 3.3 y HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="898f8-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="898f8-135">Para HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="898f8-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="898f8-136">fragmento de código de Hello anterior espera hello maven coordenadas para el paquete externo de hello en el repositorio Central de Maven.</span><span class="sxs-lookup"><span data-stu-id="898f8-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="898f8-137">En este fragmento de código, `com.databricks:spark-csv_2.10:1.4.0` es hello maven coordenada para **spark-csv** paquete.</span><span class="sxs-lookup"><span data-stu-id="898f8-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="898f8-138">Le mostramos cómo construir Hola coordenadas para un paquete.</span><span class="sxs-lookup"><span data-stu-id="898f8-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="898f8-139">a.</span><span class="sxs-lookup"><span data-stu-id="898f8-139">a.</span></span> <span data-ttu-id="898f8-140">Busque el paquete de Hola Hola Maven repositorio.</span><span class="sxs-lookup"><span data-stu-id="898f8-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="898f8-141">En este tutorial, utilizamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="898f8-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="898f8-142">b.</span><span class="sxs-lookup"><span data-stu-id="898f8-142">b.</span></span> <span data-ttu-id="898f8-143">Repositorio de hello, recopilar los valores de hello de **GroupId**, **ArtifactId**, y **versión**.</span><span class="sxs-lookup"><span data-stu-id="898f8-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="898f8-144">Asegúrese de que haya recopilado de valores de hello coinciden con el clúster.</span><span class="sxs-lookup"><span data-stu-id="898f8-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="898f8-145">En este caso, estamos usando un Scala 2.10 y un paquete de Spark 1.4.0, pero puede tener tooselect distintas versiones para la versión adecuada de Scala o Spark hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="898f8-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="898f8-146">Puede averiguar Hola Scala versión en el clúster mediante la ejecución de `scala.util.Properties.versionString` en el kernel de Spark Jupyter Hola o en enviar Spark.</span><span class="sxs-lookup"><span data-stu-id="898f8-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="898f8-147">Puede averiguar Hola Spark versión en el clúster mediante la ejecución de `sc.version` en Jupyter blocs de notas.</span><span class="sxs-lookup"><span data-stu-id="898f8-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="898f8-148">![Uso de paquetes externos con cuadernos de Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Uso de paquetes externos con cuadernos de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="898f8-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="898f8-149">c.</span><span class="sxs-lookup"><span data-stu-id="898f8-149">c.</span></span> <span data-ttu-id="898f8-150">Concatenar valores de hello tres, separados por dos puntos (**:**).</span><span class="sxs-lookup"><span data-stu-id="898f8-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="898f8-151">Ejecutar la celda de código de hello con hello `%%configure` magia.</span><span class="sxs-lookup"><span data-stu-id="898f8-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="898f8-152">Esto configurará Hola subyacente Livio sesión toouse Hola paquete proporcionado.</span><span class="sxs-lookup"><span data-stu-id="898f8-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="898f8-153">En las celdas subsiguientes hello en el Bloc de notas de hello, ahora puede usar el paquete de hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="898f8-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="898f8-154">A continuación, puede ejecutar fragmentos de código de hello, como se muestra a continuación, tooview hello los datos de trama de datos de Hola crean en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="898f8-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="898f8-155"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="898f8-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="898f8-156">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="898f8-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="898f8-157">Escenarios</span><span class="sxs-lookup"><span data-stu-id="898f8-157">Scenarios</span></span>
* [<span data-ttu-id="898f8-158">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="898f8-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="898f8-159">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="898f8-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="898f8-160">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="898f8-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="898f8-161">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="898f8-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="898f8-162">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="898f8-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="898f8-163">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="898f8-163">Create and run applications</span></span>
* [<span data-ttu-id="898f8-164">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="898f8-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="898f8-165">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="898f8-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="898f8-166">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="898f8-166">Tools and extensions</span></span>

* [<span data-ttu-id="898f8-167">Uso de paquetes externos de Python con cuadernos de Jupyter Notebook en clústeres de Apache Spark en HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="898f8-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="898f8-168">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="898f8-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="898f8-169">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="898f8-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="898f8-170">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="898f8-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="898f8-171">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="898f8-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="898f8-172">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="898f8-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="898f8-173">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="898f8-173">Manage resources</span></span>
* [<span data-ttu-id="898f8-174">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="898f8-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="898f8-175">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="898f8-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

