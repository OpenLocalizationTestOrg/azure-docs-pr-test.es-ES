---
title: Movimiento de datos de una tabla web mediante Azure Data Factory | Microsoft Docs
description: "Obtenga información sobre cómo mover datos de una tabla de una página web mediante Azure Data Factory."
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
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="1144b-103">Movimiento de datos de un origen de tabla web mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="1144b-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="1144b-104">En este artículo, se describe el uso de la actividad de copia en Azure Data Factory para mover datos de una tabla de una página web a un almacén de datos receptor compatible.</span><span class="sxs-lookup"><span data-stu-id="1144b-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="1144b-105">Este artículo se basa en el artículo sobre las [actividades de movimiento de datos](data-factory-data-movement-activities.md), que presenta una introducción general del movimiento de datos con la actividad de copia la lista de almacenes de datos compatibles como orígenes/receptores.</span><span class="sxs-lookup"><span data-stu-id="1144b-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="1144b-106">Factoría de datos solo admite actualmente el movimiento de datos desde una tabla web a otros almacenes de datos, pero no de otros almacenes de datos a un destino de tabla web.</span><span class="sxs-lookup"><span data-stu-id="1144b-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1144b-107">Actualmente, este conector web solo permite extraer contenido de tablas de una página HTML.</span><span class="sxs-lookup"><span data-stu-id="1144b-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="1144b-108">Para recuperar datos de un punto de conexión HTTP/s, utilice el [conector HTTP](data-factory-http-connector.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="1144b-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1144b-109">Introducción</span><span class="sxs-lookup"><span data-stu-id="1144b-109">Getting started</span></span>
<span data-ttu-id="1144b-110">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="1144b-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="1144b-111">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="1144b-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1144b-112">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="1144b-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="1144b-113">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="1144b-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1144b-114">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="1144b-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1144b-115">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="1144b-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="1144b-116">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="1144b-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1144b-117">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="1144b-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="1144b-118">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="1144b-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1144b-119">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="1144b-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1144b-120">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="1144b-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1144b-121">Para ver un ejemplo con definiciones de JSON para entidades de Data Factory que se emplean para copiar datos de una tabla web, consulte la sección [Ejemplo con definiciones de JSON: copia de datos de una tabla web a un blob de Azure](#json-example-copy-data-from-web-table-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1144b-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1144b-122">En las secciones siguientes, se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de una tabla web:</span><span class="sxs-lookup"><span data-stu-id="1144b-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1144b-123">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1144b-123">Linked service properties</span></span>
<span data-ttu-id="1144b-124">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de Web.</span><span class="sxs-lookup"><span data-stu-id="1144b-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="1144b-125">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1144b-125">Property</span></span> | <span data-ttu-id="1144b-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="1144b-126">Description</span></span> | <span data-ttu-id="1144b-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1144b-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1144b-128">type</span><span class="sxs-lookup"><span data-stu-id="1144b-128">type</span></span> |<span data-ttu-id="1144b-129">La propiedad type debe establecerse en: **Web**</span><span class="sxs-lookup"><span data-stu-id="1144b-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="1144b-130">Sí</span><span class="sxs-lookup"><span data-stu-id="1144b-130">Yes</span></span> |
| <span data-ttu-id="1144b-131">URL</span><span class="sxs-lookup"><span data-stu-id="1144b-131">Url</span></span> |<span data-ttu-id="1144b-132">Dirección URL para el origen de Web</span><span class="sxs-lookup"><span data-stu-id="1144b-132">URL to the Web source</span></span> |<span data-ttu-id="1144b-133">Sí</span><span class="sxs-lookup"><span data-stu-id="1144b-133">Yes</span></span> |
| <span data-ttu-id="1144b-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1144b-134">authenticationType</span></span> |<span data-ttu-id="1144b-135">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="1144b-135">Anonymous.</span></span> |<span data-ttu-id="1144b-136">Sí</span><span class="sxs-lookup"><span data-stu-id="1144b-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="1144b-137">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="1144b-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="1144b-138">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="1144b-138">Dataset properties</span></span>
<span data-ttu-id="1144b-139">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1144b-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1144b-140">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="1144b-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1144b-141">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="1144b-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1144b-142">La sección typeProperties del conjunto de datos de tipo **WebTable** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="1144b-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="1144b-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1144b-143">Property</span></span> | <span data-ttu-id="1144b-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="1144b-144">Description</span></span> | <span data-ttu-id="1144b-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1144b-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1144b-146">type</span><span class="sxs-lookup"><span data-stu-id="1144b-146">type</span></span> |<span data-ttu-id="1144b-147">Tipo del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1144b-147">type of the dataset.</span></span> <span data-ttu-id="1144b-148">Debe establecerse en **WebTable**</span><span class="sxs-lookup"><span data-stu-id="1144b-148">must be set to **WebTable**</span></span> |<span data-ttu-id="1144b-149">Sí</span><span class="sxs-lookup"><span data-stu-id="1144b-149">Yes</span></span> |
| <span data-ttu-id="1144b-150">path</span><span class="sxs-lookup"><span data-stu-id="1144b-150">path</span></span> |<span data-ttu-id="1144b-151">Dirección URL relativa al recurso que contiene la tabla.</span><span class="sxs-lookup"><span data-stu-id="1144b-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="1144b-152">No.</span><span class="sxs-lookup"><span data-stu-id="1144b-152">No.</span></span> <span data-ttu-id="1144b-153">Cuando no se especifica la ruta de acceso, se solo se usa la dirección URL especificada en la definición de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1144b-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="1144b-154">index</span><span class="sxs-lookup"><span data-stu-id="1144b-154">index</span></span> |<span data-ttu-id="1144b-155">Índice de la tabla en el recurso.</span><span class="sxs-lookup"><span data-stu-id="1144b-155">The index of the table in the resource.</span></span> <span data-ttu-id="1144b-156">Consulte la sección [Obtención de índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) para saber los pasos necesarios para obtener el índice de una tabla en una página HTML.</span><span class="sxs-lookup"><span data-stu-id="1144b-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="1144b-157">Sí</span><span class="sxs-lookup"><span data-stu-id="1144b-157">Yes</span></span> |

<span data-ttu-id="1144b-158">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="1144b-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="1144b-159">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1144b-159">Copy activity properties</span></span>
<span data-ttu-id="1144b-160">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1144b-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1144b-161">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="1144b-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="1144b-162">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="1144b-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="1144b-163">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="1144b-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1144b-164">En este momento, cuando el origen de la actividad de copia es de tipo **WebSource**, no se admite ninguna propiedad adicional.</span><span class="sxs-lookup"><span data-stu-id="1144b-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="1144b-165">Ejemplo con definiciones de JSON: copia de datos de una tabla web a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="1144b-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="1144b-166">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="1144b-166">The following sample shows:</span></span>

1. <span data-ttu-id="1144b-167">Un servicio vinculado de tipo [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1144b-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="1144b-168">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1144b-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1144b-169">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1144b-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1144b-170">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1144b-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1144b-171">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [WebSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1144b-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1144b-172">El ejemplo copia los datos de una tabla web a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="1144b-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="1144b-173">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="1144b-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1144b-174">En el ejemplo siguiente se muestra cómo copiar datos de una tabla web a un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="1144b-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="1144b-175">Sin embargo, los datos se pueden copiar directamente en cualquiera de los receptores indicados en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md) mediante la actividad de copia de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="1144b-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="1144b-176">**Servicio vinculado de tipo Web** : este ejemplo utiliza el servicio vinculado de tipo Web con la autenticación anónima.</span><span class="sxs-lookup"><span data-stu-id="1144b-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="1144b-177">Consulte la sección [Propiedades del servicio vinculado de Web](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="1144b-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="1144b-178">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="1144b-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="1144b-179">**Conjunto de datos de entrada WebTable**: si se establece **external** en **true**, se informa al servicio Data Factory que la tabla es externa a la factoría de datos y no se produce por ninguna actividad de la misma.</span><span class="sxs-lookup"><span data-stu-id="1144b-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="1144b-180">Consulte la sección [Obtención de índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) para saber los pasos necesarios para obtener el índice de una tabla en una página HTML.</span><span class="sxs-lookup"><span data-stu-id="1144b-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="1144b-181">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="1144b-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="1144b-182">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="1144b-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="1144b-183">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="1144b-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="1144b-184">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="1144b-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1144b-185">En la definición del JSON de la canalización, el tipo **source** se establece en **WebSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1144b-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="1144b-186">Consulte [Propiedades de tipo WebSource](#copy-activity-type-properties) para obtener la lista de propiedades que admite WebSource.</span><span class="sxs-lookup"><span data-stu-id="1144b-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

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
        "description": "Copy from a Web table to an Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="1144b-187">Obtención de índice de una tabla en una página HTML</span><span class="sxs-lookup"><span data-stu-id="1144b-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="1144b-188">Inicie **Excel 2016** y cambie a la pestaña **Datos**.</span><span class="sxs-lookup"><span data-stu-id="1144b-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="1144b-189">Haga clic en **Nueva consulta** en la barra de herramientas, elija **De otros orígenes** y haga clic en **Desde Web**.</span><span class="sxs-lookup"><span data-stu-id="1144b-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Menú de Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="1144b-191">En el cuadro de diálogo **Desde Web**, escriba la **dirección URL** que se use en el JSON del servicio vinculado (por ejemplo: https://en.wikipedia.org/wiki/) junto con la ruta de acceso que se especifique para el conjunto de datos (por ejemplo: AFI%27s_100_Years...100_Movies) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1144b-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Cuadro de diálogo Desde Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="1144b-193">Dirección URL usada en este ejemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="1144b-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="1144b-194">Si ve el cuadro de diálogo **Acceso a contenido web**, seleccione la **dirección URL** correcta, la **autenticación** y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="1144b-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Cuadro de diálogo Acceso a contenido web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="1144b-196">Haga clic en un elemento de **tabla** en la vista de árbol para ver el contenido de la tabla y después en el botón **Editar** ubicado en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1144b-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Cuadro de diálogo Navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="1144b-198">En la ventana **Editor de consultas**, haga clic en el botón **Editor avanzado** de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="1144b-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Botón Editor avanzado](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="1144b-200">En el cuadro de diálogo Editor avanzado, el número que aparece junto a "Origen" es el índice.</span><span class="sxs-lookup"><span data-stu-id="1144b-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Editor avanzado - Índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="1144b-202">Si usa Excel 2013, use [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) para obtener el índice.</span><span class="sxs-lookup"><span data-stu-id="1144b-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="1144b-203">Consulte el artículo [Conectarse a una página web](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) para más información.</span><span class="sxs-lookup"><span data-stu-id="1144b-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="1144b-204">Los pasos son similares si usa [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="1144b-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="1144b-205">Para asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte el artículo [Asignación de columnas de conjuntos de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1144b-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1144b-206">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="1144b-206">Performance and Tuning</span></span>
<span data-ttu-id="1144b-207">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="1144b-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
