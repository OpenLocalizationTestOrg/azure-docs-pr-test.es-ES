---
title: "conjuntos de datos de aaaCreate de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo calcula el desplazamiento con ejemplos que utilizan propiedades como en Data Factory de Azure, los conjuntos de datos toocreate y anchorDateTime."
keywords: crear conjunto de datos, ejemplo de conjunto de datos, ejemplo con offset
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="c80c9-104">Conjuntos de datos en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c80c9-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="c80c9-105">En este artículo se describe qué son los conjuntos de datos, cómo se definen en formato JSON y cómo se usan en canalizaciones de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c80c9-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="c80c9-106">Proporciona detalles sobre cada sección (por ejemplo, estructura, disponibilidad y directiva) en la definición de JSON de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="c80c9-107">Hello artículo también proporcionan ejemplos para usar hello **desplazamiento**, **anchorDateTime**, y **estilo** propiedades en una definición de JSON de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="c80c9-108">Si se tooData nueva fábrica, consulte [tooAzure Introducción factoría de datos](data-factory-introduction.md) para obtener información general.</span><span class="sxs-lookup"><span data-stu-id="c80c9-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="c80c9-109">Si no tiene experiencia práctica con la creación de generadores de datos, puede obtener una mejor comprensión por leer hello [tutorial de transformación de datos](data-factory-build-your-first-pipeline.md) hello y [tutorial de movimiento de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="c80c9-110">Información general</span><span class="sxs-lookup"><span data-stu-id="c80c9-110">Overview</span></span>
<span data-ttu-id="c80c9-111">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="c80c9-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c80c9-112">Una **canalización** es una agrupación lógica de **actividades** que realizan una tarea.</span><span class="sxs-lookup"><span data-stu-id="c80c9-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="c80c9-113">actividades de Hello en una canalización definen acciones tooperform en los datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="c80c9-114">Por ejemplo, puede usar un datos de toocopy de actividad de copia de un tooAzure de SQL Server local almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c80c9-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="c80c9-115">A continuación, puede usar una actividad de Hive que se ejecuta un script de Hive en un datos tooprocess de clúster de HDInsight de Azure de datos de salida de tooproduce de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c80c9-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="c80c9-116">Por último, puede usar una segunda copia actividad toocopy Hola salida datos tooAzure almacenamiento de datos de SQL, sobre qué inteligencia empresarial (BI) reporting soluciones se generan.</span><span class="sxs-lookup"><span data-stu-id="c80c9-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="c80c9-117">Para más información sobre canalizaciones y actividades, consulte el artículo [Canalizaciones y actividades en Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="c80c9-118">Una actividad puede tomar diversos **conjuntos de datos** de entrada, o ninguno, y generar uno o varios conjuntos de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="c80c9-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="c80c9-119">Un conjunto de datos de entrada representa la entrada de Hola para una actividad de canalización de Hola y un conjunto de datos de salida representa la salida de hello para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="c80c9-120">Los conjuntos de datos identifican datos en distintos almacenes de datos, como tablas, archivos, carpetas y documentos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="c80c9-121">Por ejemplo, un conjunto de datos de Blob de Azure especifica contenedor de blob de Hola y la carpeta de almacenamiento de blobs de qué Hola canalización debe leer los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="c80c9-122">Antes de crear un conjunto de datos, crear un **servicio vinculado** toolink toohello factoría de datos de almacén de los datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="c80c9-123">Servicios vinculados son muy similares a las cadenas de conexión, que definen la información de conexión de hello necesaria para los recursos de tooexternal tooconnect de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="c80c9-124">Conjuntos de datos para identificar datos dentro de los almacenes de datos de hello vinculado, como tablas SQL, archivos, carpetas y documentos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="c80c9-125">Por ejemplo, un almacenamiento de Azure había vinculada vínculos de servicio una factoría de datos de toohello de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c80c9-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="c80c9-126">Un conjunto de datos de Blob de Azure representa contenedor de blobs de Hola y la carpeta de Hola que contiene Hola blobs entrada toobe procesado.</span><span class="sxs-lookup"><span data-stu-id="c80c9-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="c80c9-127">Este es un escenario de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c80c9-127">Here is a sample scenario.</span></span> <span data-ttu-id="c80c9-128">datos de toocopy de base de datos SQL tooa de almacenamiento de blobs, crear dos servicios vinculados: almacenamiento de Azure y base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="c80c9-129">A continuación, cree dos conjuntos de datos: conjunto de datos de Blob de Azure (que hace referencia el servicio de almacenamiento de Azure vinculada de toohello) y un conjunto de tablas de SQL Azure (que hace la referencia de servicio de base de datos de Azure SQL vinculado toohello).</span><span class="sxs-lookup"><span data-stu-id="c80c9-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="c80c9-130">Hola almacenamiento de Azure y base de datos de SQL de Azure servicios vinculados contienen cadenas de conexión utilizado por factoría de datos en tiempo de ejecución tooconnect tooyour almacenamiento de Azure y base de datos de SQL Azure, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c80c9-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="c80c9-131">conjunto de datos de Blob de Azure de Hello especifica el contenedor de blob de Hola y la carpeta de blob que contiene el BLOB de entrada de hello en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c80c9-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="c80c9-132">conjunto de datos de tabla de SQL Azure Hola especifica la tabla SQL de hello en los datos de Hola de toowhich de base de datos SQL es toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="c80c9-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="c80c9-133">Hello diagrama siguiente muestra hello relaciones entre los servicios vinculados, actividad, conjunto de datos y canalización de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="c80c9-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relación entre la canalización, la actividad, el conjunto de datos y los servicios vinculados](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="c80c9-135">Conjunto de datos JSON</span><span class="sxs-lookup"><span data-stu-id="c80c9-135">Dataset JSON</span></span>
<span data-ttu-id="c80c9-136">Un conjunto de datos de Data Factory se define con formato JSON de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="c80c9-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="c80c9-137">Hello en la tabla siguiente describe propiedades Hola anterior JSON:</span><span class="sxs-lookup"><span data-stu-id="c80c9-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="c80c9-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c80c9-138">Property</span></span> | <span data-ttu-id="c80c9-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="c80c9-139">Description</span></span> | <span data-ttu-id="c80c9-140">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c80c9-140">Required</span></span> | <span data-ttu-id="c80c9-141">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c80c9-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c80c9-142">name</span><span class="sxs-lookup"><span data-stu-id="c80c9-142">name</span></span> |<span data-ttu-id="c80c9-143">Nombre del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-143">Name of hello dataset.</span></span> <span data-ttu-id="c80c9-144">Consulte [Azure Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para ver este tipo de reglas.</span><span class="sxs-lookup"><span data-stu-id="c80c9-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="c80c9-145">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-145">Yes</span></span> |<span data-ttu-id="c80c9-146">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-146">NA</span></span> |
| <span data-ttu-id="c80c9-147">type</span><span class="sxs-lookup"><span data-stu-id="c80c9-147">type</span></span> |<span data-ttu-id="c80c9-148">Tipo de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-148">Type of hello dataset.</span></span> <span data-ttu-id="c80c9-149">Especifique uno de los tipos de hello admitidos factoría de datos (por ejemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="c80c9-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="c80c9-150">Para más información, consulte [Tipo de conjunto de datos](#Type).</span><span class="sxs-lookup"><span data-stu-id="c80c9-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="c80c9-151">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-151">Yes</span></span> |<span data-ttu-id="c80c9-152">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-152">NA</span></span> |
| <span data-ttu-id="c80c9-153">structure</span><span class="sxs-lookup"><span data-stu-id="c80c9-153">structure</span></span> |<span data-ttu-id="c80c9-154">Esquema del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="c80c9-155">Para más información, consulte [Estructura del conjunto de datos](#Structure).</span><span class="sxs-lookup"><span data-stu-id="c80c9-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="c80c9-156">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-156">No</span></span> |<span data-ttu-id="c80c9-157">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-157">NA</span></span> |
| <span data-ttu-id="c80c9-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="c80c9-158">typeProperties</span></span> | <span data-ttu-id="c80c9-159">propiedades de tipo Hello son diferentes para cada tipo (por ejemplo: Azure Blob, tabla de SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="c80c9-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="c80c9-160">Para obtener más información sobre tipos de hello compatibles y sus propiedades, vea [tipo de conjunto de datos](#Type).</span><span class="sxs-lookup"><span data-stu-id="c80c9-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="c80c9-161">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-161">Yes</span></span> |<span data-ttu-id="c80c9-162">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-162">NA</span></span> |
| <span data-ttu-id="c80c9-163">external</span><span class="sxs-lookup"><span data-stu-id="c80c9-163">external</span></span> | <span data-ttu-id="c80c9-164">Un valor booleano marca toospecify si una canalización del generador de datos explícitamente genera un conjunto de datos o no.</span><span class="sxs-lookup"><span data-stu-id="c80c9-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="c80c9-165">Si el conjunto de datos de entrada de Hola para una actividad no se crea por la canalización actual hello, establecer este tootrue de marca.</span><span class="sxs-lookup"><span data-stu-id="c80c9-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="c80c9-166">Establecer este tootrue marca Hola entrada conjunto de datos de la primera actividad de hello en canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="c80c9-167">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-167">No</span></span> |<span data-ttu-id="c80c9-168">false</span><span class="sxs-lookup"><span data-stu-id="c80c9-168">false</span></span> |
| <span data-ttu-id="c80c9-169">availability</span><span class="sxs-lookup"><span data-stu-id="c80c9-169">availability</span></span> | <span data-ttu-id="c80c9-170">Define Hola ventana de procesamiento (por ejemplo, cada hora o diariamente) o hello segmentar el modelo para la producción de hello conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="c80c9-171">Cada unidad de datos consumida y producida por la ejecución de una actividad se denomina segmento de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="c80c9-172">Si la disponibilidad de Hola de un conjunto de datos de salida es conjunto toodaily (frecuencia - Day, intervalo - 1), se produce un segmento diariamente.</span><span class="sxs-lookup"><span data-stu-id="c80c9-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="c80c9-173">Para más información, consulte [Disponibilidad del conjunto de datos](#Availability).</span><span class="sxs-lookup"><span data-stu-id="c80c9-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="c80c9-174">Para obtener más información sobre el conjunto de datos de hello segmentar el modelo, vea hello [ejecución y programación](data-factory-scheduling-and-execution.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="c80c9-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="c80c9-175">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-175">Yes</span></span> |<span data-ttu-id="c80c9-176">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-176">NA</span></span> |
| <span data-ttu-id="c80c9-177">policy</span><span class="sxs-lookup"><span data-stu-id="c80c9-177">policy</span></span> |<span data-ttu-id="c80c9-178">Define los criterios de Hola o condición de Hola que deben cumplir los segmentos del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="c80c9-179">Para obtener más información, vea hello [directiva de conjunto de datos](#Policy) sección.</span><span class="sxs-lookup"><span data-stu-id="c80c9-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="c80c9-180">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-180">No</span></span> |<span data-ttu-id="c80c9-181">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="c80c9-182">Ejemplo de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-182">Dataset example</span></span>
<span data-ttu-id="c80c9-183">En el siguiente ejemplo de Hola Hola conjunto de datos representa una tabla denominada **MyTable** en una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c80c9-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c80c9-184">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="c80c9-184">Note hello following points:</span></span>

* <span data-ttu-id="c80c9-185">**tipo** se establece tooAzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="c80c9-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="c80c9-186">**tableName** propiedad type (tipo de tooAzureSqlTable específico) se establece tooMyTable.</span><span class="sxs-lookup"><span data-stu-id="c80c9-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="c80c9-187">**linkedServiceName** hace referencia de servicio de tooa vinculado del tipo AzureSqlDatabase, que se define en el siguiente fragmento de JSON Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="c80c9-188">**frecuencia de disponibilidad** se establece tooDay, y **intervalo** se establece too1.</span><span class="sxs-lookup"><span data-stu-id="c80c9-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="c80c9-189">Esto significa que se produce ese segmento de conjunto de datos de hello diariamente.</span><span class="sxs-lookup"><span data-stu-id="c80c9-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="c80c9-190">**AzureSqlLinkedService** se define de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="c80c9-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="c80c9-191">Hola anterior fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="c80c9-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="c80c9-192">**tipo** se establece tooAzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="c80c9-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="c80c9-193">**connectionString** propiedad type especifica información tooconnect tooa base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c80c9-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="c80c9-194">Como puede ver, hello servicio vinculado define la base de datos SQL tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="c80c9-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="c80c9-195">conjunto de datos de Hello define qué tabla se utiliza como entrada y salida de actividad de hello en una canalización.</span><span class="sxs-lookup"><span data-stu-id="c80c9-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="c80c9-196">A menos que se está produciendo un conjunto de datos por la canalización de hello, se debe marcar como **externo**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="c80c9-197">Por lo general, esta configuración aplica tooinputs de primera actividad en una canalización.</span><span class="sxs-lookup"><span data-stu-id="c80c9-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="c80c9-198"><a name="Type"></a> Tipo de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="c80c9-199">tipo de Hello del conjunto de datos de hello depende de almacén de datos de hello utilizado.</span><span class="sxs-lookup"><span data-stu-id="c80c9-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="c80c9-200">Vea Hola para obtener una lista de almacenes de datos compatibles con factoría de datos en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="c80c9-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="c80c9-201">Haga clic en un toolearn de almacén de datos cómo toocreate un servicio vinculado y un conjunto de datos para los datos de almacén.</span><span class="sxs-lookup"><span data-stu-id="c80c9-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="c80c9-202">Los almacenes de datos con * pueden ser locales o de infraestructura como servicio (IaaS) de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="c80c9-203">Estos almacenes de datos requieren tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="c80c9-204">En el ejemplo hello en la sección anterior de hello, tipo de hello del conjunto de datos de Hola se establece demasiado**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="c80c9-205">De forma similar, para un conjunto de datos Blob de Azure, Hola tipo del conjunto de datos de Hola se establece demasiado**AzureBlob**, tal y como se muestra en hello después JSON:</span><span class="sxs-lookup"><span data-stu-id="c80c9-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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

## <span data-ttu-id="c80c9-206"><a name="Structure"></a>Estructura del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="c80c9-207">Hola **estructura** sección es opcional.</span><span class="sxs-lookup"><span data-stu-id="c80c9-207">hello **structure** section is optional.</span></span> <span data-ttu-id="c80c9-208">Define el esquema de hello del conjunto de datos de hello, que contiene una colección de nombres y tipos de datos de columnas.</span><span class="sxs-lookup"><span data-stu-id="c80c9-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="c80c9-209">Utilice Hola estructura sección tooprovide información de tipo que es tooconvert usa tipos y asignar columnas de destino de hello origen toohello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="c80c9-210">En el siguiente ejemplo de Hola, conjunto de datos de hello tiene tres columnas: `slicetimestamp`, `projectname`, y `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="c80c9-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="c80c9-211">Estas columnas son del tipo String, String, y Decimal, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c80c9-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="c80c9-212">Cada columna de estructura de hello contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="c80c9-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="c80c9-213">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c80c9-213">Property</span></span> | <span data-ttu-id="c80c9-214">Descripción</span><span class="sxs-lookup"><span data-stu-id="c80c9-214">Description</span></span> | <span data-ttu-id="c80c9-215">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c80c9-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c80c9-216">name</span><span class="sxs-lookup"><span data-stu-id="c80c9-216">name</span></span> |<span data-ttu-id="c80c9-217">Nombre de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-217">Name of hello column.</span></span> |<span data-ttu-id="c80c9-218">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-218">Yes</span></span> |
| <span data-ttu-id="c80c9-219">type</span><span class="sxs-lookup"><span data-stu-id="c80c9-219">type</span></span> |<span data-ttu-id="c80c9-220">Tipo de datos de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-220">Data type of hello column.</span></span>  |<span data-ttu-id="c80c9-221">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-221">No</span></span> |
| <span data-ttu-id="c80c9-222">culture</span><span class="sxs-lookup"><span data-stu-id="c80c9-222">culture</span></span> |<span data-ttu-id="c80c9-223">. Toobe de las referencias culturales basada en red utilizado cuando el tipo de hello es un tipo .NET: `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="c80c9-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="c80c9-224">valor predeterminado de Hello es `en-us`.</span><span class="sxs-lookup"><span data-stu-id="c80c9-224">hello default is `en-us`.</span></span> |<span data-ttu-id="c80c9-225">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-225">No</span></span> |
| <span data-ttu-id="c80c9-226">formato</span><span class="sxs-lookup"><span data-stu-id="c80c9-226">format</span></span> |<span data-ttu-id="c80c9-227">Dar formato a toobe de cadena que se usa cuando el tipo de hello es un tipo .NET: `Datetime` o `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="c80c9-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="c80c9-228">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-228">No</span></span> |

<span data-ttu-id="c80c9-229">Hello instrucciones siguientes le ayudarán a determinar cuando tooinclude estructurar la información y qué tooinclude Hola **estructura** sección.</span><span class="sxs-lookup"><span data-stu-id="c80c9-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="c80c9-230">**Para los orígenes de datos estructurados**, especificar la sección de estructura de hello únicamente si desea asignar columnas de toosink de las columnas de origen y sus nombres no son Hola igual.</span><span class="sxs-lookup"><span data-stu-id="c80c9-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="c80c9-231">Este tipo de origen de datos estructurados almacena información de esquema y el tipo de datos junto con los datos de hello propio.</span><span class="sxs-lookup"><span data-stu-id="c80c9-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="c80c9-232">Ejemplos de orígenes de datos estructurados son SQL Server, Oracle y Azure Table.</span><span class="sxs-lookup"><span data-stu-id="c80c9-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="c80c9-233">Como la información de tipo ya está disponible para orígenes de datos estructurados, no debe incluir información de tipo cuando se incluye la sección sobre la estructura Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="c80c9-234">**Para el esquema en orígenes de datos de lectura (específicamente el almacenamiento de blobs)**, puede elegir toostore datos sin tener que almacenar cualquier información de tipo o esquema con datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="c80c9-235">Para estos tipos de orígenes de datos, incluyen una estructura cuando desee que las columnas toosink de columnas de origen de toomap.</span><span class="sxs-lookup"><span data-stu-id="c80c9-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="c80c9-236">También incluyen una estructura cuando hello es una entrada para una actividad de copia, y los tipos de datos del conjunto de datos de origen deben ser tipos toonative convertido para receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="c80c9-237">Factoría de datos admite Hola siguientes valores para proporcionar información de tipo de estructura: **Int16, Int32, Int64, Single, Double, Decimal, bytes [], un valor booleano, cadena, Guid, Datetime, Datetimeoffset y Timespan**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="c80c9-238">Estos valores son valores de tipos basados en .NET compatibles con Common Language Specification (CLS).</span><span class="sxs-lookup"><span data-stu-id="c80c9-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="c80c9-239">Factoría de datos realiza automáticamente las conversiones de tipos al mover el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="c80c9-240">Conjunto de datos availability</span><span class="sxs-lookup"><span data-stu-id="c80c9-240">Dataset availability</span></span>
<span data-ttu-id="c80c9-241">Hola **disponibilidad** sección en un conjunto de datos define la ventana de procesamiento de hello (por ejemplo, cada hora, diariamente, o semanal) para el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="c80c9-242">Para más información sobre las ventanas de actividad, consulte el artículo sobre [programación y ejecución](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="c80c9-243">Hola pasos de la sección de disponibilidad especifica que hello conjunto de datos de salida o generado por hora, o conjunto de datos de entrada de hello está disponible por hora:</span><span class="sxs-lookup"><span data-stu-id="c80c9-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="c80c9-244">Si canalización hello tiene Hola después de horas de inicio y finalización:</span><span class="sxs-lookup"><span data-stu-id="c80c9-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="c80c9-245">Hello conjunto de datos de salida se genera cada hora en la canalización de hello hora inicial y final.</span><span class="sxs-lookup"><span data-stu-id="c80c9-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="c80c9-246">Por lo tanto, esta canalización genera cinco segmentos de conjuntos de datos, uno por cada ventana de actividad (12 a.m. - 1 a.m., 1 a.m. - 2 a.m., 2 a.m. - 3 a.m., 3 a.m. - 4 a.m., 4 a.m. - 5 a.m.).</span><span class="sxs-lookup"><span data-stu-id="c80c9-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="c80c9-247">Hello tabla siguiente describe propiedades que puede utilizar en la sección de disponibilidad de hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="c80c9-248">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c80c9-248">Property</span></span> | <span data-ttu-id="c80c9-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="c80c9-249">Description</span></span> | <span data-ttu-id="c80c9-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c80c9-250">Required</span></span> | <span data-ttu-id="c80c9-251">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c80c9-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c80c9-252">frequency</span><span class="sxs-lookup"><span data-stu-id="c80c9-252">frequency</span></span> |<span data-ttu-id="c80c9-253">Especifica la unidad de tiempo de hello para la producción de segmento del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="c80c9-254"><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="c80c9-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="c80c9-255">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-255">Yes</span></span> |<span data-ttu-id="c80c9-256">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-256">NA</span></span> |
| <span data-ttu-id="c80c9-257">interval</span><span class="sxs-lookup"><span data-stu-id="c80c9-257">interval</span></span> |<span data-ttu-id="c80c9-258">Especifica un multiplicador para "frequency".</span><span class="sxs-lookup"><span data-stu-id="c80c9-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="c80c9-259">"Intervalo de frecuencia x" determina con qué frecuencia hello segmento se genera.</span><span class="sxs-lookup"><span data-stu-id="c80c9-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="c80c9-260">Por ejemplo, si necesita hello toobe de conjunto de datos se crean sectores de cada hora, establecer <b>frecuencia</b> demasiado<b>hora</b>, y <b>intervalo</b> demasiado<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="c80c9-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="c80c9-261">Tenga en cuenta que si especifica **frecuencia** como **minuto**, debe establecer Hola intervalo toono inferior a 15.</span><span class="sxs-lookup"><span data-stu-id="c80c9-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="c80c9-262">Sí</span><span class="sxs-lookup"><span data-stu-id="c80c9-262">Yes</span></span> |<span data-ttu-id="c80c9-263">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-263">NA</span></span> |
| <span data-ttu-id="c80c9-264">style</span><span class="sxs-lookup"><span data-stu-id="c80c9-264">style</span></span> |<span data-ttu-id="c80c9-265">Especifica si se debe generar el segmento de hello al inicio de Hola o al final del intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="c80c9-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="c80c9-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="c80c9-266">StartOfInterval</span></span></li><li><span data-ttu-id="c80c9-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="c80c9-267">EndOfInterval</span></span></li></ul><span data-ttu-id="c80c9-268">Si **frecuencia** se establece demasiado**mes**, y **estilo** se establece demasiado**EndOfInterval**, Hola segmento se genera en hello último día del mes.</span><span class="sxs-lookup"><span data-stu-id="c80c9-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="c80c9-269">Si **estilo** se establece demasiado**StartOfInterval**, se genera el segmento de hello en hello primer día del mes.</span><span class="sxs-lookup"><span data-stu-id="c80c9-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="c80c9-270">Si **frecuencia** se establece demasiado**día**, y **estilo** se establece demasiado**EndOfInterval**, Hola segmento se genera en la última hora del día de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="c80c9-271">Si **frecuencia** se establece demasiado**hora**, y **estilo** se establece demasiado**EndOfInterval**, Hola segmento se genera al final de Hola de hora de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="c80c9-272">Por ejemplo, para un intervalo de hello período 1 P.M. a 2 P.M., segmento de Hola se genera a las 2 P.M..</span><span class="sxs-lookup"><span data-stu-id="c80c9-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="c80c9-273">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-273">No</span></span> |<span data-ttu-id="c80c9-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="c80c9-274">EndOfInterval</span></span> |
| <span data-ttu-id="c80c9-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="c80c9-275">anchorDateTime</span></span> |<span data-ttu-id="c80c9-276">Define la posición absoluta de hello en el tiempo utilizado por los límites del sector de hello programador toocompute conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="c80c9-277">Tenga en cuenta que si esta propoerty tiene Dateparts más granulares de hello especifica la frecuencia, Hola partes más pormenorizadas se omiten.</span><span class="sxs-lookup"><span data-stu-id="c80c9-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="c80c9-278">Por ejemplo, si hello **intervalo** es **cada hora** (frecuencia: hora e intervalo: 1), hello y **anchorDateTime** contiene **minutos y segundos**, a continuación, Hola partes minutos y segundos de **anchorDateTime** se omiten.</span><span class="sxs-lookup"><span data-stu-id="c80c9-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="c80c9-279">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-279">No</span></span> |<span data-ttu-id="c80c9-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="c80c9-280">01/01/0001</span></span> |
| <span data-ttu-id="c80c9-281">Offset</span><span class="sxs-lookup"><span data-stu-id="c80c9-281">offset</span></span> |<span data-ttu-id="c80c9-282">Intervalo de tiempo por qué Hola se desplazan inicial y final de todos los sectores de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="c80c9-283">Tenga en cuenta que, si ambos **anchorDateTime** y **desplazamiento** se especifican, resultado de hello es Hola combinan MAYÚS.</span><span class="sxs-lookup"><span data-stu-id="c80c9-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="c80c9-284">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-284">No</span></span> |<span data-ttu-id="c80c9-285">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="c80c9-286">Ejemplo de offset</span><span class="sxs-lookup"><span data-stu-id="c80c9-286">offset example</span></span>
<span data-ttu-id="c80c9-287">De forma predeterminada, los segmentos diarios (`"frequency": "Day", "interval": 1`) comienzan a las 12 p.m. (medianoche), Hora universal coordinada (UTC).</span><span class="sxs-lookup"><span data-stu-id="c80c9-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="c80c9-288">Si desea Hola inicio toobe 6: 00 UTC hora en su lugar, establezca Hola offset tal como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="c80c9-289">Ejemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="c80c9-289">anchorDateTime example</span></span>
<span data-ttu-id="c80c9-290">En el siguiente ejemplo de Hola Hola conjunto de datos se produce una vez cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="c80c9-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="c80c9-291">Hello primer sector comienza en tiempo de hello especificado por **anchorDateTime**, que se establece demasiado`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="c80c9-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="c80c9-292">Ejemplo de offset/style</span><span class="sxs-lookup"><span data-stu-id="c80c9-292">offset/style example</span></span>
<span data-ttu-id="c80c9-293">Hola siguiente conjunto de datos es mensual y se genera en hello 3rd de cada mes a las 8:00 A.M. (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="c80c9-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="c80c9-294"><a name="Policy"></a>Directiva del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="c80c9-295">Hola **directiva** sección de definición de conjunto de datos de hello define los criterios de Hola o debe cumplir la condición de Hola que Hola segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="c80c9-296">Directivas de validación</span><span class="sxs-lookup"><span data-stu-id="c80c9-296">Validation policies</span></span>
| <span data-ttu-id="c80c9-297">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="c80c9-297">Policy name</span></span> | <span data-ttu-id="c80c9-298">Descripción</span><span class="sxs-lookup"><span data-stu-id="c80c9-298">Description</span></span> | <span data-ttu-id="c80c9-299">Aplica demasiado</span><span class="sxs-lookup"><span data-stu-id="c80c9-299">Applied too</span></span>| <span data-ttu-id="c80c9-300">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c80c9-300">Required</span></span> | <span data-ttu-id="c80c9-301">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c80c9-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c80c9-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="c80c9-302">minimumSizeMB</span></span> |<span data-ttu-id="c80c9-303">Valida datos hello en **almacenamiento de blobs de Azure** Hola de cumple los requisitos mínimos de tamaño (en megabytes).</span><span class="sxs-lookup"><span data-stu-id="c80c9-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="c80c9-304">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="c80c9-304">Azure Blob storage</span></span> |<span data-ttu-id="c80c9-305">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-305">No</span></span> |<span data-ttu-id="c80c9-306">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-306">NA</span></span> |
| <span data-ttu-id="c80c9-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="c80c9-307">minimumRows</span></span> |<span data-ttu-id="c80c9-308">Valida datos hello en un **base de datos SQL de Azure** o un **tabla de Azure** contiene Hola número mínimo de filas.</span><span class="sxs-lookup"><span data-stu-id="c80c9-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="c80c9-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c80c9-309">Azure SQL database</span></span></li><li><span data-ttu-id="c80c9-310">Tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="c80c9-310">Azure table</span></span></li></ul> |<span data-ttu-id="c80c9-311">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-311">No</span></span> |<span data-ttu-id="c80c9-312">N/D</span><span class="sxs-lookup"><span data-stu-id="c80c9-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="c80c9-313">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c80c9-313">Examples</span></span>
<span data-ttu-id="c80c9-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="c80c9-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="c80c9-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="c80c9-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="c80c9-316">Conjuntos de datos externos</span><span class="sxs-lookup"><span data-stu-id="c80c9-316">External datasets</span></span>
<span data-ttu-id="c80c9-317">Conjuntos de datos externos son hello las que no producidos por una canalización de factoría de datos de hello en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c80c9-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="c80c9-318">Si el conjunto de datos de hello está marcado como **externo**, hello **ExternalData** directiva puede ser definido tooinfluence Hola comportamiento de la disponibilidad de segmento del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="c80c9-319">A menos que se esté produciendo un conjunto de datos mediante Data Factory, debe marcarse como **external**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="c80c9-320">Esta configuración normalmente aplica toohello entradas de la primera actividad en una canalización, a menos que se está usando la actividad o el encadenamiento de canalización.</span><span class="sxs-lookup"><span data-stu-id="c80c9-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="c80c9-321">Nombre</span><span class="sxs-lookup"><span data-stu-id="c80c9-321">Name</span></span> | <span data-ttu-id="c80c9-322">Descripción</span><span class="sxs-lookup"><span data-stu-id="c80c9-322">Description</span></span> | <span data-ttu-id="c80c9-323">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c80c9-323">Required</span></span> | <span data-ttu-id="c80c9-324">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c80c9-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c80c9-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="c80c9-325">dataDelay</span></span> |<span data-ttu-id="c80c9-326">tiempo de Hola Hola toodelay Comprobar disponibilidad de Hola de datos externos de Hola de hello proporciona segmento.</span><span class="sxs-lookup"><span data-stu-id="c80c9-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="c80c9-327">Por ejemplo, puede retrasar una comprobación horaria mediante esta configuración.</span><span class="sxs-lookup"><span data-stu-id="c80c9-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="c80c9-328">Hola configuración solo aplica a toohello la hora actual.</span><span class="sxs-lookup"><span data-stu-id="c80c9-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="c80c9-329">Por ejemplo, si es 1:00 P.M. y este valor es 10 minutos, validación de hello comienza en 1:10 P.M..</span><span class="sxs-lookup"><span data-stu-id="c80c9-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="c80c9-330">Tenga en cuenta que esta configuración no afecta los segmentos en hello anterior.</span><span class="sxs-lookup"><span data-stu-id="c80c9-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="c80c9-331">Los segmentos con **Slice End Time** + **dataDelay** < **Now** se procesan sin retraso.</span><span class="sxs-lookup"><span data-stu-id="c80c9-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="c80c9-332">Veces mayor que 23:59 horas deben especificarse mediante hello `day.hours:minutes:seconds` formato.</span><span class="sxs-lookup"><span data-stu-id="c80c9-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="c80c9-333">Por ejemplo, toospecify 24 horas, no use 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="c80c9-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="c80c9-334">En su lugar, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="c80c9-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="c80c9-335">Si usa 24:00:00, se tratará como 24 días (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="c80c9-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="c80c9-336">Para 1 día y 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="c80c9-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="c80c9-337">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-337">No</span></span> |<span data-ttu-id="c80c9-338">0</span><span class="sxs-lookup"><span data-stu-id="c80c9-338">0</span></span> |
| <span data-ttu-id="c80c9-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="c80c9-339">retryInterval</span></span> |<span data-ttu-id="c80c9-340">tiempo de espera de Hello entre un intento siguiente hello y error.</span><span class="sxs-lookup"><span data-stu-id="c80c9-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="c80c9-341">Esta configuración aplica toopresent tiempo.</span><span class="sxs-lookup"><span data-stu-id="c80c9-341">This setting applies toopresent time.</span></span> <span data-ttu-id="c80c9-342">Si no se pudo try anterior hello, siguiente intento de hello es tras hello **retryInterval** período.</span><span class="sxs-lookup"><span data-stu-id="c80c9-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="c80c9-343">Si es 1:00 P.M., comenzaremos Hola primer intento.</span><span class="sxs-lookup"><span data-stu-id="c80c9-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="c80c9-344">Si Hola duración toocomplete Hola primera comprobación de validación es 1 minuto y error en la operación hello, Hola siguiente reintento es a 1:00 + 1 min (duración) + 1min (intervalo de reintento) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="c80c9-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="c80c9-345">Para los segmentos en hello anterior, no hay ningún retraso.</span><span class="sxs-lookup"><span data-stu-id="c80c9-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="c80c9-346">reintento de Hello ocurre inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c80c9-346">hello retry happens immediately.</span></span> |<span data-ttu-id="c80c9-347">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-347">No</span></span> |<span data-ttu-id="c80c9-348">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="c80c9-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="c80c9-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="c80c9-349">retryTimeout</span></span> |<span data-ttu-id="c80c9-350">tiempo de espera de Hola para cada reintento.</span><span class="sxs-lookup"><span data-stu-id="c80c9-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="c80c9-351">Si se establece esta propiedad too10 minutos, se debe completar la validación de hello dentro de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="c80c9-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="c80c9-352">Si se tarda más tiempo que la validación de hello tooperform de 10 minutos, Hola vuelva a intentar agota el tiempo.</span><span class="sxs-lookup"><span data-stu-id="c80c9-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="c80c9-353">Si todos los intentos de validación Hola vencen, Hola segmento está marcado como **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="c80c9-354">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-354">No</span></span> |<span data-ttu-id="c80c9-355">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="c80c9-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="c80c9-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="c80c9-356">maximumRetry</span></span> |<span data-ttu-id="c80c9-357">número de Hola de tiempo toocheck para disponibilidad Hola de datos externos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="c80c9-358">Hola valor máximo permitido es 10.</span><span class="sxs-lookup"><span data-stu-id="c80c9-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="c80c9-359">No</span><span class="sxs-lookup"><span data-stu-id="c80c9-359">No</span></span> |<span data-ttu-id="c80c9-360">3</span><span class="sxs-lookup"><span data-stu-id="c80c9-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="c80c9-361">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-361">Create datasets</span></span>
<span data-ttu-id="c80c9-362">Puede crear conjuntos de datos mediante el uso de algunas de estas herramientas o SDK:</span><span class="sxs-lookup"><span data-stu-id="c80c9-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="c80c9-363">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="c80c9-363">Copy Wizard</span></span> 
- <span data-ttu-id="c80c9-364">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c80c9-364">Azure portal</span></span>
- <span data-ttu-id="c80c9-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c80c9-365">Visual Studio</span></span>
- <span data-ttu-id="c80c9-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c80c9-366">PowerShell</span></span>
- <span data-ttu-id="c80c9-367">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="c80c9-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="c80c9-368">API de REST</span><span class="sxs-lookup"><span data-stu-id="c80c9-368">REST API</span></span>
- <span data-ttu-id="c80c9-369">API de .NET</span><span class="sxs-lookup"><span data-stu-id="c80c9-369">.NET API</span></span>

<span data-ttu-id="c80c9-370">Vea Hola tutoriales para obtener instrucciones paso a paso para crear canalizaciones y conjuntos de datos mediante una de estas herramientas o SDK:</span><span class="sxs-lookup"><span data-stu-id="c80c9-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="c80c9-371">Creación de una canalización con una actividad de transformación de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="c80c9-372">Creación de una canalización con una actividad de movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="c80c9-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="c80c9-373">Después de que se crea e implementa una canalización, puede administrar y supervisar sus canalizaciones mediante el uso de Hola hojas de portal de Azure, o una aplicación de supervisión y administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="c80c9-374">Vea Hola temas para obtener instrucciones paso a paso siguientes:</span><span class="sxs-lookup"><span data-stu-id="c80c9-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="c80c9-375">Supervisión y administración de canalizaciones con las hojas de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c80c9-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="c80c9-376">Supervisar y administrar las canalizaciones mediante el uso de la aplicación de supervisión y administración de hello</span><span class="sxs-lookup"><span data-stu-id="c80c9-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="c80c9-377">Conjuntos de datos limitados</span><span class="sxs-lookup"><span data-stu-id="c80c9-377">Scoped datasets</span></span>
<span data-ttu-id="c80c9-378">Puede crear conjuntos de datos con ámbito tooa canalización mediante el uso de hello **conjuntos de datos** propiedad.</span><span class="sxs-lookup"><span data-stu-id="c80c9-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="c80c9-379">Estos conjuntos de datos solo los pueden usar las actividades dentro de esta canalización, pero no las actividades de otras canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="c80c9-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="c80c9-380">Hola siguiente ejemplo define una canalización con toobe (rdc InputDataset y OutputDataset rdc) de dos conjuntos de datos utilizado en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="c80c9-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c80c9-381">Conjuntos de datos con ámbito solo son compatibles con las canalizaciones de un solo uso (donde **pipelineMode** se establece demasiado**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="c80c9-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="c80c9-382">Consulte la sección [Canalización de una vez](data-factory-create-pipelines.md#onetime-pipeline) para más información.</span><span class="sxs-lookup"><span data-stu-id="c80c9-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c80c9-383">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c80c9-383">Next steps</span></span>
- <span data-ttu-id="c80c9-384">Para más información sobre las canalizaciones, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="c80c9-385">Para más información sobre cómo programar y ejecutar canalizaciones en Azure Data Factory, consulte [este artículo](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
