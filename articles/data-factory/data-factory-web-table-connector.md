---
title: aaaMove datos de la tabla de Web mediante Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure de páginas de datos de toomove de una tabla en un servidor Web."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="5d60f-103">Movimiento de datos de un origen de tabla web mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="5d60f-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="5d60f-104">En este artículo se describe cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure de una tabla en una página Web tooa admite el almacén de datos del receptor.</span><span class="sxs-lookup"><span data-stu-id="5d60f-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="5d60f-105">En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo que presenta una visión general de movimiento de datos con la lista de hello y actividad de copia de almacenes de datos que se admiten como orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="5d60f-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="5d60f-106">Factoría de datos admite actualmente solo almacena la migración de datos de un tooother de datos de la tabla de Web, pero no mover los datos de otros datos almacena el destino de tabla de tooa Web.</span><span class="sxs-lookup"><span data-stu-id="5d60f-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d60f-107">Actualmente, este conector web solo permite extraer contenido de tablas de una página HTML.</span><span class="sxs-lookup"><span data-stu-id="5d60f-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="5d60f-108">tooretrieve de datos desde un punto de conexión HTTP/s, utilizar [conector HTTP](data-factory-http-connector.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="5d60f-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5d60f-109">Introducción</span><span class="sxs-lookup"><span data-stu-id="5d60f-109">Getting started</span></span>
<span data-ttu-id="5d60f-110">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="5d60f-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="5d60f-111">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="5d60f-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5d60f-112">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="5d60f-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="5d60f-113">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="5d60f-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5d60f-114">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="5d60f-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5d60f-115">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="5d60f-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5d60f-116">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="5d60f-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5d60f-117">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5d60f-118">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="5d60f-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5d60f-119">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="5d60f-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5d60f-120">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5d60f-121">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son toocopy usa datos de una tabla de web, consulte [ejemplo de JSON: copiar los datos de Web tabla tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="5d60f-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5d60f-122">Hola las secciones siguientes proporciona detalles acerca de propiedades JSON de tabla de toodefine usado factoría de datos entidades específicas tooa Web:</span><span class="sxs-lookup"><span data-stu-id="5d60f-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5d60f-123">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="5d60f-123">Linked service properties</span></span>
<span data-ttu-id="5d60f-124">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooWeb vinculado.</span><span class="sxs-lookup"><span data-stu-id="5d60f-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="5d60f-125">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5d60f-125">Property</span></span> | <span data-ttu-id="5d60f-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="5d60f-126">Description</span></span> | <span data-ttu-id="5d60f-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5d60f-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d60f-128">type</span><span class="sxs-lookup"><span data-stu-id="5d60f-128">type</span></span> |<span data-ttu-id="5d60f-129">propiedad de tipo Hello debe establecerse en: **Web**</span><span class="sxs-lookup"><span data-stu-id="5d60f-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="5d60f-130">Sí</span><span class="sxs-lookup"><span data-stu-id="5d60f-130">Yes</span></span> |
| <span data-ttu-id="5d60f-131">URL</span><span class="sxs-lookup"><span data-stu-id="5d60f-131">Url</span></span> |<span data-ttu-id="5d60f-132">Origen de dirección URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="5d60f-132">URL toohello Web source</span></span> |<span data-ttu-id="5d60f-133">Sí</span><span class="sxs-lookup"><span data-stu-id="5d60f-133">Yes</span></span> |
| <span data-ttu-id="5d60f-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="5d60f-134">authenticationType</span></span> |<span data-ttu-id="5d60f-135">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="5d60f-135">Anonymous.</span></span> |<span data-ttu-id="5d60f-136">Sí</span><span class="sxs-lookup"><span data-stu-id="5d60f-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="5d60f-137">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="5d60f-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="5d60f-138">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="5d60f-138">Dataset properties</span></span>
<span data-ttu-id="5d60f-139">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="5d60f-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5d60f-140">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="5d60f-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5d60f-141">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="5d60f-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5d60f-142">sección typeProperties Hello para el conjunto de datos de tipo **WebTable** tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="5d60f-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="5d60f-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5d60f-143">Property</span></span> | <span data-ttu-id="5d60f-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="5d60f-144">Description</span></span> | <span data-ttu-id="5d60f-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5d60f-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5d60f-146">type</span><span class="sxs-lookup"><span data-stu-id="5d60f-146">type</span></span> |<span data-ttu-id="5d60f-147">Tipo de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-147">type of hello dataset.</span></span> <span data-ttu-id="5d60f-148">debe establecerse demasiado**WebTable**</span><span class="sxs-lookup"><span data-stu-id="5d60f-148">must be set too**WebTable**</span></span> |<span data-ttu-id="5d60f-149">Sí</span><span class="sxs-lookup"><span data-stu-id="5d60f-149">Yes</span></span> |
| <span data-ttu-id="5d60f-150">path</span><span class="sxs-lookup"><span data-stu-id="5d60f-150">path</span></span> |<span data-ttu-id="5d60f-151">Un recurso de toohello de dirección URL relativo al que contiene la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="5d60f-152">No.</span><span class="sxs-lookup"><span data-stu-id="5d60f-152">No.</span></span> <span data-ttu-id="5d60f-153">Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="5d60f-154">index</span><span class="sxs-lookup"><span data-stu-id="5d60f-154">index</span></span> |<span data-ttu-id="5d60f-155">índice de Hola de tabla de hello en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="5d60f-156">Vea [Get índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) sección índice toogetting de pasos de una tabla en una página HTML.</span><span class="sxs-lookup"><span data-stu-id="5d60f-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="5d60f-157">Sí</span><span class="sxs-lookup"><span data-stu-id="5d60f-157">Yes</span></span> |

<span data-ttu-id="5d60f-158">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="5d60f-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="5d60f-159">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="5d60f-159">Copy activity properties</span></span>
<span data-ttu-id="5d60f-160">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="5d60f-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5d60f-161">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="5d60f-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="5d60f-162">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="5d60f-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="5d60f-163">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="5d60f-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5d60f-164">Actualmente, al origen de hello en la actividad de copia es de tipo **WebSource**, no se admiten propiedades adicionales.</span><span class="sxs-lookup"><span data-stu-id="5d60f-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="5d60f-165">Ejemplo de JSON: copiar los datos de Web tabla tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="5d60f-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="5d60f-166">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="5d60f-166">hello following sample shows:</span></span>

1. <span data-ttu-id="5d60f-167">Un servicio vinculado de tipo [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5d60f-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="5d60f-168">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="5d60f-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="5d60f-169">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5d60f-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="5d60f-170">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5d60f-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="5d60f-171">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [WebSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5d60f-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5d60f-172">ejemplo de Hola copia datos de un tooan de tabla Web blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="5d60f-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="5d60f-173">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="5d60f-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="5d60f-174">Hola siguiente ejemplo muestra cómo toocopy datos desde un tooan de tabla Web Azure blob.</span><span class="sxs-lookup"><span data-stu-id="5d60f-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="5d60f-175">Sin embargo, los datos pueden copiarse directamente Hola indicado en los receptores de tooany de hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo usando Hola actividad de copia de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d60f-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="5d60f-176">**Servicio vinculado de Web** en este ejemplo usa hello Web vinculado servicio con la autenticación anónima.</span><span class="sxs-lookup"><span data-stu-id="5d60f-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="5d60f-177">Consulte la sección [Propiedades del servicio vinculado de Web](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="5d60f-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="5d60f-178">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="5d60f-178">**Azure Storage linked service**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="5d60f-179">**Conjunto de datos de entrada de WebTable** configuración **externo** demasiado**true** informa a servicio de factoría de datos de Hola ese conjunto de datos de hello es factoría de datos de toohello externo y no se generará una actividad en hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5d60f-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="5d60f-180">Vea [Get índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) sección índice toogetting de pasos de una tabla en una página HTML.</span><span class="sxs-lookup"><span data-stu-id="5d60f-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="5d60f-181">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="5d60f-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="5d60f-182">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="5d60f-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="5d60f-183">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="5d60f-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="5d60f-184">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="5d60f-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="5d60f-185">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**WebSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5d60f-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="5d60f-186">Vea [propiedades de tipo WebSource](#copy-activity-type-properties) para lista de Hola de propiedades admitidas por hello WebSource.</span><span class="sxs-lookup"><span data-stu-id="5d60f-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="5d60f-187">Obtención de índice de una tabla en una página HTML</span><span class="sxs-lookup"><span data-stu-id="5d60f-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="5d60f-188">Iniciar **Excel 2016** y cambiar toohello **datos** ficha.</span><span class="sxs-lookup"><span data-stu-id="5d60f-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="5d60f-189">Haga clic en **nueva consulta** en la barra de herramientas de hello, seleccione demasiado**desde otros orígenes** y haga clic en **de Web**.</span><span class="sxs-lookup"><span data-stu-id="5d60f-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Menú de Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="5d60f-191">Hola **desde Web** diálogo cuadro, escriba **URL** que usaría en servicio JSON vinculado (por ejemplo: https://en.wikipedia.org/wiki/) junto con la ruta de acceso que se debe especificar para el conjunto de datos de hello (por ejemplo: AFI % 27s_100_Years... 100_Movies) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5d60f-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Cuadro de diálogo Desde Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="5d60f-193">Dirección URL usada en este ejemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="5d60f-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="5d60f-194">Si ve **contenido Web Access** cuadro de diálogo, derecha seleccione hello **URL**, **autenticación**y haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="5d60f-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Cuadro de diálogo Acceso a contenido web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="5d60f-196">Haga clic en un **tabla** elemento de contenido de toosee de Hola árbol de la vista de tabla de hello y, a continuación, haga clic en **editar** situado en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Cuadro de diálogo Navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="5d60f-198">Hola **Editor de consultas** ventana, haga clic en **Editor avanzado** botón de barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Botón Editor avanzado](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="5d60f-200">En el cuadro de diálogo del Editor avanzado de Hola Hola número junto demasiado "Origen" es el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d60f-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Editor avanzado - Índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="5d60f-202">Si usa Excel 2013, use [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) índice de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="5d60f-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="5d60f-203">Vea [página web de Connect tooa](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="5d60f-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="5d60f-204">Hola pasos son similares si utilizas [Microsoft Power BI para escritorio](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="5d60f-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="5d60f-205">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5d60f-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5d60f-206">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="5d60f-206">Performance and Tuning</span></span>
<span data-ttu-id="5d60f-207">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="5d60f-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
