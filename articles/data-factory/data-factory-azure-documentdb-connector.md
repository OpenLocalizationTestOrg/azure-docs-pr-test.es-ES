---
title: Movimiento de datos hacia y desde Azure Cosmos DB | Microsoft Docs
description: "Aprenda a mover datos hacia y desde una colección de Azure Cosmos DB mediante Azure Data Factory"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="808cb-103">Movimiento de datos hacia y desde Azure Cosmos DB mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="808cb-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="808cb-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos hacia y desde Azure Cosmos DB (API de DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="808cb-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="808cb-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="808cb-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="808cb-106">Puede copiar datos de cualquier almacén de datos de origen admitido hacia Azure Cosmos DB o desde Azure Cosmos DB hacia cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="808cb-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="808cb-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como orígenes o receptores.</span><span class="sxs-lookup"><span data-stu-id="808cb-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="808cb-108">El conector de Azure Cosmos DB solo admite la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="808cb-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="808cb-109">Para copiar datos tal cual hacia y desde archivos JSON u otra colección de Cosmos DB, consulte [Importación o exportación de documentos JSON](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="808cb-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="808cb-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="808cb-110">Getting started</span></span>
<span data-ttu-id="808cb-111">Puede crear una canalización con una actividad de copia que mueva datos hacia y desde Cosmos DB mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="808cb-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="808cb-112">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="808cb-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="808cb-113">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="808cb-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="808cb-114">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="808cb-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="808cb-115">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="808cb-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="808cb-116">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="808cb-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="808cb-117">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="808cb-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="808cb-118">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="808cb-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="808cb-119">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="808cb-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="808cb-120">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="808cb-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="808cb-121">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="808cb-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="808cb-122">Para ver ejemplos con definiciones de JSON para entidades de Data Factory que se usan para copiar datos con Cosmos DB como origen o destino, consulte la sección [Ejemplos de JSON](#json-examples) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="808cb-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="808cb-123">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="808cb-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="808cb-124">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="808cb-124">Linked service properties</span></span>
<span data-ttu-id="808cb-125">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="808cb-126">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="808cb-126">**Property**</span></span> | <span data-ttu-id="808cb-127">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="808cb-127">**Description**</span></span> | <span data-ttu-id="808cb-128">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="808cb-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="808cb-129">type</span><span class="sxs-lookup"><span data-stu-id="808cb-129">type</span></span> |<span data-ttu-id="808cb-130">La propiedad type debe establecerse en: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="808cb-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="808cb-131">Sí</span><span class="sxs-lookup"><span data-stu-id="808cb-131">Yes</span></span> |
| <span data-ttu-id="808cb-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="808cb-132">connectionString</span></span> |<span data-ttu-id="808cb-133">Especifique la información necesaria para conectarse a la base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="808cb-134">Sí</span><span class="sxs-lookup"><span data-stu-id="808cb-134">Yes</span></span> |

<span data-ttu-id="808cb-135">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="808cb-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="808cb-136">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="808cb-136">Dataset properties</span></span>
<span data-ttu-id="808cb-137">Para obtener una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="808cb-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="808cb-138">Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="808cb-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="808cb-139">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="808cb-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="808cb-140">La sección typeProperties del conjunto de datos de tipo **DocumentDbCollection** tiene las propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="808cb-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="808cb-141">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="808cb-141">**Property**</span></span> | <span data-ttu-id="808cb-142">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="808cb-142">**Description**</span></span> | <span data-ttu-id="808cb-143">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="808cb-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="808cb-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="808cb-144">collectionName</span></span> |<span data-ttu-id="808cb-145">Nombre de la colección de documentos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="808cb-146">Sí</span><span class="sxs-lookup"><span data-stu-id="808cb-146">Yes</span></span> |

<span data-ttu-id="808cb-147">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="808cb-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="808cb-148">Esquema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="808cb-148">Schema by Data Factory</span></span>
<span data-ttu-id="808cb-149">En los almacenes de datos sin esquemas como Azure Cosmos DB, el servicio Data Factory deduce el esquema de una de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="808cb-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="808cb-150">Si especifica la estructura de los datos mediante la propiedad **structure** en la definición del conjunto de datos, el servicio Data Factory respeta esta estructura como estructura del esquema.</span><span class="sxs-lookup"><span data-stu-id="808cb-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="808cb-151">En este caso, si una fila no contiene un valor para una columna, se le proporcionará un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="808cb-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="808cb-152">Si no especifica la estructura de los datos mediante la propiedad **structure** en la definición del conjunto de datos, el servicio Data Factory deduce el esquema utilizando la primera fila en los datos.</span><span class="sxs-lookup"><span data-stu-id="808cb-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="808cb-153">En este caso, si la primera fila no contiene el esquema completo, algunas columnas se pueden perder en el resultado de la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="808cb-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="808cb-154">Por lo tanto, para los orígenes de datos sin esquemas, lo mejor es especificar la estructura de los datos mediante la propiedad **structure** .</span><span class="sxs-lookup"><span data-stu-id="808cb-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="808cb-155">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="808cb-155">Copy activity properties</span></span>
<span data-ttu-id="808cb-156">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="808cb-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="808cb-157">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="808cb-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="808cb-158">La actividad de copia toma solo una entrada y genera una única salida.</span><span class="sxs-lookup"><span data-stu-id="808cb-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="808cb-159">Por otro lado, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad y, en caso de la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="808cb-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="808cb-160">En caso de la actividad de copia si el origen es de tipo **DocumentDbCollectionSource**, están disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="808cb-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="808cb-161">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="808cb-161">**Property**</span></span> | <span data-ttu-id="808cb-162">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="808cb-162">**Description**</span></span> | <span data-ttu-id="808cb-163">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="808cb-163">**Allowed values**</span></span> | <span data-ttu-id="808cb-164">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="808cb-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="808cb-165">query</span><span class="sxs-lookup"><span data-stu-id="808cb-165">query</span></span> |<span data-ttu-id="808cb-166">Especifique la consulta para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="808cb-166">Specify the query to read data.</span></span> |<span data-ttu-id="808cb-167">Cadena de consulta admitida por Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="808cb-168">Ejemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="808cb-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="808cb-169">No</span><span class="sxs-lookup"><span data-stu-id="808cb-169">No</span></span> <br/><br/><span data-ttu-id="808cb-170">Si no se especifica, la instrucción SQL que se ejecuta: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="808cb-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="808cb-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="808cb-171">nestingSeparator</span></span> |<span data-ttu-id="808cb-172">Carácter especial para indicar que el documento está anidado</span><span class="sxs-lookup"><span data-stu-id="808cb-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="808cb-173">Cualquier carácter.</span><span class="sxs-lookup"><span data-stu-id="808cb-173">Any character.</span></span> <br/><br/><span data-ttu-id="808cb-174">Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas.</span><span class="sxs-lookup"><span data-stu-id="808cb-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="808cb-175">Azure Data Factory permite al usuario indicar la jerarquía a través de nestingSeparator que es "."</span><span class="sxs-lookup"><span data-stu-id="808cb-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="808cb-176">en los ejemplos anteriores.</span><span class="sxs-lookup"><span data-stu-id="808cb-176">in the above examples.</span></span> <span data-ttu-id="808cb-177">Con el separador, la actividad de copia generará el objeto "Name" con tres elementos secundarios First, Middle y Last, según "Name.First", "Name.Middle" y "Name.Last" en la definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="808cb-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="808cb-178">No</span><span class="sxs-lookup"><span data-stu-id="808cb-178">No</span></span> |

<span data-ttu-id="808cb-179">**DocumentDbCollectionSink** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="808cb-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="808cb-180">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="808cb-180">**Property**</span></span> | <span data-ttu-id="808cb-181">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="808cb-181">**Description**</span></span> | <span data-ttu-id="808cb-182">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="808cb-182">**Allowed values**</span></span> | <span data-ttu-id="808cb-183">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="808cb-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="808cb-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="808cb-184">nestingSeparator</span></span> |<span data-ttu-id="808cb-185">Un carácter especial en el nombre de columna de origen que indica que el documento anidado es necesario.</span><span class="sxs-lookup"><span data-stu-id="808cb-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="808cb-186">En el ejemplo anterior: `Name.First` en la tabla de salida produce la siguiente estructura JSON en el documento de Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="808cb-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="808cb-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="808cb-187">"Name": {</span></span><br/>    <span data-ttu-id="808cb-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="808cb-188">"First": "John"</span></span><br/><span data-ttu-id="808cb-189">},</span><span class="sxs-lookup"><span data-stu-id="808cb-189">},</span></span> |<span data-ttu-id="808cb-190">Carácter que se usa para separar los niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="808cb-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="808cb-191">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="808cb-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="808cb-192">Carácter que se usa para separar los niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="808cb-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="808cb-193">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="808cb-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="808cb-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="808cb-194">writeBatchSize</span></span> |<span data-ttu-id="808cb-195">Número de solicitudes paralelas al servicio Azure Cosmos DB para crear documentos.</span><span class="sxs-lookup"><span data-stu-id="808cb-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="808cb-196">Puede ajustar el rendimiento cuando se copian datos hacia o desde Cosmos DB mediante esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="808cb-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="808cb-197">Puede esperar un rendimiento mejor al aumentar writeBatchSize porque se envían más solicitudes paralelas a Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="808cb-198">Sin embargo, deberá evitar una limitación de solicitudes que puede generar el mensaje de error: "La tasa de solicitudes es grande".</span><span class="sxs-lookup"><span data-stu-id="808cb-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="808cb-199">La limitación de solicitudes se decide mediante una serie de factores, incluidos tamaño de los documentos, número de términos en los documentos, directiva de indexación de colección de destino, etc. Para las operaciones de copia, puede usar una colección mejor (por ejemplo, S3) para obtener el máximo rendimiento disponible (2.500 unidades de solicitudes por segundo).</span><span class="sxs-lookup"><span data-stu-id="808cb-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="808cb-200">Entero </span><span class="sxs-lookup"><span data-stu-id="808cb-200">Integer</span></span> |<span data-ttu-id="808cb-201">No (valor predeterminado: 5)</span><span class="sxs-lookup"><span data-stu-id="808cb-201">No (default: 5)</span></span> |
| <span data-ttu-id="808cb-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="808cb-202">writeBatchTimeout</span></span> |<span data-ttu-id="808cb-203">Tiempo de espera para que la operación se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="808cb-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="808cb-204">timespan</span><span class="sxs-lookup"><span data-stu-id="808cb-204">timespan</span></span><br/><br/> <span data-ttu-id="808cb-205">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="808cb-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="808cb-206">No</span><span class="sxs-lookup"><span data-stu-id="808cb-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="808cb-207">Importación o exportación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="808cb-207">Import/Export JSON documents</span></span>
<span data-ttu-id="808cb-208">Con este conector de Cosmos DB, le resultará muy sencillo</span><span class="sxs-lookup"><span data-stu-id="808cb-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="808cb-209">Importar documentos JSON desde varios orígenes en Cosmos DB, incluido Azure Blob, Azure Data Lake, el sistema de archivos local u otros almacenes basados en archivos compatibles con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="808cb-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="808cb-210">Exportar documentos JSON de la colección de Cosmos DB a varios almacenes basados en archivos.</span><span class="sxs-lookup"><span data-stu-id="808cb-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="808cb-211">Migrar datos entre dos colecciones de Cosmos DB como están.</span><span class="sxs-lookup"><span data-stu-id="808cb-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="808cb-212">Para lograr dicha copia independiente del esquema,</span><span class="sxs-lookup"><span data-stu-id="808cb-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="808cb-213">Cuando use el Asistente para copia, active la opción **"Export as-is to JSON files or Cosmos DB collection"** (Exportar tal cual a archivos JSON o colección de Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="808cb-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="808cb-214">Al usar la edición de JSON, no especifique la sección "structure" en los conjuntos de datos de Cosmos DB ni la propiedad "nestingSeparator" en el receptor u origen de Cosmos DB en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="808cb-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="808cb-215">Para importar desde archivos JSON o exportar a ellos, en el conjunto de datos de almacén de archivos, especifique el tipo de formato como "JsonFormat", configure "filePattern" y omita la configuración de formato restante; vea la sección [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="808cb-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="808cb-216">Ejemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="808cb-216">JSON examples</span></span>
<span data-ttu-id="808cb-217">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="808cb-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="808cb-218">Muestran cómo copiar datos hacia y desde Azure Cosmos DB y Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="808cb-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="808cb-219">Sin embargo, los datos se pueden copiar **directamente** de cualquiera de los orígenes a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="808cb-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="808cb-220">Ejemplo: copia de datos de Azure Cosmos DB a Azure Blob</span><span class="sxs-lookup"><span data-stu-id="808cb-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="808cb-221">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="808cb-221">The sample below shows:</span></span>

1. <span data-ttu-id="808cb-222">Un servicio vinculado de tipo [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="808cb-223">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="808cb-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="808cb-224">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="808cb-225">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="808cb-226">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [DocumentDbCollectionSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="808cb-227">En el ejemplo se copian datos de Azure Cosmos DB en Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="808cb-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="808cb-228">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="808cb-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="808cb-229">**Servicio vinculado Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="808cb-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="808cb-230">**Servicio vinculado de Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="808cb-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="808cb-231">**Conjunto de datos de entrada de DocumentDB de Azure:**</span><span class="sxs-lookup"><span data-stu-id="808cb-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="808cb-232">En el ejemplo se supone que tiene una colección llamada **Person** en una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="808cb-233">Si se establece "external": "true" y se especifica la directiva externalData, se informa al servicio Azure Data Factory que la tabla es externa a la factoría de datos y que no se produce por ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="808cb-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="808cb-234">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="808cb-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="808cb-235">Los datos se copian a un blob nuevo cada hora con la ruta de acceso para el blob que refleja la fecha y hora específicas con granularidad de hora.</span><span class="sxs-lookup"><span data-stu-id="808cb-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="808cb-236">Documentos JSON de ejemplo en la colección Person de una base de datos de Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="808cb-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="808cb-237">Cosmos DB admite la consulta de documentos mediante una sintaxis similar a la de SQL en documentos jerárquicos JSON.</span><span class="sxs-lookup"><span data-stu-id="808cb-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="808cb-238">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="808cb-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="808cb-239">La siguiente canalización copia los datos de la colección Person de la base de datos de Azure Cosmos DB en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="808cb-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="808cb-240">Como parte de la actividad de copia, se han especificado los conjuntos de datos de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="808cb-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="808cb-241">Ejemplo: copia de datos de Azure Blob a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="808cb-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="808cb-242">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="808cb-242">The sample below shows:</span></span>

1. <span data-ttu-id="808cb-243">Un servicio vinculado de tipo [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="808cb-244">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="808cb-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="808cb-245">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="808cb-246">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="808cb-247">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="808cb-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="808cb-248">En el ejemplo se copian datos desde Azure Blob hasta Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="808cb-249">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="808cb-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="808cb-250">**Servicio vinculado de Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="808cb-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="808cb-251">**Servicio vinculado Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="808cb-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="808cb-252">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="808cb-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="808cb-253">**Conjunto de datos de salida de Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="808cb-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="808cb-254">El ejemplo copia los datos a una colección denominada "Person".</span><span class="sxs-lookup"><span data-stu-id="808cb-254">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="808cb-255">La siguiente canalización copia datos de Azure Blob en la colección Person de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="808cb-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="808cb-256">Como parte de la actividad de copia, se han especificado los conjuntos de datos de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="808cb-256">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="808cb-257">Si la entrada de blob de ejemplo es como:</span><span class="sxs-lookup"><span data-stu-id="808cb-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="808cb-258">La salida JSON en Cosmos DB será como:</span><span class="sxs-lookup"><span data-stu-id="808cb-258">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="808cb-259">Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas.</span><span class="sxs-lookup"><span data-stu-id="808cb-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="808cb-260">Azure Data Factory permite al usuario indicar la jerarquía a través de **nestingSeparator** que es "."</span><span class="sxs-lookup"><span data-stu-id="808cb-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="808cb-261">en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="808cb-261">in this example.</span></span> <span data-ttu-id="808cb-262">Con el separador, la actividad de copia generará el objeto "Name" con tres elementos secundarios First, Middle y Last, según "Name.First", "Name.Middle" y "Name.Last" en la definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="808cb-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="808cb-263">Anexo</span><span class="sxs-lookup"><span data-stu-id="808cb-263">Appendix</span></span>
1. <span data-ttu-id="808cb-264">**Pregunta:** ¿Admite la actividad de copia la actualización de los registros existentes?</span><span class="sxs-lookup"><span data-stu-id="808cb-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="808cb-265">**Respuesta:** No.</span><span class="sxs-lookup"><span data-stu-id="808cb-265">**Answer:** No.</span></span>
2. <span data-ttu-id="808cb-266">**Pregunta:** como lo hace un reintento de una copia de base de datos de Azure Cosmos solucionan ya copió registros?</span><span class="sxs-lookup"><span data-stu-id="808cb-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="808cb-267">**Respuesta:** Si los registros tienen un campo "Id" y la operación de copia intenta insertar un registro con el mismo Id., la operación de copia genera un error.</span><span class="sxs-lookup"><span data-stu-id="808cb-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="808cb-268">**Pregunta:** es compatible con la factoría de datos [intervalo o las particiones de datos basado en hash](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="808cb-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="808cb-269">**Respuesta:** No.</span><span class="sxs-lookup"><span data-stu-id="808cb-269">**Answer:** No.</span></span>
4. <span data-ttu-id="808cb-270">**Pregunta:** ¿puedo especificar más de una colección de base de datos de Azure Cosmos para una tabla?</span><span class="sxs-lookup"><span data-stu-id="808cb-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="808cb-271">**Respuesta:** No.</span><span class="sxs-lookup"><span data-stu-id="808cb-271">**Answer:** No.</span></span> <span data-ttu-id="808cb-272">Solo se puede especificar una colección cada vez.</span><span class="sxs-lookup"><span data-stu-id="808cb-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="808cb-273">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="808cb-273">Performance and Tuning</span></span>
<span data-ttu-id="808cb-274">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="808cb-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
