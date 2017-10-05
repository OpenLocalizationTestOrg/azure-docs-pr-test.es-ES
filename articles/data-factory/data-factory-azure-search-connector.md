---
title: "Inserción de datos en un índice de Search mediante Data Factory | Microsoft Docs"
description: "Obtenga información sobre cómo insertar datos en un índice de Azure Search mediante el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="b21ef-103">Inserción de datos en un índice de Azure Search mediante el uso de Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="b21ef-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="b21ef-104">Este artículo describe cómo usar la actividad de copia para insertar datos de un almacén de datos de origen admitido en un índice de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="b21ef-105">Los almacenes de datos de origen compatibles se muestran en la columna Se admite como origen de la tabla de [almacenes de datos y receptores que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b21ef-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b21ef-106">Este artículo se basa en el artículo sobre [movimiento de datos y actividad de copia](data-factory-data-movement-activities.md) que presenta una introducción general del movimiento de datos con la actividad de copia y las combinaciones de almacén de datos admitidas.</span><span class="sxs-lookup"><span data-stu-id="b21ef-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="b21ef-107">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="b21ef-107">Enabling connectivity</span></span>
<span data-ttu-id="b21ef-108">Para que el servicio Data Factory pueda conectarse con un almacén de datos local, instale la puerta de enlace de administración de datos en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="b21ef-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="b21ef-109">No podrá instalar la puerta de enlace en la misma máquina que hospeda el almacén de datos de origen ni en una independiente para evitar la competencia por los recursos con el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="b21ef-110">La puerta de enlace de administración de datos conecta orígenes de datos locales a servicios en la nube de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="b21ef-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="b21ef-111">Consulte el artículo [Mover datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="b21ef-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b21ef-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="b21ef-112">Getting started</span></span>
<span data-ttu-id="b21ef-113">Puede crear una canalización con una actividad de copia que inserte datos de un almacén de datos de origen en un índice de Azure Search mediante el uso de distintas herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="b21ef-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="b21ef-114">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="b21ef-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b21ef-115">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="b21ef-116">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="b21ef-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b21ef-117">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b21ef-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b21ef-118">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="b21ef-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="b21ef-119">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="b21ef-120">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="b21ef-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="b21ef-121">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="b21ef-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b21ef-122">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="b21ef-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b21ef-123">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b21ef-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b21ef-124">Si desea obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan con el fin de copiar datos de un índice de Azure Search, consulte la sección [Ejemplo de JSON: Copia de datos de un servidor SQL Server local a un índice de Azure Search](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="b21ef-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="b21ef-125">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de índices de Azure Search:</span><span class="sxs-lookup"><span data-stu-id="b21ef-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b21ef-126">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="b21ef-126">Linked service properties</span></span>

<span data-ttu-id="b21ef-127">En la tabla siguiente se proporcionan descripciones de los elementos JSON específicos del servicio vinculado de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="b21ef-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b21ef-128">Property</span></span> | <span data-ttu-id="b21ef-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="b21ef-129">Description</span></span> | <span data-ttu-id="b21ef-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b21ef-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="b21ef-131">type</span><span class="sxs-lookup"><span data-stu-id="b21ef-131">type</span></span> | <span data-ttu-id="b21ef-132">La propiedad type debe establecerse en **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="b21ef-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="b21ef-133">Sí</span><span class="sxs-lookup"><span data-stu-id="b21ef-133">Yes</span></span> |
| <span data-ttu-id="b21ef-134">url</span><span class="sxs-lookup"><span data-stu-id="b21ef-134">url</span></span> | <span data-ttu-id="b21ef-135">La URL del servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="b21ef-136">Sí</span><span class="sxs-lookup"><span data-stu-id="b21ef-136">Yes</span></span> |
| <span data-ttu-id="b21ef-137">key</span><span class="sxs-lookup"><span data-stu-id="b21ef-137">key</span></span> | <span data-ttu-id="b21ef-138">La clave de administración del servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="b21ef-139">Sí</span><span class="sxs-lookup"><span data-stu-id="b21ef-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b21ef-140">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="b21ef-140">Dataset properties</span></span>

<span data-ttu-id="b21ef-141">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo sobre [creación de conjuntos de datos](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="b21ef-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b21ef-142">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="b21ef-143">La sección **typeProperties** es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="b21ef-144">La sección typeProperties de un conjunto de datos del tipo **AzureSearchIndex** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="b21ef-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="b21ef-145">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b21ef-145">Property</span></span> | <span data-ttu-id="b21ef-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="b21ef-146">Description</span></span> | <span data-ttu-id="b21ef-147">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b21ef-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="b21ef-148">type</span><span class="sxs-lookup"><span data-stu-id="b21ef-148">type</span></span> | <span data-ttu-id="b21ef-149">La propiedad type debe establecerse en **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="b21ef-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="b21ef-150">Sí</span><span class="sxs-lookup"><span data-stu-id="b21ef-150">Yes</span></span> |
| <span data-ttu-id="b21ef-151">indexName</span><span class="sxs-lookup"><span data-stu-id="b21ef-151">indexName</span></span> | <span data-ttu-id="b21ef-152">Nombre del índice de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-152">Name of the Azure Search index.</span></span> <span data-ttu-id="b21ef-153">Data Factory no crea el índice.</span><span class="sxs-lookup"><span data-stu-id="b21ef-153">Data Factory does not create the index.</span></span> <span data-ttu-id="b21ef-154">El índice debe existir en Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="b21ef-155">Sí</span><span class="sxs-lookup"><span data-stu-id="b21ef-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="b21ef-156">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="b21ef-156">Copy activity properties</span></span>
<span data-ttu-id="b21ef-157">Para obtener una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo sobre [creación de canalizaciones](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="b21ef-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b21ef-158">Las propiedades (como el nombre, la descripción, las tablas de entrada y salida, y las distintas directivas) están disponibles en todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="b21ef-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="b21ef-159">Por otra parte, las propiedades disponibles en la sección typeProperties varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="b21ef-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="b21ef-160">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="b21ef-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="b21ef-161">En la actividad de copia, si el receptor es de tipo **AzureSearchIndexSink**, estarán disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="b21ef-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="b21ef-162">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b21ef-162">Property</span></span> | <span data-ttu-id="b21ef-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="b21ef-163">Description</span></span> | <span data-ttu-id="b21ef-164">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b21ef-164">Allowed values</span></span> | <span data-ttu-id="b21ef-165">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b21ef-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="b21ef-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="b21ef-166">WriteBehavior</span></span> | <span data-ttu-id="b21ef-167">Especifica si, cuando ya haya un documento en el índice, se realizará una operación de combinación o de reemplazo.</span><span class="sxs-lookup"><span data-stu-id="b21ef-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="b21ef-168">Consulte la propiedad [WriteBehavior](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="b21ef-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="b21ef-169">Combinar (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="b21ef-169">Merge (default)</span></span><br/><span data-ttu-id="b21ef-170">Cargar</span><span class="sxs-lookup"><span data-stu-id="b21ef-170">Upload</span></span>| <span data-ttu-id="b21ef-171">No</span><span class="sxs-lookup"><span data-stu-id="b21ef-171">No</span></span> |
| <span data-ttu-id="b21ef-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="b21ef-172">WriteBatchSize</span></span> | <span data-ttu-id="b21ef-173">Carga datos en el índice de Azure Search cuando el tamaño del búfer alcanza el valor de WriteBatchSize.</span><span class="sxs-lookup"><span data-stu-id="b21ef-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="b21ef-174">Consulte la propiedad [WriteBatchSize](#writebatchsize-property) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b21ef-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="b21ef-175">De 1 a 1000.</span><span class="sxs-lookup"><span data-stu-id="b21ef-175">1 to 1,000.</span></span> <span data-ttu-id="b21ef-176">El valor predeterminado es 1000.</span><span class="sxs-lookup"><span data-stu-id="b21ef-176">Default value is 1000.</span></span> | <span data-ttu-id="b21ef-177">No</span><span class="sxs-lookup"><span data-stu-id="b21ef-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="b21ef-178">Propiedad WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="b21ef-178">WriteBehavior property</span></span>
<span data-ttu-id="b21ef-179">AzureSearchSink realiza una operación upsert al escribir los datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="b21ef-180">Es decir, al crear un documento, si la clave de este ya se encuentra en el índice de Azure Search, este servicio actualiza el documento existente en lugar de generar una excepción de conflicto.</span><span class="sxs-lookup"><span data-stu-id="b21ef-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="b21ef-181">AzureSearchSink proporciona los siguientes dos comportamientos de upsert (mediante el SDK de Azure Search):</span><span class="sxs-lookup"><span data-stu-id="b21ef-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="b21ef-182">**Combinar**: combina todas las columnas del nuevo documento con el existente.</span><span class="sxs-lookup"><span data-stu-id="b21ef-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="b21ef-183">En las columnas con valor null del nuevo documento, se conserva el valor del existente.</span><span class="sxs-lookup"><span data-stu-id="b21ef-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="b21ef-184">**Cargar**: el nuevo documento reemplaza al existente.</span><span class="sxs-lookup"><span data-stu-id="b21ef-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="b21ef-185">En cuanto a las columnas no especificadas en el nuevo documento, el valor se establece en null con independencia de que haya un valor distinto de null en el documento existente.</span><span class="sxs-lookup"><span data-stu-id="b21ef-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="b21ef-186">El comportamiento predeterminado es **Combinar**.</span><span class="sxs-lookup"><span data-stu-id="b21ef-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="b21ef-187">Propiedad WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="b21ef-187">WriteBatchSize Property</span></span>
<span data-ttu-id="b21ef-188">Azure Search puede crear documentos como lotes.</span><span class="sxs-lookup"><span data-stu-id="b21ef-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="b21ef-189">Un lote puede contener entre 1 y 1000 acciones.</span><span class="sxs-lookup"><span data-stu-id="b21ef-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="b21ef-190">Una acción controla un documento para llevar a cabo la operación de combinación o de carga.</span><span class="sxs-lookup"><span data-stu-id="b21ef-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="b21ef-191">Compatibilidad con los tipos de datos</span><span class="sxs-lookup"><span data-stu-id="b21ef-191">Data type support</span></span>
<span data-ttu-id="b21ef-192">En la tabla siguiente se especifica si se admite o no un tipo de datos de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b21ef-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="b21ef-193">Tipo de datos de Azure Search</span><span class="sxs-lookup"><span data-stu-id="b21ef-193">Azure Search data type</span></span> | <span data-ttu-id="b21ef-194">Compatible con el receptor de Azure Search</span><span class="sxs-lookup"><span data-stu-id="b21ef-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="b21ef-195">Cadena</span><span class="sxs-lookup"><span data-stu-id="b21ef-195">String</span></span> | <span data-ttu-id="b21ef-196">Y</span><span class="sxs-lookup"><span data-stu-id="b21ef-196">Y</span></span> |
| <span data-ttu-id="b21ef-197">Int32</span><span class="sxs-lookup"><span data-stu-id="b21ef-197">Int32</span></span> | <span data-ttu-id="b21ef-198">Y</span><span class="sxs-lookup"><span data-stu-id="b21ef-198">Y</span></span> |
| <span data-ttu-id="b21ef-199">Int64</span><span class="sxs-lookup"><span data-stu-id="b21ef-199">Int64</span></span> | <span data-ttu-id="b21ef-200">Y</span><span class="sxs-lookup"><span data-stu-id="b21ef-200">Y</span></span> |
| <span data-ttu-id="b21ef-201">Double</span><span class="sxs-lookup"><span data-stu-id="b21ef-201">Double</span></span> | <span data-ttu-id="b21ef-202">Y</span><span class="sxs-lookup"><span data-stu-id="b21ef-202">Y</span></span> |
| <span data-ttu-id="b21ef-203">Booleano</span><span class="sxs-lookup"><span data-stu-id="b21ef-203">Boolean</span></span> | <span data-ttu-id="b21ef-204">Y</span><span class="sxs-lookup"><span data-stu-id="b21ef-204">Y</span></span> |
| <span data-ttu-id="b21ef-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="b21ef-205">DataTimeOffset</span></span> | <span data-ttu-id="b21ef-206">Y</span><span class="sxs-lookup"><span data-stu-id="b21ef-206">Y</span></span> |
| <span data-ttu-id="b21ef-207">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="b21ef-207">String Array</span></span> | <span data-ttu-id="b21ef-208">N</span><span class="sxs-lookup"><span data-stu-id="b21ef-208">N</span></span> |
| <span data-ttu-id="b21ef-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="b21ef-209">GeographyPoint</span></span> | <span data-ttu-id="b21ef-210">N</span><span class="sxs-lookup"><span data-stu-id="b21ef-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="b21ef-211">Ejemplo de JSON: Copia de datos de un servidor SQL Server local a un índice de Azure Search</span><span class="sxs-lookup"><span data-stu-id="b21ef-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="b21ef-212">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="b21ef-212">The following sample shows:</span></span>

1.  <span data-ttu-id="b21ef-213">Un servicio vinculado de tipo [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b21ef-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="b21ef-214">Un servicio vinculado de tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b21ef-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="b21ef-215">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b21ef-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="b21ef-216">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b21ef-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="b21ef-217">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) y [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b21ef-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b21ef-218">En el ejemplo se copian datos de serie temporal de una base de datos de SQL Server local a un índice de Azure Search cada hora.</span><span class="sxs-lookup"><span data-stu-id="b21ef-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="b21ef-219">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de ellos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="b21ef-220">En primer lugar, configure la puerta de enlace de administración de datos en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="b21ef-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="b21ef-221">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="b21ef-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b21ef-222">**Servicio vinculado de Azure Search**:</span><span class="sxs-lookup"><span data-stu-id="b21ef-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="b21ef-223">**Servicio vinculado de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b21ef-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="b21ef-224">**Conjunto de datos de entrada de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b21ef-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="b21ef-225">El ejemplo supone que ha creado una tabla "MyTable" en SQL Server y que contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="b21ef-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="b21ef-226">Puede consultar en varias tablas dentro de la misma base de datos mediante un único conjunto de datos, pero se debe utilizar una única tabla para typeProperty tableName del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="b21ef-227">Si se establece external: true, se informa al servicio Data Factory de que el conjunto de datos es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="b21ef-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="b21ef-228">**Conjunto de datos de salida Azure Search**:</span><span class="sxs-lookup"><span data-stu-id="b21ef-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="b21ef-229">En el ejemplo se copian los datos a un índice de Azure Search denominado "**products**".</span><span class="sxs-lookup"><span data-stu-id="b21ef-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="b21ef-230">Data Factory no crea el índice.</span><span class="sxs-lookup"><span data-stu-id="b21ef-230">Data Factory does not create the index.</span></span> <span data-ttu-id="b21ef-231">Para probar el ejemplo, cree un índice con este nombre.</span><span class="sxs-lookup"><span data-stu-id="b21ef-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="b21ef-232">Cree el índice de Azure Search con el mismo número de columnas que el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="b21ef-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="b21ef-233">Las nuevas entradas se agregan al índice de Azure Search cada hora.</span><span class="sxs-lookup"><span data-stu-id="b21ef-233">New entries are added to the Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="b21ef-234">**Actividad de copia en una canalización con origen SQL y receptor de índice de Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="b21ef-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="b21ef-235">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="b21ef-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b21ef-236">En la definición JSON de la canalización, el tipo **source** se establece en **SqlSource**, y el tipo **sink**, en **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="b21ef-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="b21ef-237">La consulta SQL especificada para la propiedad **SqlReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="b21ef-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="b21ef-238">Si va a copiar datos desde un almacén de datos en la nube a Azure Search, la propiedad `executionLocation` es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="b21ef-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="b21ef-239">El siguiente fragmento de código JSON muestra el cambio necesario en la actividad de copia `typeProperties` como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b21ef-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="b21ef-240">Comprobar [copiar datos entre almacenes de datos en la nube](data-factory-data-movement-activities.md#global) para obtener más detalles y los valores admitidos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="b21ef-241">Copia desde un origen en la nube</span><span class="sxs-lookup"><span data-stu-id="b21ef-241">Copy from a cloud source</span></span>
<span data-ttu-id="b21ef-242">Si va a copiar datos desde un almacén de datos en la nube a Azure Search, la propiedad `executionLocation` es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="b21ef-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="b21ef-243">El siguiente fragmento de código JSON muestra el cambio necesario en la actividad de copia `typeProperties` como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b21ef-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="b21ef-244">Comprobar [copiar datos entre almacenes de datos en la nube](data-factory-data-movement-activities.md#global) para obtener más detalles y los valores admitidos.</span><span class="sxs-lookup"><span data-stu-id="b21ef-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="b21ef-245">También puede asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor en la definición de actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b21ef-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="b21ef-246">Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b21ef-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b21ef-247">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="b21ef-247">Performance and tuning</span></span>  
<span data-ttu-id="b21ef-248">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para obtener más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="b21ef-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b21ef-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b21ef-249">Next steps</span></span>
<span data-ttu-id="b21ef-250">Consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b21ef-250">See the following articles:</span></span>

* <span data-ttu-id="b21ef-251">[Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b21ef-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
