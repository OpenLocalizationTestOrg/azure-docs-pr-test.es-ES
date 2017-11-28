---
title: Traslado de datos hacia la Tabla de Azure y desde ella | Microsoft Docs
description: "Obtenga información acerca de cómo mover los datos hacia y desde Almacenamiento de tablas de Azure mediante Factoría de datos de Azure."
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
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="28294-103">Movimiento de datos hacia y desde Tabla de Azure mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="28294-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="28294-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos hacia Azure Table Storage y desde este servicio.</span><span class="sxs-lookup"><span data-stu-id="28294-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="28294-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="28294-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="28294-106">Puede copiar datos de cualquier almacén de datos de origen compatible a Azure Table Storage o de Azure Table Storage a cualquier almacén de datos receptor compatible.</span><span class="sxs-lookup"><span data-stu-id="28294-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="28294-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como orígenes o receptores.</span><span class="sxs-lookup"><span data-stu-id="28294-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="28294-108">Introducción</span><span class="sxs-lookup"><span data-stu-id="28294-108">Getting started</span></span>
<span data-ttu-id="28294-109">Puede crear una canalización con una actividad de copia que mueva datos con Azure Table Storage como origen o destino mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="28294-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="28294-110">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="28294-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="28294-111">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="28294-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="28294-112">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="28294-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="28294-113">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="28294-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="28294-114">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="28294-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="28294-115">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="28294-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="28294-116">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="28294-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="28294-117">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="28294-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="28294-118">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="28294-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="28294-119">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="28294-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="28294-120">Para obtener ejemplos con definiciones de JSON para entidades de Data Factory que se utilizan para copiar datos con Azure Table Storage como origen o destino, consulte la sección [Ejemplos de JSON](#json-examples) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="28294-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="28294-121">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Azure Table Storage:</span><span class="sxs-lookup"><span data-stu-id="28294-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="28294-122">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="28294-122">Linked service properties</span></span>
<span data-ttu-id="28294-123">Hay dos tipos de servicios vinculados que puede usar para vincular un almacenamiento de blobs de Azure a una Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="28294-124">Se trata del servicio vinculado **AzureStorage** y el servicio vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="28294-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="28294-125">El servicio vinculado de Almacenamiento de Azure proporciona a la factoría de datos acceso global al Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="28294-126">Mientras que el servicio vinculado de SAS (firma de acceso compartido) de Almacenamiento de Azure proporciona a la factoría de datos acceso restringido/controlado por tiempo al Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="28294-127">No existen otras diferencias entre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="28294-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="28294-128">Elija el servicio vinculado que se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="28294-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="28294-129">En las siguientes secciones se ofrecen más detalles sobre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="28294-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="28294-130">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="28294-130">Dataset properties</span></span>
<span data-ttu-id="28294-131">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="28294-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="28294-132">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="28294-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="28294-133">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="28294-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="28294-134">La sección **typeProperties** del conjunto de datos de tipo **AzureTable** tiene las propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="28294-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="28294-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28294-135">Property</span></span> | <span data-ttu-id="28294-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="28294-136">Description</span></span> | <span data-ttu-id="28294-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="28294-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28294-138">tableName</span><span class="sxs-lookup"><span data-stu-id="28294-138">tableName</span></span> |<span data-ttu-id="28294-139">Nombre de la tabla en la instancia de Base de datos de tablas de Azure a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="28294-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="28294-140">Sí.</span><span class="sxs-lookup"><span data-stu-id="28294-140">Yes.</span></span> <span data-ttu-id="28294-141">Cuando se especifica un elemento tableName sin azureTableSourceQuery, se copian todos los registros de la tabla en el destino.</span><span class="sxs-lookup"><span data-stu-id="28294-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="28294-142">Si también se especifica azureTableSourceQuery, los registros de la tabla que satisfacen los requisitos de la consulta se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="28294-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="28294-143">Esquema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="28294-143">Schema by Data Factory</span></span>
<span data-ttu-id="28294-144">En los almacenes de datos sin esquemas como Tabla de Azure, el servicio Data Factory deduce el esquema de una de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="28294-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="28294-145">Si especifica la estructura de los datos mediante la propiedad **structure** en la definición del conjunto de datos, el servicio Data Factory respeta esta como la estructura del esquema.</span><span class="sxs-lookup"><span data-stu-id="28294-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="28294-146">En este caso, si una fila no contiene un valor para una columna, se proporciona un valor nulo para ella.</span><span class="sxs-lookup"><span data-stu-id="28294-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="28294-147">Si no especifica la estructura de los datos mediante la propiedad **structure** en la definición del conjunto de datos, Data Factory deduce el esquema usando la primera fila de los datos.</span><span class="sxs-lookup"><span data-stu-id="28294-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="28294-148">En este caso, si la primera fila no contiene el esquema completo, algunas columnas se pierden en el resultado de la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="28294-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="28294-149">Por lo tanto, para los orígenes de datos sin esquemas, lo mejor es especificar la estructura de los datos mediante la propiedad **structure** .</span><span class="sxs-lookup"><span data-stu-id="28294-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="28294-150">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="28294-150">Copy activity properties</span></span>
<span data-ttu-id="28294-151">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="28294-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="28294-152">Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="28294-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="28294-153">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="28294-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="28294-154">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="28294-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="28294-155">**AzureTableSource** admite las siguientes propiedades en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="28294-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="28294-156">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28294-156">Property</span></span> | <span data-ttu-id="28294-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="28294-157">Description</span></span> | <span data-ttu-id="28294-158">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="28294-158">Allowed values</span></span> | <span data-ttu-id="28294-159">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="28294-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="28294-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="28294-160">azureTableSourceQuery</span></span> |<span data-ttu-id="28294-161">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="28294-161">Use the custom query to read data.</span></span> |<span data-ttu-id="28294-162">Cadena de consulta de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-162">Azure table query string.</span></span> <span data-ttu-id="28294-163">Consulte los ejemplos en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="28294-163">See examples in the next section.</span></span> |<span data-ttu-id="28294-164">No.</span><span class="sxs-lookup"><span data-stu-id="28294-164">No.</span></span> <span data-ttu-id="28294-165">Cuando se especifica un elemento tableName sin azureTableSourceQuery, se copian todos los registros de la tabla en el destino.</span><span class="sxs-lookup"><span data-stu-id="28294-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="28294-166">Si también se especifica azureTableSourceQuery, los registros de la tabla que satisfacen los requisitos de la consulta se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="28294-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="28294-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="28294-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="28294-168">Indica si se omite la excepción de la tabla inexistente.</span><span class="sxs-lookup"><span data-stu-id="28294-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="28294-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="28294-169">TRUE</span></span><br/><span data-ttu-id="28294-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="28294-170">FALSE</span></span> |<span data-ttu-id="28294-171">No</span><span class="sxs-lookup"><span data-stu-id="28294-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="28294-172">ejemplos de azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="28294-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="28294-173">Si la columna de la Tabla de Azure es de tipo cadena:</span><span class="sxs-lookup"><span data-stu-id="28294-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="28294-174">Si la columna de la Tabla de Azure es de tipo datetime:</span><span class="sxs-lookup"><span data-stu-id="28294-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="28294-175">**AzureTableSink** admite las siguientes propiedades en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="28294-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="28294-176">Propiedad</span><span class="sxs-lookup"><span data-stu-id="28294-176">Property</span></span> | <span data-ttu-id="28294-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="28294-177">Description</span></span> | <span data-ttu-id="28294-178">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="28294-178">Allowed values</span></span> | <span data-ttu-id="28294-179">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="28294-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="28294-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="28294-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="28294-181">Valor predeterminado de la clave de la partición que puede usar el receptor.</span><span class="sxs-lookup"><span data-stu-id="28294-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="28294-182">Valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="28294-182">A string value.</span></span> |<span data-ttu-id="28294-183">No</span><span class="sxs-lookup"><span data-stu-id="28294-183">No</span></span> |
| <span data-ttu-id="28294-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="28294-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="28294-185">Especifique el nombre de la columna cuyos valores se usan como claves de partición.</span><span class="sxs-lookup"><span data-stu-id="28294-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="28294-186">Si no se especifica, se utiliza AzureTableDefaultPartitionKeyValue como clave de la partición.</span><span class="sxs-lookup"><span data-stu-id="28294-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="28294-187">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="28294-187">A column name.</span></span> |<span data-ttu-id="28294-188">No</span><span class="sxs-lookup"><span data-stu-id="28294-188">No</span></span> |
| <span data-ttu-id="28294-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="28294-189">azureTableRowKeyName</span></span> |<span data-ttu-id="28294-190">Especifique el nombre de la columna cuyos valores se usan como claves de fila.</span><span class="sxs-lookup"><span data-stu-id="28294-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="28294-191">Si no se especifica, use un GUID para cada fila.</span><span class="sxs-lookup"><span data-stu-id="28294-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="28294-192">Un nombre de columna.</span><span class="sxs-lookup"><span data-stu-id="28294-192">A column name.</span></span> |<span data-ttu-id="28294-193">No</span><span class="sxs-lookup"><span data-stu-id="28294-193">No</span></span> |
| <span data-ttu-id="28294-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="28294-194">azureTableInsertType</span></span> |<span data-ttu-id="28294-195">Modo de insertar datos en la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="28294-196">Esta propiedad controla si los valores de las filas existentes en la tabla de salida con claves de partición y de fila coincidentes se van a reemplazar o a combinar.</span><span class="sxs-lookup"><span data-stu-id="28294-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="28294-197">Consulte los temas [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Insertar o combinar entidad) e [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Insertar o remplazar entidad) para más información sobre cómo funcionan estas opciones (combinación y reemplazo).</span><span class="sxs-lookup"><span data-stu-id="28294-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="28294-198">Esta configuración se aplica en el nivel de fila, no en el nivel de tabla, y ninguna opción elimina filas de la tabla de salida que no existan en la entrada.</span><span class="sxs-lookup"><span data-stu-id="28294-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="28294-199">merge (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="28294-199">merge (default)</span></span><br/><span data-ttu-id="28294-200">replace</span><span class="sxs-lookup"><span data-stu-id="28294-200">replace</span></span> |<span data-ttu-id="28294-201">No</span><span class="sxs-lookup"><span data-stu-id="28294-201">No</span></span> |
| <span data-ttu-id="28294-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="28294-202">writeBatchSize</span></span> |<span data-ttu-id="28294-203">Inserta datos en la tabla de Azure cuando se alcanza el valor de writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="28294-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="28294-204">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="28294-204">Integer (number of rows)</span></span> |<span data-ttu-id="28294-205">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="28294-205">No (default: 10000)</span></span> |
| <span data-ttu-id="28294-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="28294-206">writeBatchTimeout</span></span> |<span data-ttu-id="28294-207">Inserta datos en la tabla de Azure cuando se alcanza el valor de writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="28294-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="28294-208">timespan</span><span class="sxs-lookup"><span data-stu-id="28294-208">timespan</span></span><br/><br/><span data-ttu-id="28294-209">Ejemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="28294-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="28294-210">No (el valor predeterminado de intervalo de tiempo del cliente de almacenamiento es 90 segundos)</span><span class="sxs-lookup"><span data-stu-id="28294-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="28294-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="28294-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="28294-212">Asigne una columna de origen a una columna de destino con la propiedad JSON de traductor para poder usar la columna de destino como azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="28294-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="28294-213">En el ejemplo siguiente, la columna de origen DivisionID se asigna a la columna de destino DivisionID.</span><span class="sxs-lookup"><span data-stu-id="28294-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="28294-214">El valor DivisionID se especifica como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="28294-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="28294-215">Ejemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="28294-215">JSON examples</span></span>
<span data-ttu-id="28294-216">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="28294-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="28294-217">En ellos se muestra cómo copiar datos entre Almacenamiento de tablas de Azure y Base de datos de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="28294-218">En cambio, los datos pueden copiarse **directamente** desde cualquiera de los orígenes a cualquiera de los receptores admitidos.</span><span class="sxs-lookup"><span data-stu-id="28294-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="28294-219">Para más información, vea la sección "Almacenes de datos y formatos que se admiten" del artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="28294-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="28294-220">Ejemplo: Copia de datos de una tabla de Azure a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="28294-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="28294-221">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="28294-221">The following sample shows:</span></span>

1. <span data-ttu-id="28294-222">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabla y blob).</span><span class="sxs-lookup"><span data-stu-id="28294-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="28294-223">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="28294-224">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="28294-225">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [AzureTableSource](#activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="28294-226">El ejemplo copia los datos que pertenecen a la partición predeterminada de una tabla de Azure a un blob cada hora.</span><span class="sxs-lookup"><span data-stu-id="28294-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="28294-227">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="28294-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="28294-228">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="28294-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="28294-229">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="28294-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="28294-230">En el primer caso, especifique la cadena de conexión que incluye la clave de cuenta. En el segundo, especifique el Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="28294-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="28294-231">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="28294-232">**Conjunto de datos de entrada de tabla de Azure:**</span><span class="sxs-lookup"><span data-stu-id="28294-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="28294-233">El ejemplo se supone que ha creado una tabla "MyTable" en la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="28294-234">Si se establece "external": "true", se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="28294-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="28294-235">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="28294-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="28294-236">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="28294-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="28294-237">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="28294-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="28294-238">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="28294-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="28294-239">**Actividad de copia en una canalización con AzureTableSource y BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="28294-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="28294-240">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="28294-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="28294-241">En la definición de JSON de canalización, el tipo **source** se establece en **AzureTableSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="28294-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="28294-242">La consulta SQL especificada con la propiedad **AzureTableSourceQuery** selecciona los datos de la partición predeterminada cada hora, que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="28294-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="28294-243">Ejemplo: Copia de datos de un blob de Azure a una tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="28294-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="28294-244">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="28294-244">The following sample shows:</span></span>

1. <span data-ttu-id="28294-245">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabla y blob)</span><span class="sxs-lookup"><span data-stu-id="28294-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="28294-246">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="28294-247">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="28294-248">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="28294-249">En el ejemplo se copian datos de series temporales de un blob de Azure a una tabla de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="28294-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="28294-250">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="28294-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="28294-251">**Servicio vinculado de Azure Storage (para tabla y blob de Azure):**</span><span class="sxs-lookup"><span data-stu-id="28294-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="28294-252">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="28294-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="28294-253">En el primer caso, especifique la cadena de conexión que incluye la clave de cuenta. En el segundo, especifique el Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="28294-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="28294-254">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="28294-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="28294-255">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="28294-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="28294-256">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="28294-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="28294-257">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="28294-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="28294-258">La ruta de acceso de la carpeta usa la parte year, month y day de la hora de inicio y el nombre de archivo, la parte hour.</span><span class="sxs-lookup"><span data-stu-id="28294-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="28294-259">El valor external: true informa al servicio Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="28294-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="28294-260">**Conjunto de datos de salida de tabla de Azure:**</span><span class="sxs-lookup"><span data-stu-id="28294-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="28294-261">El ejemplo copia los datos a una tabla denominada "MyTable" en la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="28294-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="28294-262">Cree una tabla de Azure con el mismo número de columnas que espera que contenga el archivo CSV de blob.</span><span class="sxs-lookup"><span data-stu-id="28294-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="28294-263">Se agregan nuevas filas a la tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="28294-263">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="28294-264">**Actividad de copia en una canalización con BlobSource y AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="28294-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="28294-265">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="28294-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="28294-266">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="28294-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="28294-267">Asignación de tipos para tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="28294-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="28294-268">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="28294-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="28294-269">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="28294-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="28294-270">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="28294-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="28294-271">Al mover datos a y desde Azure Table, se usan las siguientes [asignaciones definidas por Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) desde tipos OData de Azure Table a tipos .NET y viceversa.</span><span class="sxs-lookup"><span data-stu-id="28294-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="28294-272">Tipo de datos OData</span><span class="sxs-lookup"><span data-stu-id="28294-272">OData Data Type</span></span> | <span data-ttu-id="28294-273">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="28294-273">.NET Type</span></span> | <span data-ttu-id="28294-274">Detalles</span><span class="sxs-lookup"><span data-stu-id="28294-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28294-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="28294-275">Edm.Binary</span></span> |<span data-ttu-id="28294-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="28294-276">byte[]</span></span> |<span data-ttu-id="28294-277">Matriz de bytes de hasta 64 KB.</span><span class="sxs-lookup"><span data-stu-id="28294-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="28294-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="28294-278">Edm.Boolean</span></span> |<span data-ttu-id="28294-279">booleano</span><span class="sxs-lookup"><span data-stu-id="28294-279">bool</span></span> |<span data-ttu-id="28294-280">Valor booleano.</span><span class="sxs-lookup"><span data-stu-id="28294-280">A Boolean value.</span></span> |
| <span data-ttu-id="28294-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="28294-281">Edm.DateTime</span></span> |<span data-ttu-id="28294-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="28294-282">DateTime</span></span> |<span data-ttu-id="28294-283">Valor de 64 bits expresado como hora universal coordinada (UTC).</span><span class="sxs-lookup"><span data-stu-id="28294-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="28294-284">El intervalo admitido de DateTime comienza a las 12:00 de la noche del 1 de enero de 1601 D.C.</span><span class="sxs-lookup"><span data-stu-id="28294-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="28294-285">(E.C.), UTC.</span><span class="sxs-lookup"><span data-stu-id="28294-285">(C.E.), UTC.</span></span> <span data-ttu-id="28294-286">El intervalo finaliza el 31 de diciembre de 9999.</span><span class="sxs-lookup"><span data-stu-id="28294-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="28294-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="28294-287">Edm.Double</span></span> |<span data-ttu-id="28294-288">double</span><span class="sxs-lookup"><span data-stu-id="28294-288">double</span></span> |<span data-ttu-id="28294-289">Valor de punto flotante de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="28294-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="28294-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="28294-290">Edm.Guid</span></span> |<span data-ttu-id="28294-291">Guid</span><span class="sxs-lookup"><span data-stu-id="28294-291">Guid</span></span> |<span data-ttu-id="28294-292">Identificador único global de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="28294-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="28294-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="28294-293">Edm.Int32</span></span> |<span data-ttu-id="28294-294">Int32</span><span class="sxs-lookup"><span data-stu-id="28294-294">Int32</span></span> |<span data-ttu-id="28294-295">Entero de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="28294-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="28294-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="28294-296">Edm.Int64</span></span> |<span data-ttu-id="28294-297">Int64</span><span class="sxs-lookup"><span data-stu-id="28294-297">Int64</span></span> |<span data-ttu-id="28294-298">Entero de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="28294-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="28294-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="28294-299">Edm.String</span></span> |<span data-ttu-id="28294-300">String</span><span class="sxs-lookup"><span data-stu-id="28294-300">String</span></span> |<span data-ttu-id="28294-301">Valor codificado mediante UTF-16.</span><span class="sxs-lookup"><span data-stu-id="28294-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="28294-302">Los valores de cadena pueden tener hasta 64 KB.</span><span class="sxs-lookup"><span data-stu-id="28294-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="28294-303">Ejemplo de conversión de tipo</span><span class="sxs-lookup"><span data-stu-id="28294-303">Type Conversion Sample</span></span>
<span data-ttu-id="28294-304">El siguiente es un ejemplo de la copia de datos desde un blob de Azure a una tabla de Azure con conversiones de tipo.</span><span class="sxs-lookup"><span data-stu-id="28294-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="28294-305">Supongamos que el conjunto de datos de Blob está en formato CSV y contiene tres columnas.</span><span class="sxs-lookup"><span data-stu-id="28294-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="28294-306">Una de ellas es una columna de fecha y hora con un formato de fecha y hora personalizado mediante los nombres abreviados de los días de la semana en francés.</span><span class="sxs-lookup"><span data-stu-id="28294-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="28294-307">Defina el conjunto de datos de origen de Blob como se indica a continuación, junto con las definiciones de tipo para las columnas.</span><span class="sxs-lookup"><span data-stu-id="28294-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

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
<span data-ttu-id="28294-308">Teniendo en cuenta la asignación del tipo OData de Azure Table al tipo .NET anterior, definiría la tabla en Azure Table con el siguiente esquema.</span><span class="sxs-lookup"><span data-stu-id="28294-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="28294-309">**Esquema de tabla de Azure:**</span><span class="sxs-lookup"><span data-stu-id="28294-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="28294-310">Nombre de la columna</span><span class="sxs-lookup"><span data-stu-id="28294-310">Column name</span></span> | <span data-ttu-id="28294-311">Tipo</span><span class="sxs-lookup"><span data-stu-id="28294-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="28294-312">userid</span><span class="sxs-lookup"><span data-stu-id="28294-312">userid</span></span> |<span data-ttu-id="28294-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="28294-313">Edm.Int64</span></span> |
| <span data-ttu-id="28294-314">name</span><span class="sxs-lookup"><span data-stu-id="28294-314">name</span></span> |<span data-ttu-id="28294-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="28294-315">Edm.String</span></span> |
| <span data-ttu-id="28294-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="28294-316">lastlogindate</span></span> |<span data-ttu-id="28294-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="28294-317">Edm.DateTime</span></span> |

<span data-ttu-id="28294-318">A continuación, defina el conjunto de datos de Azure Table de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="28294-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="28294-319">No es necesario especificar la sección "structure" con la información de tipo porque ya se especificó en el almacén de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="28294-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

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

<span data-ttu-id="28294-320">En este caso, Data Factory realiza automáticamente conversiones de tipos, incluido el campo Datetime con el formato personalizado de fecha y hora, siguiendo la referencia cultural fr-fr al mover datos de Blob a Azure Table.</span><span class="sxs-lookup"><span data-stu-id="28294-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="28294-321">Para asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte el artículo [Asignación de columnas de conjuntos de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="28294-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="28294-322">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="28294-322">Performance and Tuning</span></span>
<span data-ttu-id="28294-323">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="28294-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
