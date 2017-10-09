---
title: "índice de tooSearch aaaPush datos mediante el uso de la factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopush datos tooAzure índice de búsqueda mediante el uso de Data Factory de Azure."
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
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="4ccd5-103">Inserción de índice de búsqueda de Azure de tooan de datos mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="4ccd5-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="4ccd5-104">Este artículo describe cómo toouse Hola actividad de copia toopush los datos de un origen compatible datos almacenan tooAzure índice de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="4ccd5-105">Almacenes de datos de origen compatible se muestran en la columna de origen de Hola de hello [admite orígenes y receptores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4ccd5-106">En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia y combinaciones de almacén de datos admitidos.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="4ccd5-107">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="4ccd5-107">Enabling connectivity</span></span>
<span data-ttu-id="4ccd5-108">tooallow servicio Data Factory conectarse tooan un almacén de datos local, instale Data Management Gateway en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="4ccd5-109">Puerta de enlace se puede instalar en hello mismo equipo que hospeda los datos de origen de hello almacenar o en un tooavoid máquina independiente que compiten por los recursos con datos de hello almacenar.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="4ccd5-110">Puerta de enlace de administración de datos se conecta a servicios de toocloud de orígenes de datos locales de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="4ccd5-111">Consulte el artículo [Mover datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4ccd5-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="4ccd5-112">Getting started</span></span>
<span data-ttu-id="4ccd5-113">Puede crear una canalización con la actividad de copia que traslada los datos de un índice de búsqueda de tooAzure del almacén de datos de origen mediante el uso de distintas herramientas y API.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="4ccd5-114">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4ccd5-115">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="4ccd5-116">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4ccd5-117">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4ccd5-118">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="4ccd5-119">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4ccd5-120">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="4ccd5-121">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4ccd5-122">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4ccd5-123">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4ccd5-124">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son el índice de búsqueda de tooAzure de toocopy usa datos, vea [ejemplo de JSON: copiar los datos de índice de búsqueda de tooAzure de SQL Server local](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="4ccd5-125">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure índice de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4ccd5-126">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="4ccd5-126">Linked service properties</span></span>

<span data-ttu-id="4ccd5-127">Hello en la tabla siguiente proporciona descripciones para los elementos JSON que son toohello específico del servicio Búsqueda de Azure vinculada.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="4ccd5-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4ccd5-128">Property</span></span> | <span data-ttu-id="4ccd5-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="4ccd5-129">Description</span></span> | <span data-ttu-id="4ccd5-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="4ccd5-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4ccd5-131">type</span><span class="sxs-lookup"><span data-stu-id="4ccd5-131">type</span></span> | <span data-ttu-id="4ccd5-132">propiedad de tipo Hello debe establecerse en: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="4ccd5-133">Sí</span><span class="sxs-lookup"><span data-stu-id="4ccd5-133">Yes</span></span> |
| <span data-ttu-id="4ccd5-134">url</span><span class="sxs-lookup"><span data-stu-id="4ccd5-134">url</span></span> | <span data-ttu-id="4ccd5-135">Dirección URL de hello servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="4ccd5-136">Sí</span><span class="sxs-lookup"><span data-stu-id="4ccd5-136">Yes</span></span> |
| <span data-ttu-id="4ccd5-137">key</span><span class="sxs-lookup"><span data-stu-id="4ccd5-137">key</span></span> | <span data-ttu-id="4ccd5-138">Clave de administrador de hello servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="4ccd5-139">Sí</span><span class="sxs-lookup"><span data-stu-id="4ccd5-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="4ccd5-140">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="4ccd5-140">Dataset properties</span></span>

<span data-ttu-id="4ccd5-141">Para obtener una lista completa de secciones y propiedades que están disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4ccd5-142">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="4ccd5-143">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="4ccd5-144">Hola typeProperties sección un conjunto de datos de tipo hello **AzureSearchIndex** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="4ccd5-145">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4ccd5-145">Property</span></span> | <span data-ttu-id="4ccd5-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="4ccd5-146">Description</span></span> | <span data-ttu-id="4ccd5-147">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="4ccd5-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4ccd5-148">type</span><span class="sxs-lookup"><span data-stu-id="4ccd5-148">type</span></span> | <span data-ttu-id="4ccd5-149">se debe establecer propiedad de tipo Hello demasiado**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="4ccd5-150">Sí</span><span class="sxs-lookup"><span data-stu-id="4ccd5-150">Yes</span></span> |
| <span data-ttu-id="4ccd5-151">indexName</span><span class="sxs-lookup"><span data-stu-id="4ccd5-151">indexName</span></span> | <span data-ttu-id="4ccd5-152">Nombre del índice de búsqueda de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="4ccd5-153">Factoría de datos no crea el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="4ccd5-154">índice de Hello debe existir en la búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="4ccd5-155">Sí</span><span class="sxs-lookup"><span data-stu-id="4ccd5-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="4ccd5-156">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="4ccd5-156">Copy activity properties</span></span>
<span data-ttu-id="4ccd5-157">Para obtener una lista completa de secciones y propiedades que están disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4ccd5-158">Las propiedades (como el nombre, la descripción, las tablas de entrada y salida, y las distintas directivas) están disponibles en todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="4ccd5-159">Mientras que las propiedades disponibles en la sección de hello typeProperties varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="4ccd5-160">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4ccd5-161">Actividad de copia al receptor de hello es de tipo hello **AzureSearchIndexSink**, Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4ccd5-162">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4ccd5-162">Property</span></span> | <span data-ttu-id="4ccd5-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="4ccd5-163">Description</span></span> | <span data-ttu-id="4ccd5-164">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="4ccd5-164">Allowed values</span></span> | <span data-ttu-id="4ccd5-165">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="4ccd5-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="4ccd5-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="4ccd5-166">WriteBehavior</span></span> | <span data-ttu-id="4ccd5-167">Especifica si toomerge o reemplazar cuando un documento ya existe en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="4ccd5-168">Vea hello [WriteBehavior propiedad](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="4ccd5-169">Combinar (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="4ccd5-169">Merge (default)</span></span><br/><span data-ttu-id="4ccd5-170">Cargar</span><span class="sxs-lookup"><span data-stu-id="4ccd5-170">Upload</span></span>| <span data-ttu-id="4ccd5-171">No</span><span class="sxs-lookup"><span data-stu-id="4ccd5-171">No</span></span> |
| <span data-ttu-id="4ccd5-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="4ccd5-172">WriteBatchSize</span></span> | <span data-ttu-id="4ccd5-173">Carga datos en el índice de búsqueda de Azure de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="4ccd5-174">Vea hello [propiedad valor WriteBatchSize](#writebatchsize-property) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="4ccd5-175">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-175">1 too1,000.</span></span> <span data-ttu-id="4ccd5-176">El valor predeterminado es 1000.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-176">Default value is 1000.</span></span> | <span data-ttu-id="4ccd5-177">No</span><span class="sxs-lookup"><span data-stu-id="4ccd5-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="4ccd5-178">Propiedad WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="4ccd5-178">WriteBehavior property</span></span>
<span data-ttu-id="4ccd5-179">AzureSearchSink realiza una operación upsert al escribir los datos.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="4ccd5-180">En otras palabras, al escribir un documento, si la clave de documento de hello ya existe en el índice de búsqueda de Azure de hello, búsqueda de Azure actualiza documento existente de hello en lugar de producir una excepción de conflicto.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="4ccd5-181">Hola AzureSearchSink proporciona Hola siguiendo dos comportamientos upsert (mediante el uso de AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="4ccd5-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="4ccd5-182">**Mezcla**: combinar todas las columnas de Hola de nuevo documento de hello con hello uno existente.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="4ccd5-183">Para las columnas con valor null en el nuevo documento de hello, se conserva el valor de Hola Hola uno existente.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="4ccd5-184">**Cargar**: reemplaza el documento nuevo Hola Hola uno ya existente.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="4ccd5-185">Para las columnas no especificadas en el nuevo documento de hello, Hola valor toonull si hay un valor distinto de null en el documento existente de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="4ccd5-186">es el comportamiento predeterminado de Hello **mezcla**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="4ccd5-187">Propiedad WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="4ccd5-187">WriteBatchSize Property</span></span>
<span data-ttu-id="4ccd5-188">Azure Search puede crear documentos como lotes.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="4ccd5-189">Un lote puede contener 1 too1, 000 acciones.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="4ccd5-190">Una acción controla una operación de carga/merge Hola de documento tooperform.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="4ccd5-191">Compatibilidad con los tipos de datos</span><span class="sxs-lookup"><span data-stu-id="4ccd5-191">Data type support</span></span>
<span data-ttu-id="4ccd5-192">Hello siguiente tabla especifica si se admite un tipo de datos de búsqueda de Azure o no.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="4ccd5-193">Tipo de datos de Azure Search</span><span class="sxs-lookup"><span data-stu-id="4ccd5-193">Azure Search data type</span></span> | <span data-ttu-id="4ccd5-194">Compatible con el receptor de Azure Search</span><span class="sxs-lookup"><span data-stu-id="4ccd5-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="4ccd5-195">Cadena</span><span class="sxs-lookup"><span data-stu-id="4ccd5-195">String</span></span> | <span data-ttu-id="4ccd5-196">Y</span><span class="sxs-lookup"><span data-stu-id="4ccd5-196">Y</span></span> |
| <span data-ttu-id="4ccd5-197">Int32</span><span class="sxs-lookup"><span data-stu-id="4ccd5-197">Int32</span></span> | <span data-ttu-id="4ccd5-198">Y</span><span class="sxs-lookup"><span data-stu-id="4ccd5-198">Y</span></span> |
| <span data-ttu-id="4ccd5-199">Int64</span><span class="sxs-lookup"><span data-stu-id="4ccd5-199">Int64</span></span> | <span data-ttu-id="4ccd5-200">Y</span><span class="sxs-lookup"><span data-stu-id="4ccd5-200">Y</span></span> |
| <span data-ttu-id="4ccd5-201">Double</span><span class="sxs-lookup"><span data-stu-id="4ccd5-201">Double</span></span> | <span data-ttu-id="4ccd5-202">Y</span><span class="sxs-lookup"><span data-stu-id="4ccd5-202">Y</span></span> |
| <span data-ttu-id="4ccd5-203">Booleano</span><span class="sxs-lookup"><span data-stu-id="4ccd5-203">Boolean</span></span> | <span data-ttu-id="4ccd5-204">Y</span><span class="sxs-lookup"><span data-stu-id="4ccd5-204">Y</span></span> |
| <span data-ttu-id="4ccd5-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="4ccd5-205">DataTimeOffset</span></span> | <span data-ttu-id="4ccd5-206">Y</span><span class="sxs-lookup"><span data-stu-id="4ccd5-206">Y</span></span> |
| <span data-ttu-id="4ccd5-207">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="4ccd5-207">String Array</span></span> | <span data-ttu-id="4ccd5-208">N</span><span class="sxs-lookup"><span data-stu-id="4ccd5-208">N</span></span> |
| <span data-ttu-id="4ccd5-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="4ccd5-209">GeographyPoint</span></span> | <span data-ttu-id="4ccd5-210">N</span><span class="sxs-lookup"><span data-stu-id="4ccd5-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="4ccd5-211">Ejemplo de JSON: copiar los datos de índice de búsqueda de tooAzure de SQL Server local</span><span class="sxs-lookup"><span data-stu-id="4ccd5-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="4ccd5-212">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="4ccd5-213">Un servicio vinculado de tipo [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="4ccd5-214">Un servicio vinculado de tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="4ccd5-215">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="4ccd5-216">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="4ccd5-217">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) y [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="4ccd5-218">ejemplo de Hola copia datos de serie temporal de un índice de búsqueda de Azure local tooan de base de datos de SQL Server cada hora.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="4ccd5-219">propiedades JSON de Hello utilizados en este ejemplo se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="4ccd5-220">Como primer paso, configurar la puerta de enlace de hello datos administración en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="4ccd5-221">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="4ccd5-222">**Servicio vinculado de Azure Search**:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="4ccd5-223">**Servicio vinculado de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="4ccd5-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="4ccd5-224">**Conjunto de datos de entrada de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="4ccd5-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="4ccd5-225">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Server y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="4ccd5-226">Puede consultar a través de varias tablas dentro de hello misma mediante un único conjunto de datos, pero una sola tabla de base de datos debe utilizarse para typeProperty de nombre de tabla del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="4ccd5-227">Establecer "externo": "true" informa a servicio de factoría de datos ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="4ccd5-228">**Conjunto de datos de salida Azure Search**:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="4ccd5-229">Hola copias datos tooan búsqueda de Azure índice de ejemplo denominado **productos**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="4ccd5-230">Factoría de datos no crea el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="4ccd5-231">Hola tootest de ejemplo, cree un índice con este nombre.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="4ccd5-232">Crear el índice de búsqueda de Azure de hello con hello mismo número de columnas como en el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="4ccd5-233">Se agregan entradas nuevas toohello índice de búsqueda de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-233">New entries are added toohello Azure Search index every hour.</span></span>

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

<span data-ttu-id="4ccd5-234">**Actividad de copia en una canalización con origen SQL y receptor de índice de Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="4ccd5-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="4ccd5-235">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="4ccd5-236">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="4ccd5-237">consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

<span data-ttu-id="4ccd5-238">Si va a copiar datos desde un almacén de datos en la nube a Azure Search, la propiedad `executionLocation` es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="4ccd5-239">Hello siguiente fragmento JSON muestra es necesario en la actividad de copia de cambio de hello `typeProperties` como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="4ccd5-240">Comprobar [copiar datos entre almacenes de datos en la nube](data-factory-data-movement-activities.md#global) para obtener más detalles y los valores admitidos.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="4ccd5-241">Copia desde un origen en la nube</span><span class="sxs-lookup"><span data-stu-id="4ccd5-241">Copy from a cloud source</span></span>
<span data-ttu-id="4ccd5-242">Si va a copiar datos desde un almacén de datos en la nube a Azure Search, la propiedad `executionLocation` es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="4ccd5-243">Hello siguiente fragmento JSON muestra es necesario en la actividad de copia de cambio de hello `typeProperties` como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="4ccd5-244">Comprobar [copiar datos entre almacenes de datos en la nube](data-factory-data-movement-activities.md#global) para obtener más detalles y los valores admitidos.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="4ccd5-245">También puede asignar columnas de toocolumns de conjunto de datos de origen del conjunto de datos de receptor en la definición de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="4ccd5-246">Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4ccd5-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4ccd5-247">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="4ccd5-247">Performance and tuning</span></span>  
<span data-ttu-id="4ccd5-248">Vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento del movimiento de datos (actividad de copia) y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ccd5-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ccd5-249">Next steps</span></span>
<span data-ttu-id="4ccd5-250">Vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="4ccd5-250">See hello following articles:</span></span>

* <span data-ttu-id="4ccd5-251">[Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="4ccd5-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
