---
title: aaaMicrosoft cognitivos Toolkit con Azure HDInsight Spark para aprendizaje profundo | Documentos de Microsoft
description: "Obtenga información acerca de cómo un entrenado cognitivos Kit de herramientas Microsoft profundo modelo de aprendizaje puede ser el conjunto de datos de tooa aplicada mediante Hola Spark Python API en un clúster de Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="b6ee4-103">Uso del modelo de aprendizaje profundo de Microsoft Cognitive Toolkit con un clúster de Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b6ee4-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="b6ee4-104">En este artículo, Hola lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="b6ee4-105">Ejecutar un tooinstall de secuencia de comandos personalizada cognitivos Kit de herramientas de Microsoft en un clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="b6ee4-106">Cargar un toosee Jupyter notebook toohello Spark clúster cómo tooapply un entrenado cognitivos Kit de herramientas Microsoft profundo aprendizaje toofiles de modelo en una cuenta de almacenamiento de blobs de Azure con hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="b6ee4-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6ee4-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b6ee4-107">Prerequisites</span></span>

* <span data-ttu-id="b6ee4-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-108">**An Azure subscription**.</span></span> <span data-ttu-id="b6ee4-109">Antes de comenzar este tutorial, debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b6ee4-110">Consulte la página [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="b6ee4-111">**Clúster de Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="b6ee4-112">Para este artículo, cree un clúster de Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="b6ee4-113">Para obtener instrucciones, consulte [Creación de un clúster de Apache Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="b6ee4-114">¿Cómo funciona esta solución?</span><span class="sxs-lookup"><span data-stu-id="b6ee4-114">How does this solution flow?</span></span>

<span data-ttu-id="b6ee4-115">Esta solución se divide entre este artículo y un cuaderno de Jupyter que se carga como parte de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="b6ee4-116">En este artículo, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b6ee4-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="b6ee4-117">Ejecutar una acción de secuencia de comandos en un clúster de HDInsight Spark tooinstall paquetes de Microsoft cognitivos Toolkit y Python.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="b6ee4-118">Cargue el Bloc de notas de Jupyter de Hola que se ejecuta la solución de hello toohello clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="b6ee4-119">Hola se tratan estos pasos restantes en el Bloc de notas de hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="b6ee4-120">Carga de imágenes de ejemplo en un conjunto de datos distribuido resistente o RDD de Spark</span><span class="sxs-lookup"><span data-stu-id="b6ee4-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="b6ee4-121">Carga de los módulos y definición de los valores preestablecidos</span><span class="sxs-lookup"><span data-stu-id="b6ee4-121">Load modules and define presets</span></span>
   - <span data-ttu-id="b6ee4-122">Descargar conjunto de datos de hello localmente en el clúster de Spark Hola</span><span class="sxs-lookup"><span data-stu-id="b6ee4-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="b6ee4-123">Convertir el conjunto de datos de hello en un diseño dirigido por responsabilidades</span><span class="sxs-lookup"><span data-stu-id="b6ee4-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="b6ee4-124">Imágenes de puntuación hello mediante un Kit de herramientas cognitivos entrenado</span><span class="sxs-lookup"><span data-stu-id="b6ee4-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="b6ee4-125">Descargar Hola entrenado Toolkit cognitivos modelo toohello Spark clúster</span><span class="sxs-lookup"><span data-stu-id="b6ee4-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="b6ee4-126">Definir toobe funciones utilizado por los nodos de trabajador</span><span class="sxs-lookup"><span data-stu-id="b6ee4-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="b6ee4-127">Imágenes de puntuación hello en los nodos de trabajador</span><span class="sxs-lookup"><span data-stu-id="b6ee4-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="b6ee4-128">Evaluación de la precisión del modelo</span><span class="sxs-lookup"><span data-stu-id="b6ee4-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="b6ee4-129">Instalación de Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="b6ee4-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="b6ee4-130">Puede instalar Microsoft Cognitive Toolkit en un clúster de Spark mediante la acción de scripts.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="b6ee4-131">Acción de secuencia de comandos usa componentes de tooinstall scripts personalizados en clúster de Hola que no están disponibles de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="b6ee4-132">Puede usar secuencias de comandos personalizadas Hola de hello Portal de Azure, mediante el SDK de HDInsight .NET o mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="b6ee4-133">También puede usar el Kit de herramientas de hello script tooinstall hello como parte de la creación del clúster, o después de que el clúster de hello está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="b6ee4-134">En este artículo, usamos hello tooinstall portal Hola toolkit, una vez creado el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="b6ee4-135">Para otra formas toorun hello secuencia de comandos personalizada, consulte [HDInsight personalizar clústeres mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="b6ee4-136">Uso de hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee4-136">Using hello Azure Portal</span></span>

<span data-ttu-id="b6ee4-137">Para obtener instrucciones sobre cómo toouse hello Azure Portal toorun secuencia de comandos de acción, vea [HDInsight personalizar clústeres mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="b6ee4-138">Asegúrese de que proporcionar Hola después entradas tooinstall cognitivos Kit de herramientas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="b6ee4-139">Proporcione un valor para el nombre de acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="b6ee4-140">Para el **URI de script de Bash**, escriba `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="b6ee4-141">Asegúrese de que ejecuta el script de Hola solo en hello nodos principal y de trabajo y desactive todos Hola otras casillas de verificación.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="b6ee4-142">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="b6ee4-143">Cargar hello Jupyter notebook tooAzure clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b6ee4-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="b6ee4-144">Hola toouse Microsoft cognitivos Toolkit con clúster de Azure HDInsight Spark hello, debe cargar el Bloc de notas de hello Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="b6ee4-145">Este cuaderno está disponible en GitHub en [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="b6ee4-146">Repositorio de GitHub de clon hello [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="b6ee4-147">Para obtener instrucciones tooclone, consulte [clonación de un repositorio](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="b6ee4-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="b6ee4-148">Desde el Portal de Azure hello, abrir la hoja de clúster de Spark de Hola que ya ha aprovisionado, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter notebook**.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="b6ee4-149">También puede iniciar el Bloc de notas de hello Jupyter yendo toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="b6ee4-150">Reemplace \<clustername > con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="b6ee4-151">En el Bloc de notas de Jupyter hello, haga clic en **cargar** en Hola esquina superior derecha y, a continuación, navegue ubicación toohello donde clonó repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="b6ee4-152">![Cargar Jupyter notebook tooAzure clúster de HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "cargar Jupyter notebook tooAzure clúster de HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="b6ee4-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="b6ee4-153">Haga clic en **Cargar** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="b6ee4-154">Después de carga el Bloc de notas de hello, haga clic en nombre Hola de Bloc de notas de Hola y, a continuación, siga las instrucciones de hello en Bloc de notas de hello propio acerca de cómo tooload Hola conjunto de datos y realizar el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ee4-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="b6ee4-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b6ee4-155">See also</span></span>
* [<span data-ttu-id="b6ee4-156">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee4-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b6ee4-157">Escenarios</span><span class="sxs-lookup"><span data-stu-id="b6ee4-157">Scenarios</span></span>
* [<span data-ttu-id="b6ee4-158">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="b6ee4-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b6ee4-159">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee4-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b6ee4-160">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="b6ee4-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b6ee4-161">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="b6ee4-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b6ee4-162">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ee4-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="b6ee4-163">Análisis de datos de telemetría de Application Insights con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ee4-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b6ee4-164">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b6ee4-164">Create and run applications</span></span>
* [<span data-ttu-id="b6ee4-165">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="b6ee4-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b6ee4-166">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="b6ee4-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b6ee4-167">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="b6ee4-167">Tools and extensions</span></span>
* [<span data-ttu-id="b6ee4-168">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="b6ee4-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b6ee4-169">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="b6ee4-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b6ee4-170">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ee4-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b6ee4-171">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ee4-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b6ee4-172">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="b6ee4-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b6ee4-173">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b6ee4-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b6ee4-174">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="b6ee4-174">Manage resources</span></span>
* [<span data-ttu-id="b6ee4-175">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee4-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b6ee4-176">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b6ee4-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
