---
title: "aaaInstall y el uso de clústeres de Giraph en Hadoop en HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toocustomize HDInsight con Giraph y cómo toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="66e19-103">Instalación y uso de Giraph en clústeres de HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="66e19-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="66e19-104">Obtenga información acerca de cómo toocustomize Windows en función de clúster de HDInsight con Giraph mediante la acción de secuencia de comandos y cómo toouse Giraph tooprocess a gran escala gráficos.</span><span class="sxs-lookup"><span data-stu-id="66e19-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="66e19-105">Para obtener información sobre el uso de Giraph con un clúster basado en Linux, consulte [Instalación de Giraph en clústeres Hadoop de HDinsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)</span><span class="sxs-lookup"><span data-stu-id="66e19-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66e19-106">Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="66e19-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="66e19-107">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="66e19-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="66e19-108">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="66e19-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="66e19-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="66e19-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="66e19-110">Para obtener información acerca de cómo tooinstall Giraph en un clúster de HDInsight basados en Linux, consulte [Giraph instalar en clústeres de Hadoop de HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="66e19-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="66e19-111">Puede instalar Giraph en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*.</span><span class="sxs-lookup"><span data-stu-id="66e19-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="66e19-112">Tooinstall de secuencia de comandos de ejemplo Giraph en un clúster de HDInsight está disponible en un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="66e19-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="66e19-113">script de ejemplo de Hola solo funciona con la versión de clúster de HDInsight 3.1.</span><span class="sxs-lookup"><span data-stu-id="66e19-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="66e19-114">Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="66e19-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="66e19-115">**Artículos relacionados**</span><span class="sxs-lookup"><span data-stu-id="66e19-115">**Related articles**</span></span>

* [<span data-ttu-id="66e19-116">Instalación de Giraph en clústeres de Hadoop de HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="66e19-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="66e19-117">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66e19-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="66e19-118">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="66e19-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="66e19-119">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="66e19-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="66e19-120">¿Qué es Giraph?</span><span class="sxs-lookup"><span data-stu-id="66e19-120">What is Giraph?</span></span>
<span data-ttu-id="66e19-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="66e19-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="66e19-122">Gráficos de modelar las relaciones entre objetos, como las conexiones de hello entre enrutadores de una red de gran tamaño como Hola Internet, o las relaciones entre las personas en las redes sociales (en ocasiones denominado tooas un gráfico sociales).</span><span class="sxs-lookup"><span data-stu-id="66e19-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="66e19-123">Procesamiento de gráficos le permite tooreason acerca de las relaciones de hello entre los objetos en un gráfico, como:</span><span class="sxs-lookup"><span data-stu-id="66e19-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="66e19-124">Identificar los posibles amigos según las relaciones actuales.</span><span class="sxs-lookup"><span data-stu-id="66e19-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="66e19-125">Identifica la ruta más corta de hello entre dos equipos en una red.</span><span class="sxs-lookup"><span data-stu-id="66e19-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="66e19-126">Calcular la clasificación de la página de Hola de páginas Web.</span><span class="sxs-lookup"><span data-stu-id="66e19-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="66e19-127">Instalación de Giraph mediante el portal</span><span class="sxs-lookup"><span data-stu-id="66e19-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="66e19-128">Empezar a crear un clúster mediante el uso de hello **creación personalizada** opción, como se describe en [Hadoop crear clústeres de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="66e19-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="66e19-129">En hello **acciones de Script** página del Asistente de hello, haga clic en **Agregar acción de secuencia de comandos** tooprovide detalles sobre la acción de secuencia de comandos de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="66e19-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="66e19-130">![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize de acción de secuencia de comandos de uso un clúster")</span><span class="sxs-lookup"><span data-stu-id="66e19-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="66e19-131">Propiedad</span><span class="sxs-lookup"><span data-stu-id="66e19-131">Property</span></span></th><th><span data-ttu-id="66e19-132">Valor</span><span class="sxs-lookup"><span data-stu-id="66e19-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="66e19-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="66e19-133">Name</span></span></td>
            <td><span data-ttu-id="66e19-134">Especifique un nombre para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-134">Specify a name for hello script action.</span></span> <span data-ttu-id="66e19-135">Por ejemplo, <b>Instalar Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="66e19-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="66e19-136">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="66e19-136">Script URI</span></span></td>
            <td><span data-ttu-id="66e19-137">Especificar una secuencia toohello de hello identificador uniforme de recursos (URI) que es invocado toocustomize Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="66e19-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="66e19-138">Por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="66e19-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="66e19-139">Tipo de nodo</span><span class="sxs-lookup"><span data-stu-id="66e19-139">Node Type</span></span></td>
            <td><span data-ttu-id="66e19-140">Especifique los nodos de hello en el que se ejecuta el script de personalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="66e19-141">Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.</span><span class="sxs-lookup"><span data-stu-id="66e19-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="66e19-142">parameters</span><span class="sxs-lookup"><span data-stu-id="66e19-142">Parameters</span></span></td>
            <td><span data-ttu-id="66e19-143">Especificar parámetros de hello, si así lo requiere el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="66e19-144">Hola script tooinstall Giraph no requiere ningún parámetro, por lo que puede dejar en blanco.</span><span class="sxs-lookup"><span data-stu-id="66e19-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="66e19-145">Puede agregar más de una secuencia de comandos acción tooinstall varios componentes en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="66e19-146">Después de haber agregado las secuencias de comandos de hello, haga clic en toostart de marca de verificación de hello crear clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="66e19-147">Uso de Giraph</span><span class="sxs-lookup"><span data-stu-id="66e19-147">Use Giraph</span></span>
<span data-ttu-id="66e19-148">Usamos hello SimpleShortestPathsComputation ejemplo toodemonstrate Hola basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementación para buscar la ruta de acceso más corta de hello entre los objetos de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="66e19-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="66e19-149">Usar hello siguiendo los pasos tooupload Hola ejemplo hello y datos de ejemplo jar, ejecute un trabajo mediante el uso de ejemplo de Hola a SimpleShortestPathsComputation y, a continuación, ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="66e19-150">Cargar un archivo de datos ejemplo tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="66e19-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="66e19-151">En la estación de trabajo local, cree un archivo nuevo llamado **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="66e19-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="66e19-152">Debe contener Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="66e19-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="66e19-153">Cargar hello tiny_graph.txt archivo toohello almacenamiento principal para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66e19-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="66e19-154">Para obtener instrucciones sobre cómo ver datos tooupload, [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="66e19-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="66e19-155">Estos datos describen una relación entre los objetos de un gráfico dirigido, con formato de hello [origen\_Id., origen\_valor, [[dest\_id], [borde\_valor],...]]. Cada línea representa una relación entre un objeto **source\_id** y uno más objetos **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="66e19-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="66e19-156">Hola **borde\_valor** (o peso) puede considerarse como la intensidad de Hola o distancia de conexión de hello entre **source_id** y **dest\_identificador**.</span><span class="sxs-lookup"><span data-stu-id="66e19-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="66e19-157">Dibujar, y con el valor de hello (o peso) como la distancia de hello entre objetos, Hola por encima de los datos podría ser similar a esto:</span><span class="sxs-lookup"><span data-stu-id="66e19-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="66e19-159">Ejecutar el ejemplo de Hola a SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="66e19-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="66e19-160">Usar hello después toorun cmdlets de PowerShell de Azure, hello (ejemplo) mediante el uso de archivo de hello tiny_graph.txt como entrada.</span><span class="sxs-lookup"><span data-stu-id="66e19-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="66e19-161">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="66e19-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="66e19-162">Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="66e19-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="66e19-163">Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="66e19-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="66e19-164">Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="66e19-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="66e19-165">Hola ejemplo anterior, reemplace **clustername** con el nombre de Hola de su clúster de HDInsight con Giraph instalado.</span><span class="sxs-lookup"><span data-stu-id="66e19-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="66e19-166">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-166">View hello results.</span></span> <span data-ttu-id="66e19-167">Una vez que haya finalizado el trabajo de hello, resultados de Hola se almacenarán en dos archivos de salida de hello **wasb: / / / ejemplo/out/shotestpaths** carpeta.</span><span class="sxs-lookup"><span data-stu-id="66e19-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="66e19-168">se denominan archivos Hello **parte-m-00001** y **parte-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="66e19-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="66e19-169">Lleve a cabo Hola siguiendo la salida de hello toodownload y vista de pasos:</span><span class="sxs-lookup"><span data-stu-id="66e19-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="66e19-170">Esto creará hello **ejemplo/salida/shortestpaths** estructura de directorios en el directorio actual de hello en la estación de trabajo y archivos toothat ubicación de descarga Hola dos resultados.</span><span class="sxs-lookup"><span data-stu-id="66e19-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="66e19-171">Hola de uso **Cat** contenido de Hola de cmdlet toodisplay de los archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="66e19-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="66e19-172">salida de Hello debe aparecer toohello similar a continuación:</span><span class="sxs-lookup"><span data-stu-id="66e19-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="66e19-173">ejemplo de Hola a SimpleShortestPathComputation es toostart codificado con objeto de identificador 1 y buscar objetos de tooother de ruta de acceso más cortos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e19-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="66e19-174">Por lo que debe leerse la salida de hello como `destination_id distance`, donde la distancia es valor hello (o peso) de los bordes de hello recorridos entre objeto identificador 1 y Hola Id. de destino.</span><span class="sxs-lookup"><span data-stu-id="66e19-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="66e19-175">Visualizar esto, puede comprobar los resultados de Hola por las rutas de acceso más cortas de hello en viaje entre el identificador 1 y todos los demás objetos.</span><span class="sxs-lookup"><span data-stu-id="66e19-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="66e19-176">Tenga en cuenta que Hola ruta más corta entre el identificador 1 y 4 de identificador es 5.</span><span class="sxs-lookup"><span data-stu-id="66e19-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="66e19-177">Se trata de la distancia total de hello entre <span style="color:orange">identificador 1 y 3</span>y, a continuación, <span style="color:red">identificador 3 y 4</span>.</span><span class="sxs-lookup"><span data-stu-id="66e19-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="66e19-179">Instalación de Giraph con Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="66e19-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="66e19-180">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="66e19-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="66e19-181">ejemplo de Hola se muestra cómo tooinstall Spark con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66e19-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="66e19-182">Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="66e19-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="66e19-183">Instalación de Giraph mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="66e19-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="66e19-184">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="66e19-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="66e19-185">ejemplo de Hola se muestra cómo tooinstall Spark utilizando Hola .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="66e19-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="66e19-186">Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="66e19-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="66e19-187">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="66e19-187">See also</span></span>
* [<span data-ttu-id="66e19-188">Instalación de Giraph en clústeres de Hadoop de HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="66e19-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="66e19-189">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66e19-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="66e19-190">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="66e19-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="66e19-191">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="66e19-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="66e19-192">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.</span><span class="sxs-lookup"><span data-stu-id="66e19-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="66e19-193">[Instalación de R en clústeres de HDInsight][hdinsight-install-r]: ejemplo de acción de script sobre la instalación de R.</span><span class="sxs-lookup"><span data-stu-id="66e19-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="66e19-194">[Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md): ejemplo de acción de script sobre la instalación de Solr.</span><span class="sxs-lookup"><span data-stu-id="66e19-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
