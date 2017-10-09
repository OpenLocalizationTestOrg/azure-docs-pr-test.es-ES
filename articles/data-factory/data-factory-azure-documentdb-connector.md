---
title: aaaMove datos hacia y desde la base de datos de Azure Cosmos | Documentos de Microsoft
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
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="16d94-103">Mover datos tooand de base de datos de Azure Cosmos con Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="16d94-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="16d94-104">Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove de base de datos de Azure Cosmos (API de documentos).</span><span class="sxs-lookup"><span data-stu-id="16d94-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="16d94-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="16d94-106">Puede copiar datos desde cualquier origen compatible datos almacenan tooAzure Cosmos DB o de datos de base de datos de Azure Cosmos tooany admitida receptores almacenan.</span><span class="sxs-lookup"><span data-stu-id="16d94-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="16d94-107">Para obtener una lista de almacenes de datos admite como orígenes o receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="16d94-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="16d94-108">El conector de Azure Cosmos DB solo admite la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="16d94-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="16d94-109">datos de toocopy como-es hacia/desde archivos JSON o a otra colección de Cosmos DB, vea [documentos JSON de importación y exportación de](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="16d94-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="16d94-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="16d94-110">Getting started</span></span>
<span data-ttu-id="16d94-111">Puede crear una canalización con una actividad de copia que mueva datos hacia y desde Cosmos DB mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="16d94-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="16d94-112">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="16d94-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="16d94-113">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="16d94-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="16d94-114">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="16d94-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="16d94-115">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="16d94-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="16d94-116">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="16d94-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="16d94-117">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="16d94-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="16d94-118">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="16d94-119">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="16d94-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="16d94-120">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="16d94-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="16d94-121">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="16d94-122">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy hacia/desde la base de datos de Cosmos, vea [ejemplos JSON](#json-examples) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="16d94-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="16d94-123">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específicas tooCosmos base de datos:</span><span class="sxs-lookup"><span data-stu-id="16d94-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="16d94-124">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="16d94-124">Linked service properties</span></span>
<span data-ttu-id="16d94-125">Hello en la tabla siguiente proporciona la descripción de JSON elementos específico tooAzure servicio vinculado de base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="16d94-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="16d94-126">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="16d94-126">**Property**</span></span> | <span data-ttu-id="16d94-127">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="16d94-127">**Description**</span></span> | <span data-ttu-id="16d94-128">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="16d94-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16d94-129">type</span><span class="sxs-lookup"><span data-stu-id="16d94-129">type</span></span> |<span data-ttu-id="16d94-130">propiedad de tipo Hello debe establecerse en: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="16d94-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="16d94-131">Sí</span><span class="sxs-lookup"><span data-stu-id="16d94-131">Yes</span></span> |
| <span data-ttu-id="16d94-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="16d94-132">connectionString</span></span> |<span data-ttu-id="16d94-133">Especifique la información necesaria de base de datos de tooconnect tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="16d94-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="16d94-134">Sí</span><span class="sxs-lookup"><span data-stu-id="16d94-134">Yes</span></span> |

<span data-ttu-id="16d94-135">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="16d94-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="16d94-136">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="16d94-136">Dataset properties</span></span>
<span data-ttu-id="16d94-137">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, consulte toohello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="16d94-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="16d94-138">Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="16d94-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="16d94-139">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="16d94-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="16d94-140">Hola typeProperties sección Hola conjunto de datos de tipo **DocumentDbCollection** tiene Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="16d94-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="16d94-141">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="16d94-141">**Property**</span></span> | <span data-ttu-id="16d94-142">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="16d94-142">**Description**</span></span> | <span data-ttu-id="16d94-143">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="16d94-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16d94-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="16d94-144">collectionName</span></span> |<span data-ttu-id="16d94-145">Nombre de la colección de documentos de base de datos de Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="16d94-146">Sí</span><span class="sxs-lookup"><span data-stu-id="16d94-146">Yes</span></span> |

<span data-ttu-id="16d94-147">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="16d94-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="16d94-148">Esquema de Data Factory</span><span class="sxs-lookup"><span data-stu-id="16d94-148">Schema by Data Factory</span></span>
<span data-ttu-id="16d94-149">En los almacenes de datos sin esquema como base de datos de Azure Cosmos, Hola servicio Data Factory deduce el esquema de hello en uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="16d94-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="16d94-150">Si especifica estructura Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, Hola servicio Data Factory respeta esta estructura como esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="16d94-151">En este caso, si una fila no contiene un valor para una columna, se le proporcionará un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="16d94-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="16d94-152">Si no especifica estructura Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, Hola servicio Data Factory deduce el esquema de hello utilizando Hola primera fila de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="16d94-153">En este caso, si la primera fila de hello no contiene el esquema completo de hello, algunas columnas faltará en el resultado de hello de operación de copia.</span><span class="sxs-lookup"><span data-stu-id="16d94-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="16d94-154">Por lo tanto, para orígenes de datos sin esquemas, se recomienda Hola es toospecify estructura de Hola de datos mediante Hola **estructura** propiedad.</span><span class="sxs-lookup"><span data-stu-id="16d94-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="16d94-155">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="16d94-155">Copy activity properties</span></span>
<span data-ttu-id="16d94-156">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, consulte toohello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="16d94-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="16d94-157">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="16d94-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="16d94-158">Hola actividad de copia toma solo una entrada y produce un único resultado.</span><span class="sxs-lookup"><span data-stu-id="16d94-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="16d94-159">Propiedades disponibles en la sección de typeProperties Hola de actividad de hello en hello otra parte varían con cada tipo de actividad y en el caso de actividad de copia varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="16d94-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="16d94-160">En el caso de actividad de copia cuando el origen es de tipo **DocumentDbCollectionSource** Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="16d94-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="16d94-161">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="16d94-161">**Property**</span></span> | <span data-ttu-id="16d94-162">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="16d94-162">**Description**</span></span> | <span data-ttu-id="16d94-163">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="16d94-163">**Allowed values**</span></span> | <span data-ttu-id="16d94-164">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="16d94-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="16d94-165">query</span><span class="sxs-lookup"><span data-stu-id="16d94-165">query</span></span> |<span data-ttu-id="16d94-166">Especifique los datos de hello consulta tooread.</span><span class="sxs-lookup"><span data-stu-id="16d94-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="16d94-167">Cadena de consulta admitida por Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="16d94-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="16d94-168">Ejemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="16d94-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="16d94-169">No</span><span class="sxs-lookup"><span data-stu-id="16d94-169">No</span></span> <br/><br/><span data-ttu-id="16d94-170">Si no se especifica, Hola instrucción SQL que se ejecuta:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="16d94-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="16d94-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="16d94-171">nestingSeparator</span></span> |<span data-ttu-id="16d94-172">Tooindicate de carácter especial que Hola documento está anidada</span><span class="sxs-lookup"><span data-stu-id="16d94-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="16d94-173">Cualquier carácter.</span><span class="sxs-lookup"><span data-stu-id="16d94-173">Any character.</span></span> <br/><br/><span data-ttu-id="16d94-174">Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas.</span><span class="sxs-lookup"><span data-stu-id="16d94-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="16d94-175">Factoría de datos de Azure permite jerarquía toodenote de usuario a través de nestingSeparator, que es "."</span><span class="sxs-lookup"><span data-stu-id="16d94-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="16d94-176">Hola por encima de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="16d94-176">in hello above examples.</span></span> <span data-ttu-id="16d94-177">Con separador de hello, actividad de copia de hello generará un objeto de Hola "Name" con los elementos secundarios de tres too"Name.First primera, central y Last, función", "Name.Middle" y "Name.Last" Hola de definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="16d94-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="16d94-178">No</span><span class="sxs-lookup"><span data-stu-id="16d94-178">No</span></span> |

<span data-ttu-id="16d94-179">**DocumentDbCollectionSink** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="16d94-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="16d94-180">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="16d94-180">**Property**</span></span> | <span data-ttu-id="16d94-181">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="16d94-181">**Description**</span></span> | <span data-ttu-id="16d94-182">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="16d94-182">**Allowed values**</span></span> | <span data-ttu-id="16d94-183">**Obligatorio**</span><span class="sxs-lookup"><span data-stu-id="16d94-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="16d94-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="16d94-184">nestingSeparator</span></span> |<span data-ttu-id="16d94-185">Se necesita un carácter especial en hello tooindicate de nombre de columna de origen que anidados de documento.</span><span class="sxs-lookup"><span data-stu-id="16d94-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="16d94-186">Por ejemplo anteriormente: `Name.First` en la salida de hello tabla genera Hola siguiendo la estructura JSON en el documento de base de datos de Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="16d94-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="16d94-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="16d94-187">"Name": {</span></span><br/>    <span data-ttu-id="16d94-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="16d94-188">"First": "John"</span></span><br/><span data-ttu-id="16d94-189">},</span><span class="sxs-lookup"><span data-stu-id="16d94-189">},</span></span> |<span data-ttu-id="16d94-190">Carácter que es usado tooseparate niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="16d94-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="16d94-191">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="16d94-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="16d94-192">Carácter que es usado tooseparate niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="16d94-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="16d94-193">El valor predeterminado es `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="16d94-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="16d94-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="16d94-194">writeBatchSize</span></span> |<span data-ttu-id="16d94-195">Número de paralelo solicita documentos de toocreate de servicio de base de datos de Cosmos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="16d94-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="16d94-196">Puede ajustar el rendimiento de hello cuando se copian datos de base de datos de Cosmos mediante esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="16d94-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="16d94-197">Puede esperar un rendimiento mejor al aumentar el valor writeBatchSize porque se envían más solicitudes paralelas tooCosmos base de datos.</span><span class="sxs-lookup"><span data-stu-id="16d94-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="16d94-198">Sin embargo deberá tooavoid limitación que puede producir mensajes de bienvenida del error: "Solicitud velocidad es grande".</span><span class="sxs-lookup"><span data-stu-id="16d94-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="16d94-199">La limitación de solicitudes se decide mediante una serie de factores, incluidos tamaño de los documentos, número de términos en los documentos, directiva de indexación de colección de destino, etc. Para las operaciones de copia, puede usar una mejor hello toohave de colección (por ejemplo, S3) mayoría rendimiento disponible (2500 solicitud unidades/segundo).</span><span class="sxs-lookup"><span data-stu-id="16d94-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="16d94-200">Entero</span><span class="sxs-lookup"><span data-stu-id="16d94-200">Integer</span></span> |<span data-ttu-id="16d94-201">No (valor predeterminado: 5)</span><span class="sxs-lookup"><span data-stu-id="16d94-201">No (default: 5)</span></span> |
| <span data-ttu-id="16d94-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="16d94-202">writeBatchTimeout</span></span> |<span data-ttu-id="16d94-203">Tiempo de espera para hello operación toocomplete antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="16d94-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="16d94-204">timespan</span><span class="sxs-lookup"><span data-stu-id="16d94-204">timespan</span></span><br/><br/> <span data-ttu-id="16d94-205">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="16d94-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="16d94-206">No</span><span class="sxs-lookup"><span data-stu-id="16d94-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="16d94-207">Importación o exportación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="16d94-207">Import/Export JSON documents</span></span>
<span data-ttu-id="16d94-208">Con este conector de Cosmos DB, le resultará muy sencillo</span><span class="sxs-lookup"><span data-stu-id="16d94-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="16d94-209">Importar documentos JSON desde varios orígenes en Cosmos DB, incluido Azure Blob, Azure Data Lake, el sistema de archivos local u otros almacenes basados en archivos compatibles con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="16d94-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="16d94-210">Exportar documentos JSON de la colección de Cosmos DB a varios almacenes basados en archivos.</span><span class="sxs-lookup"><span data-stu-id="16d94-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="16d94-211">Migrar datos entre dos colecciones de Cosmos DB como están.</span><span class="sxs-lookup"><span data-stu-id="16d94-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="16d94-212">copiar de este tipo independiente del esquema tooachieve,</span><span class="sxs-lookup"><span data-stu-id="16d94-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="16d94-213">Cuando utilice el Asistente para copiar, compruebe hello **"Exportar como-es tooJSON archivos o un conjunto de Cosmos DB"** opción.</span><span class="sxs-lookup"><span data-stu-id="16d94-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="16d94-214">Cuando con la edición de JSON, no se especifican Hola "estructura" sección en conjuntos de datos de base de datos de Cosmos ni propiedad "nestingSeparator" en la base de datos de Cosmos origen/receptor en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="16d94-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="16d94-215">tooimport de / tooJSON archivos de exportación, en el conjunto de datos de almacén de archivos de hello especificar tipo de formato como "JsonFormat", "filePattern" de la configuración y omitir la configuración de formato de hello rest, vea [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) sección de detalles.</span><span class="sxs-lookup"><span data-stu-id="16d94-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="16d94-216">Ejemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="16d94-216">JSON examples</span></span>
<span data-ttu-id="16d94-217">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="16d94-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="16d94-218">Muestran cómo toocopy tooand de datos de la base de datos de Azure Cosmos y almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="16d94-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="16d94-219">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de hello orígenes tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="16d94-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="16d94-220">Ejemplo: Copiar los datos de base de datos de Azure Cosmos tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="16d94-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="16d94-221">ejemplo de Hola a continuación se muestra:</span><span class="sxs-lookup"><span data-stu-id="16d94-221">hello sample below shows:</span></span>

1. <span data-ttu-id="16d94-222">Un servicio vinculado de tipo [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="16d94-223">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="16d94-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="16d94-224">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="16d94-225">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="16d94-226">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [DocumentDbCollectionSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="16d94-227">ejemplo de Hola copia los datos en la base de datos de Azure Cosmos tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="16d94-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="16d94-228">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="16d94-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="16d94-229">**Servicio vinculado Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="16d94-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="16d94-230">**Servicio vinculado de Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="16d94-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="16d94-231">**Conjunto de datos de entrada de DocumentDB de Azure:**</span><span class="sxs-lookup"><span data-stu-id="16d94-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="16d94-232">ejemplo de Hola se supone que tiene una colección denominada **persona** en una base de datos de la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="16d94-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="16d94-233">Establecer "externo": "true" y especifica externalData información de directiva Hola Data Factory de Azure del servicio tabla Hola se factoría de datos externos toohello no producidos por una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="16d94-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="16d94-234">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="16d94-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="16d94-235">Datos son tooa copiado nuevo blob cada hora con la ruta de acceso de Hola para blob Hola reflejar Hola específico datetime con granularidad de hora.</span><span class="sxs-lookup"><span data-stu-id="16d94-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="16d94-236">Documento JSON de ejemplo de Hola colección persona en una base de datos de la base de datos de Cosmos:</span><span class="sxs-lookup"><span data-stu-id="16d94-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="16d94-237">Cosmos DB admite la consulta de documentos mediante una sintaxis similar a la de SQL en documentos jerárquicos JSON.</span><span class="sxs-lookup"><span data-stu-id="16d94-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="16d94-238">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="16d94-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="16d94-239">siguiente Hola canalización copia datos de hello colección persona Hola tooan de base de datos de base de datos de Azure Cosmos blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="16d94-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="16d94-240">Como parte de Hola Hola de actividad de copia se han especificado los conjuntos de datos de entrada y salidas.</span><span class="sxs-lookup"><span data-stu-id="16d94-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="16d94-241">Ejemplo: Copiar los datos de Blob de Azure tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="16d94-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="16d94-242">ejemplo de Hola a continuación se muestra:</span><span class="sxs-lookup"><span data-stu-id="16d94-242">hello sample below shows:</span></span>

1. <span data-ttu-id="16d94-243">Un servicio vinculado de tipo [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="16d94-244">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="16d94-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="16d94-245">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="16d94-246">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="16d94-247">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="16d94-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="16d94-248">ejemplo de Hola copia datos de blob de Azure tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="16d94-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="16d94-249">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="16d94-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="16d94-250">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="16d94-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="16d94-251">**Servicio vinculado Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="16d94-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="16d94-252">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="16d94-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="16d94-253">**Conjunto de datos de salida de Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="16d94-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="16d94-254">ejemplo de Hola copia la colección de tooa de datos denominado a "Persona".</span><span class="sxs-lookup"><span data-stu-id="16d94-254">hello sample copies data tooa collection named “Person”.</span></span>

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
<span data-ttu-id="16d94-255">siguiente Hola canalización copia datos de Blob de Azure toohello colección persona Hola Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="16d94-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="16d94-256">Como parte de Hola Hola de actividad de copia se han especificado los conjuntos de datos de entrada y salidas.</span><span class="sxs-lookup"><span data-stu-id="16d94-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="16d94-257">Si la entrada de blob de ejemplo de Hola es como</span><span class="sxs-lookup"><span data-stu-id="16d94-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="16d94-258">Hola, a continuación, la salida que JSON en la base de datos de Cosmos será como:</span><span class="sxs-lookup"><span data-stu-id="16d94-258">Then hello output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="16d94-259">Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas.</span><span class="sxs-lookup"><span data-stu-id="16d94-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="16d94-260">Factoría de datos de Azure permite jerarquía toodenote de usuario a través de **nestingSeparator**, que es "."</span><span class="sxs-lookup"><span data-stu-id="16d94-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="16d94-261">en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="16d94-261">in this example.</span></span> <span data-ttu-id="16d94-262">Con separador de hello, actividad de copia de hello generará un objeto de Hola "Name" con los elementos secundarios de tres too"Name.First primera, central y Last, función", "Name.Middle" y "Name.Last" Hola de definición de tabla.</span><span class="sxs-lookup"><span data-stu-id="16d94-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="16d94-263">Anexo</span><span class="sxs-lookup"><span data-stu-id="16d94-263">Appendix</span></span>
1. <span data-ttu-id="16d94-264">**Pregunta:** Hola actualización de soporte técnico de la actividad de copia de los registros existentes?</span><span class="sxs-lookup"><span data-stu-id="16d94-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="16d94-265">**Respuesta:** No.</span><span class="sxs-lookup"><span data-stu-id="16d94-265">**Answer:** No.</span></span>
2. <span data-ttu-id="16d94-266">**Pregunta:** como lo hace un reintento de una solución de base de datos de Cosmos tooAzure copia con ya copió registros?</span><span class="sxs-lookup"><span data-stu-id="16d94-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="16d94-267">**Respuesta:** si registros tienen un campo de "ID" y la operación de copia de hello intenta tooinsert un registro con hello mismo Id. de operación de copia de hello produce un error.</span><span class="sxs-lookup"><span data-stu-id="16d94-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="16d94-268">**Pregunta:** ¿Admite Data Factory el [intervalo o las particiones de datos basadas en hash](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="16d94-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="16d94-269">**Respuesta:** No.</span><span class="sxs-lookup"><span data-stu-id="16d94-269">**Answer:** No.</span></span>
4. <span data-ttu-id="16d94-270">**Pregunta:** ¿Puedo especificar más de una colección de Azure Cosmos DB para una tabla?</span><span class="sxs-lookup"><span data-stu-id="16d94-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="16d94-271">**Respuesta:** No.</span><span class="sxs-lookup"><span data-stu-id="16d94-271">**Answer:** No.</span></span> <span data-ttu-id="16d94-272">Solo se puede especificar una colección cada vez.</span><span class="sxs-lookup"><span data-stu-id="16d94-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="16d94-273">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="16d94-273">Performance and Tuning</span></span>
<span data-ttu-id="16d94-274">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="16d94-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
