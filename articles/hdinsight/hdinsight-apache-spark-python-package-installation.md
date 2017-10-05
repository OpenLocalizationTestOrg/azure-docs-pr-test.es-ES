---
title: "Acción de script: instalación de paquetes de Python con Jupyter en Azure HDInsight | Microsoft Docs"
description: "Instrucciones detalladas sobre cómo usar la acción de script para configurar cuadernos de Jupyter disponibles con clústeres de HDInsight Spark para usar paquetes externos de Python."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="428d9-103">Uso de acción de script para instalar paquetes externos de Python para cuadernos de Jupyter en clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="428d9-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="428d9-104">Uso de magic cell</span><span class="sxs-lookup"><span data-stu-id="428d9-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="428d9-105">Uso de acciones de script</span><span class="sxs-lookup"><span data-stu-id="428d9-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="428d9-106">Aprenda a usar acciones de script para configurar un clúster de Apache Spark en HDInsight (Linux) para el uso de paquetes de **Python** externos aportados por la comunidad que no están incluidos de serie en el clúster.</span><span class="sxs-lookup"><span data-stu-id="428d9-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="428d9-107">También puede configurar un cuaderno de Jupyter mediante `%%configure` para usar paquetes externos.</span><span class="sxs-lookup"><span data-stu-id="428d9-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="428d9-108">Para obtener instrucciones, consulte [Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight Linux](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="428d9-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="428d9-109">Puede buscar en el [índice de paquetes](https://pypi.python.org/pypi) la lista completa de paquetes que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="428d9-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="428d9-110">También puede obtener una lista de paquetes disponibles de otras fuentes.</span><span class="sxs-lookup"><span data-stu-id="428d9-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="428d9-111">Por ejemplo, puede instalar paquetes que están disponibles a través de [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) o [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="428d9-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="428d9-112">En este artículo, aprenderá a instalar el paquete [TensorFlow](https://www.tensorflow.org/) mediante una acción de script en su clúster y a usarlo mediante el cuaderno de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="428d9-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="428d9-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="428d9-113">Prerequisites</span></span>
<span data-ttu-id="428d9-114">Debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="428d9-114">You must have the following:</span></span>

* <span data-ttu-id="428d9-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="428d9-115">An Azure subscription.</span></span> <span data-ttu-id="428d9-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="428d9-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="428d9-117">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="428d9-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="428d9-118">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="428d9-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="428d9-119">Si aún no tiene un clúster de Spark en HDInsight Linux, puede ejecutar acciones de script durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="428d9-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="428d9-120">Consulte la documentación sobre [cómo usar acciones de script personalizadas](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="428d9-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="428d9-121">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="428d9-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="428d9-122">Desde el [Portal de Azure](https://portal.azure.com/), en el panel de inicio, haga clic en el icono del clúster Spark (si lo ancló al panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="428d9-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="428d9-123">También puede navegar hasta el clúster en **Examinar todo** > **Clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="428d9-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="428d9-124">En la hoja del clúster de Spark, haga clic en **Acciones de script** en **Uso**.</span><span class="sxs-lookup"><span data-stu-id="428d9-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="428d9-125">Ejecute la acción personalizada que instala TensorFlow en los nodos principales y los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="428d9-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="428d9-126">Se puede hacer referencia al script de Bash desde: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Consulte la documentación sobre [cómo usar acciones de script personalizadas](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="428d9-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="428d9-127">Hay dos instalaciones de Python en el clúster.</span><span class="sxs-lookup"><span data-stu-id="428d9-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="428d9-128">Spark usará la instalación de Python de Anaconda ubicada en `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="428d9-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="428d9-129">Haga referencia a esa instalación en sus acciones personalizadas mediante `/usr/bin/anaconda/bin/pip` y `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="428d9-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="428d9-130">Abrir un cuaderno de Jupyter de PySpark</span><span class="sxs-lookup"><span data-stu-id="428d9-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="428d9-131">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="428d9-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="428d9-132">Se crea y se abre un nuevo cuaderno con el nombre Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="428d9-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="428d9-133">Haga clic en el nombre del cuaderno en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="428d9-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="428d9-134">![Proporcionar un nombre para el cuaderno](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Proporcionar un nombre para el cuaderno")</span><span class="sxs-lookup"><span data-stu-id="428d9-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="428d9-135">Ahora realizará la acción `import tensorflow` y ejecutará un ejemplo de saludo (Hola mundo).</span><span class="sxs-lookup"><span data-stu-id="428d9-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="428d9-136">Código para copiar:</span><span class="sxs-lookup"><span data-stu-id="428d9-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="428d9-137">El resultado tendrá este aspecto:</span><span class="sxs-lookup"><span data-stu-id="428d9-137">The result will look like this:</span></span>
    
    <span data-ttu-id="428d9-138">![Ejecución de código de TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Ejecución de código de TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="428d9-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="428d9-139"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="428d9-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="428d9-140">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="428d9-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="428d9-141">Escenarios</span><span class="sxs-lookup"><span data-stu-id="428d9-141">Scenarios</span></span>
* [<span data-ttu-id="428d9-142">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="428d9-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="428d9-143">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="428d9-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="428d9-144">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="428d9-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="428d9-145">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="428d9-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="428d9-146">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="428d9-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="428d9-147">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="428d9-147">Create and run applications</span></span>
* [<span data-ttu-id="428d9-148">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="428d9-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="428d9-149">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="428d9-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="428d9-150">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="428d9-150">Tools and extensions</span></span>
* [<span data-ttu-id="428d9-151">Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="428d9-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="428d9-152">Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="428d9-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="428d9-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="428d9-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="428d9-154">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="428d9-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="428d9-155">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="428d9-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="428d9-156">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="428d9-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="428d9-157">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="428d9-157">Manage resources</span></span>
* [<span data-ttu-id="428d9-158">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="428d9-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="428d9-159">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="428d9-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
