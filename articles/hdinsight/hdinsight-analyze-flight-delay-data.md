---
title: datos de retrasos de vuelos aaaAnalyze con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse una Windows PowerShell script toocreate un clúster de HDInsight, ejecute un trabajo de Hive, ejecutar un trabajo de Sqoop y eliminar el clúster de Hola."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="1ae73-103">Análisis de datos de retraso de vuelos con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1ae73-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="1ae73-104">Hive ofrece un modo de ejecutar trabajos de MapReduce de Hadoop mediante un lenguaje de scripting de tipo SQL, denominado *[HiveQL][hadoop-hiveql]*, que se puede usar para resumir, consultar y analizar grandes volúmenes de datos.</span><span class="sxs-lookup"><span data-stu-id="1ae73-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ae73-105">Hello pasos de este documento requieren un clúster de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="1ae73-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="1ae73-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="1ae73-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1ae73-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1ae73-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1ae73-108">Para conocer el procedimiento que funciona con un clúster basado en Linux, vea [Análisis de datos de retraso de vuelos con Hive en HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1ae73-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="1ae73-109">Una de las principales ventajas de Hola de HDInsight de Azure es la separación de Hola de almacenamiento de datos y el cálculo.</span><span class="sxs-lookup"><span data-stu-id="1ae73-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="1ae73-110">HDInsight usa el almacenamiento de blobs de Azure para almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="1ae73-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="1ae73-111">Un trabajo típico implica tres partes:</span><span class="sxs-lookup"><span data-stu-id="1ae73-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="1ae73-112">**Almacenar los datos en el almacenamiento de blobs de Azure.**</span><span class="sxs-lookup"><span data-stu-id="1ae73-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="1ae73-113">Por ejemplo, los datos meteorológicos, datos de sensores, registros web y, en este caso, datos de retraso de vuelos se guardan en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="1ae73-114">**Ejecutar trabajos.**</span><span class="sxs-lookup"><span data-stu-id="1ae73-114">**Run jobs.**</span></span> <span data-ttu-id="1ae73-115">Cuando se trata de datos en tiempo de tooprocess hello, ejecutar un script de Windows PowerShell (o una aplicación cliente) toocreate un clúster de HDInsight, ejecutar trabajos y eliminar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="1ae73-116">trabajos de Hello guardar datos de salida tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="1ae73-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="1ae73-117">datos de salida de Hello se conservan incluso después de que se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="1ae73-118">De este modo, solo paga por lo que ha consumido.</span><span class="sxs-lookup"><span data-stu-id="1ae73-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="1ae73-119">**Recuperar la salida de hello desde el almacenamiento de blobs de Azure**, o en este tutorial, exportar base de datos de SQL Azure de hello datos tooan.</span><span class="sxs-lookup"><span data-stu-id="1ae73-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="1ae73-120">Hello siguiente diagrama ilustra el escenario de Hola y la estructura de Hola de este tutorial:</span><span class="sxs-lookup"><span data-stu-id="1ae73-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="1ae73-122">Tenga en cuenta que los números de hello en el diagrama de hello corresponden toohello títulos de sección.</span><span class="sxs-lookup"><span data-stu-id="1ae73-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="1ae73-123">**M** hace referencia al proceso principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-123">**M** stands for hello main process.</span></span> <span data-ttu-id="1ae73-124">**Un** hace referencia al contenido de hello en el apéndice de hello.</span><span class="sxs-lookup"><span data-stu-id="1ae73-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="1ae73-125">parte principal de Hola de tutorial de hello muestra cómo toouse una Windows PowerShell script tooperform Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="1ae73-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="1ae73-126">Cree un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ae73-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="1ae73-127">Ejecutar un trabajo de Hive en retrasos promedio de hello clúster toocalculate en aeropuertos.</span><span class="sxs-lookup"><span data-stu-id="1ae73-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="1ae73-128">datos de retrasos de vuelos de Hola se almacenan en una cuenta de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="1ae73-129">Ejecute Sqoop trabajo tooexport Hola Hive trabajo salida tooan Azure base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="1ae73-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="1ae73-130">Eliminar el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="1ae73-131">Apéndices hello, encontrará instrucciones de Hola para cargar datos de retrasos de vuelos, crear o cargar una cadena de consulta de Hive y preparar la base de datos de SQL Azure de hello para el trabajo de Sqoop Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="1ae73-132">pasos de Hello en este documento son los clústeres de HDInsight de tooWindows-based específicos.</span><span class="sxs-lookup"><span data-stu-id="1ae73-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="1ae73-133">Para conocer el procedimiento que funciona con un clúster basado en Linux, vea [Análisis de datos de retraso de vuelos con Hive en HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1ae73-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1ae73-134">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1ae73-134">Prerequisites</span></span>
<span data-ttu-id="1ae73-135">Antes de comenzar este tutorial, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1ae73-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="1ae73-136">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ae73-136">**An Azure subscription**.</span></span> <span data-ttu-id="1ae73-137">Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1ae73-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1ae73-138">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1ae73-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1ae73-139">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="1ae73-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="1ae73-140">Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1ae73-141">Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="1ae73-142">Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="1ae73-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="1ae73-143">**Archivos usados en este tutorial**</span><span class="sxs-lookup"><span data-stu-id="1ae73-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="1ae73-144">Este tutorial usa hello en rendimiento de datos de vuelo airline de [investigación y administración de tecnología innovadora, centro de estadísticas de transporte o RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="1ae73-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="1ae73-145">Una copia del programa Hola a datos ha sido cargado tooan contenedor de almacenamiento de blobs de Azure con permiso de acceso de Blob público Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="1ae73-146">Una parte de la secuencia de comandos de PowerShell copia datos de Hola de contenedor de blobs de predeterminado toohello contenedor de blob público Hola del clúster.</span><span class="sxs-lookup"><span data-stu-id="1ae73-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="1ae73-147">Hola HiveQL script también está copia toohello mismo contenedor de Blob.</span><span class="sxs-lookup"><span data-stu-id="1ae73-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="1ae73-148">Si desea que toolearn cómo tooget/cargar Hola datos tooyour posee cuenta de almacenamiento y cómo toocreate/cargar hello HiveQL script archivo, consulte [Apéndice A](#appendix-a) y [Apéndice B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="1ae73-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="1ae73-149">Hello siguiente tabla enumeran Hola archivos utilizados en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="1ae73-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="1ae73-150">Archivos</span><span class="sxs-lookup"><span data-stu-id="1ae73-150">Files</span></span></th><th><span data-ttu-id="1ae73-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="1ae73-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="1ae73-152">archivo de script de HiveQL Hello usa Hola trabajo de Hive.</span><span class="sxs-lookup"><span data-stu-id="1ae73-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="1ae73-153">Esta secuencia de comandos ha sido cargado tooan cuenta de almacenamiento de blobs de Azure con acceso público de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="1ae73-154"><a href="#appendix-b">Apéndice B</a> contiene instrucciones sobre la preparación y carga de esta cuenta de almacenamiento de blobs de Azure propia de archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="1ae73-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="1ae73-155">Datos de entrada para el trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-155">Input data for hello Hive job.</span></span> <span data-ttu-id="1ae73-156">datos de Hello ha sido cargado tooan cuenta de almacenamiento de blobs de Azure con acceso público de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="1ae73-157"><a href="#appendix-a">Apéndice a:</a> contiene instrucciones sobre obtención de datos de Hola y cargar la cuenta de almacenamiento de hello datos tooyour propio Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="1ae73-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="1ae73-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="1ae73-159">ruta de acceso de salida de Hello para el trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="1ae73-160">contenedor de Hello predeterminado se utiliza para almacenar los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="1ae73-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="1ae73-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="1ae73-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="1ae73-162">carpeta de estado del trabajo de Hive Hello en contenedor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="1ae73-163">Creación de clústeres y ejecución de trabajos de Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="1ae73-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="1ae73-164">Hadoop MapReduce se está procesando por lotes.</span><span class="sxs-lookup"><span data-stu-id="1ae73-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="1ae73-165">Hello toorun mayoría de forma eficaz un trabajo de Hive es toocreate un clúster para el trabajo de Hola y eliminar el trabajo de hello después de que se complete el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="1ae73-166">Hello secuencia de comandos siguiente cubre todo proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="1ae73-167">Para obtener más información sobre la creación de un clúster de HDInsight y la ejecución de trabajos de Hive, consulte [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision] y [Uso de Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="1ae73-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="1ae73-168">**consultas de Hive de hello toorun PowerShell de Azure**</span><span class="sxs-lookup"><span data-stu-id="1ae73-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="1ae73-169">Cree una tabla de hello y base de datos de SQL Azure para la salida de trabajo de Sqoop Hola siguiendo las instrucciones de hello en [Apéndice C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="1ae73-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="1ae73-170">Abra Windows PowerShell ISE y ejecute hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="1ae73-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="1ae73-171">Conectar la base de datos SQL tooyour y vea retrasos de vuelos promedio por ciudad en la tabla de Hola AvgDelays:</span><span class="sxs-lookup"><span data-stu-id="1ae73-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="1ae73-173"><a id="appendix-a"></a>Apéndice A - carga vuelo retraso datos tooAzure almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="1ae73-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="1ae73-174">Cargar archivo de datos de hello y los archivos de script de HiveQL Hola (vea [Apéndice B](#appendix-b)) requiere cierta planeación.</span><span class="sxs-lookup"><span data-stu-id="1ae73-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="1ae73-175">idea de Hello es archivos de datos de toostore hello y archivo de HiveQL hello antes de crear un clúster de HDInsight y ejecutar el trabajo de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="1ae73-176">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="1ae73-176">You have two options:</span></span>

* <span data-ttu-id="1ae73-177">**Use Hola misma cuenta de almacenamiento de Azure que se usará por clúster de HDInsight de hello como sistema de archivos predeterminado de Hola.**</span><span class="sxs-lookup"><span data-stu-id="1ae73-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="1ae73-178">Porque clúster de HDInsight de hello disponen de tecla de acceso de cuenta de almacenamiento de hello, no es necesario toomake ningún cambio adicional.</span><span class="sxs-lookup"><span data-stu-id="1ae73-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="1ae73-179">**Usar una cuenta de almacenamiento de Azure diferente de hello sistema de archivos de predeterminado de clúster de HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="1ae73-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="1ae73-180">Si éste es el caso de hello, debe modificar la parte de la creación de hello de hello Windows PowerShell script se encuentra en [HDInsight crear clúster y ejecución de los trabajos de Hive y Sqoop](#runjob) toolink Hola cuenta de almacenamiento como una cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="1ae73-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="1ae73-181">Para instrucciones, vea [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="1ae73-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="1ae73-182">clúster de HDInsight de Hello, a continuación, conoce la clave de acceso de Hola para hello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1ae73-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1ae73-183">Hola ruta de acceso de almacenamiento de blobs para hello archivo de datos está codificado en el archivo de script de HiveQL Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="1ae73-184">Debe actualizarse en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="1ae73-184">You must update it accordingly.</span></span>

<span data-ttu-id="1ae73-185">**datos del vuelo hello toodownload**</span><span class="sxs-lookup"><span data-stu-id="1ae73-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="1ae73-186">Examinar demasiado[investigación y administración de tecnología innovadora, centro de transporte estadísticas][rita-website].</span><span class="sxs-lookup"><span data-stu-id="1ae73-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="1ae73-187">En página de hello, seleccione Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="1ae73-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="1ae73-188">Nombre</span><span class="sxs-lookup"><span data-stu-id="1ae73-188">Name</span></span></th><th><span data-ttu-id="1ae73-189">Valor</span><span class="sxs-lookup"><span data-stu-id="1ae73-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="1ae73-190">Filter Year</span><span class="sxs-lookup"><span data-stu-id="1ae73-190">Filter Year</span></span></td><td><span data-ttu-id="1ae73-191">2013</span><span class="sxs-lookup"><span data-stu-id="1ae73-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="1ae73-192">Filter Period</span><span class="sxs-lookup"><span data-stu-id="1ae73-192">Filter Period</span></span></td><td><span data-ttu-id="1ae73-193">January</span><span class="sxs-lookup"><span data-stu-id="1ae73-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-194">Fields</span><span class="sxs-lookup"><span data-stu-id="1ae73-194">Fields</span></span></td><td><span data-ttu-id="1ae73-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (borrar todos los demás campos)</span><span class="sxs-lookup"><span data-stu-id="1ae73-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="1ae73-196">
3. Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="1ae73-196">
3. Click **Download**.</span></span>
<span data-ttu-id="1ae73-197">4.</span><span class="sxs-lookup"><span data-stu-id="1ae73-197">4.</span></span> <span data-ttu-id="1ae73-198">Descomprima Hola archivo toohello **C:\Tutorials\FlightDelay\2013Data** carpeta.</span><span class="sxs-lookup"><span data-stu-id="1ae73-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="1ae73-199">Cada archivo es un archivo CSV y tiene un tamaño aproximado de 60 GB.</span><span class="sxs-lookup"><span data-stu-id="1ae73-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="1ae73-200">5.</span><span class="sxs-lookup"><span data-stu-id="1ae73-200">5.</span></span> <span data-ttu-id="1ae73-201">Cambiar el nombre de toohello de archivo de hello del mes de Hola que contiene datos de.</span><span class="sxs-lookup"><span data-stu-id="1ae73-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="1ae73-202">Por ejemplo, archivo de Hola que contiene datos de enero de saludo se denominará *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="1ae73-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="1ae73-203">6.</span><span class="sxs-lookup"><span data-stu-id="1ae73-203">6.</span></span> <span data-ttu-id="1ae73-204">Repita toodownload un archivo de los pasos 2 y 5 para cada uno de hello 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="1ae73-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="1ae73-205">Necesitará un mínimo de un tutorial de hello toorun de archivo.</span><span class="sxs-lookup"><span data-stu-id="1ae73-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="1ae73-206">**tooupload Hola vuelo retraso datos tooAzure almacenamiento de blobs**</span><span class="sxs-lookup"><span data-stu-id="1ae73-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="1ae73-207">Preparar los parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="1ae73-208">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="1ae73-208">Variable Name</span></span></th><th><span data-ttu-id="1ae73-209">Notas</span><span class="sxs-lookup"><span data-stu-id="1ae73-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="1ae73-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="1ae73-210">$storageAccountName</span></span></td><td><span data-ttu-id="1ae73-211">Hola donde desea que los datos de Hola de tooupload de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="1ae73-212">$blobContainerName</span></span></td><td><span data-ttu-id="1ae73-213">Hola donde desea tooupload Hola datos para el contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="1ae73-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="1ae73-214">Abra Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1ae73-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="1ae73-215">3.</span><span class="sxs-lookup"><span data-stu-id="1ae73-215">3.</span></span> <span data-ttu-id="1ae73-216">Pegue Hola siguiente secuencia de comandos en el panel de scripts de hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="1ae73-217">Presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="1ae73-218">Si elige un método diferente para cargar archivos de hello toouse, asegúrese de ruta de acceso de archivo de hello es tutoriales/flightdelay/datos.</span><span class="sxs-lookup"><span data-stu-id="1ae73-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="1ae73-219">sintaxis de Hello para tener acceso a archivos de hello es:</span><span class="sxs-lookup"><span data-stu-id="1ae73-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="1ae73-220">ruta de acceso de Hello tutoriales/flightdelay/datos es carpeta virtual de hello creado al cargar archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="1ae73-221">Compruebe que haya 12 archivos, uno para cada mes.</span><span class="sxs-lookup"><span data-stu-id="1ae73-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="1ae73-222">Debe actualizar tooread de consulta de Hive Hola desde nueva ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="1ae73-223">Debe configurar Hola contenedor acceso permiso toobe público o enlazar toohello cuenta de almacenamiento Hola clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ae73-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="1ae73-224">En caso contrario, la cadena de consulta de Hive de Hola no estará tooaccess capaz de archivos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="1ae73-225"><a id="appendix-b"></a>Apéndice B: Creación y carga de un script de HiveQL</span><span class="sxs-lookup"><span data-stu-id="1ae73-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="1ae73-226">Uso de PowerShell de Azure, puede ejecutar varias instrucciones de HiveQL uno a una hora u Hola paquete HiveQL instrucción en un archivo de script.</span><span class="sxs-lookup"><span data-stu-id="1ae73-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="1ae73-227">Esta sección muestra cómo toocreate un script de HiveQL Hola de carga de script y el almacenamiento de blobs de tooAzure mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ae73-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="1ae73-228">Subárbol requiere hello HiveQL scripts toobe almacenado en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="1ae73-229">Hola script de HiveQL llevará a cabo siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="1ae73-230">**Quitar tabla de hello delays_raw**, en caso de hello tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="1ae73-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="1ae73-231">**Crear tabla de Hive externo de hello delays_raw** que apuntan toohello ubicación de almacenamiento de blobs con archivos de retraso de vuelos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="1ae73-232">Esta consulta especifica que los campos están delimitados por "," y que las líneas terminan en "\n".</span><span class="sxs-lookup"><span data-stu-id="1ae73-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="1ae73-233">Esto supone un problema cuando los valores de campo contienen comas porque Hive no puede diferenciar entre una coma que es un delimitador de campo y otra que forma parte de un valor de campo (que es el caso de hello en valores de campo de origen\_CITY\_nombre y DEST\_ Ciudad\_nombre).</span><span class="sxs-lookup"><span data-stu-id="1ae73-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="1ae73-234">tooaddress, Hola consulta crea columnas TEMP datos toohold incorrectamente se división en las columnas.</span><span class="sxs-lookup"><span data-stu-id="1ae73-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="1ae73-235">**Quitar tabla de retrasos de hello**, en caso de hello tabla ya existe.</span><span class="sxs-lookup"><span data-stu-id="1ae73-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="1ae73-236">**Crear tabla de retrasos de hello**.</span><span class="sxs-lookup"><span data-stu-id="1ae73-236">**Create hello delays table**.</span></span> <span data-ttu-id="1ae73-237">Resulta útil tooclean los datos de hello antes de su posterior procesamiento.</span><span class="sxs-lookup"><span data-stu-id="1ae73-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="1ae73-238">Esta consulta crea una nueva tabla, *retrasos*, de tabla de delays_raw Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="1ae73-239">Tenga en cuenta que no se copian las columnas TEMP de hello (como se mencionó anteriormente) y ese hello **subcadena** función es tooremove utilizado comillas de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="1ae73-240">**Proceso Hola tiempo promedio retraso y grupos Hola los resultados por nombre de ciudad.**</span><span class="sxs-lookup"><span data-stu-id="1ae73-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="1ae73-241">También dará como resultado el almacenamiento de información de hello resultados tooBlob.</span><span class="sxs-lookup"><span data-stu-id="1ae73-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="1ae73-242">Tenga en cuenta esa consulta Hola quitará apóstrofos de datos de Hola y excluirá filas donde valor hello **weather_delay** es null.</span><span class="sxs-lookup"><span data-stu-id="1ae73-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="1ae73-243">Esto es necesario porque Sqoop, que se usa más adelante en este tutorial, no trata estos valores correctamente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1ae73-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="1ae73-244">Para obtener una lista completa de comandos de HiveQL hello, consulte [lenguaje de definición de datos de Hive][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="1ae73-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="1ae73-245">Cada comando de HiveQL debe terminar con un punto y coma.</span><span class="sxs-lookup"><span data-stu-id="1ae73-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="1ae73-246">**un archivo de script de HiveQL toocreate**</span><span class="sxs-lookup"><span data-stu-id="1ae73-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="1ae73-247">Preparar los parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="1ae73-248">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="1ae73-248">Variable Name</span></span></th><th><span data-ttu-id="1ae73-249">Notas</span><span class="sxs-lookup"><span data-stu-id="1ae73-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="1ae73-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="1ae73-250">$storageAccountName</span></span></td><td><span data-ttu-id="1ae73-251">Hola cuenta de almacenamiento de Azure donde desea tooupload hello HiveQL script.</span><span class="sxs-lookup"><span data-stu-id="1ae73-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="1ae73-252">$blobContainerName</span></span></td><td><span data-ttu-id="1ae73-253">Hola donde desea que el script de HiveQL tooupload hello para el contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="1ae73-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="1ae73-254">Abra Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1ae73-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="1ae73-255">3.</span><span class="sxs-lookup"><span data-stu-id="1ae73-255">3.</span></span> <span data-ttu-id="1ae73-256">Copie y pegue la siguiente secuencia de comandos en el panel de scripts de Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="1ae73-257">Estas son las variables de hello utilizadas en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="1ae73-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="1ae73-258">**$hqlLocalFileName** -script de Hola guarda el archivo de script de Hola HiveQL localmente antes de cargarlo tooBlob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1ae73-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="1ae73-259">Éste es el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-259">This is hello file name.</span></span> <span data-ttu-id="1ae73-260">es el valor predeterminado de Hello <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="1ae73-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="1ae73-261">**$hqlBlobName** -se trata de hello HiveQL script blob nombre del archivo utilizado en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="1ae73-262">valor predeterminado de Hello es tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="1ae73-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="1ae73-263">Dado que se escribirán archivo hello directamente tooAzure almacenamiento de blobs, no hay un "/" al principio de hello del nombre de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="1ae73-264">Si desea que el archivo de hello tooaccess desde almacenamiento de blobs, deberá tooadd un "/" al principio de Hola Hola del nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="1ae73-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="1ae73-265">**$srcDataFolder** y **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="1ae73-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="1ae73-266"><a id="appendix-c"></a>Apéndice C - preparar una base de datos de SQL Azure para hello salida del trabajo de Sqoop</span><span class="sxs-lookup"><span data-stu-id="1ae73-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="1ae73-267">**base de datos SQL tooprepare Hola (combinar esto con hello Sqoop script)**</span><span class="sxs-lookup"><span data-stu-id="1ae73-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="1ae73-268">Preparar los parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="1ae73-269">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="1ae73-269">Variable Name</span></span></th><th><span data-ttu-id="1ae73-270">Notas</span><span class="sxs-lookup"><span data-stu-id="1ae73-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="1ae73-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="1ae73-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="1ae73-272">nombre de Hola del servidor de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="1ae73-273">Escriba nada toocreate un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="1ae73-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="1ae73-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="1ae73-275">nombre de inicio de sesión Hello para el servidor de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="1ae73-276">Si $sqlDatabaseServerName es un servidor existente, el inicio de sesión de Hola y la contraseña de inicio de sesión son tooauthenticate usado con el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="1ae73-277">En caso contrario, son toocreate usa un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="1ae73-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="1ae73-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="1ae73-279">contraseña de inicio de sesión de Hello para el servidor de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="1ae73-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="1ae73-281">Este valor se usa solo cuando se crea un nuevo servidor de base de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="1ae73-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="1ae73-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="1ae73-283">base de datos SQL de Hello utiliza tabla AvgDelays de toocreate hello para el trabajo de Sqoop Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="1ae73-284">Si se deja en blanco, se creará una base de datos denominada HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="1ae73-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="1ae73-285">nombre de la tabla de Hola para hello salida del trabajo de Sqoop es AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="1ae73-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="1ae73-286">Abra Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1ae73-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="1ae73-287">3.</span><span class="sxs-lookup"><span data-stu-id="1ae73-287">3.</span></span> <span data-ttu-id="1ae73-288">Copie y pegue la siguiente secuencia de comandos en el panel de scripts de Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="1ae73-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="1ae73-289">Hello secuencia de comandos utiliza un servicio de representational state Transfer (REST) de transferencia, http://bot.whatismyipaddress.com, tooretrieve su dirección IP externa.</span><span class="sxs-lookup"><span data-stu-id="1ae73-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="1ae73-290">dirección IP de Hola se usa para crear una regla de firewall para el servidor de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="1ae73-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="1ae73-291">Estas son algunas variables utilizadas en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="1ae73-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="1ae73-292">**$ipAddressRestService** -valor predeterminado de hello es http://bot.whatismyipaddress.com. Es un Es un servicio de REST de direcciones IP públicas para obtener la dirección IP externa.</span><span class="sxs-lookup"><span data-stu-id="1ae73-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="1ae73-293">Puede usar los servicios que desee.</span><span class="sxs-lookup"><span data-stu-id="1ae73-293">You can use other services if you want.</span></span> <span data-ttu-id="1ae73-294">dirección IP externa Hola recuperado a través del servicio Hola será toocreate usa una regla de firewall para el servidor de base de datos SQL de Azure, para que se puede tener acceso a base de datos de Hola desde su estación de trabajo (mediante un script de Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1ae73-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="1ae73-295">**$fireWallRuleName** -este es el nombre de Hola Hola de regla de firewall para el servidor de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="1ae73-296">es el nombre predeterminado de Hello <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="1ae73-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="1ae73-297">Puede cambiarlo si lo desea.</span><span class="sxs-lookup"><span data-stu-id="1ae73-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="1ae73-298">**$sqlDatabaseMaxSizeGB** : este valor se usa solo cuando se crea un nuevo servidor de Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="1ae73-299">valor predeterminado de Hello es de 10GB.</span><span class="sxs-lookup"><span data-stu-id="1ae73-299">hello default value is 10GB.</span></span> <span data-ttu-id="1ae73-300">10 GB es suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ae73-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="1ae73-301">**$sqlDatabaseName** : este valor se usa solo cuando se crea una nueva Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae73-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="1ae73-302">valor predeterminado de Hello es HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="1ae73-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="1ae73-303">Si cambia el nombre, debe actualizar script de Windows PowerShell de Sqoop de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="1ae73-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="1ae73-304">Presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="1ae73-305">Validar salida de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ae73-305">Validate hello script output.</span></span> <span data-ttu-id="1ae73-306">Asegúrese de que el script de Hola se ejecutó correctamente.</span><span class="sxs-lookup"><span data-stu-id="1ae73-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="1ae73-307"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ae73-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="1ae73-308">Ahora que comprende cómo tooupload una tooAzure archivo almacenamiento de blobs, cómo tabla toopopulate un subárbol mediante Hola datos desde el almacenamiento de blobs de Azure, ¿cómo toorun Hive consultas y cómo toouse Sqoop tooexport datos de base de datos de SQL Azure HDFS tooan.</span><span class="sxs-lookup"><span data-stu-id="1ae73-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="1ae73-309">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="1ae73-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="1ae73-310">[Introducción a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1ae73-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="1ae73-311">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1ae73-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1ae73-312">[Uso de Oozie con HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="1ae73-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="1ae73-313">[Uso de Sqoop con HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="1ae73-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="1ae73-314">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1ae73-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1ae73-315">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1ae73-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
