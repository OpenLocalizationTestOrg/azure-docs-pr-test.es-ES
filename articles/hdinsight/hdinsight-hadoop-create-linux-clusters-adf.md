---
title: "Creación de clústeres de Hadoop a petición mediante Data Factory - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear clústeres de Hadoop en HDInsight mediante Azure Data Factory."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="abea0-103">Creación de clústeres de Hadoop en HDInsight mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="abea0-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="abea0-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) es un servicio de integración de datos basado en la nube que organiza y automatiza el movimiento y la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="abea0-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="abea0-105">Puede crear un clúster Hadoop de HDInsight Just-In-Time para procesar un segmento de datos de entrada y eliminar el clúster cuando el procesamiento está completo.</span><span class="sxs-lookup"><span data-stu-id="abea0-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="abea0-106">Algunas de las ventajas de usar un clúster de Hadoop de HDInsight a petición son:</span><span class="sxs-lookup"><span data-stu-id="abea0-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="abea0-107">Solo se paga por el tiempo en que el trabajo se ejecuta en el clúster de Hadoop de HDInsight (más un breve período de inactividad configurable).</span><span class="sxs-lookup"><span data-stu-id="abea0-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="abea0-108">La facturación de los clústeres de HDInsight se prorratea por minuto, tanto si se usan como si no.</span><span class="sxs-lookup"><span data-stu-id="abea0-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="abea0-109">Cuando se usa un servicio vinculado de HDInsight de petición en Data Factory, los clústeres se crean a petición.</span><span class="sxs-lookup"><span data-stu-id="abea0-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="abea0-110">Además, los clústeres se eliminan automáticamente cuando se completan los trabajos.</span><span class="sxs-lookup"><span data-stu-id="abea0-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="abea0-111">Por lo tanto, solo se paga por tiempo durante el que se ejecuta el trabajo y el breve tiempo de inactividad (configuración del período de vida).</span><span class="sxs-lookup"><span data-stu-id="abea0-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="abea0-112">Puede crear un flujo de trabajo mediante una canalización de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="abea0-113">Por ejemplo, puede hacer que la canalización copie datos de un servidor de SQL Server local a una instancia de Azure Blob Storage, procesar los datos mediante la ejecución de un script de Hive y un script de Pig en un clúster de Hadoop de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="abea0-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="abea0-114">Después, copie los datos de resultado a una instancia de Azure SQL Data Warehouse para que las aplicaciones BI los consuman.</span><span class="sxs-lookup"><span data-stu-id="abea0-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="abea0-115">Puede programar que el flujo de trabajo se ejecute periódicamente (cada hora, diariamente, semanalmente, mensualmente, etcétera).</span><span class="sxs-lookup"><span data-stu-id="abea0-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="abea0-116">En Azure Data Factory, una factoría de datos puede tener una o varias canalizaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="abea0-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="abea0-117">Una canalización de datos consta de una o varias actividades.</span><span class="sxs-lookup"><span data-stu-id="abea0-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="abea0-118">Hay dos tipos de actividades: [actividades de movimiento de datos](../data-factory/data-factory-data-movement-activities.md) y [actividades de transformación de datos](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="abea0-119">Las actividades de movimiento de datos (en la actualidad, solo actividad de copia) se usan para mover datos de un almacén de datos de origen a un almacén de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="abea0-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="abea0-120">Los actividades de transformación de datos se usan para procesar o transformar datos.</span><span class="sxs-lookup"><span data-stu-id="abea0-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="abea0-121">La actividad de Hive de HDInsight es una de las actividades de transformación de datos compatibles con Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="abea0-122">En este tutorial se usa la actividad de transformación de Hive.</span><span class="sxs-lookup"><span data-stu-id="abea0-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="abea0-123">Puede configurar una actividad de Hive para usar su propio clúster de Hadoop de HDInsight o un clúster de Hadoop de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="abea0-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="abea0-124">En este tutorial, la actividad de Hive de la canalización de la factoría de datos está configurada para utilizar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="abea0-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="abea0-125">Por lo tanto, cuando se ejecuta la actividad para procesar un segmento de datos, esto es lo que ocurre:</span><span class="sxs-lookup"><span data-stu-id="abea0-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="abea0-126">Se crea automáticamente un clúster de Hadoop de HDInsight para que just-in-time procese el segmento.</span><span class="sxs-lookup"><span data-stu-id="abea0-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="abea0-127">Los datos de entrada se procesan mediante la ejecución de un script de HiveQL en el clúster.</span><span class="sxs-lookup"><span data-stu-id="abea0-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="abea0-128">El clúster de Hadoop de HDInsight se elimina cuando se ha completado el procesamiento y el clúster está inactivo durante el período configurado (valor timeToLive).</span><span class="sxs-lookup"><span data-stu-id="abea0-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="abea0-129">Si el siguiente segmento de datos está disponible para su procesamiento con en este tiempo de inactividad timeToLive, el mismo clúster se usa para procesar el segmento.</span><span class="sxs-lookup"><span data-stu-id="abea0-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="abea0-130">En este tutorial, el script de HiveQL asociado con la actividad de Hive realiza las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="abea0-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="abea0-131">Crea primero una tabla externa que hace referencia a los datos de registro web sin procesar que se almacenan en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="abea0-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="abea0-132">Separa los datos sin procesar por año y mes.</span><span class="sxs-lookup"><span data-stu-id="abea0-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="abea0-133">Almacena los datos separados en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="abea0-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="abea0-134">En este tutorial, el script de HiveQL asociado con la actividad de Hive crea una tabla externa que hace referencia a los datos de registro web sin procesar almacenados en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="abea0-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="abea0-135">Aquí están las filas de ejemplo para cada mes en el archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="abea0-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="abea0-136">El script de HiveQL crea particiones de los datos sin procesar por año y mes.</span><span class="sxs-lookup"><span data-stu-id="abea0-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="abea0-137">Crea tres carpetas de salida basadas en la entrada anterior.</span><span class="sxs-lookup"><span data-stu-id="abea0-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="abea0-138">Cada carpeta contiene un archivo con las entradas de cada mes.</span><span class="sxs-lookup"><span data-stu-id="abea0-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="abea0-139">Para obtener una lista de actividades de transformación de datos de Data Factory además de la actividad de Hive, vea [Transformar y analizar mediante Data Factory de Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="abea0-140">Actualmente, solo se puede crear un clúster de HDInsight versión 3.2 desde Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abea0-141">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="abea0-141">Prerequisites</span></span>
<span data-ttu-id="abea0-142">Antes de empezar las instrucciones de este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="abea0-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="abea0-143">[Suscripción de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="abea0-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="abea0-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abea0-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="abea0-145">Preparación de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="abea0-145">Prepare storage account</span></span>
<span data-ttu-id="abea0-146">Puede utilizar hasta tres cuentas de almacenamiento en este escenario:</span><span class="sxs-lookup"><span data-stu-id="abea0-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="abea0-147">la cuenta de almacenamiento predeterminado para el clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="abea0-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="abea0-148">la cuenta de almacenamiento para los datos de entrada</span><span class="sxs-lookup"><span data-stu-id="abea0-148">storage account for the input data</span></span>
- <span data-ttu-id="abea0-149">la cuenta de almacenamiento para los datos de salida</span><span class="sxs-lookup"><span data-stu-id="abea0-149">storage account for the output data</span></span>

<span data-ttu-id="abea0-150">Para simplificar el tutorial, utilizará una cuenta de almacenamiento para los 3 objetivos.</span><span class="sxs-lookup"><span data-stu-id="abea0-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="abea0-151">El script de ejemplo de Azure PowerShell de esta sección realiza las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="abea0-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="abea0-152">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-152">Log in to Azure.</span></span>
2. <span data-ttu-id="abea0-153">Cree un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="abea0-154">Cree una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="abea0-155">Cree un contenedor de blobs en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="abea0-156">Copie los dos archivos siguientes en el contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="abea0-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="abea0-157">Archivo de datos de entrada: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="abea0-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="abea0-158">Script de HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="abea0-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="abea0-159">Ambos archivos se almacenan en un contenedor de blobs público.</span><span class="sxs-lookup"><span data-stu-id="abea0-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="abea0-160">**Para preparar el almacenamiento y copiar los archivos mediante Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="abea0-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="abea0-161">Especifique los nombres del grupo de recursos de Azure y la cuenta de Azure Storage que creará el script.</span><span class="sxs-lookup"><span data-stu-id="abea0-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="abea0-162">Anote el **nombre del grupo de recursos**, el **nombre de la cuenta de almacenamiento** y la **clave de la cuenta de almacenamiento** que genere el script.</span><span class="sxs-lookup"><span data-stu-id="abea0-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="abea0-163">Los necesitará en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="abea0-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="abea0-164">Si necesita ayuda con el script de PowerShell, consulte [Uso de Azure PowerShell con Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="abea0-165">Si desea usar la CLI de Azure en su lugar, consulte la sección [Apéndice](#appendix) del script de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="abea0-166">**Para examinar la cuenta de almacenamiento y el contenido**</span><span class="sxs-lookup"><span data-stu-id="abea0-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="abea0-167">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abea0-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abea0-168">Haga clic en **Grupos de recursos** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="abea0-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="abea0-169">Haga doble clic en el nombre del grupo de recursos que creó en el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abea0-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="abea0-170">Utilice el filtro si se muestran demasiados grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="abea0-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="abea0-171">En el icono **Recursos** , aparecerá un recurso a menos que comparta el grupo de recursos con otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="abea0-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="abea0-172">Ese recurso es la cuenta de almacenamiento con el nombre que especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="abea0-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="abea0-173">Haga clic en el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-173">Click the storage account name.</span></span>
5. <span data-ttu-id="abea0-174">Haga clic en los iconos **Blobs** .</span><span class="sxs-lookup"><span data-stu-id="abea0-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="abea0-175">Haga clic en el contenedor **adfgetstarted** .</span><span class="sxs-lookup"><span data-stu-id="abea0-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="abea0-176">Verá dos carpetas: **inputdata** y **script**.</span><span class="sxs-lookup"><span data-stu-id="abea0-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="abea0-177">Abra la carpeta y compruebe los archivos en las carpetas.</span><span class="sxs-lookup"><span data-stu-id="abea0-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="abea0-178">La carpeta inputdata contiene el archivo input.log con datos de entrada, mientras que la carpeta script contiene el archivo de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="abea0-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="abea0-179">Creación de una factoría de datos mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abea0-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="abea0-180">Con la cuenta de almacenamiento, los datos de entrada y el script de HiveQL preparados, está listo para crear Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="abea0-181">Existen varios métodos para crear Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="abea0-182">En este tutorial, creará una factoría de datos mediante la implementación de una plantilla de Azure Resource Manager mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="abea0-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="abea0-183">También puede implementar una plantilla de Resource Manager mediante la [CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) y [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="abea0-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="abea0-184">Para otros métodos de creación de Data Factory, vea [Tutorial: creación de la  primera Data Factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="abea0-185">Haga clic en la imagen siguiente para iniciar sesión en Azure y abrir la plantilla de Resource Manager en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="abea0-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="abea0-186">La plantilla se encuentra en https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="abea0-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="abea0-187">Consulte la sección [Entidades de Data Factory en la plantilla](#data-factory-entities-in-the-template) para obtener información detallada acerca de las entidades definidas en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="abea0-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="abea0-188">Seleccione la opción **Usar existente** de la configuración de **Grupo de recursos** y seleccione el nombre del grupo de recursos que creó en el paso anterior (mediante el script de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="abea0-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="abea0-189">Escriba el nombre de la factoría de datos (**Nombre de factoría de datos**).</span><span class="sxs-lookup"><span data-stu-id="abea0-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="abea0-190">Este nombre debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="abea0-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="abea0-191">Escriba el **nombre de la cuenta de almacenamiento** y la **clave de la cuenta de almacenamiento** que anotó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="abea0-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="abea0-192">Tras leer los **términos y condiciones** seleccione **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="abea0-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="abea0-193">Seleccione la opción **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="abea0-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="abea0-194">Haga clic en **Comprar o crear**.</span><span class="sxs-lookup"><span data-stu-id="abea0-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="abea0-195">Verá un icono en el Panel denominado **Realización de implementación de la plantilla**.</span><span class="sxs-lookup"><span data-stu-id="abea0-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="abea0-196">Espere a que se abra la hoja **Grupo de recursos** de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="abea0-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="abea0-197">También puede hacer clic en el icono con el mismo nombre que el grupo de recursos para abrir la hoja del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="abea0-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="abea0-198">Si la hoja del grupo de recursos no está abierta, haga clic en el icono para abrir el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="abea0-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="abea0-199">Ahora verá un recurso de Data Factory más, además del recurso de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="abea0-200">Haga clic en el nombre de la factoría de datos (el valor que especificó en el parámetro **Nombre de factoría de datos**).</span><span class="sxs-lookup"><span data-stu-id="abea0-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="abea0-201">En la hoja Data Factory, haga clic en el icono **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="abea0-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="abea0-202">El diagrama muestra una actividad con un conjunto de datos de entrada y un conjunto de datos de salida:</span><span class="sxs-lookup"><span data-stu-id="abea0-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagrama de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="abea0-204">Los nombres se definen en la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abea0-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="abea0-205">Haga doble clic en **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="abea0-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="abea0-206">En los **segmentos actualizados recientemente**, verá un segmento.</span><span class="sxs-lookup"><span data-stu-id="abea0-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="abea0-207">Si el estado es **En curso**, espere hasta que se cambie a **Listo**.</span><span class="sxs-lookup"><span data-stu-id="abea0-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="abea0-208">Se suele tarda aproximadamente **20 minutos** en crear un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abea0-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="abea0-209">Comprobación de la salida de Data Factory</span><span class="sxs-lookup"><span data-stu-id="abea0-209">Check the data factory output</span></span>

1. <span data-ttu-id="abea0-210">Utilice el mismo procedimiento en la última sesión para comprobar el contenido de los contenedores adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="abea0-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="abea0-211">Hay dos nuevos contenedores además de **adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="abea0-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="abea0-212">Un contenedor con nombre que sigue el patrón: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="abea0-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="abea0-213">Este es el contenedor predeterminado del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abea0-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="abea0-214">adfjobs: este es el contenedor de los registros de trabajo de ADF.</span><span class="sxs-lookup"><span data-stu-id="abea0-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="abea0-215">La salida de Data Factory se almacena en **afgetstarted**, tal lo configuró en la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abea0-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="abea0-216">Haga clic en **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="abea0-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="abea0-217">Haga doble clic en **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="abea0-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="abea0-218">Se ve una carpeta **year=2014**, ya que todos los registros de web son del año 2014.</span><span class="sxs-lookup"><span data-stu-id="abea0-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Salida de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="abea0-220">Si profundiza en la lista, verá 3 carpetas de enero, febrero y marzo.</span><span class="sxs-lookup"><span data-stu-id="abea0-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="abea0-221">Además, hay un registro para cada mes.</span><span class="sxs-lookup"><span data-stu-id="abea0-221">And there is a log for each month.</span></span>

    ![Salida de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="abea0-223">Entidades de Data Factory en la plantilla</span><span class="sxs-lookup"><span data-stu-id="abea0-223">Data Factory entities in the template</span></span>
<span data-ttu-id="abea0-224">Este es el aspecto de la plantilla de Resource Manager de nivel superior para una factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="abea0-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="abea0-225">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="abea0-225">Define data factory</span></span>
<span data-ttu-id="abea0-226">Puede definir una factoría de datos en la plantilla de Resource Manager como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="abea0-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="abea0-227">dataFactoryName es el nombre de la factoría de datos que se especifica al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="abea0-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="abea0-228">Data Factory solo se admite actualmente en las zonas del este de EE. UU., oeste de EE. UU. y Europa del Norte.</span><span class="sxs-lookup"><span data-stu-id="abea0-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="abea0-229">Definición de entidades en la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="abea0-229">Defining entities within the data factory</span></span>
<span data-ttu-id="abea0-230">Las siguientes entidades de Data Factory se definen en la plantilla JSON:</span><span class="sxs-lookup"><span data-stu-id="abea0-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="abea0-231">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="abea0-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="abea0-232">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="abea0-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="abea0-233">Conjunto de datos de entrada de blob de Azure:</span><span class="sxs-lookup"><span data-stu-id="abea0-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="abea0-234">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="abea0-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="abea0-235">Canalización de datos con una actividad de copia</span><span class="sxs-lookup"><span data-stu-id="abea0-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="abea0-236">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="abea0-236">Azure Storage linked service</span></span>
<span data-ttu-id="abea0-237">El servicio vinculado Azure Storage vincula una cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="abea0-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="abea0-238">En este tutorial, la misma cuenta de almacenamiento se usa como la cuenta de almacenamiento para HDInsight predeterminada, el almacenamiento de datos de entrada y el almacenamiento de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="abea0-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="abea0-239">Por consiguiente, se define solo un servicio vinculado Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="abea0-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="abea0-240">En la definición del servicio vinculado, especifique el nombre y la clave de su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="abea0-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="abea0-241">Consulte [Servicio vinculado de Azure Storage](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) para más información sobre las propiedades JSON usadas para definir un servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="abea0-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="abea0-242">**connectionString** usa los parámetros storageAccountName y storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="abea0-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="abea0-243">Especifique los valores de estos parámetros al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="abea0-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="abea0-244">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="abea0-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="abea0-245">En la definición del servicio vinculado de HDInsight a petición, especifique los valores de los parámetros de configuración que usa el servicio Data Factory para crear un clúster de Hadoop de HDInsight en runtime.</span><span class="sxs-lookup"><span data-stu-id="abea0-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="abea0-246">Consulte el artículo [Servicios vinculados de proceso](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para más información sobre las propiedades JSON que se usan para definir un servicio vinculado a petición de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abea0-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="abea0-247">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="abea0-247">Note the following points:</span></span>

* <span data-ttu-id="abea0-248">Data Factory crea automáticamente un cluster de HDInsight **basado en Linux**.</span><span class="sxs-lookup"><span data-stu-id="abea0-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="abea0-249">El clúster de Hadoop de HDInsight se crea en la misma región que la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="abea0-250">Observe la configuración de *timeToLive* .</span><span class="sxs-lookup"><span data-stu-id="abea0-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="abea0-251">Data Factory elimina el clúster automáticamente después de que esté inactivo durante 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="abea0-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="abea0-252">El clúster de HDInsight crea un **contenedor predeterminado** en el almacenamiento de blobs que especificó en JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="abea0-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="abea0-253">HDInsight no elimina este contenedor cuando se elimina el clúster.</span><span class="sxs-lookup"><span data-stu-id="abea0-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="abea0-254">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="abea0-254">This behavior is by design.</span></span> <span data-ttu-id="abea0-255">Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez tenga que procesarse un segmento, a menos que haya un clúster existente activo (**timeToLive**), que se elimina cuando finaliza el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="abea0-256">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="abea0-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abea0-257">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="abea0-258">Si no los necesita para solucionar problemas de trabajos, puede eliminarlos para reducir el costo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="abea0-259">Los nombres de estos contenedores siguen este patrón: "adf**nombredefactoría dedatos**-**nombredelserviciovinculado**-marcadefechayhora".</span><span class="sxs-lookup"><span data-stu-id="abea0-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="abea0-260">Use herramientas como el [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) para eliminar contenedores de Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="abea0-261">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="abea0-261">Azure blob input dataset</span></span>
<span data-ttu-id="abea0-262">En la definición del conjunto de datos de entrada, especifique los nombres del contenedor de blobs, la carpeta y el archivo que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="abea0-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="abea0-263">Consulte las [propiedades del conjunto de datos de Azure Blob](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para más información sobre las propiedades JSON usadas para definir un conjunto de datos de Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="abea0-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="abea0-264">Observe la siguiente configuración concreta en la definición de JSON:</span><span class="sxs-lookup"><span data-stu-id="abea0-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="abea0-265">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="abea0-265">Azure Blob output dataset</span></span>
<span data-ttu-id="abea0-266">En la definición del conjunto de datos de salida, especifique los nombres del contenedor de blobs y de la carpeta que contiene los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="abea0-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="abea0-267">Consulte las [propiedades del conjunto de datos de Azure Blob](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para más información sobre las propiedades JSON usadas para definir un conjunto de datos de Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="abea0-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="abea0-268">folderPath especifica la ruta de acceso a la carpeta que contiene los datos de salida:</span><span class="sxs-lookup"><span data-stu-id="abea0-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="abea0-269">La configuración de [disponibilidad del conjunto de datos](../data-factory/data-factory-create-datasets.md#dataset-availability) es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="abea0-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="abea0-270">En Data Factory de Azure, la disponibilidad del conjunto de datos de salida activa la canalización.</span><span class="sxs-lookup"><span data-stu-id="abea0-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="abea0-271">En este ejemplo, el segmento se genera el último día de cada mes (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="abea0-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="abea0-272">Para obtener más información, vea [Programación y ejecución de Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="abea0-273">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="abea0-273">Data pipeline</span></span>
<span data-ttu-id="abea0-274">Defina una canalización que transforme los datos mediante la ejecución de un script de Hive en un clúster de Azure HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="abea0-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="abea0-275">Consulte [JSON de canalización](../data-factory/data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos JSON que se usan para definir una canalización en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="abea0-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="abea0-276">La canalización contiene una actividad, la actividad de HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="abea0-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="abea0-277">Como las fechas de inicio y finalización están en enero de 2016, se procesan los datos de un solo mes (un segmento).</span><span class="sxs-lookup"><span data-stu-id="abea0-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="abea0-278">Las fechas de *inicio* y *finalización* de la actividad tienen una fecha pasada, por lo que Data Factory procesa los datos del mes de inmediato.</span><span class="sxs-lookup"><span data-stu-id="abea0-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="abea0-279">Si el extremo es una fecha futura, Data Factory creará otro segmento cuando llegue la hora.</span><span class="sxs-lookup"><span data-stu-id="abea0-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="abea0-280">Para obtener más información, vea [Programación y ejecución de Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="abea0-281">Limpieza del tutorial</span><span class="sxs-lookup"><span data-stu-id="abea0-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="abea0-282">Elimine los contenedores de blobs creados por el clúster de HDInsight a petición</span><span class="sxs-lookup"><span data-stu-id="abea0-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="abea0-283">Con el servicio vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento debe procesarse, a menos que haya un clúster existente activo (timeToLive), y el clúster se elimina cuando se realiza el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="abea0-284">Para cada clúster, Azure Data Factory crea un contenedor de blobs en Azure Blob Storage que se usa como cuenta de almacenamiento predeterminada del clúster.</span><span class="sxs-lookup"><span data-stu-id="abea0-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="abea0-285">Aunque se elimine el clúster de HDInsight, el contenedor de almacenamiento de blobs predeterminado y la cuenta de almacenamiento asociada no se eliminan.</span><span class="sxs-lookup"><span data-stu-id="abea0-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="abea0-286">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="abea0-286">This behavior is by design.</span></span> <span data-ttu-id="abea0-287">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="abea0-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="abea0-288">Si no los necesita para solucionar problemas de trabajos, puede eliminarlos para reducir el costo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="abea0-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="abea0-289">Los nombres de estos contenedores siguen un patrón: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="abea0-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="abea0-290">Elimine las carpetas **adfjobs** y **adfyourdatafactoryname-linkedservicename-datetimestamp**.</span><span class="sxs-lookup"><span data-stu-id="abea0-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="abea0-291">El contenedor adfjobs contiene registros de trabajo de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="abea0-292">Eliminar el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="abea0-292">Delete the resource group</span></span>
<span data-ttu-id="abea0-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) se usa para implementar, administrar y supervisar una solución como un grupo.</span><span class="sxs-lookup"><span data-stu-id="abea0-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="abea0-294">Al eliminar un grupo de recursos, se eliminan todos sus componentes.</span><span class="sxs-lookup"><span data-stu-id="abea0-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="abea0-295">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abea0-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abea0-296">Haga clic en **Grupos de recursos** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="abea0-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="abea0-297">Haga clic en el nombre del grupo de recursos que creó en el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abea0-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="abea0-298">Utilice el filtro si se muestran demasiados grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="abea0-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="abea0-299">El grupo de recursos se abre en una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="abea0-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="abea0-300">En el icono **Recursos** , aparecerá la cuenta de almacenamiento predeterminada y Data Factory a menos que comparta el grupo de recursos con otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="abea0-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="abea0-301">Haga clic en **Eliminar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="abea0-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="abea0-302">Así se eliminan también la cuenta de almacenamiento y los datos almacenados en ella.</span><span class="sxs-lookup"><span data-stu-id="abea0-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="abea0-303">Escriba el nombre del grupo de recursos para confirmar la eliminación y, después, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="abea0-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="abea0-304">Si no desea eliminar la cuenta de almacenamiento al eliminar el grupo de recursos, considere la siguiente arquitectura mediante la separación de los datos empresariales de la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="abea0-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="abea0-305">En este caso, tiene un grupo de recursos para la cuenta de almacenamiento con los datos empresariales y el otro grupo de recursos para la cuenta de almacenamiento predeterminada del servicio vinculado de HDInsight y Data Factory.</span><span class="sxs-lookup"><span data-stu-id="abea0-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="abea0-306">Cuando se elimina el segundo grupo de recursos, no afecta a la cuenta de almacenamiento de datos empresariales.</span><span class="sxs-lookup"><span data-stu-id="abea0-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="abea0-307">Para ello:</span><span class="sxs-lookup"><span data-stu-id="abea0-307">To do so:</span></span>

* <span data-ttu-id="abea0-308">Agregue lo siguiente al grupo de recursos de nivel superior junto con el recurso Microsoft.DataFactory/datafactories en la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abea0-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="abea0-309">Crea una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="abea0-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="abea0-310">Agregue un nuevo punto de servicio vinculado a la nueva cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="abea0-310">Add a new linked service point to the new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="abea0-311">Configure el servicio vinculado bajo demanda de HDInsight con un dependsOn y un additionalLinkedServiceNames adicionales:</span><span class="sxs-lookup"><span data-stu-id="abea0-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="abea0-312">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abea0-312">Next steps</span></span>
<span data-ttu-id="abea0-313">En este artículo, ha aprendido cómo utilizar la Data Factory de Azure para crear el clúster de HDInsight bajo demanda para procesar los trabajos de Hive.</span><span class="sxs-lookup"><span data-stu-id="abea0-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="abea0-314">Para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="abea0-314">To read more:</span></span>

* [<span data-ttu-id="abea0-315">Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="abea0-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="abea0-316">Creación de clústeres de Hadoop basados en Linux en HDInsight</span><span class="sxs-lookup"><span data-stu-id="abea0-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="abea0-317">Documentación de HDInsight</span><span class="sxs-lookup"><span data-stu-id="abea0-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="abea0-318">Documentación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="abea0-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="abea0-319">Anexo</span><span class="sxs-lookup"><span data-stu-id="abea0-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="abea0-320">Script de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="abea0-320">Azure CLI script</span></span>
<span data-ttu-id="abea0-321">Para realizar el tutorial se puede utilizar la CLI de Azure, en lugar de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abea0-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="abea0-322">Para usar la CLI de Azure, instálela siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="abea0-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="abea0-323">Use la CLI de Azure para preparar el almacenamiento y copiar los archivos</span><span class="sxs-lookup"><span data-stu-id="abea0-323">Use Azure CLI to prepare the storage and copy the files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="abea0-324">El nombre del contenedor es *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="abea0-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="abea0-325">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="abea0-325">Keep it as it is.</span></span> <span data-ttu-id="abea0-326">De lo contrario, tendrá que actualizar la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abea0-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="abea0-327">Si necesita ayuda con este script de la CLI, vea [Uso de la CLI de Azure con Almacenamiento de Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="abea0-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
