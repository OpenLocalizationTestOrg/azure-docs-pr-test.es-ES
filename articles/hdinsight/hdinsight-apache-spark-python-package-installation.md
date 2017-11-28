---
title: "acción de aaaScript: paquetes de instalar Python con Jupyter en HDInsight de Azure | Documentos de Microsoft"
description: "Instrucciones paso a paso sobre cómo toouse script acción tooconfigure Jupyter blocs de notas disponibles con HDInsight Spark clústeres paquetes de python externo toouse."
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="36210-103">Utilizar paquetes de Python externos de acción de secuencia de comandos tooinstall en blocs de notas de Jupyter en clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="36210-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36210-104">Uso de magic cell</span><span class="sxs-lookup"><span data-stu-id="36210-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="36210-105">Uso de acciones de script</span><span class="sxs-lookup"><span data-stu-id="36210-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="36210-106">Obtenga información acerca de cómo toouse acciones de Script tooconfigure un clúster de Apache Spark en HDInsight (Linux) toouse externa, Comunidad proporcionado **python** paquetes que no están incluyen de cuadro en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="36210-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="36210-107">También puede configurar Jupyter notebook mediante `%%configure` mágico toouse los paquetes externos.</span><span class="sxs-lookup"><span data-stu-id="36210-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="36210-108">Para obtener instrucciones, consulte [Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight Linux](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="36210-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="36210-109">Puede buscar hello [índice del paquete](https://pypi.python.org/pypi) para la lista completa de Hola de paquetes que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="36210-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="36210-110">También puede obtener una lista de paquetes disponibles de otras fuentes.</span><span class="sxs-lookup"><span data-stu-id="36210-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="36210-111">Por ejemplo, puede instalar paquetes que están disponibles a través de [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) o [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="36210-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="36210-112">En este artículo, aprenderá cómo hello tooinstall [TensorFlow](https://www.tensorflow.org/) empaquetar mediante Script Actoin en el clúster y usar mediante el Bloc de notas de hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="36210-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36210-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="36210-113">Prerequisites</span></span>
<span data-ttu-id="36210-114">Debe disponer de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="36210-114">You must have hello following:</span></span>

* <span data-ttu-id="36210-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="36210-115">An Azure subscription.</span></span> <span data-ttu-id="36210-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="36210-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="36210-117">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36210-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="36210-118">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="36210-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="36210-119">Si aún no tiene un clúster de Spark en HDInsight Linux, puede ejecutar acciones de script durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="36210-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="36210-120">Visite la documentación de hello en [cómo toouse custom script acciones](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="36210-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="36210-121">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="36210-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="36210-122">De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="36210-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="36210-123">También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="36210-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="36210-124">En la hoja de clúster de Spark hello, haga clic en **acciones de Script** en **uso**.</span><span class="sxs-lookup"><span data-stu-id="36210-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="36210-125">Ejecutar la acción personalizada de Hola instala TensorFlow en nodos principales de Hola y nodos de trabajador de Hola.</span><span class="sxs-lookup"><span data-stu-id="36210-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="36210-126">pueden hacer referencia a scripts de bash Hola desde: documentación de hello https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh visita en [cómo toouse custom script acciones](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="36210-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="36210-127">Hay dos python instalaciones en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="36210-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="36210-128">Spark usará la instalación de python Anaconda Hola ubicado en `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="36210-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="36210-129">Haga referencia a esa instalación en sus acciones personalizadas mediante `/usr/bin/anaconda/bin/pip` y `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="36210-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="36210-130">Abrir un cuaderno de Jupyter de PySpark</span><span class="sxs-lookup"><span data-stu-id="36210-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="36210-131">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="36210-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="36210-132">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="36210-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="36210-133">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="36210-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="36210-134">![Proporcione un nombre para el Bloc de notas de hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "proporcione un nombre para el Bloc de notas de Hola")</span><span class="sxs-lookup"><span data-stu-id="36210-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="36210-135">Ahora realizará la acción `import tensorflow` y ejecutará un ejemplo de saludo (Hola mundo).</span><span class="sxs-lookup"><span data-stu-id="36210-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="36210-136">Toocopy de código:</span><span class="sxs-lookup"><span data-stu-id="36210-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="36210-137">resultado de Hello tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="36210-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="36210-138">![Ejecución de código de TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Ejecución de código de TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="36210-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="36210-139"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="36210-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="36210-140">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="36210-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="36210-141">Escenarios</span><span class="sxs-lookup"><span data-stu-id="36210-141">Scenarios</span></span>
* [<span data-ttu-id="36210-142">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="36210-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="36210-143">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="36210-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="36210-144">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="36210-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="36210-145">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="36210-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="36210-146">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="36210-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="36210-147">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="36210-147">Create and run applications</span></span>
* [<span data-ttu-id="36210-148">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="36210-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="36210-149">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="36210-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="36210-150">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="36210-150">Tools and extensions</span></span>
* [<span data-ttu-id="36210-151">Uso de paquetes externos con cuadernos de Jupyter en clústeres de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="36210-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="36210-152">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="36210-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="36210-153">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="36210-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="36210-154">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="36210-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="36210-155">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="36210-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="36210-156">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="36210-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="36210-157">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="36210-157">Manage resources</span></span>
* [<span data-ttu-id="36210-158">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="36210-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="36210-159">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="36210-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
