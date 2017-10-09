---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "almacenamiento de blobs de datos de aaaLoad de Azure en almacenamiento de datos de SQL Azure (factoría de datos de Azure) | Documentos de Microsoft"
description: "Obtenga información acerca de los datos de tooload con Data Factory de Azure"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="f59dc-103">Carga de datos del Almacenamiento de blobs de Azure en Almacenamiento de datos SQL de Azure (Data Factory de Azure)</span><span class="sxs-lookup"><span data-stu-id="f59dc-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f59dc-104">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="f59dc-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="f59dc-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="f59dc-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="f59dc-106">Este tutorial muestra cómo toocreate una canalización de datos de Data Factory de Azure toomove desde tooSQL almacenamiento de datos de Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-106">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooSQL Data Warehouse.</span></span> <span data-ttu-id="f59dc-107">Con hello pasos hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f59dc-107">With hello following steps you will:</span></span>

* <span data-ttu-id="f59dc-108">Configurar datos de ejemplo en un blob de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="f59dc-109">Conectar recursos tooAzure factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="f59dc-109">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="f59dc-110">Crear una canalización de datos de toomove de Blobs de almacenamiento tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="f59dc-110">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="f59dc-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f59dc-111">Before you begin</span></span>
<span data-ttu-id="f59dc-112">toofamiliarize usted mismo con Data Factory de Azure, consulte [tooAzure Introducción factoría de datos][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="f59dc-112">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="f59dc-113">Creación o identificación de recursos</span><span class="sxs-lookup"><span data-stu-id="f59dc-113">Create or identify resources</span></span>
<span data-ttu-id="f59dc-114">Antes de iniciar este tutorial, necesita hello toohave recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="f59dc-114">Before starting this tutorial, you need toohave hello following resources.</span></span>

* <span data-ttu-id="f59dc-115">**Blob de almacenamiento de Azure**: este tutorial utiliza el Blob de almacenamiento de Azure como origen de datos de hello de la canalización de factoría de datos de Azure de hello y, por lo que necesita datos de ejemplo de toohave una disponible toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="f59dc-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="f59dc-116">Si no tiene ninguno todavía, obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="f59dc-116">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="f59dc-117">**Almacenamiento de datos SQL**: este tutorial mueve Hola los datos de Blob de almacenamiento de Azure demasiado almacenamiento de datos SQL de modo que necesitan un almacenamiento de datos en línea que se ha cargado con datos de ejemplo AdventureWorksDW hello toohave.</span><span class="sxs-lookup"><span data-stu-id="f59dc-117">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="f59dc-118">Si no dispone de un almacén de datos, obtenga información acerca de cómo demasiado[aprovisionar una][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f59dc-118">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="f59dc-119">Si tiene un almacén de datos pero no lo aprovisiona con datos de ejemplo de Hola, puede [cargarlos manualmente][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f59dc-119">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="f59dc-120">**Factoría de datos de Azure**: Data Factory de Azure se completará la carga real de Hola y por lo que deberá toohave uno que puede usar la canalización de movimiento de datos de toobuild Hola. Si no tiene ninguno todavía, obtenga información acerca de cómo toocreate uno en el paso 1 de [Introducción a Data Factory de Azure (Editor de generador de datos)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="f59dc-120">**Azure Data Factory**: Azure Data Factory will complete hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="f59dc-121">**AZCopy**: necesita datos de ejemplo de Hola de AZCopy toocopy de su tooyour de cliente local Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-121">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="f59dc-122">Para obtener instrucciones de instalación, vea hello [AZCopy documentación][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="f59dc-122">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="f59dc-123">Paso 1: Copiar datos de ejemplo tooAzure Blob de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f59dc-123">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="f59dc-124">Una vez que tenga todas las fichas de hello listo, son tooyour de datos de ejemplo listo toocopy Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-124">Once you have all of hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="f59dc-125">[Descargue los datos de ejemplo][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="f59dc-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="f59dc-126">Estos datos agregarán otro tres años de datos de ventas tooyour datos de ejemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="f59dc-126">This data will add another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="f59dc-127">Utilice este comando de AZCopy toocopy hello tres años de tooyour de datos Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-127">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="f59dc-128">Paso 2: Conectar recursos tooAzure factoría de datos</span><span class="sxs-lookup"><span data-stu-id="f59dc-128">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="f59dc-129">Ahora que los datos de hello están en su lugar podemos crear datos de saludo de hello Data Factory de Azure canalización toomove desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="f59dc-129">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="f59dc-130">tooget iniciado, abra hello [portal de Azure] [ Azure portal] y seleccione su factoría de datos en el menú izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="f59dc-130">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="f59dc-131">Paso 2.1: Creación del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="f59dc-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="f59dc-132">Vincular su cuenta de almacenamiento de Azure y la factoría de datos de almacenamiento de datos de SQL tooyour.</span><span class="sxs-lookup"><span data-stu-id="f59dc-132">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="f59dc-133">En primer lugar, comenzar el proceso de registro de hello haciendo clic en la sección de hello 'Servicios vinculados' de la factoría de datos y, a continuación, haga clic en 'Nuevo almacén de datos'.</span><span class="sxs-lookup"><span data-stu-id="f59dc-133">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="f59dc-134">Elija un nombre tooregister su almacenamiento de azure en, seleccione el almacenamiento de Azure como su tipo y, a continuación, escriba el nombre de cuenta y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="f59dc-134">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="f59dc-135">tooregister almacenamiento de datos SQL vaya toohello 'Autor e implementar' sección, seleccione 'Nuevo almacén de datos' y, a continuación, 'Almacenamiento de datos de SQL de Azure'.</span><span class="sxs-lookup"><span data-stu-id="f59dc-135">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="f59dc-136">Copie y pegue en esta plantilla y, a continuación, rellene su información específica.</span><span class="sxs-lookup"><span data-stu-id="f59dc-136">Copy and paste in this template, and then fill in your specific information.</span></span>

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="f59dc-137">Paso 2.2: Definir el conjunto de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="f59dc-137">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="f59dc-138">Después de crear Hola servicios vinculados, tenemos conjuntos de datos de toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="f59dc-138">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="f59dc-139">Aquí, esto significa definir Hola estructura de datos de Hola que se ha movido desde el almacenamiento de datos de tooyour de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f59dc-139">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="f59dc-140">Puede leer más sobre creación.</span><span class="sxs-lookup"><span data-stu-id="f59dc-140">You can read more about creating</span></span>

1. <span data-ttu-id="f59dc-141">Iniciar este proceso, vaya toohello sección 'Crear e implementar' de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="f59dc-141">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="f59dc-142">Haga clic en 'Nuevo conjunto de datos' y, a continuación, 'Almacenamiento de blobs de Azure' toolink su factoría de datos de tooyour de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f59dc-142">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="f59dc-143">Puede usar Hola por debajo de la secuencia de comandos toodefine los datos en el almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="f59dc-143">You can use hello below script toodefine your data in Azure Blob storage:</span></span>

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```


1. <span data-ttu-id="f59dc-144">Ahora definiremos también nuestro conjunto de datos para Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f59dc-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="f59dc-145">Comenzamos en hello igual, haciendo clic en 'Nuevo conjunto de datos' y, a continuación, 'Almacenamiento de datos de SQL de Azure'.</span><span class="sxs-lookup"><span data-stu-id="f59dc-145">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="f59dc-146">Paso 3: Creación y ejecución de la canalización</span><span class="sxs-lookup"><span data-stu-id="f59dc-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="f59dc-147">Por último, haremos canalización Hola de instalación y ejecución de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-147">Finally, we will set-up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="f59dc-148">Se trata de una operación de Hola que se completará el movimiento de datos reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59dc-148">This is hello operation that will complete hello actual data movement.</span></span>  <span data-ttu-id="f59dc-149">Puede encontrar una vista completa de las operaciones de Hola que puede completar con el almacenamiento de datos de SQL y Data Factory de Azure [aquí][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="f59dc-149">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="f59dc-150">En sección 'Crear e implementar' de hello ahora haga clic en 'Más comandos' y, a continuación, 'Nueva canalización'.</span><span class="sxs-lookup"><span data-stu-id="f59dc-150">In hello 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="f59dc-151">Después de crear la canalización de hello, puede usar hello debajo de almacenamiento de datos de código tootransfer Hola datos tooyour:</span><span class="sxs-lookup"><span data-stu-id="f59dc-151">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f59dc-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f59dc-152">Next steps</span></span>
<span data-ttu-id="f59dc-153">toolearn más, inicio, consulte:</span><span class="sxs-lookup"><span data-stu-id="f59dc-153">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="f59dc-154">[Ruta de aprendizaje para Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="f59dc-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="f59dc-155">[Conector de Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="f59dc-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="f59dc-156">Se trata de un tema de referencia de núcleo de hello para el uso de Data Factory de Azure con almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-156">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="f59dc-157">En estos temas se proporciona información detallada sobre Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="f59dc-158">Debaten HDinsight o base de datos de SQL Azure, pero también aplica la información de hello tooAzure almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f59dc-158">They discuss Azure SQL Database or HDinsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="f59dc-159">[Tutorial: Introducción a Data Factory de Azure] [ Tutorial: Get started with Azure Data Factory] se trata de tutorial de núcleo de hello para el procesamiento de datos con Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59dc-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="f59dc-160">En este tutorial se compile su primera canalización que usa tootransform de HDInsight y analizar registros web mensualmente.</span><span class="sxs-lookup"><span data-stu-id="f59dc-160">In this tutorial you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="f59dc-161">Tenga en cuenta que no hay ninguna actividad de copia en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f59dc-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="f59dc-162">[Tutorial: Copiar los datos de Blob de almacenamiento de Azure tooAzure base de datos SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="f59dc-162">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="f59dc-163">En este tutorial, creará una canalización de datos de Data Factory de Azure toocopy de Blob de almacenamiento de Azure tooAzure base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f59dc-163">In this tutorial, you will create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
