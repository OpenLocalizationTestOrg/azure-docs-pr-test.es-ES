---
title: "Carga de grandes cantidades de datos en Data Lake Store mediante el empleo de métodos sin conexión | Microsoft Docs"
description: Use la herramienta AdlCopy para copiar datos desde los blobs de Azure Storage a Data Lake Store.
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
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="619ac-103">Uso del servicio Azure Import/Export para la copia de datos sin conexión en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="619ac-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="619ac-104">En este artículo, aprenderá a copiar conjuntos de datos de gran tamaño (más de 200 GB) en Azure Data Lake Store mediante el empleo de métodos de copia sin conexión, como el [servicio Azure Import/Export](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="619ac-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="619ac-105">En concreto, el archivo de ejemplo que utilizamos en este artículo tiene 339 420 860 416 bytes; es decir, ocupa unos 319 GB de espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="619ac-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="619ac-106">Llamaremos a este archivo "319GB.tsv".</span><span class="sxs-lookup"><span data-stu-id="619ac-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="619ac-107">El servicio Azure Import/Export le permite transferir de forma segura grandes cantidades de datos a Azure Blob Storage mediante el envío de unidades de disco duro a un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="619ac-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="619ac-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="619ac-108">Prerequisites</span></span>
<span data-ttu-id="619ac-109">Antes de empezar, debe disponer de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="619ac-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="619ac-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="619ac-110">**An Azure subscription**.</span></span> <span data-ttu-id="619ac-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="619ac-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="619ac-112">Una **cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="619ac-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="619ac-113">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="619ac-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="619ac-114">Para obtener instrucciones sobre cómo crear una, consulte la [introducción al Almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="619ac-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="619ac-115">Preparación de los datos</span><span class="sxs-lookup"><span data-stu-id="619ac-115">Preparing the data</span></span>
<span data-ttu-id="619ac-116">Antes de usar el servicio Import/Export, divida el archivo de datos para transferirlo **en copias de menos de 200 GB**.</span><span class="sxs-lookup"><span data-stu-id="619ac-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="619ac-117">La herramienta de importación no funciona con archivos con un tamaño superior a 200 GB.</span><span class="sxs-lookup"><span data-stu-id="619ac-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="619ac-118">En este tutorial, el archivo se divide en fragmentos de 100 GB.</span><span class="sxs-lookup"><span data-stu-id="619ac-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="619ac-119">Puede hacerlo si utiliza [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="619ac-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="619ac-120">Cygwin admite comandos de Linux.</span><span class="sxs-lookup"><span data-stu-id="619ac-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="619ac-121">En este caso, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="619ac-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="619ac-122">La operación de división crea archivos con los nombres siguientes.</span><span class="sxs-lookup"><span data-stu-id="619ac-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="619ac-123">Preparación de los discos con datos</span><span class="sxs-lookup"><span data-stu-id="619ac-123">Get disks ready with data</span></span>
<span data-ttu-id="619ac-124">Siga las instrucciones de [Uso del servicio Azure Import/Export para transferir datos a Azure Storage](../storage/common/storage-import-export-service.md) (sección **Preparación de las unidades**) para preparar los discos duros.</span><span class="sxs-lookup"><span data-stu-id="619ac-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="619ac-125">Aquí se muestra la secuencia general:</span><span class="sxs-lookup"><span data-stu-id="619ac-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="619ac-126">Adquiera un disco duro que cumpla los requisitos para poder utilizarse con el servicio Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="619ac-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="619ac-127">Identifique una cuenta de Azure Storage donde vayan a copiarse los datos cuando se envíen al centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="619ac-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="619ac-128">Utilice la [herramienta Azure Import/Export](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), una utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="619ac-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="619ac-129">Abajo, podrá encontrar un fragmento de código de ejemplo que muestra cómo utilizar la herramienta.</span><span class="sxs-lookup"><span data-stu-id="619ac-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="619ac-130">Consulte [Uso del servicio Azure Import/Export](../storage/common/storage-import-export-service.md) para obtener más fragmentos de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="619ac-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="619ac-131">El comando anterior crea un archivo de diario en la ubicación especificada.</span><span class="sxs-lookup"><span data-stu-id="619ac-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="619ac-132">Use este archivo de diario para crear un trabajo de importación desde el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="619ac-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="619ac-133">Crear un trabajo de importación</span><span class="sxs-lookup"><span data-stu-id="619ac-133">Create an import job</span></span>
<span data-ttu-id="619ac-134">Ahora puede crear un trabajo de importación con las instrucciones de [Uso del servicio Azure Import/Export ](../storage/common/storage-import-export-service.md) (sección **Creación de un trabajo de importación**).</span><span class="sxs-lookup"><span data-stu-id="619ac-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="619ac-135">Para este trabajo de importación, proporcione también el archivo de diario creado al preparar las unidades de disco, además de otros detalles.</span><span class="sxs-lookup"><span data-stu-id="619ac-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="619ac-136">Envío físico de los discos</span><span class="sxs-lookup"><span data-stu-id="619ac-136">Physically ship the disks</span></span>
<span data-ttu-id="619ac-137">Ahora puede enviar físicamente los discos a un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="619ac-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="619ac-138">Allí, se copiarán los datos a los blobs de Azure Storage que proporcionó al crear el trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="619ac-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="619ac-139">Además, al crear el trabajo, si eligió proporcionar la información de seguimiento más adelante, ahora podrá volver al trabajo de importación y actualizar el número de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="619ac-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="619ac-140">Copia de datos de blobs de Azure Storage en Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="619ac-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="619ac-141">Cuando se muestre el estado del trabajo de importación como completado, podrá comprobar si los datos están disponibles en los blobs de Azure Storage que había especificado.</span><span class="sxs-lookup"><span data-stu-id="619ac-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="619ac-142">Después, podrá utilizar diversos métodos para mover estos datos de los blobs de Azure Storage a Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="619ac-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="619ac-143">Para ver todas las opciones disponibles para cargar datos, consulte el artículo sobre cómo [ingerir datos en Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="619ac-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="619ac-144">En esta sección, proporcionamos las definiciones de JSON que puede usar para crear una canalización de Azure Data Factory con el objetivo de copiar datos.</span><span class="sxs-lookup"><span data-stu-id="619ac-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="619ac-145">Puede utilizar estas definiciones de JSON en [Azure Portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="619ac-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="619ac-146">Servicio vinculado de origen (blob de Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="619ac-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="619ac-147">Servicio vinculado de destino (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="619ac-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="619ac-148">Conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="619ac-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="619ac-149">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="619ac-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="619ac-150">Canalización (actividad de copia)</span><span class="sxs-lookup"><span data-stu-id="619ac-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="619ac-151">Para más información, consulte [Movimiento de datos hacia y desde Azure Data Lake Store mediante Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="619ac-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="619ac-152">Reconstrucción de los archivos de datos de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="619ac-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="619ac-153">Comenzamos con un archivo de 319 GB y lo dividimos en fragmentos de menor tamaño para que se pudiesen transferir mediante el servicio Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="619ac-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="619ac-154">Ahora que los datos están en Azure Data Lake Store, podemos reconstruir el archivo para que vuelva a tener su tamaño original.</span><span class="sxs-lookup"><span data-stu-id="619ac-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="619ac-155">También puede utilizar el siguiente cmdlet de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="619ac-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="619ac-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="619ac-156">Next steps</span></span>
* [<span data-ttu-id="619ac-157">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="619ac-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="619ac-158">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="619ac-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="619ac-159">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="619ac-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
