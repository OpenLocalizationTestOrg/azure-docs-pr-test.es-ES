---
title: "aaaCreate clústeres de Hadoop de petición con factoría de datos: HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate clústeres de petición Hadoop en HDInsight con Data Factory de Azure."
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
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="a261c-103">Creación de clústeres de Hadoop en HDInsight mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a261c-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a261c-104">[Factoría de datos de Azure](../data-factory/data-factory-introduction.md) es un servicio de integración de datos en la nube que organiza y automatiza el movimiento de Hola y la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="a261c-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="a261c-105">Puede crear un tooprocess de just-in-time de clúster de Hadoop de HDInsight un segmento de datos de entrada y eliminar el clúster de hello cuando se completa el procesamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="a261c-106">Algunas de las ventajas de hello del uso de un clúster de Hadoop de HDInsight a petición son:</span><span class="sxs-lookup"><span data-stu-id="a261c-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="a261c-107">Pago solo para el trabajo de temporizador de Hola se está ejecutando en hello Hadoop de HDInsight de clúster (más un breve tiempo de inactividad configurable).</span><span class="sxs-lookup"><span data-stu-id="a261c-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="a261c-108">facturación de Hola para clústeres de HDInsight es proporcional por minuto, independientemente de si se usa o no.</span><span class="sxs-lookup"><span data-stu-id="a261c-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="a261c-109">Cuando se usa un servicio vinculado de HDInsight de petición de factoría de datos, clústeres de Hola se crean a petición.</span><span class="sxs-lookup"><span data-stu-id="a261c-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="a261c-110">Y clústeres de Hola se eliminan automáticamente cuando se completan los trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="a261c-111">Por lo tanto, solo se paga por trabajo Hola duración y el tiempo de inactividad breve de hello (opción de período de vida).</span><span class="sxs-lookup"><span data-stu-id="a261c-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="a261c-112">Puede crear un flujo de trabajo mediante una canalización de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a261c-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="a261c-113">Por ejemplo, puede tener datos de toocopy de canalización de saludo de un tooan de SQL Server local almacenamiento de blobs de Azure, proceso Hola datos ejecutando un script de Hive y un script de Pig en un clúster de Hadoop de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="a261c-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a261c-114">A continuación, copie el resultado de hello datos tooan almacenamiento de datos de SQL Azure para tooconsume de aplicaciones de BI.</span><span class="sxs-lookup"><span data-stu-id="a261c-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="a261c-115">Puede programar Hola flujo de trabajo toorun periódicamente (cada hora, diariamente, semanalmente, mensualmente, etcetera).</span><span class="sxs-lookup"><span data-stu-id="a261c-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="a261c-116">En Azure Data Factory, una factoría de datos puede tener una o varias canalizaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="a261c-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="a261c-117">Una canalización de datos consta de una o varias actividades.</span><span class="sxs-lookup"><span data-stu-id="a261c-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="a261c-118">Hay dos tipos de actividades: [actividades de movimiento de datos](../data-factory/data-factory-data-movement-activities.md) y [actividades de transformación de datos](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="a261c-119">Utiliza los datos de toomove de actividades (en la actualidad, solo copia) de movimiento de datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="a261c-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="a261c-120">Usar datos de tootransform o proceso de las actividades de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="a261c-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="a261c-121">Actividad de Hive de HDInsight es una de las actividades de transformación de hello admitidas factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="a261c-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="a261c-122">Usar la actividad de transformación de Hive de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a261c-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="a261c-123">Puede configurar una toouse de actividad de hive su propio clúster de Hadoop de HDInsight o un clúster de Hadoop de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="a261c-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a261c-124">En este tutorial, actividad de Hive en la canalización de factoría de datos de Hola Hola es toouse configurado un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="a261c-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="a261c-125">Por lo tanto, cuando la actividad hello ejecuta tooprocess un segmento de datos, sucede lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a261c-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="a261c-126">Automáticamente se crea un clúster de Hadoop de HDInsight de sector hello tooprocess just-in-time.</span><span class="sxs-lookup"><span data-stu-id="a261c-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="a261c-127">datos de entrada de Hola se procesan mediante la ejecución de un script de HiveQL en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="a261c-128">Hola clúster de Hadoop de HDInsight se elimina cuando ha finalizado el procesamiento de Hola y clúster Hola está inactivo durante la cantidad de hello configurado de tiempo (valor timeToLive).</span><span class="sxs-lookup"><span data-stu-id="a261c-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="a261c-129">Si el segmento de datos de hello siguiente está disponible para su procesamiento con en este tiempo de inactividad timeToLive, hello mismo clúster es tooprocess usado Hola sector.</span><span class="sxs-lookup"><span data-stu-id="a261c-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="a261c-130">En este tutorial, Hola script de HiveQL asociado a la actividad de hive hello realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="a261c-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="a261c-131">Crea una tabla externa que Hola de referencias de datos de registro de web sin formato almacenados en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="a261c-132">Datos sin procesar de saludo de particiones por año y mes.</span><span class="sxs-lookup"><span data-stu-id="a261c-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="a261c-133">Hola a almacenes de datos particionados en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="a261c-134">En este tutorial, Hola script de HiveQL asociado a la actividad de hive hello crea una tabla externa que Hola de referencias de datos de registro de web sin formato almacenados en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="a261c-135">Aquí son filas de ejemplo de Hola para cada mes en el archivo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="a261c-136">particiones de script de HiveQL Hola Hola datos sin procesar por año y mes.</span><span class="sxs-lookup"><span data-stu-id="a261c-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="a261c-137">Crea tres carpetas de salida basadas en la entrada anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="a261c-138">Cada carpeta contiene un archivo con las entradas de cada mes.</span><span class="sxs-lookup"><span data-stu-id="a261c-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="a261c-139">Para obtener una lista de actividades de transformación de datos de factoría de datos en la actividad de tooHive de adición, vea [transformar y analizar con Data Factory de Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a261c-140">Actualmente, solo se puede crear un clúster de HDInsight versión 3.2 desde Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a261c-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a261c-141">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a261c-141">Prerequisites</span></span>
<span data-ttu-id="a261c-142">Antes de comenzar con instrucciones de hello en este artículo, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a261c-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="a261c-143">[Suscripción de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a261c-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a261c-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a261c-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="a261c-145">Preparación de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a261c-145">Prepare storage account</span></span>
<span data-ttu-id="a261c-146">Puede usar las cuentas de almacenamiento de toothree en este escenario:</span><span class="sxs-lookup"><span data-stu-id="a261c-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="a261c-147">cuenta de almacenamiento predeterminada para el clúster de HDInsight de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="a261c-148">cuenta de almacenamiento de datos de entrada de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-148">storage account for hello input data</span></span>
- <span data-ttu-id="a261c-149">cuenta de almacenamiento de datos de salida de hello</span><span class="sxs-lookup"><span data-stu-id="a261c-149">storage account for hello output data</span></span>

<span data-ttu-id="a261c-150">tutorial de hello toosimplify, use una cuenta tooserve Hola tres propósitos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a261c-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="a261c-151">script de ejemplo de Hola PowerShell de Azure en esta sección incluyen realiza Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="a261c-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="a261c-152">Inicie sesión en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a261c-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="a261c-153">Cree un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="a261c-154">Cree una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="a261c-155">Crear un contenedor de Blob en la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="a261c-156">Copie Hola después de contenedor de blobs de toohello de dos archivos:</span><span class="sxs-lookup"><span data-stu-id="a261c-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="a261c-157">Archivo de datos de entrada: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="a261c-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="a261c-158">Script de HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="a261c-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="a261c-159">Ambos archivos se almacenan en un contenedor de blobs público.</span><span class="sxs-lookup"><span data-stu-id="a261c-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="a261c-160">**tooprepare Hola almacenamiento y copiar Hola archivos mediante Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="a261c-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a261c-161">Especifique nombres de cuenta de almacenamiento de Azure de Hola que va a crear script de Hola y el grupo de recursos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="a261c-162">Anote **nombre del grupo de recursos**, **nombre de la cuenta de almacenamiento**, y **clave de la cuenta de almacenamiento** arroja script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="a261c-163">Se necesita en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="a261c-164">Si necesita ayuda con la secuencia de comandos de PowerShell de hello, consulte [hello mediante PowerShell de Azure con el almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="a261c-165">Si le gustaría toouse CLI de Azure en su lugar, vea hello [apéndice](#appendix) sección para hello secuencia de comandos de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="a261c-166">**tooexamine Hola almacenamiento cuenta Hola tipos de contenido y**</span><span class="sxs-lookup"><span data-stu-id="a261c-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="a261c-167">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a261c-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a261c-168">Haga clic en **grupos de recursos** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="a261c-169">Haga doble clic en el nombre del grupo de recursos de Hola que creó en el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a261c-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="a261c-170">Utilice el filtro de hello si tiene demasiados grupos de recursos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="a261c-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="a261c-171">En hello **recursos** mosaico, debe tener un recurso, a menos que el grupo de recursos de Hola se comparte con otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="a261c-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="a261c-172">Ese recurso es la cuenta de almacenamiento de hello con nombre hello especificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a261c-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="a261c-173">Haga clic en el nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="a261c-174">Haga clic en hello **Blobs** iconos.</span><span class="sxs-lookup"><span data-stu-id="a261c-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="a261c-175">Haga clic en hello **adfgetstarted** contenedor.</span><span class="sxs-lookup"><span data-stu-id="a261c-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="a261c-176">Verá dos carpetas: **inputdata** y **script**.</span><span class="sxs-lookup"><span data-stu-id="a261c-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="a261c-177">Abra la carpeta de Hola y compruebe Hola archivos en carpetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="a261c-178">Hola inputdata contiene archivos de hello input.log con datos de entrada y la carpeta de script de Hola contiene el archivo de script de HiveQL Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="a261c-179">Creación de una factoría de datos mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a261c-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="a261c-180">Con la cuenta de almacenamiento de hello, datos de entrada de Hola y Hola script de HiveQL preparado, está listo toocreate un generador de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="a261c-181">Existen varios métodos para crear Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a261c-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="a261c-182">En este tutorial, creará una factoría de datos mediante la implementación de una plantilla de Azure Resource Manager con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="a261c-183">También puede implementar una plantilla de Resource Manager mediante la [CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) y [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="a261c-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="a261c-184">Para otros métodos de creación de Data Factory, vea [Tutorial: creación de la  primera Data Factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="a261c-185">Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="a261c-186">plantilla de Hola se encuentra en https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="a261c-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="a261c-187">Vea hello [las entidades de la factoría de datos de plantilla de hello](#data-factory-entities-in-the-template) sección para obtener información detallada sobre las entidades definidas en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="a261c-188">Seleccione **usar existente** opción para hello **grupo de recursos** configuración y el nombre de select Hola Hola del grupo de recursos creado en el paso anterior hello (mediante el script de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a261c-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="a261c-189">Escriba un nombre para la factoría de datos de hello (**nombre de la factoría de datos**).</span><span class="sxs-lookup"><span data-stu-id="a261c-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="a261c-190">Este nombre debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="a261c-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="a261c-191">Escriba hello **nombre de la cuenta de almacenamiento** y **clave de la cuenta de almacenamiento** anotó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="a261c-192">Seleccione **muestro mi conformidad toohello términos y condiciones** indicados anteriormente después de leer **términos y condiciones**.</span><span class="sxs-lookup"><span data-stu-id="a261c-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="a261c-193">Seleccione **toodashboard Pin** opción.</span><span class="sxs-lookup"><span data-stu-id="a261c-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="a261c-194">Haga clic en **Comprar o crear**.</span><span class="sxs-lookup"><span data-stu-id="a261c-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="a261c-195">Verá un icono en hello panel denominado **implementación de plantilla de implementación de**.</span><span class="sxs-lookup"><span data-stu-id="a261c-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="a261c-196">Espere hasta que hello **grupo de recursos** abre el módulo para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a261c-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="a261c-197">También puede hacer clic en icono Hola titulada como su hoja de grupo de recursos grupo nombre tooopen Hola recursos.</span><span class="sxs-lookup"><span data-stu-id="a261c-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="a261c-198">Si la hoja de grupo de recursos de hello ya no está abierto, haga clic en grupo de recursos de hello mosaico tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="a261c-199">Ahora verá un recurso de factoría de datos más aparece además toohello recurso de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a261c-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="a261c-200">Haga clic en nombre de saludo de la factoría de datos (valor especificado para hello **nombre de la factoría de datos** parámetro).</span><span class="sxs-lookup"><span data-stu-id="a261c-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="a261c-201">En la hoja de la factoría de datos de hello, haga clic en hello **diagrama** icono.</span><span class="sxs-lookup"><span data-stu-id="a261c-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="a261c-202">diagrama de Hello muestra una actividad con un conjunto de datos de entrada y un conjunto de datos de salida:</span><span class="sxs-lookup"><span data-stu-id="a261c-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagrama de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="a261c-204">Hola nombres se definen en la plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="a261c-205">Haga doble clic en **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="a261c-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="a261c-206">En hello **recientes actualizan sectores**, verá un sector.</span><span class="sxs-lookup"><span data-stu-id="a261c-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="a261c-207">Si el estado de hello es **en curso**, espere hasta que se cambie demasiado**listo**.</span><span class="sxs-lookup"><span data-stu-id="a261c-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="a261c-208">Proceso suele tardar aproximadamente **20 minutos** toocreate un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a261c-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="a261c-209">Compruebe la salida de factoría de datos de hello</span><span class="sxs-lookup"><span data-stu-id="a261c-209">Check hello data factory output</span></span>

1. <span data-ttu-id="a261c-210">Use Hola mismo procedimiento descrito en hello última sesión toocheck Hola contenedores hello adfgetstarted del contenedor de.</span><span class="sxs-lookup"><span data-stu-id="a261c-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="a261c-211">Hay dos nuevos contenedores además demasiado**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="a261c-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="a261c-212">Un contenedor con nombre que sigue el patrón de hello: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="a261c-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="a261c-213">Este contenedor es el contenedor predeterminado de hello para el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="a261c-214">adfjobs: este contenedor es el contenedor de Hola Hola ADF registros de trabajos.</span><span class="sxs-lookup"><span data-stu-id="a261c-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="a261c-215">resultado de factoría de datos de Hola se almacena en **afgetstarted** que haya configurado en la plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="a261c-216">Haga clic en **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="a261c-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="a261c-217">Haga doble clic en **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="a261c-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="a261c-218">Verá un **año = 2014** carpeta porque todos los registros de hello web con una fecha en el año 2014.</span><span class="sxs-lookup"><span data-stu-id="a261c-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Salida de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="a261c-220">Si se profundiza lista hello, verá tres carpetas de enero, febrero y marzo.</span><span class="sxs-lookup"><span data-stu-id="a261c-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="a261c-221">Además, hay un registro para cada mes.</span><span class="sxs-lookup"><span data-stu-id="a261c-221">And there is a log for each month.</span></span>

    ![Salida de la canalización de la actividad de Hive bajo demanda de HDInsight para Data Factory de Azure](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="a261c-223">Entidades de generador de datos en la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="a261c-224">Aquí es cómo Hola plantilla nivel superior de administrador de recursos de una factoría de datos tiene un aspecto como:</span><span class="sxs-lookup"><span data-stu-id="a261c-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="a261c-225">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="a261c-225">Define data factory</span></span>
<span data-ttu-id="a261c-226">Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="a261c-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="a261c-227">Hola dataFactoryName es nombre Hola Hola factoría de datos que especifique al implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="a261c-228">Factoría de datos está actualmente solo se admite en regiones del este de EE., oeste de Estados Unidos y Europa del Norte Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="a261c-229">Definir las entidades de la factoría de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="a261c-230">Hello siguientes entidades de la factoría de datos definidas en hello JSON plantilla:</span><span class="sxs-lookup"><span data-stu-id="a261c-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="a261c-231">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a261c-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="a261c-232">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="a261c-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="a261c-233">Conjunto de datos de entrada de blob de Azure:</span><span class="sxs-lookup"><span data-stu-id="a261c-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="a261c-234">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="a261c-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="a261c-235">Canalización de datos con una actividad de copia</span><span class="sxs-lookup"><span data-stu-id="a261c-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="a261c-236">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a261c-236">Azure Storage linked service</span></span>
<span data-ttu-id="a261c-237">Hola almacenamiento de Azure vinculados a los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello.</span><span class="sxs-lookup"><span data-stu-id="a261c-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="a261c-238">En este tutorial, hello misma cuenta de almacenamiento se usa como cuenta de almacenamiento de HDInsight de hello predeterminada, el almacenamiento de datos de entrada y almacenamiento de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="a261c-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="a261c-239">Por consiguiente, se define solo un servicio vinculado Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a261c-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="a261c-240">En definición de servicio vinculado de hello, especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="a261c-241">Vea [servicio vinculado de almacenamiento de Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="a261c-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

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
<span data-ttu-id="a261c-242">Hola **connectionString** usa Hola parámetros storageAccountName y storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="a261c-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="a261c-243">Especifique valores para estos parámetros durante la implementación de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="a261c-244">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="a261c-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="a261c-245">Hola HDInsight a petición había vinculada definición de servicio, especifique valores para parámetros de configuración que se utilizan por toocreate de servicio de factoría de datos de hello clúster de Hadoop de HDInsight en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a261c-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="a261c-246">Vea [servicios vinculados de proceso](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) un servicio vinculado de HDInsight a petición del artículo para obtener más información acerca de toodefine de propiedades que se usan JSON.</span><span class="sxs-lookup"><span data-stu-id="a261c-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="a261c-247">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="a261c-247">Note hello following points:</span></span>

* <span data-ttu-id="a261c-248">Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight para usted.</span><span class="sxs-lookup"><span data-stu-id="a261c-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="a261c-249">Hello clúster de Hadoop de HDInsight se crea en Hola misma región que la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="a261c-250">Hola aviso *timeToLive* configuración.</span><span class="sxs-lookup"><span data-stu-id="a261c-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="a261c-251">factoría de datos de Hello elimina clúster Hola automáticamente después de clúster de saludo se está inactivo durante 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="a261c-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="a261c-252">clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="a261c-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="a261c-253">HDInsight no elimine este contenedor cuando se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="a261c-254">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="a261c-254">This behavior is by design.</span></span> <span data-ttu-id="a261c-255">Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="a261c-256">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="a261c-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a261c-257">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="a261c-258">Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="a261c-259">nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="a261c-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="a261c-260">Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="a261c-261">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="a261c-261">Azure blob input dataset</span></span>
<span data-ttu-id="a261c-262">En la definición de conjunto de datos de entrada de hello, especifique nombres Hola de contenedor de blobs, carpeta y archivo que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="a261c-263">Vea [propiedades de conjunto de datos de Blob de Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

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

<span data-ttu-id="a261c-264">Tenga en cuenta Hola después de una configuración específica en la definición de JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="a261c-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a261c-265">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="a261c-265">Azure Blob output dataset</span></span>
<span data-ttu-id="a261c-266">En la definición de conjunto de datos de salida de hello, especificar nombres de Hola de contenedor de blob y la carpeta que contiene los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a261c-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="a261c-267">Vea [propiedades de conjunto de datos de Blob de Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="a261c-268">Hola folderPath especifica hello toohello ruta de acceso que contiene los datos de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="a261c-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="a261c-269">Hola [disponibilidad del conjunto de datos](../data-factory/data-factory-create-datasets.md#dataset-availability) configuración es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a261c-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="a261c-270">En la factoría de datos de Azure, canalización de salida de conjunto de datos disponibilidad unidades Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="a261c-271">En este ejemplo, hello segmento se genera mensualmente Hola último día del mes (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="a261c-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="a261c-272">Para obtener más información, vea [Programación y ejecución de Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="a261c-273">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="a261c-273">Data pipeline</span></span>
<span data-ttu-id="a261c-274">Defina una canalización que transforme los datos mediante la ejecución de un script de Hive en un clúster de Azure HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="a261c-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="a261c-275">Vea [JSON de canalización](../data-factory/data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos que se usan de JSON toodefine una canalización en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a261c-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

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

<span data-ttu-id="a261c-276">canalización de Hello contiene una actividad, actividad de HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="a261c-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="a261c-277">Como las fechas de inicio y finalización están en enero de 2016, se procesan los datos de un solo mes (un segmento).</span><span class="sxs-lookup"><span data-stu-id="a261c-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="a261c-278">Ambos *iniciar* y *final* de actividad hello tienen una fecha pasada, por lo que Hola factoría de datos procesa los datos de mes de hello inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="a261c-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="a261c-279">Si el final de hello es una fecha futura, factoría de datos de hello crea otro segmento cuando llega la hora de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="a261c-280">Para obtener más información, vea [Programación y ejecución de Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="a261c-281">Limpiar el tutorial Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="a261c-282">Eliminar contenedores de blobs de hello creados por clúster de HDInsight a petición</span><span class="sxs-lookup"><span data-stu-id="a261c-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="a261c-283">Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (timeToLive); y clúster Hola se elimina cuando se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="a261c-284">Para cada clúster, Data Factory de Azure crea un contenedor de blobs en almacenamiento de blobs de Azure que se usará como cuenta de almacenamiento (SAN) de hello predeterminada para el clúster de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="a261c-285">Incluso si se elimina el clúster de HDInsight, contenedor de almacenamiento de blobs predeterminado de Hola y cuenta de almacenamiento de hello asociada no se eliminan.</span><span class="sxs-lookup"><span data-stu-id="a261c-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="a261c-286">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="a261c-286">This behavior is by design.</span></span> <span data-ttu-id="a261c-287">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="a261c-288">Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="a261c-289">nombres de Hola de estos contenedores siguen un patrón: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="a261c-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="a261c-290">Eliminar hello **adfjobs** y **adfyourdatafactoryname-linkedservicename-datetimestamp** carpetas.</span><span class="sxs-lookup"><span data-stu-id="a261c-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="a261c-291">contenedor de Hello adfjobs contiene registros de trabajos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="a261c-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="a261c-292">Eliminar grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-292">Delete hello resource group</span></span>
<span data-ttu-id="a261c-293">[El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) es toodeploy usado, administrar y supervisar la solución como un grupo.</span><span class="sxs-lookup"><span data-stu-id="a261c-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="a261c-294">Eliminar un grupo de recursos, elimina todos los componentes de hello dentro de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="a261c-295">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a261c-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a261c-296">Haga clic en **grupos de recursos** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="a261c-297">Haga clic en el nombre del grupo de recursos de Hola que creó en el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a261c-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="a261c-298">Utilice el filtro de hello si tiene demasiados grupos de recursos que se muestran.</span><span class="sxs-lookup"><span data-stu-id="a261c-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="a261c-299">Grupo de recursos de Hola se abre en una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="a261c-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="a261c-300">En hello **recursos** mosaico, debe tener cuenta de almacenamiento predeterminada de Hola y el generador de datos de hello, a menos que el grupo de recursos de Hola se comparte con otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="a261c-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="a261c-301">Haga clic en **eliminar** en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="a261c-302">Si lo hace, elimina la cuenta de almacenamiento de Hola y datos de hello almacenados en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="a261c-303">Escriba la eliminación de tooconfirm del nombre del grupo de recursos de hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="a261c-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="a261c-304">En caso de que no desea cuenta de almacenamiento de hello toodelete cuando se elimina el grupo de recursos de hello, considere la posibilidad de hello después arquitectura mediante la separación de datos de negocio de saludo de cuenta de almacenamiento predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="a261c-305">En este caso, tiene un grupo de recursos Hola cuenta de almacenamiento con datos de negocio de Hola y Hola a otro grupo de recursos de cuenta de almacenamiento predeterminada de Hola para HDInsight vinculado hello y servicio de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="a261c-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="a261c-306">Cuando se elimina el segundo grupo de recursos de hello, que no afecte a cuenta de almacenamiento de datos de negocio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="a261c-307">toodo para:</span><span class="sxs-lookup"><span data-stu-id="a261c-307">toodo so:</span></span>

* <span data-ttu-id="a261c-308">Agregar Hola después el grupo de recursos de nivel superior de toohello junto con hello Microsoft.DataFactory/datafactories recursos en la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a261c-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="a261c-309">Crea una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a261c-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="a261c-310">Agregar una nueva toohello de punto de servicio vinculado nueva cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a261c-310">Add a new linked service point toohello new storage account:</span></span>

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
* <span data-ttu-id="a261c-311">Configurar el servicio de ondemand vinculado de HDInsight de hello con un dependsOn adicional y un additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="a261c-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="a261c-312">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a261c-312">Next steps</span></span>
<span data-ttu-id="a261c-313">En este artículo, ha aprendido cómo tooprocess de clúster de HDInsight de toouse toocreate Data Factory de Azure a petición trabajos de Hive.</span><span class="sxs-lookup"><span data-stu-id="a261c-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="a261c-314">tooread más:</span><span class="sxs-lookup"><span data-stu-id="a261c-314">tooread more:</span></span>

* [<span data-ttu-id="a261c-315">Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="a261c-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="a261c-316">Creación de clústeres de Hadoop basados en Linux en HDInsight</span><span class="sxs-lookup"><span data-stu-id="a261c-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="a261c-317">Documentación de HDInsight</span><span class="sxs-lookup"><span data-stu-id="a261c-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="a261c-318">Documentación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="a261c-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="a261c-319">Anexo</span><span class="sxs-lookup"><span data-stu-id="a261c-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="a261c-320">Script de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a261c-320">Azure CLI script</span></span>
<span data-ttu-id="a261c-321">Puede utilizar la CLI de Azure en lugar de utilizar el tutorial de Azure PowerShell toodo Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="a261c-322">toouse CLI de Azure, instale primero la CLI de Azure según Hola siguiendo las instrucciones:</span><span class="sxs-lookup"><span data-stu-id="a261c-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="a261c-323">Usar el almacenamiento de Azure CLI tooprepare hello y copie los archivos de Hola</span><span class="sxs-lookup"><span data-stu-id="a261c-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

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

<span data-ttu-id="a261c-324">es el nombre del contenedor de Hello *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="a261c-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="a261c-325">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="a261c-325">Keep it as it is.</span></span> <span data-ttu-id="a261c-326">En caso contrario es necesaria una plantilla de administrador de recursos de tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="a261c-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="a261c-327">Si necesita ayuda para esta secuencia de comandos CLI, consulte [Using Hola CLI de Azure con el almacenamiento de Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a261c-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
