---
title: "Instalar y usar Giraph en clústeres de Hadoop en HDInsight - Azure | Microsoft Docs"
description: "Obtenga información sobre cómo personalizar el clúster de HDInsight con Giraph y cómo usar Giraph."
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
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="ee73e-103">Instalación y uso de Giraph en clústeres de HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="ee73e-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="ee73e-104">Obtenga información acerca de cómo personalizar un clúster de HDInsight basado en Windows con Giraph mediante la acción de script, y cómo usar Giraph para procesar gráficos a gran escala.</span><span class="sxs-lookup"><span data-stu-id="ee73e-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="ee73e-105">Para obtener información sobre el uso de Giraph con un clúster basado en Linux, consulte [Instalación de Giraph en clústeres Hadoop de HDinsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)</span><span class="sxs-lookup"><span data-stu-id="ee73e-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee73e-106">Los pasos de este tutorial solo se aplican a los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="ee73e-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ee73e-107">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="ee73e-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="ee73e-108">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="ee73e-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee73e-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ee73e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="ee73e-110">Para más información sobre cómo instalar Giraph con un clúster de HDInsight basado en Linux, consulte [Instalación de Giraph en clústeres de Hadoop en HDinsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ee73e-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="ee73e-111">Puede instalar Giraph en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*.</span><span class="sxs-lookup"><span data-stu-id="ee73e-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="ee73e-112">Hay un script de ejemplo para instalar Giraph en un clúster de HDInsight disponible desde un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="ee73e-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="ee73e-113">El script de ejemplo solo funciona con el clúster de HDInsight versión 3.1.</span><span class="sxs-lookup"><span data-stu-id="ee73e-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="ee73e-114">Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ee73e-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="ee73e-115">**Artículos relacionados**</span><span class="sxs-lookup"><span data-stu-id="ee73e-115">**Related articles**</span></span>

* [<span data-ttu-id="ee73e-116">Instalación de Giraph en clústeres de Hadoop de HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="ee73e-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="ee73e-117">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee73e-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="ee73e-118">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="ee73e-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="ee73e-119">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="ee73e-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="ee73e-120">¿Qué es Giraph?</span><span class="sxs-lookup"><span data-stu-id="ee73e-120">What is Giraph?</span></span>
<span data-ttu-id="ee73e-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permite realizar un procesamiento gráfico mediante Hadoop, y se puede usar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee73e-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="ee73e-122">Los gráficos modelan las relaciones entre los objetos, como las conexiones entre los enrutadores en una red de gran tamaño como Internet, o las relaciones entre personas de las redes sociales (conocidas en ocasiones como gráficos sociales).</span><span class="sxs-lookup"><span data-stu-id="ee73e-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="ee73e-123">El procesamiento gráfico le permite razonar sobre las relaciones entre los objetos de un gráfico. En este sentido, le ayuda por ejemplo a:</span><span class="sxs-lookup"><span data-stu-id="ee73e-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="ee73e-124">Identificar los posibles amigos según las relaciones actuales.</span><span class="sxs-lookup"><span data-stu-id="ee73e-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="ee73e-125">Identificar la ruta más corta entre dos equipos de una red.</span><span class="sxs-lookup"><span data-stu-id="ee73e-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="ee73e-126">Calcular la posición de las páginas web.</span><span class="sxs-lookup"><span data-stu-id="ee73e-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="ee73e-127">Instalación de Giraph mediante el portal</span><span class="sxs-lookup"><span data-stu-id="ee73e-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="ee73e-128">Comience a crear un clúster mediante la opción **CREACIÓN PERSONALIZADA**, como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="ee73e-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="ee73e-129">En la página **Acciones de script** del asistente, haga clic en **Agregar acción de script** para proporcionar detalles acerca de la acción de script, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="ee73e-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="ee73e-130">![Uso de la acción de script para personalizar un clúster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Uso de la acción de script para personalizar un clúster")</span><span class="sxs-lookup"><span data-stu-id="ee73e-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="ee73e-131">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ee73e-131">Property</span></span></th><th><span data-ttu-id="ee73e-132">Valor</span><span class="sxs-lookup"><span data-stu-id="ee73e-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="ee73e-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee73e-133">Name</span></span></td>
            <td><span data-ttu-id="ee73e-134">Especifique un nombre para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="ee73e-134">Specify a name for the script action.</span></span> <span data-ttu-id="ee73e-135">Por ejemplo, <b>Instalar Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="ee73e-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="ee73e-136">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="ee73e-136">Script URI</span></span></td>
            <td><span data-ttu-id="ee73e-137">Especifique el Identificador uniforme de recursos (URI) al script que se ha invocado para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="ee73e-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="ee73e-138">Por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="ee73e-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="ee73e-139">Tipo de nodo</span><span class="sxs-lookup"><span data-stu-id="ee73e-139">Node Type</span></span></td>
            <td><span data-ttu-id="ee73e-140">Especifique los nodos en los que se ejecuta el script de personalización.</span><span class="sxs-lookup"><span data-stu-id="ee73e-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="ee73e-141">Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.</span><span class="sxs-lookup"><span data-stu-id="ee73e-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="ee73e-142">Parámetros</span><span class="sxs-lookup"><span data-stu-id="ee73e-142">Parameters</span></span></td>
            <td><span data-ttu-id="ee73e-143">Especifique los parámetros, si lo requiere el script.</span><span class="sxs-lookup"><span data-stu-id="ee73e-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="ee73e-144">El script para instalar Giraph no requiere ningún parámetro, por lo que puede dejarlo en blanco.</span><span class="sxs-lookup"><span data-stu-id="ee73e-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="ee73e-145">Puede agregar más de una acción de script para instalar varios componentes en el clúster.</span><span class="sxs-lookup"><span data-stu-id="ee73e-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="ee73e-146">Después de haber agregado los scripts, haga clic en la marca de verificación para comenzar a crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="ee73e-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="ee73e-147">Uso de Giraph</span><span class="sxs-lookup"><span data-stu-id="ee73e-147">Use Giraph</span></span>
<span data-ttu-id="ee73e-148">Usamos el ejemplo SimpleShortestPathsComputation para mostrar la implementación básica de <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> para encontrar la ruta más corta entre objetos en un gráfico.</span><span class="sxs-lookup"><span data-stu-id="ee73e-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="ee73e-149">Use los siguientes pasos para cargar los datos de ejemplo y el jar de muestra, ejecutar un trabajo mediante el ejemplo SimpleShortestPathsComputation y luego ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="ee73e-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="ee73e-150">Cargue un archivo de datos de ejemplo en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee73e-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="ee73e-151">En la estación de trabajo local, cree un archivo nuevo llamado **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="ee73e-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="ee73e-152">Debe contener las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ee73e-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="ee73e-153">Cargue el archivo tiny_graph.txt en el almacenamiento principal del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee73e-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="ee73e-154">Para obtener instrucciones sobre cómo cargar datos, consulte [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="ee73e-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="ee73e-155">Estos datos describen una relación entre los objetos de un gráfico dirigido, con el formato [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span><span class="sxs-lookup"><span data-stu-id="ee73e-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="ee73e-156">Cada línea representa una relación entre un objeto **source\_id** y uno más objetos **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="ee73e-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="ee73e-157">El valor **edge\_value** (o peso) se puede considerar como la fuerza o la distancia de la conexión entre **source_id** y **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="ee73e-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="ee73e-158">Extrapolados, y usando el valor (o peso) como la distancia entre los objetos, los datos anteriores podrían parecerse a estos:</span><span class="sxs-lookup"><span data-stu-id="ee73e-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="ee73e-160">Ejecute el ejemplo SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="ee73e-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="ee73e-161">Utilice los siguientes cmdlets de PowerShell de Azure para ejecutar el ejemplo mediante el archivo tiny_graph.txt como entrada.</span><span class="sxs-lookup"><span data-stu-id="ee73e-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ee73e-162">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="ee73e-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="ee73e-163">En los pasos descritos en este documento, se usan los nuevos cmdlets de HDInsight que funcionan con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee73e-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="ee73e-164">Para instalar la versión más reciente, siga los pasos descritos en [Cómo instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="ee73e-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="ee73e-165">Si tiene scripts que se deben modificar para usar los nuevos cmdlets que funcionan con Azure Resource Manager, consulte [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migración a herramientas de desarrollo basadas en Azure Resource Manager para clústeres de HDInsight) para más información.</span><span class="sxs-lookup"><span data-stu-id="ee73e-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="ee73e-166">En el ejemplo anterior, reemplace **clustername** por el nombre del clúster de HDInsight donde está instalado Giraph.</span><span class="sxs-lookup"><span data-stu-id="ee73e-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="ee73e-167">Vea los resultados.</span><span class="sxs-lookup"><span data-stu-id="ee73e-167">View the results.</span></span> <span data-ttu-id="ee73e-168">Una vez finalizado el trabajo, los resultados se almacenarán en dos archivos de salida en la carpeta **wasb:///example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="ee73e-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="ee73e-169">Los archivos se llaman **part-m-00001** y **part-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="ee73e-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="ee73e-170">Realice los pasos siguientes para descargar y ver el resultado:</span><span class="sxs-lookup"><span data-stu-id="ee73e-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="ee73e-171">Esto creará la estructura de directorios **example/output/shortestpaths** en el directorio actual de la estación de trabajo y se descargarán los dos archivos de salida a esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="ee73e-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="ee73e-172">Use el cmdlet **Cat** para mostrar el contenido de los archivos:</span><span class="sxs-lookup"><span data-stu-id="ee73e-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="ee73e-173">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee73e-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="ee73e-174">El ejemplo SimpleShortestPathComputation se ha codificado de forma rígida para comenzar por el identificador de objeto 1 y encontrar la ruta más corta a los demás objetos.</span><span class="sxs-lookup"><span data-stu-id="ee73e-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="ee73e-175">Así que la salida se debe leer como `destination_id distance`, donde la distancia es el valor (o peso) de los bordes recorridos entre el identificador de objeto 1 y el identificador de destino.</span><span class="sxs-lookup"><span data-stu-id="ee73e-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="ee73e-176">Visualizando esto, puede verificar los resultados recorriendo las rutas más cortas entre el Id. 1 y todos los demás objetos.</span><span class="sxs-lookup"><span data-stu-id="ee73e-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="ee73e-177">Tenga en cuenta que la ruta más corta entre el Id. 1 y el Id. 4 es 5.</span><span class="sxs-lookup"><span data-stu-id="ee73e-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="ee73e-178">Esta es la distancia total entre el <span style="color:orange">identificador 1 y 3</span>, y, a continuación, <span style="color:red">identificador 3 y 4</span>.</span><span class="sxs-lookup"><span data-stu-id="ee73e-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="ee73e-180">Instalación de Giraph con Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee73e-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="ee73e-181">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="ee73e-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="ee73e-182">El ejemplo muestra cómo instalar Spark con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee73e-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="ee73e-183">Deberá personalizar el script para usar [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="ee73e-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="ee73e-184">Instalación de Giraph mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ee73e-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="ee73e-185">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="ee73e-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="ee73e-186">El ejemplo muestra cómo instalar Spark con .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="ee73e-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="ee73e-187">Deberá personalizar el script para usar [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="ee73e-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="ee73e-188">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ee73e-188">See also</span></span>
* [<span data-ttu-id="ee73e-189">Instalación de Giraph en clústeres de Hadoop de HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="ee73e-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="ee73e-190">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee73e-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="ee73e-191">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="ee73e-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="ee73e-192">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="ee73e-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="ee73e-193">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.</span><span class="sxs-lookup"><span data-stu-id="ee73e-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="ee73e-194">[Instalación de R en clústeres de HDInsight][hdinsight-install-r]: ejemplo de acción de script sobre la instalación de R.</span><span class="sxs-lookup"><span data-stu-id="ee73e-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="ee73e-195">[Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md): ejemplo de acción de script sobre la instalación de Solr.</span><span class="sxs-lookup"><span data-stu-id="ee73e-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
