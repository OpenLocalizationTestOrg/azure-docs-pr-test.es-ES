---
title: "grandes cantidades de datos en el almacén de Data Lake mediante métodos sin conexión de aaaUpload | Documentos de Microsoft"
description: "TooData Lake almacén de blobs de hello uso AdlCopy datos de toocopy la herramienta desde el almacenamiento de Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="6db80-103">Utilizar el servicio de importación y exportación de Azure de hello para la copia sin conexión del almacén de datos tooData Lake</span><span class="sxs-lookup"><span data-stu-id="6db80-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="6db80-104">En este artículo, aprenderá cómo establece datos enorme toocopy (> 200 GB) en un almacén de Azure Data Lake mediante el uso de métodos de copia sin conexión, como hello [servicio de importación y exportación de Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="6db80-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="6db80-105">En concreto, archivo hello utilizado como ejemplo en este artículo es 339,420,860,416 bytes, o aproximadamente 319 GB en el disco.</span><span class="sxs-lookup"><span data-stu-id="6db80-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="6db80-106">Llamaremos a este archivo "319GB.tsv".</span><span class="sxs-lookup"><span data-stu-id="6db80-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="6db80-107">Hola servicio de importación y exportación de Azure le ayuda a tootransfer grandes cantidades de datos más segura tooAzure almacenamiento de blobs de disco duro de envío unidades tooan centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6db80-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6db80-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6db80-108">Prerequisites</span></span>
<span data-ttu-id="6db80-109">Antes de comenzar, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6db80-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="6db80-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="6db80-110">**An Azure subscription**.</span></span> <span data-ttu-id="6db80-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6db80-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6db80-112">Una **cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="6db80-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="6db80-113">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="6db80-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="6db80-114">Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6db80-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="6db80-115">Preparar los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="6db80-115">Preparing hello data</span></span>
<span data-ttu-id="6db80-116">Antes de usar el servicio de importación/exportación de hello, transfiere salto Hola datos archivo toobe **en copias que son menos de 200 GB** de tamaño.</span><span class="sxs-lookup"><span data-stu-id="6db80-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="6db80-117">herramienta de importación de Hello no funciona con archivos de más de 200 GB.</span><span class="sxs-lookup"><span data-stu-id="6db80-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="6db80-118">En este tutorial, dividiremos archivo hello en fragmentos de 100 GB.</span><span class="sxs-lookup"><span data-stu-id="6db80-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="6db80-119">Puede hacerlo si utiliza [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="6db80-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="6db80-120">Cygwin admite comandos de Linux.</span><span class="sxs-lookup"><span data-stu-id="6db80-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="6db80-121">En este caso, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6db80-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="6db80-122">operación de división de Hello crea archivos con hello después de nombres.</span><span class="sxs-lookup"><span data-stu-id="6db80-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="6db80-123">Preparación de los discos con datos</span><span class="sxs-lookup"><span data-stu-id="6db80-123">Get disks ready with data</span></span>
<span data-ttu-id="6db80-124">Siga las instrucciones de hello en [mediante el servicio de importación y exportación de Azure de hello](../storage/common/storage-import-export-service.md) (en hello **preparar las unidades de disco** sección) tooprepare las unidades de disco duras.</span><span class="sxs-lookup"><span data-stu-id="6db80-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="6db80-125">Aquí es hello secuencia general:</span><span class="sxs-lookup"><span data-stu-id="6db80-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="6db80-126">Adquiera un disco duro que cumpla Hola requisito toobe destinada Hola servicio de importación y exportación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6db80-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="6db80-127">Identificar una cuenta de almacenamiento de Azure donde se copiarán los datos de hello una vez enviada toohello centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6db80-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="6db80-128">Hola de uso [herramienta de importación y exportación de Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), una utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="6db80-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="6db80-129">Este es un fragmento de código de ejemplo que muestra cómo toouse Hola herramienta.</span><span class="sxs-lookup"><span data-stu-id="6db80-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="6db80-130">Vea [mediante el servicio de importación y exportación de Azure de hello](../storage/common/storage-import-export-service.md) para varios fragmentos de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6db80-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="6db80-131">Hello comando anterior crea un diario de ubicación de archivo en hello especificada.</span><span class="sxs-lookup"><span data-stu-id="6db80-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="6db80-132">Utilice este toocreate de archivo diario un trabajo de importación de hello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6db80-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="6db80-133">Crear un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="6db80-133">Create an import job</span></span>
<span data-ttu-id="6db80-134">Ahora puede crear un trabajo de importación mediante instrucciones de hello en [mediante el servicio de importación y exportación de Azure de hello](../storage/common/storage-import-export-service.md) (en hello **crear trabajo de importación de hello** sección).</span><span class="sxs-lookup"><span data-stu-id="6db80-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="6db80-135">Para este trabajo de importación, con los otros detalles, proporcionar también archivo diario de hello creado durante la preparación de unidades de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="6db80-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="6db80-136">Enviar físicamente los discos de Hola</span><span class="sxs-lookup"><span data-stu-id="6db80-136">Physically ship hello disks</span></span>
<span data-ttu-id="6db80-137">Ahora puede distribuir físicamente Hola discos tooan centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6db80-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="6db80-138">No existe, se copian datos de hello en blobs de almacenamiento de Azure toohello que proporcionó al crear un trabajo de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6db80-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="6db80-139">Además, al crear un trabajo de hello, si ha elegido hello tooprovide más adelante, la información de seguimiento puede ahora volver Hola de trabajo y actualización de la importación de tooyour número de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="6db80-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="6db80-140">Copiar los datos de almacén de almacenamiento de Azure BLOB tooAzure Data Lake</span><span class="sxs-lookup"><span data-stu-id="6db80-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="6db80-141">Después de estado de Hola de hello trabajo de importación muestra que se completan, puede comprobar si hay datos de hello en blobs de almacenamiento de Azure de Hola que se había especificado.</span><span class="sxs-lookup"><span data-stu-id="6db80-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="6db80-142">A continuación, puede utilizar una variedad de toomove de métodos que los datos de hello blobs tooAzure almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6db80-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="6db80-143">Para todos los hello las opciones disponibles para cargar los datos, consulte [introducción de datos en el almacén de Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="6db80-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="6db80-144">En esta sección, se proporcionan con definiciones de hello JSON que puede usar toocreate una canalización del generador de datos de Azure para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="6db80-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="6db80-145">Puede utilizar estas definiciones de JSON de hello [portal de Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6db80-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="6db80-146">Servicio vinculado de origen (blob de Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="6db80-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="6db80-147">Servicio vinculado de destino (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="6db80-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="6db80-148">Conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="6db80-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="6db80-149">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="6db80-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="6db80-150">Canalización (actividad de copia)</span><span class="sxs-lookup"><span data-stu-id="6db80-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="6db80-151">Para obtener más información, consulte [mover datos desde el almacenamiento de Azure blob almacén de Data Lake tooAzure con Data Factory de Azure](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6db80-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="6db80-152">Reconstruir los archivos de datos de hello en el almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="6db80-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="6db80-153">Comenzamos con un archivo que 319 GB e interrumpió hacia abajo de en archivos de tamaño más pequeño para que puede transferirse mediante el servicio de importación y exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6db80-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="6db80-154">Ahora que los datos de hello están en el almacén de Data Lake de Azure, se puede reconstruir tamaño original del archivo tooits de Hola.</span><span class="sxs-lookup"><span data-stu-id="6db80-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="6db80-155">Puede usar Hola después Azure PowerShell cmldts toodo por lo que.</span><span class="sxs-lookup"><span data-stu-id="6db80-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="6db80-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6db80-156">Next steps</span></span>
* [<span data-ttu-id="6db80-157">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="6db80-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="6db80-158">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="6db80-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6db80-159">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="6db80-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
