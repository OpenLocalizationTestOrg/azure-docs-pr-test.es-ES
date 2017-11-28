---
title: aaaCopy datos hacia y desde la base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy datos hacia y desde la base de datos de SQL de Azure mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="6dcdd-103">Copiar datos tooand de base de datos de SQL de Azure mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="6dcdd-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="6dcdd-104">Este artículo explica cómo toouse Hola actividad de copia de Data Factory de Azure toomove datos tooand de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="6dcdd-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="6dcdd-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="6dcdd-106">Supported scenarios</span></span>
<span data-ttu-id="6dcdd-107">Puede copiar datos **de base de datos de SQL Azure** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6dcdd-108">Puede copiar los datos de hello siguientes almacenes de datos **tooAzure base de datos SQL**:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="6dcdd-109">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="6dcdd-109">Supported authentication type</span></span>
<span data-ttu-id="6dcdd-110">El conector de Azure SQL Database admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6dcdd-111">Introducción</span><span class="sxs-lookup"><span data-stu-id="6dcdd-111">Getting started</span></span>
<span data-ttu-id="6dcdd-112">Puede crear una canalización con actividad de copia que mueva los datos hacia Azure SQL Database y desde esta base de datos mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="6dcdd-113">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6dcdd-114">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6dcdd-115">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6dcdd-116">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6dcdd-117">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="6dcdd-118">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-118">Create a **data factory**.</span></span> <span data-ttu-id="6dcdd-119">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6dcdd-120">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6dcdd-121">Por ejemplo, si va a copiar datos desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="6dcdd-122">Para las propiedades de servicio vinculado que son específico tooAzure base de datos SQL, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="6dcdd-123">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6dcdd-124">En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="6dcdd-125">Y crear tabla de otro conjunto de datos toospecify Hola SQL en la base de datos de SQL Azure de Hola que contiene los datos de hello copiados desde el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="6dcdd-126">Para las propiedades del conjunto de datos que son específico tooAzure almacén de Data Lake, consulte [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="6dcdd-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6dcdd-128">En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y SqlSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6dcdd-129">De forma similar, si va a copiar desde la base de datos de SQL Azure tooAzure almacenamiento de blobs, utilice SqlSource y BlobSink en la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="6dcdd-130">Para copiar propiedades de actividad que son específico tooAzure base de datos SQL, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6dcdd-131">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="6dcdd-132">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6dcdd-133">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6dcdd-134">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde una base de datos de SQL Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-sql-database) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="6dcdd-135">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="6dcdd-136">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="6dcdd-136">Linked service properties</span></span>
<span data-ttu-id="6dcdd-137">SQL Azure había vinculado a los vínculos de servicio una factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="6dcdd-138">Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooAzure SQL servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="6dcdd-139">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6dcdd-139">Property</span></span> | <span data-ttu-id="6dcdd-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcdd-140">Description</span></span> | <span data-ttu-id="6dcdd-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6dcdd-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dcdd-142">type</span><span class="sxs-lookup"><span data-stu-id="6dcdd-142">type</span></span> |<span data-ttu-id="6dcdd-143">propiedad de tipo Hello debe establecerse en: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="6dcdd-144">Sí</span><span class="sxs-lookup"><span data-stu-id="6dcdd-144">Yes</span></span> |
| <span data-ttu-id="6dcdd-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="6dcdd-145">connectionString</span></span> |<span data-ttu-id="6dcdd-146">Especifique la información necesaria la instancia de base de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="6dcdd-147">Solo se admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="6dcdd-148">Sí</span><span class="sxs-lookup"><span data-stu-id="6dcdd-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6dcdd-149">Configurar [Firewall de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) Hola servidor de base de datos demasiado[permitir servidor de servicios de Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="6dcdd-150">Además, si va a copiar datos tooAzure base de datos SQL de incluido Azure fuera de orígenes de datos local con la puerta de enlace de generador de datos, configurar el intervalo de direcciones IP adecuado para la máquina de Hola que está enviando datos tooAzure base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="6dcdd-151">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="6dcdd-151">Dataset properties</span></span>
<span data-ttu-id="6dcdd-152">toospecify un conjunto de datos toorepresent datos de entrada o salidas de una base de datos de SQL Azure, Establece Hola de propiedad de tipo de conjunto de datos de Hola para: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="6dcdd-153">Conjunto hello **linkedServiceName** servicio vinculado de propiedad del nombre de toohello de conjunto de datos de Hola de hello SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="6dcdd-154">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6dcdd-155">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6dcdd-156">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6dcdd-157">Hola **typeProperties** sección Hola conjunto de datos de tipo **AzureSqlTable** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="6dcdd-158">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6dcdd-158">Property</span></span> | <span data-ttu-id="6dcdd-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcdd-159">Description</span></span> | <span data-ttu-id="6dcdd-160">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6dcdd-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dcdd-161">tableName</span><span class="sxs-lookup"><span data-stu-id="6dcdd-161">tableName</span></span> |<span data-ttu-id="6dcdd-162">Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Azure Hola que servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="6dcdd-163">Sí</span><span class="sxs-lookup"><span data-stu-id="6dcdd-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6dcdd-164">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="6dcdd-164">Copy activity properties</span></span>
<span data-ttu-id="6dcdd-165">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6dcdd-166">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6dcdd-167">Hola actividad de copia toma solo una entrada y produce un único resultado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="6dcdd-168">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6dcdd-169">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="6dcdd-170">Si va a mover datos desde una base de datos de SQL Azure, configure tipo de origen de hello en la actividad de copia de hello demasiado**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="6dcdd-171">De forma similar, si va a mover la base de datos de SQL Azure de tooan de datos, Establece el tipo de receptor de hello en actividad de copia de hello demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="6dcdd-172">Esta sección proporciona una lista de propiedades admitidas por SqlSource y SqlSink.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="6dcdd-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="6dcdd-173">SqlSource</span></span>
<span data-ttu-id="6dcdd-174">En la actividad de copia, cuando el origen de hello es de tipo **SqlSource**, Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="6dcdd-175">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6dcdd-175">Property</span></span> | <span data-ttu-id="6dcdd-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcdd-176">Description</span></span> | <span data-ttu-id="6dcdd-177">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6dcdd-177">Allowed values</span></span> | <span data-ttu-id="6dcdd-178">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6dcdd-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dcdd-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6dcdd-179">sqlReaderQuery</span></span> |<span data-ttu-id="6dcdd-180">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6dcdd-181">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-181">SQL query string.</span></span> <span data-ttu-id="6dcdd-182">Ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="6dcdd-183">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-183">No</span></span> |
| <span data-ttu-id="6dcdd-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dcdd-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="6dcdd-185">Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="6dcdd-186">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-186">Name of hello stored procedure.</span></span> <span data-ttu-id="6dcdd-187">Hola última instrucción de SQL debe ser una instrucción SELECT en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="6dcdd-188">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-188">No</span></span> |
| <span data-ttu-id="6dcdd-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dcdd-189">storedProcedureParameters</span></span> |<span data-ttu-id="6dcdd-190">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="6dcdd-191">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-191">Name/value pairs.</span></span> <span data-ttu-id="6dcdd-192">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="6dcdd-193">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-193">No</span></span> |

<span data-ttu-id="6dcdd-194">Si hello **sqlReaderQuery** se especifica para hello SqlSource, hello actividad de copia ejecuta esta consulta en datos de Hola de hello base de datos de SQL Azure origen tooget.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="6dcdd-195">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="6dcdd-196">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, columnas de hello definidas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usa una consulta (`select column1, column2 from mytable`) toorun contra Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="6dcdd-197">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="6dcdd-198">Cuando usas **sqlReaderStoredProcedureName**, seguirá necesitando toospecify un valor para hello **tableName** propiedad Hola de conjunto de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="6dcdd-199">Pero no se ha realizado ninguna validación en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="6dcdd-200">Ejemplo de SqlSource</span><span class="sxs-lookup"><span data-stu-id="6dcdd-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="6dcdd-201">**Hola almacena la definición del procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-201">**hello stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a><span data-ttu-id="6dcdd-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="6dcdd-202">SqlSink</span></span>
<span data-ttu-id="6dcdd-203">**SqlSink** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="6dcdd-204">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6dcdd-204">Property</span></span> | <span data-ttu-id="6dcdd-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcdd-205">Description</span></span> | <span data-ttu-id="6dcdd-206">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6dcdd-206">Allowed values</span></span> | <span data-ttu-id="6dcdd-207">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6dcdd-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dcdd-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6dcdd-208">writeBatchTimeout</span></span> |<span data-ttu-id="6dcdd-209">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="6dcdd-210">timespan</span><span class="sxs-lookup"><span data-stu-id="6dcdd-210">timespan</span></span><br/><br/> <span data-ttu-id="6dcdd-211">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6dcdd-212">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-212">No</span></span> |
| <span data-ttu-id="6dcdd-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6dcdd-213">writeBatchSize</span></span> |<span data-ttu-id="6dcdd-214">Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6dcdd-215">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="6dcdd-215">Integer (number of rows)</span></span> |<span data-ttu-id="6dcdd-216">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="6dcdd-216">No (default: 10000)</span></span> |
| <span data-ttu-id="6dcdd-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6dcdd-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6dcdd-218">Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="6dcdd-219">Para más información, consulte [Copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="6dcdd-220">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-220">A query statement.</span></span> |<span data-ttu-id="6dcdd-221">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-221">No</span></span> |
| <span data-ttu-id="6dcdd-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6dcdd-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6dcdd-223">Especifique un nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="6dcdd-224">Para más información, consulte [Copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="6dcdd-225">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6dcdd-226">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-226">No</span></span> |
| <span data-ttu-id="6dcdd-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6dcdd-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="6dcdd-228">Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="6dcdd-229">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="6dcdd-230">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-230">No</span></span> |
| <span data-ttu-id="6dcdd-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6dcdd-231">storedProcedureParameters</span></span> |<span data-ttu-id="6dcdd-232">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="6dcdd-233">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-233">Name/value pairs.</span></span> <span data-ttu-id="6dcdd-234">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="6dcdd-235">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-235">No</span></span> |
| <span data-ttu-id="6dcdd-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="6dcdd-236">sqlWriterTableType</span></span> |<span data-ttu-id="6dcdd-237">Especifique un toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="6dcdd-238">Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="6dcdd-239">Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="6dcdd-240">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-240">A table type name.</span></span> |<span data-ttu-id="6dcdd-241">No</span><span class="sxs-lookup"><span data-stu-id="6dcdd-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="6dcdd-242">Ejemplo de SqlSink</span><span class="sxs-lookup"><span data-stu-id="6dcdd-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="6dcdd-243">Ejemplos JSON para copiar datos tooand de base de datos de SQL</span><span class="sxs-lookup"><span data-stu-id="6dcdd-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="6dcdd-244">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6dcdd-245">Muestran cómo toocopy tooand de datos de la base de datos de SQL Azure y almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="6dcdd-246">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="6dcdd-247">Ejemplo: Copiar los datos de base de datos de SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="6dcdd-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="6dcdd-248">Hello mismo define Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="6dcdd-249">Un servicio vinculado de tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="6dcdd-250">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="6dcdd-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6dcdd-251">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6dcdd-252">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6dcdd-253">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [SqlSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6dcdd-254">ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de una tabla de blob de tooa de base de datos de SQL Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="6dcdd-255">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="6dcdd-256">**Servicio vinculado a Azure SQL Database:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="6dcdd-257">Vea hello [servicio vinculado de SQL Azure](#linked-service) sección para obtener lista de Hola de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="6dcdd-258">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="6dcdd-259">Vea hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artículo para obtener lista de Hola de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="6dcdd-260">**Conjunto de datos de entrada SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="6dcdd-261">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Azure y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6dcdd-262">Establecer "externo": "true" informa a servicio de Azure Data Factory de Hola ese conjunto de datos de hello es toohello externo factoría de datos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="6dcdd-263">Vea hello [propiedades de tipo de conjunto de datos de SQL Azure](#dataset) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="6dcdd-264">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6dcdd-265">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6dcdd-266">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6dcdd-267">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="6dcdd-268">Vea hello [propiedades de tipo de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="6dcdd-269">**Actividad de copia en una canalización con el origen SQL y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="6dcdd-270">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6dcdd-271">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6dcdd-272">consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="6dcdd-273">En el ejemplo de Hola, **sqlReaderQuery** se especifica para hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="6dcdd-274">Hola actividad de copia ejecuta esta consulta en datos de base de datos de SQL Azure origen tooget Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="6dcdd-275">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="6dcdd-276">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usado un toorun consulta contra Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="6dcdd-277">Por ejemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="6dcdd-278">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="6dcdd-279">Vea hello [origen Sql](#sqlsource) sección y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de Hola de propiedades admitidas por SqlSource y BlobSink.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="6dcdd-280">Ejemplo: Copiar los datos de Blob de Azure tooAzure base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="6dcdd-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="6dcdd-281">ejemplo de Hola define Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="6dcdd-282">Un servicio vinculado de tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="6dcdd-283">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="6dcdd-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6dcdd-284">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6dcdd-285">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="6dcdd-286">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="6dcdd-287">ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de tabla de tooa de blobs de Azure en la base de datos SQL de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="6dcdd-288">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6dcdd-289">**Servicio vinculado SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="6dcdd-290">Vea hello [servicio vinculado de SQL Azure](#linked-service) sección para obtener lista de Hola de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="6dcdd-291">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="6dcdd-292">Vea hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artículo para obtener lista de Hola de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="6dcdd-293">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="6dcdd-294">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6dcdd-295">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6dcdd-296">ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6dcdd-297">"externo": "true" configuración informa a servicio de factoría de datos de Hola que esta tabla es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="6dcdd-298">Vea hello [propiedades de tipo de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="6dcdd-299">**Conjunto de datos de salida de Azure SQL Database:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="6dcdd-300">ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="6dcdd-301">Crear tabla de hello en SQL Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6dcdd-302">Se agregan nuevas filas toohello tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-302">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="6dcdd-303">Vea hello [propiedades de tipo de conjunto de datos de SQL Azure](#dataset) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="6dcdd-304">**Una actividad de copia en una canalización con el origen de blob y el receptor SQL:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="6dcdd-305">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6dcdd-306">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="6dcdd-307">Vea hello [receptor de Sql](#sqlsink) sección y [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de Hola de propiedades admitidas por SqlSink y BlobSource.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="6dcdd-308">Columnas de identidad en la base de datos de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="6dcdd-308">Identity columns in hello target database</span></span>
<span data-ttu-id="6dcdd-309">En esta sección se proporciona un ejemplo para copiar datos de una tabla de origen sin una tabla de destino de tooa de columna de identidad con una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="6dcdd-310">**Tabla de origen:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="6dcdd-311">**Tabla de destino:**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="6dcdd-312">Tenga en cuenta que esa tabla de destino de hello tiene una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="6dcdd-313">**Definición de JSON del conjunto de datos de origen**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="6dcdd-314">**Definición de JSON del conjunto de datos de destino**</span><span class="sxs-lookup"><span data-stu-id="6dcdd-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="6dcdd-315">Tenga en cuenta que la tabla de origen y de destino tienen un esquema diferente (el destino tiene una columna adicional con identidad).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="6dcdd-316">En este escenario, necesita toospecify **estructura** propiedad en la definición de conjunto de datos de destino de hello, que no incluye la columna de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="6dcdd-317">Invocación del procedimiento almacenado desde el receptor de SQL</span><span class="sxs-lookup"><span data-stu-id="6dcdd-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="6dcdd-318">Para obtener un ejemplo de invocación a un procedimiento almacenado de receptor SQL en una actividad de copia de una canalización, consulte el artículo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocación de un procedimiento almacenado para el receptor SQL en la actividad de copia).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="6dcdd-319">Asignación de tipos para Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6dcdd-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="6dcdd-320">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="6dcdd-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="6dcdd-321">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="6dcdd-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6dcdd-322">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="6dcdd-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6dcdd-323">Al mover datos tooand de base de datos de SQL Azure, hello siguientes usan las asignaciones son del tipo de too.NET de tipo SQL y viceversa.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="6dcdd-324">asignación de Hello es igual a la asignación de tipo de datos de SQL Server para ADO.NET Hola.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="6dcdd-325">Tipo de motor de base de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="6dcdd-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="6dcdd-326">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6dcdd-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="6dcdd-327">bigint</span><span class="sxs-lookup"><span data-stu-id="6dcdd-327">bigint</span></span> |<span data-ttu-id="6dcdd-328">Int64</span><span class="sxs-lookup"><span data-stu-id="6dcdd-328">Int64</span></span> |
| <span data-ttu-id="6dcdd-329">binary</span><span class="sxs-lookup"><span data-stu-id="6dcdd-329">binary</span></span> |<span data-ttu-id="6dcdd-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-330">Byte[]</span></span> |
| <span data-ttu-id="6dcdd-331">bit</span><span class="sxs-lookup"><span data-stu-id="6dcdd-331">bit</span></span> |<span data-ttu-id="6dcdd-332">Booleano</span><span class="sxs-lookup"><span data-stu-id="6dcdd-332">Boolean</span></span> |
| <span data-ttu-id="6dcdd-333">char</span><span class="sxs-lookup"><span data-stu-id="6dcdd-333">char</span></span> |<span data-ttu-id="6dcdd-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-334">String, Char[]</span></span> |
| <span data-ttu-id="6dcdd-335">fecha</span><span class="sxs-lookup"><span data-stu-id="6dcdd-335">date</span></span> |<span data-ttu-id="6dcdd-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dcdd-336">DateTime</span></span> |
| <span data-ttu-id="6dcdd-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dcdd-337">Datetime</span></span> |<span data-ttu-id="6dcdd-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dcdd-338">DateTime</span></span> |
| <span data-ttu-id="6dcdd-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="6dcdd-339">datetime2</span></span> |<span data-ttu-id="6dcdd-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dcdd-340">DateTime</span></span> |
| <span data-ttu-id="6dcdd-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="6dcdd-341">Datetimeoffset</span></span> |<span data-ttu-id="6dcdd-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="6dcdd-342">DateTimeOffset</span></span> |
| <span data-ttu-id="6dcdd-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="6dcdd-343">Decimal</span></span> |<span data-ttu-id="6dcdd-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="6dcdd-344">Decimal</span></span> |
| <span data-ttu-id="6dcdd-345">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="6dcdd-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="6dcdd-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-346">Byte[]</span></span> |
| <span data-ttu-id="6dcdd-347">Float</span><span class="sxs-lookup"><span data-stu-id="6dcdd-347">Float</span></span> |<span data-ttu-id="6dcdd-348">Doble</span><span class="sxs-lookup"><span data-stu-id="6dcdd-348">Double</span></span> |
| <span data-ttu-id="6dcdd-349">imagen</span><span class="sxs-lookup"><span data-stu-id="6dcdd-349">image</span></span> |<span data-ttu-id="6dcdd-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-350">Byte[]</span></span> |
| <span data-ttu-id="6dcdd-351">int</span><span class="sxs-lookup"><span data-stu-id="6dcdd-351">int</span></span> |<span data-ttu-id="6dcdd-352">Int32</span><span class="sxs-lookup"><span data-stu-id="6dcdd-352">Int32</span></span> |
| <span data-ttu-id="6dcdd-353">money</span><span class="sxs-lookup"><span data-stu-id="6dcdd-353">money</span></span> |<span data-ttu-id="6dcdd-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="6dcdd-354">Decimal</span></span> |
| <span data-ttu-id="6dcdd-355">nchar</span><span class="sxs-lookup"><span data-stu-id="6dcdd-355">nchar</span></span> |<span data-ttu-id="6dcdd-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-356">String, Char[]</span></span> |
| <span data-ttu-id="6dcdd-357">ntext</span><span class="sxs-lookup"><span data-stu-id="6dcdd-357">ntext</span></span> |<span data-ttu-id="6dcdd-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-358">String, Char[]</span></span> |
| <span data-ttu-id="6dcdd-359">numeric</span><span class="sxs-lookup"><span data-stu-id="6dcdd-359">numeric</span></span> |<span data-ttu-id="6dcdd-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="6dcdd-360">Decimal</span></span> |
| <span data-ttu-id="6dcdd-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="6dcdd-361">nvarchar</span></span> |<span data-ttu-id="6dcdd-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-362">String, Char[]</span></span> |
| <span data-ttu-id="6dcdd-363">real</span><span class="sxs-lookup"><span data-stu-id="6dcdd-363">real</span></span> |<span data-ttu-id="6dcdd-364">Single</span><span class="sxs-lookup"><span data-stu-id="6dcdd-364">Single</span></span> |
| <span data-ttu-id="6dcdd-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="6dcdd-365">rowversion</span></span> |<span data-ttu-id="6dcdd-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-366">Byte[]</span></span> |
| <span data-ttu-id="6dcdd-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="6dcdd-367">smalldatetime</span></span> |<span data-ttu-id="6dcdd-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dcdd-368">DateTime</span></span> |
| <span data-ttu-id="6dcdd-369">smallint</span><span class="sxs-lookup"><span data-stu-id="6dcdd-369">smallint</span></span> |<span data-ttu-id="6dcdd-370">Int16</span><span class="sxs-lookup"><span data-stu-id="6dcdd-370">Int16</span></span> |
| <span data-ttu-id="6dcdd-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="6dcdd-371">smallmoney</span></span> |<span data-ttu-id="6dcdd-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="6dcdd-372">Decimal</span></span> |
| <span data-ttu-id="6dcdd-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="6dcdd-373">sql_variant</span></span> |<span data-ttu-id="6dcdd-374">Object *</span><span class="sxs-lookup"><span data-stu-id="6dcdd-374">Object *</span></span> |
| <span data-ttu-id="6dcdd-375">text</span><span class="sxs-lookup"><span data-stu-id="6dcdd-375">text</span></span> |<span data-ttu-id="6dcdd-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-376">String, Char[]</span></span> |
| <span data-ttu-id="6dcdd-377">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="6dcdd-377">time</span></span> |<span data-ttu-id="6dcdd-378">timespan</span><span class="sxs-lookup"><span data-stu-id="6dcdd-378">TimeSpan</span></span> |
| <span data-ttu-id="6dcdd-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="6dcdd-379">timestamp</span></span> |<span data-ttu-id="6dcdd-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-380">Byte[]</span></span> |
| <span data-ttu-id="6dcdd-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="6dcdd-381">tinyint</span></span> |<span data-ttu-id="6dcdd-382">Byte</span><span class="sxs-lookup"><span data-stu-id="6dcdd-382">Byte</span></span> |
| <span data-ttu-id="6dcdd-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="6dcdd-383">uniqueidentifier</span></span> |<span data-ttu-id="6dcdd-384">Guid</span><span class="sxs-lookup"><span data-stu-id="6dcdd-384">Guid</span></span> |
| <span data-ttu-id="6dcdd-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="6dcdd-385">varbinary</span></span> |<span data-ttu-id="6dcdd-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-386">Byte[]</span></span> |
| <span data-ttu-id="6dcdd-387">varchar</span><span class="sxs-lookup"><span data-stu-id="6dcdd-387">varchar</span></span> |<span data-ttu-id="6dcdd-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6dcdd-388">String, Char[]</span></span> |
| <span data-ttu-id="6dcdd-389">xml</span><span class="sxs-lookup"><span data-stu-id="6dcdd-389">xml</span></span> |<span data-ttu-id="6dcdd-390">xml</span><span class="sxs-lookup"><span data-stu-id="6dcdd-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="6dcdd-391">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="6dcdd-391">Map source toosink columns</span></span>
<span data-ttu-id="6dcdd-392">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="6dcdd-393">Copia repetible</span><span class="sxs-lookup"><span data-stu-id="6dcdd-393">Repeatable copy</span></span>
<span data-ttu-id="6dcdd-394">Cuando se copian datos tooSQL base de datos de servidor, actividad de copia de hello anexa la tabla de datos toohello receptor de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="6dcdd-395">en su lugar, vea tooperform un UPSERT [tooSqlSink escritura repetible](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artículo.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="6dcdd-396">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="6dcdd-397">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6dcdd-398">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6dcdd-399">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6dcdd-400">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6dcdd-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6dcdd-401">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="6dcdd-401">Performance and Tuning</span></span>
<span data-ttu-id="6dcdd-402">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="6dcdd-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
