---
title: aaaMove datos hacia y desde la tabla de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos hacia y desde almacenamiento de tabla de Azure mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="48d35-103">Mover tooand de datos de la tabla de Azure mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="48d35-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="48d35-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="48d35-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="48d35-106">Puede copiar datos desde cualquier origen compatible datos almacenan tooAzure almacenamiento de tabla o de datos de receptor de almacenamiento de tablas Azure tooany admitida almacenan.</span><span class="sxs-lookup"><span data-stu-id="48d35-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="48d35-107">Para obtener una lista de almacenes de datos admite como orígenes o receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="48d35-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="48d35-108">Introducción</span><span class="sxs-lookup"><span data-stu-id="48d35-108">Getting started</span></span>
<span data-ttu-id="48d35-109">Puede crear una canalización con una actividad de copia que mueva datos con Azure Table Storage como origen o destino mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="48d35-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="48d35-110">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="48d35-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="48d35-111">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="48d35-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="48d35-112">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="48d35-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="48d35-113">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="48d35-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="48d35-114">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="48d35-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="48d35-115">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="48d35-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="48d35-116">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="48d35-117">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="48d35-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="48d35-118">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="48d35-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="48d35-119">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="48d35-120">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia/desde un almacenamiento de tablas de Azure, vea [ejemplos JSON](#json-examples) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="48d35-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="48d35-121">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure almacenamiento de tabla:</span><span class="sxs-lookup"><span data-stu-id="48d35-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="48d35-122">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="48d35-122">Linked service properties</span></span>
<span data-ttu-id="48d35-123">Hay dos tipos de servicios vinculados que se puede usar toolink un generador de datos de Azure de tooan de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="48d35-124">Se trata del servicio vinculado **AzureStorage** y el servicio vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="48d35-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="48d35-125">Hola servicio vinculado de almacenamiento de Azure proporciona factoría de datos de hello con acceso global toohello almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="48d35-126">Mientras que vinculado hello Azure almacenamiento SAS (firma de acceso compartido) servicio proporciona factoría de datos de hello con acceso restringido tiempo enlazadas toohello almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="48d35-127">No existen otras diferencias entre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="48d35-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="48d35-128">Elegir servicio de hello vinculado que se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="48d35-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="48d35-129">Hello las secciones siguientes proporcionan más detalles sobre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="48d35-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="48d35-130">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="48d35-130">Dataset properties</span></span>
<span data-ttu-id="48d35-131">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="48d35-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="48d35-132">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="48d35-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="48d35-133">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="48d35-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="48d35-134">Hola **typeProperties** sección Hola conjunto de datos de tipo **AzureTable** tiene Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="48d35-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="48d35-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="48d35-135">Property</span></span> | <span data-ttu-id="48d35-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="48d35-136">Description</span></span> | <span data-ttu-id="48d35-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="48d35-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48d35-138">tableName</span><span class="sxs-lookup"><span data-stu-id="48d35-138">tableName</span></span> |<span data-ttu-id="48d35-139">Nombre de tabla de hello en la instancia de base de datos de tabla de Azure de Hola que servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="48d35-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="48d35-140">Sí.</span><span class="sxs-lookup"><span data-stu-id="48d35-140">Yes.</span></span> <span data-ttu-id="48d35-141">Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="48d35-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="48d35-142">Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="48d35-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="48d35-143">Esquema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="48d35-143">Schema by Data Factory</span></span>
<span data-ttu-id="48d35-144">En los almacenes de datos sin esquema como tabla de Azure, Hola servicio Data Factory deduce el esquema de hello en uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="48d35-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="48d35-145">Si especifica estructura Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, Hola servicio Data Factory respeta esta estructura como esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="48d35-146">En este caso, si una fila no contiene un valor para una columna, se proporciona un valor nulo para ella.</span><span class="sxs-lookup"><span data-stu-id="48d35-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="48d35-147">Si no especifica la estructura de Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, factoría de datos deduce el esquema de hello utilizando Hola primera fila de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="48d35-148">En este caso, si la primera fila de hello no contiene el esquema completo de hello, algunas columnas se omiten en el resultado de hello de operación de copia.</span><span class="sxs-lookup"><span data-stu-id="48d35-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="48d35-149">Por lo tanto, para orígenes de datos sin esquemas, se recomienda Hola es toospecify estructura de Hola de datos mediante Hola **estructura** propiedad.</span><span class="sxs-lookup"><span data-stu-id="48d35-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="48d35-150">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="48d35-150">Copy activity properties</span></span>
<span data-ttu-id="48d35-151">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="48d35-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="48d35-152">Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="48d35-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="48d35-153">Propiedades disponibles en la sección de typeProperties Hola de actividad de hello en hello otra parte varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="48d35-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="48d35-154">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="48d35-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="48d35-155">**AzureTableSource** admite Hola propiedades en la sección typeProperties siguientes:</span><span class="sxs-lookup"><span data-stu-id="48d35-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="48d35-156">Propiedad</span><span class="sxs-lookup"><span data-stu-id="48d35-156">Property</span></span> | <span data-ttu-id="48d35-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="48d35-157">Description</span></span> | <span data-ttu-id="48d35-158">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="48d35-158">Allowed values</span></span> | <span data-ttu-id="48d35-159">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="48d35-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48d35-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="48d35-160">azureTableSourceQuery</span></span> |<span data-ttu-id="48d35-161">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="48d35-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="48d35-162">Cadena de consulta de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-162">Azure table query string.</span></span> <span data-ttu-id="48d35-163">Vea los ejemplos en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-163">See examples in hello next section.</span></span> |<span data-ttu-id="48d35-164">No.</span><span class="sxs-lookup"><span data-stu-id="48d35-164">No.</span></span> <span data-ttu-id="48d35-165">Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="48d35-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="48d35-166">Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="48d35-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="48d35-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="48d35-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="48d35-168">Indica si debe Hola excepción de tabla no existe.</span><span class="sxs-lookup"><span data-stu-id="48d35-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="48d35-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="48d35-169">TRUE</span></span><br/><span data-ttu-id="48d35-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="48d35-170">FALSE</span></span> |<span data-ttu-id="48d35-171">No</span><span class="sxs-lookup"><span data-stu-id="48d35-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="48d35-172">ejemplos de azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="48d35-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="48d35-173">Si la columna de la Tabla de Azure es de tipo cadena:</span><span class="sxs-lookup"><span data-stu-id="48d35-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="48d35-174">Si la columna de la Tabla de Azure es de tipo datetime:</span><span class="sxs-lookup"><span data-stu-id="48d35-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="48d35-175">**AzureTableSink** admite Hola propiedades en la sección typeProperties siguientes:</span><span class="sxs-lookup"><span data-stu-id="48d35-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="48d35-176">Propiedad</span><span class="sxs-lookup"><span data-stu-id="48d35-176">Property</span></span> | <span data-ttu-id="48d35-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="48d35-177">Description</span></span> | <span data-ttu-id="48d35-178">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="48d35-178">Allowed values</span></span> | <span data-ttu-id="48d35-179">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="48d35-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="48d35-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="48d35-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="48d35-181">Partición clave valor predeterminado que se puede usar en el receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="48d35-182">Valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="48d35-182">A string value.</span></span> |<span data-ttu-id="48d35-183">No</span><span class="sxs-lookup"><span data-stu-id="48d35-183">No</span></span> |
| <span data-ttu-id="48d35-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="48d35-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="48d35-185">Especifique el nombre de columna de hello cuyos valores se usan como claves de partición.</span><span class="sxs-lookup"><span data-stu-id="48d35-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="48d35-186">Si no se especifica, AzureTableDefaultPartitionKeyValue se usa como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="48d35-187">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="48d35-187">A column name.</span></span> |<span data-ttu-id="48d35-188">No</span><span class="sxs-lookup"><span data-stu-id="48d35-188">No</span></span> |
| <span data-ttu-id="48d35-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="48d35-189">azureTableRowKeyName</span></span> |<span data-ttu-id="48d35-190">Especifique el nombre de columna de hello cuyos valores de columna se utilizan como clave de fila.</span><span class="sxs-lookup"><span data-stu-id="48d35-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="48d35-191">Si no se especifica, use un GUID para cada fila.</span><span class="sxs-lookup"><span data-stu-id="48d35-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="48d35-192">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="48d35-192">A column name.</span></span> |<span data-ttu-id="48d35-193">No</span><span class="sxs-lookup"><span data-stu-id="48d35-193">No</span></span> |
| <span data-ttu-id="48d35-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="48d35-194">azureTableInsertType</span></span> |<span data-ttu-id="48d35-195">datos de tooinsert de modo de saludo en tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="48d35-196">Esta propiedad controla si las filas existentes en la tabla de salida de hello con claves de partición y fila coincidentes tienen sus valores reemplazará o se combinará.</span><span class="sxs-lookup"><span data-stu-id="48d35-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="48d35-197">toolearn acerca de cómo funcionan estas configuraciones (combinación y reemplazo), consulte [Insert o Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) y [insertar o reemplazar entidades](https://msdn.microsoft.com/library/azure/hh452242.aspx) temas.</span><span class="sxs-lookup"><span data-stu-id="48d35-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="48d35-198">Esta configuración se aplica a nivel de fila de hello, no nivel de tabla de hello, y ninguna de estas opciones eliminan las filas de tabla de salida de hello que no existen en la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="48d35-199">merge (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="48d35-199">merge (default)</span></span><br/><span data-ttu-id="48d35-200">replace</span><span class="sxs-lookup"><span data-stu-id="48d35-200">replace</span></span> |<span data-ttu-id="48d35-201">No</span><span class="sxs-lookup"><span data-stu-id="48d35-201">No</span></span> |
| <span data-ttu-id="48d35-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="48d35-202">writeBatchSize</span></span> |<span data-ttu-id="48d35-203">Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="48d35-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="48d35-204">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="48d35-204">Integer (number of rows)</span></span> |<span data-ttu-id="48d35-205">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="48d35-205">No (default: 10000)</span></span> |
| <span data-ttu-id="48d35-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="48d35-206">writeBatchTimeout</span></span> |<span data-ttu-id="48d35-207">Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="48d35-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="48d35-208">timespan</span><span class="sxs-lookup"><span data-stu-id="48d35-208">timespan</span></span><br/><br/><span data-ttu-id="48d35-209">Ejemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="48d35-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="48d35-210">No (valor de tiempo de espera predeterminado toostorage cliente predeterminado 90 seg)</span><span class="sxs-lookup"><span data-stu-id="48d35-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="48d35-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="48d35-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="48d35-212">Asignar una columna de destino tooa de columna de origen mediante la propiedad JSON de traductor de Hola para poder usar las columnas de destino hello como Hola azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="48d35-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="48d35-213">En el siguiente ejemplo de Hola, columna de origen DivisionID es toohello asignado las columnas de destino: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="48d35-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="48d35-214">Hola DivisionID se especifica como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="48d35-215">Ejemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="48d35-215">JSON examples</span></span>
<span data-ttu-id="48d35-216">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="48d35-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="48d35-217">Muestran cómo toocopy tooand de datos de almacenamiento de tabla de Azure y base de datos de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="48d35-218">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de hello orígenes tooany de receptores de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="48d35-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="48d35-219">Para obtener más información, consulte sección de Hola "almacenes de datos admitidos y formatos" en [mover datos mediante la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="48d35-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="48d35-220">Ejemplo: Copiar los datos de tabla de Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="48d35-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="48d35-221">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="48d35-221">hello following sample shows:</span></span>

1. <span data-ttu-id="48d35-222">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabla y blob).</span><span class="sxs-lookup"><span data-stu-id="48d35-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="48d35-223">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="48d35-224">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="48d35-225">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [AzureTableSource](#activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="48d35-226">ejemplo de Hola copia los datos que pertenecen a partición predeterminada de toohello en un blob de tooa de la tabla de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="48d35-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="48d35-227">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="48d35-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="48d35-228">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="48d35-228">**Azure storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="48d35-229">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="48d35-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="48d35-230">Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="48d35-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="48d35-231">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="48d35-232">**Conjunto de datos de entrada de tabla de Azure:**</span><span class="sxs-lookup"><span data-stu-id="48d35-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="48d35-233">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="48d35-234">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

<span data-ttu-id="48d35-235">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="48d35-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="48d35-236">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="48d35-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="48d35-237">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="48d35-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="48d35-238">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="48d35-239">**Actividad de copia en una canalización con AzureTableSource y BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="48d35-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="48d35-240">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="48d35-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="48d35-241">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**AzureTableSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="48d35-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="48d35-242">consulta SQL Hola especificada con **AzureTableSourceQuery** propiedad selecciona datos de Hola de partición predeterminada de hello toocopy de cada hora.</span><span class="sxs-lookup"><span data-stu-id="48d35-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="48d35-243">Ejemplo: Copiar los datos de Blob de Azure tooAzure tabla</span><span class="sxs-lookup"><span data-stu-id="48d35-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="48d35-244">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="48d35-244">hello following sample shows:</span></span>

1. <span data-ttu-id="48d35-245">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabla y blob)</span><span class="sxs-lookup"><span data-stu-id="48d35-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="48d35-246">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="48d35-247">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="48d35-248">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="48d35-249">ejemplo de Hola copia datos de serie temporal de una tabla de Azure tooan de blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="48d35-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="48d35-250">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="48d35-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="48d35-251">**Servicio vinculado de Azure Storage (para tabla y blob de Azure):**</span><span class="sxs-lookup"><span data-stu-id="48d35-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="48d35-252">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="48d35-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="48d35-253">Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="48d35-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="48d35-254">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="48d35-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="48d35-255">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="48d35-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="48d35-256">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="48d35-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="48d35-257">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="48d35-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="48d35-258">ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="48d35-259">"externo": "true" configuración informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
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

<span data-ttu-id="48d35-260">**Conjunto de datos de salida de tabla de Azure:**</span><span class="sxs-lookup"><span data-stu-id="48d35-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="48d35-261">ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="48d35-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="48d35-262">Crear una tabla de Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="48d35-263">Se agregan nuevas filas toohello tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="48d35-263">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="48d35-264">**Actividad de copia en una canalización con BlobSource y AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="48d35-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="48d35-265">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="48d35-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="48d35-266">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="48d35-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="48d35-267">Asignación de tipos para tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="48d35-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="48d35-268">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="48d35-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="48d35-269">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="48d35-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="48d35-270">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="48d35-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="48d35-271">Cuando se mueven datos demasiado & de tabla de Azure, Hola después [asignaciones definidas por el servicio tabla de Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) sirven del tipo de too.NET de tipos de OData de la tabla de Azure y viceversa.</span><span class="sxs-lookup"><span data-stu-id="48d35-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="48d35-272">Tipo de datos OData</span><span class="sxs-lookup"><span data-stu-id="48d35-272">OData Data Type</span></span> | <span data-ttu-id="48d35-273">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="48d35-273">.NET Type</span></span> | <span data-ttu-id="48d35-274">Detalles</span><span class="sxs-lookup"><span data-stu-id="48d35-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48d35-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="48d35-275">Edm.Binary</span></span> |<span data-ttu-id="48d35-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="48d35-276">byte[]</span></span> |<span data-ttu-id="48d35-277">Una matriz de bytes de too64 KB.</span><span class="sxs-lookup"><span data-stu-id="48d35-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="48d35-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="48d35-278">Edm.Boolean</span></span> |<span data-ttu-id="48d35-279">booleano</span><span class="sxs-lookup"><span data-stu-id="48d35-279">bool</span></span> |<span data-ttu-id="48d35-280">Valor booleano.</span><span class="sxs-lookup"><span data-stu-id="48d35-280">A Boolean value.</span></span> |
| <span data-ttu-id="48d35-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="48d35-281">Edm.DateTime</span></span> |<span data-ttu-id="48d35-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="48d35-282">DateTime</span></span> |<span data-ttu-id="48d35-283">Valor de 64 bits expresado como hora universal coordinada (UTC).</span><span class="sxs-lookup"><span data-stu-id="48d35-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="48d35-284">Hola admite DateTime intervalo comienza desde 12:00 de la medianoche del 1 de enero de 1601 D.C.</span><span class="sxs-lookup"><span data-stu-id="48d35-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="48d35-285">(E.C.), UTC.</span><span class="sxs-lookup"><span data-stu-id="48d35-285">(C.E.), UTC.</span></span> <span data-ttu-id="48d35-286">intervalo de Hello finaliza en 31 de diciembre de 9999.</span><span class="sxs-lookup"><span data-stu-id="48d35-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="48d35-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="48d35-287">Edm.Double</span></span> |<span data-ttu-id="48d35-288">double</span><span class="sxs-lookup"><span data-stu-id="48d35-288">double</span></span> |<span data-ttu-id="48d35-289">Valor de punto flotante de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="48d35-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="48d35-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="48d35-290">Edm.Guid</span></span> |<span data-ttu-id="48d35-291">Guid</span><span class="sxs-lookup"><span data-stu-id="48d35-291">Guid</span></span> |<span data-ttu-id="48d35-292">Identificador único global de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="48d35-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="48d35-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="48d35-293">Edm.Int32</span></span> |<span data-ttu-id="48d35-294">Int32</span><span class="sxs-lookup"><span data-stu-id="48d35-294">Int32</span></span> |<span data-ttu-id="48d35-295">Entero de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="48d35-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="48d35-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="48d35-296">Edm.Int64</span></span> |<span data-ttu-id="48d35-297">Int64</span><span class="sxs-lookup"><span data-stu-id="48d35-297">Int64</span></span> |<span data-ttu-id="48d35-298">Entero de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="48d35-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="48d35-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="48d35-299">Edm.String</span></span> |<span data-ttu-id="48d35-300">String</span><span class="sxs-lookup"><span data-stu-id="48d35-300">String</span></span> |<span data-ttu-id="48d35-301">Valor codificado mediante UTF-16.</span><span class="sxs-lookup"><span data-stu-id="48d35-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="48d35-302">Valores de cadena pueden ser up too64 KB.</span><span class="sxs-lookup"><span data-stu-id="48d35-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="48d35-303">Ejemplo de conversión de tipo</span><span class="sxs-lookup"><span data-stu-id="48d35-303">Type Conversion Sample</span></span>
<span data-ttu-id="48d35-304">Hola según muestra es para copiar datos de una tabla de tooAzure de Blob de Azure con conversiones de tipos.</span><span class="sxs-lookup"><span data-stu-id="48d35-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="48d35-305">Suponga que el conjunto de datos de hello Blob está en formato CSV y contiene tres columnas.</span><span class="sxs-lookup"><span data-stu-id="48d35-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="48d35-306">Uno de ellos es una columna de fecha y hora con un formato de fecha y hora personalizado mediante francés abreviaturas para el día de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="48d35-307">Definir el conjunto de datos de origen de blobs de hello como se indica a continuación junto con las definiciones de tipo para las columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="48d35-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="48d35-308">Proporciona asignación de tipos de Hola de OData de la tabla de Azure tipo too.NET, tendría que definir tabla hello en la tabla de Azure con hello después de esquema.</span><span class="sxs-lookup"><span data-stu-id="48d35-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="48d35-309">**Esquema de tabla de Azure:**</span><span class="sxs-lookup"><span data-stu-id="48d35-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="48d35-310">Nombre de la columna</span><span class="sxs-lookup"><span data-stu-id="48d35-310">Column name</span></span> | <span data-ttu-id="48d35-311">Tipo</span><span class="sxs-lookup"><span data-stu-id="48d35-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="48d35-312">userid</span><span class="sxs-lookup"><span data-stu-id="48d35-312">userid</span></span> |<span data-ttu-id="48d35-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="48d35-313">Edm.Int64</span></span> |
| <span data-ttu-id="48d35-314">name</span><span class="sxs-lookup"><span data-stu-id="48d35-314">name</span></span> |<span data-ttu-id="48d35-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="48d35-315">Edm.String</span></span> |
| <span data-ttu-id="48d35-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="48d35-316">lastlogindate</span></span> |<span data-ttu-id="48d35-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="48d35-317">Edm.DateTime</span></span> |

<span data-ttu-id="48d35-318">A continuación, definir el conjunto de datos de tabla de Azure de Hola de como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="48d35-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="48d35-319">No es necesario toospecify sección de "estructura" con la información de tipo hello puesto que ya se ha especificado información de tipo hello Hola subyacente de almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="48d35-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="48d35-320">En este caso, el generador de datos automáticamente conversiones de tipos incluidos los campos de fecha y hora de hello con formato de fecha y hora personalizado hello mediante una referencia cultural "fr-fr" hello al mover los datos de Blob tooAzure tabla.</span><span class="sxs-lookup"><span data-stu-id="48d35-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="48d35-321">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="48d35-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="48d35-322">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="48d35-322">Performance and Tuning</span></span>
<span data-ttu-id="48d35-323">toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas formas, consulte [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="48d35-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
