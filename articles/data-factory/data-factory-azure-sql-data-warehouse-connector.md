---
title: datos de aaaCopy hacia/desde el almacenamiento de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy datos hacia y desde el almacenamiento de datos de SQL Azure mediante Data Factory de Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="280bd-103">Copiar datos tooand de almacenamiento de datos de SQL Azure mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="280bd-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="280bd-104">Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="280bd-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="280bd-106">tooachieve el mejor rendimiento, utilice datos de PolyBase tooload en almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="280bd-107">Hola [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sección con información detallada.</span><span class="sxs-lookup"><span data-stu-id="280bd-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="280bd-108">Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="280bd-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="280bd-109">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="280bd-109">Supported scenarios</span></span>
<span data-ttu-id="280bd-110">Puede copiar datos **de almacenamiento de datos de SQL Azure** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="280bd-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="280bd-111">Puede copiar los datos de hello siguientes almacenes de datos **tooAzure almacenamiento de datos SQL**:</span><span class="sxs-lookup"><span data-stu-id="280bd-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="280bd-112">Cuando se copian datos desde SQL Server o base de datos de SQL Azure tooAzure almacenamiento de datos de SQL, si no existe la tabla de hello en el almacén de destino de hello, factoría de datos puede crear automáticamente tabla hello en el almacén de datos de SQL mediante Hola un esquema de tabla de hello en origen Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="280bd-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="280bd-113">Vea [Creación automática de tablas](#auto-table-creation) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="280bd-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="280bd-114">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="280bd-114">Supported authentication type</span></span>
<span data-ttu-id="280bd-115">El conector de Azure SQL Data Warehouse admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="280bd-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="280bd-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="280bd-116">Getting started</span></span>
<span data-ttu-id="280bd-117">Puede crear una canalización con una actividad de copia que mueva datos con Azure SQL Data Warehouse como origen o destino mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="280bd-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="280bd-118">toocreate de manera más fácil de Hello una canalización que copia los datos de almacenamiento de datos de SQL Azure es el Asistente para datos de copia de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="280bd-119">Vea [Tutorial: cargar datos en almacenamiento de datos de SQL con factoría de datos](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="280bd-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="280bd-120">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="280bd-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="280bd-121">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="280bd-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="280bd-122">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="280bd-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="280bd-123">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="280bd-123">Create a **data factory**.</span></span> <span data-ttu-id="280bd-124">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="280bd-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="280bd-125">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="280bd-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="280bd-126">Por ejemplo, si va a copiar datos desde un almacén de datos de Azure blob storage tooan SQL Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="280bd-127">Para las propiedades de servicio vinculado que son específico tooAzure almacenamiento de datos SQL, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="280bd-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="280bd-128">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="280bd-129">En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="280bd-130">Y crear otra tabla de hello toospecify de conjunto de datos en almacenamiento de datos de SQL Azure Hola que contiene los datos de hello copiados desde el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="280bd-131">Para las propiedades de conjunto de datos que son específico tooAzure almacenamiento de datos SQL, consulte [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="280bd-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="280bd-132">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="280bd-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="280bd-133">En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y SqlDWSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="280bd-134">De forma similar, si va a copiar desde el almacenamiento de datos de SQL Azure tooAzure almacenamiento de blobs, usar SqlDWSource y BlobSink de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="280bd-135">Para copiar propiedades de actividad que son específico tooAzure almacenamiento de datos SQL, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="280bd-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="280bd-136">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="280bd-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="280bd-137">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="280bd-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="280bd-138">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="280bd-139">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy hacia/desde un almacén de datos de SQL Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="280bd-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="280bd-140">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure almacenamiento de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="280bd-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="280bd-141">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="280bd-141">Linked service properties</span></span>
<span data-ttu-id="280bd-142">Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooAzure servicio de almacenamiento de datos de SQL vinculado.</span><span class="sxs-lookup"><span data-stu-id="280bd-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="280bd-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280bd-143">Property</span></span> | <span data-ttu-id="280bd-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="280bd-144">Description</span></span> | <span data-ttu-id="280bd-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280bd-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="280bd-146">type</span><span class="sxs-lookup"><span data-stu-id="280bd-146">type</span></span> |<span data-ttu-id="280bd-147">propiedad de tipo Hello debe establecerse en: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="280bd-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="280bd-148">Sí</span><span class="sxs-lookup"><span data-stu-id="280bd-148">Yes</span></span> |
| <span data-ttu-id="280bd-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="280bd-149">connectionString</span></span> |<span data-ttu-id="280bd-150">Especifique la información necesaria la instancia de almacenamiento de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="280bd-151">Solo se admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="280bd-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="280bd-152">Sí</span><span class="sxs-lookup"><span data-stu-id="280bd-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="280bd-153">Configurar [Firewall de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) y Hola servidor de base de datos demasiado[permitir servidor de servicios de Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="280bd-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="280bd-154">Además, si va a copiar datos tooAzure almacenamiento de datos SQL de incluido Azure fuera de orígenes de datos local con la puerta de enlace de generador de datos, configurar el intervalo de direcciones IP adecuado para la máquina de Hola que está enviando datos tooAzure almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="280bd-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="280bd-155">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="280bd-155">Dataset properties</span></span>
<span data-ttu-id="280bd-156">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="280bd-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="280bd-157">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="280bd-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="280bd-158">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="280bd-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="280bd-159">Hola **typeProperties** sección Hola conjunto de datos de tipo **AzureSqlDWTable** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="280bd-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="280bd-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280bd-160">Property</span></span> | <span data-ttu-id="280bd-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="280bd-161">Description</span></span> | <span data-ttu-id="280bd-162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280bd-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="280bd-163">tableName</span><span class="sxs-lookup"><span data-stu-id="280bd-163">tableName</span></span> |<span data-ttu-id="280bd-164">Nombre de tabla de Hola o vista de base de datos de almacenamiento de datos de SQL Azure de Hola Hola servicio vinculado hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="280bd-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="280bd-165">Sí</span><span class="sxs-lookup"><span data-stu-id="280bd-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="280bd-166">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="280bd-166">Copy activity properties</span></span>
<span data-ttu-id="280bd-167">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="280bd-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="280bd-168">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="280bd-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="280bd-169">Hola actividad de copia toma solo una entrada y produce un único resultado.</span><span class="sxs-lookup"><span data-stu-id="280bd-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="280bd-170">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="280bd-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="280bd-171">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="280bd-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="280bd-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="280bd-172">SqlDWSource</span></span>
<span data-ttu-id="280bd-173">Cuando el origen es del tipo **SqlDWSource**, Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="280bd-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="280bd-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280bd-174">Property</span></span> | <span data-ttu-id="280bd-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="280bd-175">Description</span></span> | <span data-ttu-id="280bd-176">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="280bd-176">Allowed values</span></span> | <span data-ttu-id="280bd-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280bd-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="280bd-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="280bd-178">sqlReaderQuery</span></span> |<span data-ttu-id="280bd-179">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="280bd-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="280bd-180">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="280bd-180">SQL query string.</span></span> <span data-ttu-id="280bd-181">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="280bd-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="280bd-182">No</span><span class="sxs-lookup"><span data-stu-id="280bd-182">No</span></span> |
| <span data-ttu-id="280bd-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="280bd-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="280bd-184">Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="280bd-185">Nombre del programa Hola a procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="280bd-185">Name of hello stored procedure.</span></span> <span data-ttu-id="280bd-186">Hola última instrucción de SQL debe ser una instrucción SELECT en el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="280bd-187">No</span><span class="sxs-lookup"><span data-stu-id="280bd-187">No</span></span> |
| <span data-ttu-id="280bd-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="280bd-188">storedProcedureParameters</span></span> |<span data-ttu-id="280bd-189">Parámetros de hello procedimiento almacenan.</span><span class="sxs-lookup"><span data-stu-id="280bd-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="280bd-190">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="280bd-190">Name/value pairs.</span></span> <span data-ttu-id="280bd-191">Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="280bd-192">No</span><span class="sxs-lookup"><span data-stu-id="280bd-192">No</span></span> |

<span data-ttu-id="280bd-193">Si hello **sqlReaderQuery** se especifica para hello SqlDWSource, hello actividad de copia se ejecuta esta consulta contra Hola datos de almacenamiento de datos de SQL Azure origen tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="280bd-194">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="280bd-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="280bd-195">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usado un toorun consulta contra Hola almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="280bd-196">Ejemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="280bd-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="280bd-197">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="280bd-198">Ejemplo de SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="280bd-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="280bd-199">**Hola almacena la definición del procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="280bd-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="280bd-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="280bd-200">SqlDWSink</span></span>
<span data-ttu-id="280bd-201">**SqlDWSink** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="280bd-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="280bd-202">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280bd-202">Property</span></span> | <span data-ttu-id="280bd-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="280bd-203">Description</span></span> | <span data-ttu-id="280bd-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="280bd-204">Allowed values</span></span> | <span data-ttu-id="280bd-205">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280bd-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="280bd-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="280bd-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="280bd-207">Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian.</span><span class="sxs-lookup"><span data-stu-id="280bd-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="280bd-208">Consulte la [sección sobre repetibilidad](#repeatability-during-copy)para más información.</span><span class="sxs-lookup"><span data-stu-id="280bd-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="280bd-209">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="280bd-209">A query statement.</span></span> |<span data-ttu-id="280bd-210">No</span><span class="sxs-lookup"><span data-stu-id="280bd-210">No</span></span> |
| <span data-ttu-id="280bd-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="280bd-211">allowPolyBase</span></span> |<span data-ttu-id="280bd-212">Indica si toouse PolyBase (si procede) en lugar de mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="280bd-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="280bd-213">**El uso de PolyBase es Hola recomendado de forma que los datos tooload en almacenamiento de datos de SQL.**</span><span class="sxs-lookup"><span data-stu-id="280bd-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="280bd-214">Vea [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sección para las restricciones y los detalles.</span><span class="sxs-lookup"><span data-stu-id="280bd-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="280bd-215">True</span><span class="sxs-lookup"><span data-stu-id="280bd-215">True</span></span> <br/><span data-ttu-id="280bd-216">False (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="280bd-216">False (default)</span></span> |<span data-ttu-id="280bd-217">No</span><span class="sxs-lookup"><span data-stu-id="280bd-217">No</span></span> |
| <span data-ttu-id="280bd-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="280bd-218">polyBaseSettings</span></span> |<span data-ttu-id="280bd-219">Un grupo de propiedades que se pueden especificar cuando hello **allowPolybase** propiedad se establece demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="280bd-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="280bd-220">No</span><span class="sxs-lookup"><span data-stu-id="280bd-220">No</span></span> |
| <span data-ttu-id="280bd-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="280bd-221">rejectValue</span></span> |<span data-ttu-id="280bd-222">Especifica el número de Hola o porcentaje de filas que se pueda rechazar antes de que se produce un error en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="280bd-223">Obtener más información acerca de hello PolyBase rechazan opciones Hola **argumentos** sección de [crear tabla externa (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="280bd-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="280bd-224">0 (predeterminado), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="280bd-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="280bd-225">No</span><span class="sxs-lookup"><span data-stu-id="280bd-225">No</span></span> |
| <span data-ttu-id="280bd-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="280bd-226">rejectType</span></span> |<span data-ttu-id="280bd-227">Especifica si se especifica la opción de hello rejectValue como un valor literal o un porcentaje.</span><span class="sxs-lookup"><span data-stu-id="280bd-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="280bd-228">Valor (predeterminado), Porcentaje</span><span class="sxs-lookup"><span data-stu-id="280bd-228">Value (default), Percentage</span></span> |<span data-ttu-id="280bd-229">No</span><span class="sxs-lookup"><span data-stu-id="280bd-229">No</span></span> |
| <span data-ttu-id="280bd-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="280bd-230">rejectSampleValue</span></span> |<span data-ttu-id="280bd-231">Determina el número de Hola de tooretrieve filas antes de hello PolyBase vuelve a calcular el porcentaje de Hola de filas rechazados.</span><span class="sxs-lookup"><span data-stu-id="280bd-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="280bd-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="280bd-232">1, 2, …</span></span> |<span data-ttu-id="280bd-233">Sí, si el valor de **rejectType** es **percentage**</span><span class="sxs-lookup"><span data-stu-id="280bd-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="280bd-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="280bd-234">useTypeDefault</span></span> |<span data-ttu-id="280bd-235">Especifica cómo toohandle valores que falten en archivos delimitados por texto cuando PolyBase recupera datos de archivo de texto hello.</span><span class="sxs-lookup"><span data-stu-id="280bd-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="280bd-236">Más información acerca de esta propiedad desde la sección de argumentos de hello en [crear EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="280bd-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="280bd-237">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="280bd-237">True, False (default)</span></span> |<span data-ttu-id="280bd-238">No</span><span class="sxs-lookup"><span data-stu-id="280bd-238">No</span></span> |
| <span data-ttu-id="280bd-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="280bd-239">writeBatchSize</span></span> |<span data-ttu-id="280bd-240">Inserta los datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="280bd-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="280bd-241">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="280bd-241">Integer (number of rows)</span></span> |<span data-ttu-id="280bd-242">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="280bd-242">No (default: 10000)</span></span> |
| <span data-ttu-id="280bd-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="280bd-243">writeBatchTimeout</span></span> |<span data-ttu-id="280bd-244">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="280bd-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="280bd-245">timespan</span><span class="sxs-lookup"><span data-stu-id="280bd-245">timespan</span></span><br/><br/> <span data-ttu-id="280bd-246">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="280bd-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="280bd-247">No</span><span class="sxs-lookup"><span data-stu-id="280bd-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="280bd-248">Ejemplo de SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="280bd-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="280bd-249">Usar datos de PolyBase tooload en almacenamiento de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="280bd-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="280bd-250">Usar **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** es una manera eficaz de cargar grandes cantidades de datos en Azure SQL Data Warehouse con un alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="280bd-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="280bd-251">Puede ver grande ganancia en rendimiento hello mediante PolyBase en lugar de mecanismo BULKINSERT Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="280bd-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="280bd-252">Vea la [copia del número de referencia de rendimiento](data-factory-copy-activity-performance.md#performance-reference) con una comparación detallada.</span><span class="sxs-lookup"><span data-stu-id="280bd-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="280bd-253">Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="280bd-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="280bd-254">Si los datos de origen están en **blobs de Azure o almacén de Azure Data Lake**y formato de hello es compatible con PolyBase, puede copiar directamente tooAzure con PolyBase de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="280bd-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="280bd-255">Consulte **[Copias directas con PolyBase](#direct-copy-using-polybase)** para detalles.</span><span class="sxs-lookup"><span data-stu-id="280bd-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="280bd-256">Si el almacén de datos de origen y el formato no es compatible originalmente con PolyBase, puede usar hello  **[copia provisionalmente mediante PolyBase](#staged-copy-using-polybase)**  característica en su lugar.</span><span class="sxs-lookup"><span data-stu-id="280bd-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="280bd-257">También proporciona un mejor rendimiento al convertir datos de hello en formato compatible con PolyBase y almacenar datos de hello en el almacenamiento de blobs de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="280bd-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="280bd-258">Luego los carga en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="280bd-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="280bd-259">Conjunto hello `allowPolyBase` propiedad demasiado**true** tal y como se muestra en el siguiente ejemplo para Data Factory de Azure toouse PolyBase toocopy datos en almacenamiento de datos de SQL Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="280bd-260">Al establecer allowPolyBase tootrue, puede especificar propiedades específicas de PolyBase con hello `polyBaseSettings` grupo de propiedades.</span><span class="sxs-lookup"><span data-stu-id="280bd-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="280bd-261">vea hello [SqlDWSink](#SqlDWSink) sección para obtener más información acerca de las propiedades que puede usar con polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="280bd-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="280bd-262">Copias directas con PolyBase</span><span class="sxs-lookup"><span data-stu-id="280bd-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="280bd-263">PolyBase de SQL Data Warehouse admite directamente Azure Blob y Azure Data Lake Store (con la entidad de servicio) como origen y con los requisitos de formato de archivo específico.</span><span class="sxs-lookup"><span data-stu-id="280bd-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="280bd-264">Si los datos de origen cumplen los criterios de hello descritos en esta sección, puede copiar directamente de tooAzure de almacén de datos de origen que del almacenamiento de datos SQL con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="280bd-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="280bd-265">De lo contrario, puede usar [Copias almacenadas provisionalmente con PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="280bd-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="280bd-266">datos de toocopy de almacenamiento de datos del almacén de Data Lake tooSQL eficazmente, obtener más información en [Data Factory de Azure hace incluso más fácil y cómodo toouncover visión de datos cuando se usa el almacén de Data Lake con almacenamiento de datos de SQL](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="280bd-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="280bd-267">Si no se cumplen los requisitos de hello, Data Factory de Azure comprueba la configuración de Hola y vuelve automáticamente mecanismo BULKINSERT toohello Hola para movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="280bd-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="280bd-268">El **servicio de origen vinculado** es de tipo **AzureStorage** o **AzureDataLakeStore con autenticación de la entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="280bd-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="280bd-269">Hola **conjunto de datos de entrada** es de tipo: **AzureBlob** o **AzureDataLakeStore**, y Hola tipo de formato en `type` propiedades es **OrcFormat** , o **TextFormat** con hello siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="280bd-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="280bd-270">`rowDelimiter` debe ser **\n**.</span><span class="sxs-lookup"><span data-stu-id="280bd-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="280bd-271">`nullValue`se establece demasiado**una cadena vacía** (""), o `treatEmptyAsNull` se establece demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="280bd-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="280bd-272">`encodingName`se establece demasiado**utf-8**, que es **predeterminado** valor.</span><span class="sxs-lookup"><span data-stu-id="280bd-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="280bd-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` y `skipLineCount` no se especifican.</span><span class="sxs-lookup"><span data-stu-id="280bd-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="280bd-274">`compression` puede ser **no compression**, **GZip** o **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="280bd-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="280bd-275">No hay ningún `skipHeaderLineCount` en **BlobSource** o **AzureDataLakeStore** para la actividad de copia de canalización de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="280bd-276">No hay ningún `sliceIdentifierColumnName` en **SqlDWSink** para la actividad de copia de canalización de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="280bd-277">(PolyBase garantiza que todos los datos se actualizan o que no se actualiza ninguno en una única ejecución.</span><span class="sxs-lookup"><span data-stu-id="280bd-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="280bd-278">tooachieve **repetibilidad**, podría utilizar `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="280bd-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="280bd-279">No hay ningún `columnMapping` que se usan en hello asociado en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="280bd-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="280bd-280">Copias almacenadas provisionalmente con PolyBase</span><span class="sxs-lookup"><span data-stu-id="280bd-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="280bd-281">Cuando los datos de origen no cumplen los criterios de hello introducidos en la sección anterior de hello, puede habilitar la copia de datos a través de un almacenamiento de blobs de Azure ensayo provisional (no puede ser almacenamiento Premium).</span><span class="sxs-lookup"><span data-stu-id="280bd-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="280bd-282">En este caso, Data Factory de Azure automáticamente realiza transformaciones en hello toomeet datos formato requisitos de datos de PolyBase y, a continuación, use datos de PolyBase tooload en almacenamiento de datos de SQL y en la última limpieza los datos temporales Hola del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="280bd-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="280bd-283">Consulte [Copias almacenadas provisionalmente](data-factory-copy-activity-performance.md#staged-copy) para más información sobre cómo funciona en general la copia de datos por medio de un blob de Azure de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="280bd-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="280bd-284">Cuando se copian datos desde un dato local almacenan en almacenamiento de datos de SQL Azure con PolyBase y el almacenamiento provisional, si la versión de Data Management Gateway está por debajo de 2.4, JRE (Java Runtime Environment) es necesario en la puerta de enlace automático que es tootransform usa los datos de origen en el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="280bd-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="280bd-285">Sugerir que actualizar su tooavoid más reciente de puerta de enlace toohello esta dependencia.</span><span class="sxs-lookup"><span data-stu-id="280bd-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="280bd-286">toouse esta característica, cree un [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) que hace referencia toohello cuenta de almacenamiento de Azure que tiene el almacenamiento de blobs provisionales de hello, a continuación, especifique hello `enableStaging` y `stagingSettings` propiedades de actividad de copia de Hola como se muestra en el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="280bd-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="280bd-287">Procedimientos recomendados al usar PolyBase</span><span class="sxs-lookup"><span data-stu-id="280bd-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="280bd-288">Hello las secciones siguientes proporcionan toohello de prácticas recomendada adicionales que se mencionan en [prácticas recomendadas para el almacenamiento de datos de SQL Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="280bd-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="280bd-289">Permiso de base de datos necesario</span><span class="sxs-lookup"><span data-stu-id="280bd-289">Required database permission</span></span>
<span data-ttu-id="280bd-290">toouse PolyBase, requiere Hola usuario está tooload usa datos en almacenamiento de datos de SQL se Hola [permiso "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) en base de datos de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="280bd-291">Una manera de tooachieve que es tooadd ese usuario como miembro del rol "db_owner".</span><span class="sxs-lookup"><span data-stu-id="280bd-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="280bd-292">Obtenga información acerca de cómo toodo que siguiendo [en esta sección](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="280bd-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="280bd-293">Limitación del tipo de datos y del tamaño de fila</span><span class="sxs-lookup"><span data-stu-id="280bd-293">Row size and data type limitation</span></span>
<span data-ttu-id="280bd-294">Cargas de Polybase se limitan tooloading ambas filas inferior **1 MB** y no se puede cargar tooVARCHR(MAX), nvarchar (max) o varbinary (max).</span><span class="sxs-lookup"><span data-stu-id="280bd-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="280bd-295">Consulte demasiado[aquí](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="280bd-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="280bd-296">Si tiene datos de origen con filas de un tamaño superior a 1 MB, puede que desee tablas de origen de hello toosplit verticalmente en varios pequeños donde mayor tamaño de fila Hola de cada uno de ellos no supere el límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="280bd-297">a continuación, se pueden cargar tablas más pequeñas de Hello mediante PolyBase y combinar juntos en el almacén de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="280bd-298">Clase de recursos de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="280bd-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="280bd-299">tooachieve mejor rendimiento posible, considere la posibilidad de tooassign mayores recursos clase toohello usuario que se va a usar datos tooload en almacenamiento de datos de SQL a través de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="280bd-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="280bd-300">Obtenga información acerca de cómo toodo que siguiendo [cambiar un ejemplo de clase del recurso de usuario](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="280bd-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="280bd-301">tableName en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="280bd-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="280bd-302">Hello tabla siguiente proporciona ejemplos sobre cómo hello toospecify **tableName** propiedad JSON de diversas combinaciones de nombre de esquema y tabla de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="280bd-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="280bd-303">Esquema de base de datos</span><span class="sxs-lookup"><span data-stu-id="280bd-303">DB Schema</span></span> | <span data-ttu-id="280bd-304">Nombre de tabla</span><span class="sxs-lookup"><span data-stu-id="280bd-304">Table name</span></span> | <span data-ttu-id="280bd-305">Propiedad JSON tableName</span><span class="sxs-lookup"><span data-stu-id="280bd-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="280bd-306">dbo</span><span class="sxs-lookup"><span data-stu-id="280bd-306">dbo</span></span> |<span data-ttu-id="280bd-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="280bd-307">MyTable</span></span> |<span data-ttu-id="280bd-308">MyTable o dbo.MyTable o [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="280bd-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="280bd-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="280bd-309">dbo1</span></span> |<span data-ttu-id="280bd-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="280bd-310">MyTable</span></span> |<span data-ttu-id="280bd-311">dbo1.MyTable o [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="280bd-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="280bd-312">dbo</span><span class="sxs-lookup"><span data-stu-id="280bd-312">dbo</span></span> |<span data-ttu-id="280bd-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="280bd-313">My.Table</span></span> |<span data-ttu-id="280bd-314">[My.Table] o [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="280bd-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="280bd-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="280bd-315">dbo1</span></span> |<span data-ttu-id="280bd-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="280bd-316">My.Table</span></span> |<span data-ttu-id="280bd-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="280bd-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="280bd-318">Si ve Hola tras error, es posible que un problema con el valor de Hola que especificó para la propiedad tableName de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="280bd-319">Consulte tabla Hola Hola forma correcta toospecify valores de propiedad JSON de hello tableName.</span><span class="sxs-lookup"><span data-stu-id="280bd-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="280bd-320">Columnas con valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="280bd-320">Columns with default values</span></span>
<span data-ttu-id="280bd-321">Actualmente, solo acepta la característica de factoría de datos de PolyBase Hola mismo número de columnas como en la tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="280bd-322">Supongamos que tiene una tabla con cuatro columnas y una de ellas está definida con un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="280bd-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="280bd-323">datos de entrada de Hello todavía deben contener cuatro columnas.</span><span class="sxs-lookup"><span data-stu-id="280bd-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="280bd-324">Proporciona un conjunto de datos de entrada de 3 columnas produciría un toohello de error similar siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="280bd-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="280bd-325">El valor NULL es una forma especial de valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="280bd-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="280bd-326">Si la columna hello es que aceptan valores NULL, Hola entrada datos (blob) para esa columna pudieron estar vacías (no puede faltar de conjunto de datos de entrada de hello).</span><span class="sxs-lookup"><span data-stu-id="280bd-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="280bd-327">PolyBase, inserta NULL para ellos en hello almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="280bd-328">Creación automáticamente de tablas</span><span class="sxs-lookup"><span data-stu-id="280bd-328">Auto table creation</span></span>
<span data-ttu-id="280bd-329">Si va a usar Asistente para copiar toocopy datos de SQL Server o base de datos de SQL Azure tooAzure hello y almacenamiento de datos SQL tabla correspondiente de la tabla de origen toohello no existen en el almacén de destino de hello, factoría de datos puede crear automáticamente la tabla de Hola Hola almacenamiento de datos mediante el uso de esquema de tabla de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="280bd-330">Factoría de datos crea la tabla de hello en el almacén de destino de hello con hello mismo nombre de la tabla en el almacén de datos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="280bd-331">tipos de datos de Hola para las columnas se eligen en función del Hola después de la asignación de tipos.</span><span class="sxs-lookup"><span data-stu-id="280bd-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="280bd-332">Si es necesario, realiza toofix de conversiones de tipo las incompatibilidades entre los almacenes de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="280bd-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="280bd-333">También se utiliza la distribución Round Robin.</span><span class="sxs-lookup"><span data-stu-id="280bd-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="280bd-334">Tipo de columna de SQL Database de origen</span><span class="sxs-lookup"><span data-stu-id="280bd-334">Source SQL Database column type</span></span> | <span data-ttu-id="280bd-335">Tipo de columna de SQL DataWarehouse de destino (limitación de tamaño)</span><span class="sxs-lookup"><span data-stu-id="280bd-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="280bd-336">int</span><span class="sxs-lookup"><span data-stu-id="280bd-336">Int</span></span> | <span data-ttu-id="280bd-337">int</span><span class="sxs-lookup"><span data-stu-id="280bd-337">Int</span></span> |
| <span data-ttu-id="280bd-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="280bd-338">BigInt</span></span> | <span data-ttu-id="280bd-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="280bd-339">BigInt</span></span> |
| <span data-ttu-id="280bd-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="280bd-340">SmallInt</span></span> | <span data-ttu-id="280bd-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="280bd-341">SmallInt</span></span> |
| <span data-ttu-id="280bd-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="280bd-342">TinyInt</span></span> | <span data-ttu-id="280bd-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="280bd-343">TinyInt</span></span> |
| <span data-ttu-id="280bd-344">Bit</span><span class="sxs-lookup"><span data-stu-id="280bd-344">Bit</span></span> | <span data-ttu-id="280bd-345">Bit</span><span class="sxs-lookup"><span data-stu-id="280bd-345">Bit</span></span> |
| <span data-ttu-id="280bd-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-346">Decimal</span></span> | <span data-ttu-id="280bd-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-347">Decimal</span></span> |
| <span data-ttu-id="280bd-348">Numeric</span><span class="sxs-lookup"><span data-stu-id="280bd-348">Numeric</span></span> | <span data-ttu-id="280bd-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-349">Decimal</span></span> |
| <span data-ttu-id="280bd-350">Float</span><span class="sxs-lookup"><span data-stu-id="280bd-350">Float</span></span> | <span data-ttu-id="280bd-351">Float</span><span class="sxs-lookup"><span data-stu-id="280bd-351">Float</span></span> |
| <span data-ttu-id="280bd-352">Money</span><span class="sxs-lookup"><span data-stu-id="280bd-352">Money</span></span> | <span data-ttu-id="280bd-353">Money</span><span class="sxs-lookup"><span data-stu-id="280bd-353">Money</span></span> |
| <span data-ttu-id="280bd-354">Real</span><span class="sxs-lookup"><span data-stu-id="280bd-354">Real</span></span> | <span data-ttu-id="280bd-355">Real</span><span class="sxs-lookup"><span data-stu-id="280bd-355">Real</span></span> |
| <span data-ttu-id="280bd-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="280bd-356">SmallMoney</span></span> | <span data-ttu-id="280bd-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="280bd-357">SmallMoney</span></span> |
| <span data-ttu-id="280bd-358">Binary</span><span class="sxs-lookup"><span data-stu-id="280bd-358">Binary</span></span> | <span data-ttu-id="280bd-359">Binary</span><span class="sxs-lookup"><span data-stu-id="280bd-359">Binary</span></span> |
| <span data-ttu-id="280bd-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="280bd-360">Varbinary</span></span> | <span data-ttu-id="280bd-361">Varbinary (arriba too8000)</span><span class="sxs-lookup"><span data-stu-id="280bd-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="280bd-362">Date</span><span class="sxs-lookup"><span data-stu-id="280bd-362">Date</span></span> | <span data-ttu-id="280bd-363">Date</span><span class="sxs-lookup"><span data-stu-id="280bd-363">Date</span></span> |
| <span data-ttu-id="280bd-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-364">DateTime</span></span> | <span data-ttu-id="280bd-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-365">DateTime</span></span> |
| <span data-ttu-id="280bd-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="280bd-366">DateTime2</span></span> | <span data-ttu-id="280bd-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="280bd-367">DateTime2</span></span> |
| <span data-ttu-id="280bd-368">Hora</span><span class="sxs-lookup"><span data-stu-id="280bd-368">Time</span></span> | <span data-ttu-id="280bd-369">Hora</span><span class="sxs-lookup"><span data-stu-id="280bd-369">Time</span></span> |
| <span data-ttu-id="280bd-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="280bd-370">DateTimeOffset</span></span> | <span data-ttu-id="280bd-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="280bd-371">DateTimeOffset</span></span> |
| <span data-ttu-id="280bd-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-372">SmallDateTime</span></span> | <span data-ttu-id="280bd-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-373">SmallDateTime</span></span> |
| <span data-ttu-id="280bd-374">Texto</span><span class="sxs-lookup"><span data-stu-id="280bd-374">Text</span></span> | <span data-ttu-id="280bd-375">Varchar (arriba too8000)</span><span class="sxs-lookup"><span data-stu-id="280bd-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="280bd-376">NText</span><span class="sxs-lookup"><span data-stu-id="280bd-376">NText</span></span> | <span data-ttu-id="280bd-377">NVarChar (arriba too4000)</span><span class="sxs-lookup"><span data-stu-id="280bd-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="280bd-378">Imagen</span><span class="sxs-lookup"><span data-stu-id="280bd-378">Image</span></span> | <span data-ttu-id="280bd-379">VarBinary (arriba too8000)</span><span class="sxs-lookup"><span data-stu-id="280bd-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="280bd-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="280bd-380">UniqueIdentifier</span></span> | <span data-ttu-id="280bd-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="280bd-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="280bd-382">Char</span><span class="sxs-lookup"><span data-stu-id="280bd-382">Char</span></span> | <span data-ttu-id="280bd-383">Char</span><span class="sxs-lookup"><span data-stu-id="280bd-383">Char</span></span> |
| <span data-ttu-id="280bd-384">NChar</span><span class="sxs-lookup"><span data-stu-id="280bd-384">NChar</span></span> | <span data-ttu-id="280bd-385">NChar</span><span class="sxs-lookup"><span data-stu-id="280bd-385">NChar</span></span> |
| <span data-ttu-id="280bd-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="280bd-386">VarChar</span></span> | <span data-ttu-id="280bd-387">VarChar (arriba too8000)</span><span class="sxs-lookup"><span data-stu-id="280bd-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="280bd-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="280bd-388">NVarChar</span></span> | <span data-ttu-id="280bd-389">NVarChar (arriba too4000)</span><span class="sxs-lookup"><span data-stu-id="280bd-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="280bd-390">xml</span><span class="sxs-lookup"><span data-stu-id="280bd-390">Xml</span></span> | <span data-ttu-id="280bd-391">Varchar (arriba too8000)</span><span class="sxs-lookup"><span data-stu-id="280bd-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="280bd-392">Asignación de tipos para Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="280bd-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="280bd-393">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="280bd-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="280bd-394">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="280bd-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="280bd-395">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="280bd-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="280bd-396">Cuando se mueven datos demasiado & de almacenamiento de datos de SQL Azure, hello asignaciones siguientes se usan del tipo de too.NET de tipo SQL y viceversa.</span><span class="sxs-lookup"><span data-stu-id="280bd-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="280bd-397">asignación de Hello es el mismo que hello [asignación de tipo de datos de SQL Server para ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="280bd-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="280bd-398">Tipo de motor de base de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="280bd-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="280bd-399">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="280bd-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="280bd-400">bigint</span><span class="sxs-lookup"><span data-stu-id="280bd-400">bigint</span></span> |<span data-ttu-id="280bd-401">Int64</span><span class="sxs-lookup"><span data-stu-id="280bd-401">Int64</span></span> |
| <span data-ttu-id="280bd-402">binary</span><span class="sxs-lookup"><span data-stu-id="280bd-402">binary</span></span> |<span data-ttu-id="280bd-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="280bd-403">Byte[]</span></span> |
| <span data-ttu-id="280bd-404">bit</span><span class="sxs-lookup"><span data-stu-id="280bd-404">bit</span></span> |<span data-ttu-id="280bd-405">Booleano</span><span class="sxs-lookup"><span data-stu-id="280bd-405">Boolean</span></span> |
| <span data-ttu-id="280bd-406">char</span><span class="sxs-lookup"><span data-stu-id="280bd-406">char</span></span> |<span data-ttu-id="280bd-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="280bd-407">String, Char[]</span></span> |
| <span data-ttu-id="280bd-408">fecha</span><span class="sxs-lookup"><span data-stu-id="280bd-408">date</span></span> |<span data-ttu-id="280bd-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-409">DateTime</span></span> |
| <span data-ttu-id="280bd-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-410">Datetime</span></span> |<span data-ttu-id="280bd-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-411">DateTime</span></span> |
| <span data-ttu-id="280bd-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="280bd-412">datetime2</span></span> |<span data-ttu-id="280bd-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-413">DateTime</span></span> |
| <span data-ttu-id="280bd-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="280bd-414">Datetimeoffset</span></span> |<span data-ttu-id="280bd-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="280bd-415">DateTimeOffset</span></span> |
| <span data-ttu-id="280bd-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-416">Decimal</span></span> |<span data-ttu-id="280bd-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-417">Decimal</span></span> |
| <span data-ttu-id="280bd-418">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="280bd-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="280bd-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="280bd-419">Byte[]</span></span> |
| <span data-ttu-id="280bd-420">Float</span><span class="sxs-lookup"><span data-stu-id="280bd-420">Float</span></span> |<span data-ttu-id="280bd-421">Doble</span><span class="sxs-lookup"><span data-stu-id="280bd-421">Double</span></span> |
| <span data-ttu-id="280bd-422">imagen</span><span class="sxs-lookup"><span data-stu-id="280bd-422">image</span></span> |<span data-ttu-id="280bd-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="280bd-423">Byte[]</span></span> |
| <span data-ttu-id="280bd-424">int</span><span class="sxs-lookup"><span data-stu-id="280bd-424">int</span></span> |<span data-ttu-id="280bd-425">Int32</span><span class="sxs-lookup"><span data-stu-id="280bd-425">Int32</span></span> |
| <span data-ttu-id="280bd-426">money</span><span class="sxs-lookup"><span data-stu-id="280bd-426">money</span></span> |<span data-ttu-id="280bd-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-427">Decimal</span></span> |
| <span data-ttu-id="280bd-428">nchar</span><span class="sxs-lookup"><span data-stu-id="280bd-428">nchar</span></span> |<span data-ttu-id="280bd-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="280bd-429">String, Char[]</span></span> |
| <span data-ttu-id="280bd-430">ntext</span><span class="sxs-lookup"><span data-stu-id="280bd-430">ntext</span></span> |<span data-ttu-id="280bd-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="280bd-431">String, Char[]</span></span> |
| <span data-ttu-id="280bd-432">numeric</span><span class="sxs-lookup"><span data-stu-id="280bd-432">numeric</span></span> |<span data-ttu-id="280bd-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-433">Decimal</span></span> |
| <span data-ttu-id="280bd-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="280bd-434">nvarchar</span></span> |<span data-ttu-id="280bd-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="280bd-435">String, Char[]</span></span> |
| <span data-ttu-id="280bd-436">real</span><span class="sxs-lookup"><span data-stu-id="280bd-436">real</span></span> |<span data-ttu-id="280bd-437">Single</span><span class="sxs-lookup"><span data-stu-id="280bd-437">Single</span></span> |
| <span data-ttu-id="280bd-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="280bd-438">rowversion</span></span> |<span data-ttu-id="280bd-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="280bd-439">Byte[]</span></span> |
| <span data-ttu-id="280bd-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="280bd-440">smalldatetime</span></span> |<span data-ttu-id="280bd-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="280bd-441">DateTime</span></span> |
| <span data-ttu-id="280bd-442">smallint</span><span class="sxs-lookup"><span data-stu-id="280bd-442">smallint</span></span> |<span data-ttu-id="280bd-443">Int16</span><span class="sxs-lookup"><span data-stu-id="280bd-443">Int16</span></span> |
| <span data-ttu-id="280bd-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="280bd-444">smallmoney</span></span> |<span data-ttu-id="280bd-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="280bd-445">Decimal</span></span> |
| <span data-ttu-id="280bd-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="280bd-446">sql_variant</span></span> |<span data-ttu-id="280bd-447">Object *</span><span class="sxs-lookup"><span data-stu-id="280bd-447">Object *</span></span> |
| <span data-ttu-id="280bd-448">text</span><span class="sxs-lookup"><span data-stu-id="280bd-448">text</span></span> |<span data-ttu-id="280bd-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="280bd-449">String, Char[]</span></span> |
| <span data-ttu-id="280bd-450">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="280bd-450">time</span></span> |<span data-ttu-id="280bd-451">timespan</span><span class="sxs-lookup"><span data-stu-id="280bd-451">TimeSpan</span></span> |
| <span data-ttu-id="280bd-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="280bd-452">timestamp</span></span> |<span data-ttu-id="280bd-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="280bd-453">Byte[]</span></span> |
| <span data-ttu-id="280bd-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="280bd-454">tinyint</span></span> |<span data-ttu-id="280bd-455">Byte</span><span class="sxs-lookup"><span data-stu-id="280bd-455">Byte</span></span> |
| <span data-ttu-id="280bd-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="280bd-456">uniqueidentifier</span></span> |<span data-ttu-id="280bd-457">Guid</span><span class="sxs-lookup"><span data-stu-id="280bd-457">Guid</span></span> |
| <span data-ttu-id="280bd-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="280bd-458">varbinary</span></span> |<span data-ttu-id="280bd-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="280bd-459">Byte[]</span></span> |
| <span data-ttu-id="280bd-460">varchar</span><span class="sxs-lookup"><span data-stu-id="280bd-460">varchar</span></span> |<span data-ttu-id="280bd-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="280bd-461">String, Char[]</span></span> |
| <span data-ttu-id="280bd-462">xml</span><span class="sxs-lookup"><span data-stu-id="280bd-462">xml</span></span> |<span data-ttu-id="280bd-463">xml</span><span class="sxs-lookup"><span data-stu-id="280bd-463">Xml</span></span> |

<span data-ttu-id="280bd-464">También puede asignar columnas de toocolumns de conjunto de datos de origen del conjunto de datos de receptor en la definición de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="280bd-465">Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="280bd-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="280bd-466">Ejemplos JSON para copiar datos tooand de almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="280bd-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="280bd-467">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="280bd-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="280bd-468">Muestran cómo toocopy tooand de datos de almacenamiento de datos de SQL Azure y almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="280bd-469">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="280bd-470">Ejemplo: Copiar los datos de Blob del almacenamiento de datos de SQL Azure tooAzure</span><span class="sxs-lookup"><span data-stu-id="280bd-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="280bd-471">ejemplo de Hola define Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="280bd-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="280bd-472">Un servicio vinculado de tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="280bd-473">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="280bd-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="280bd-474">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="280bd-475">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="280bd-476">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlDWSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="280bd-477">ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de una tabla de blob de tooa de base de datos de almacenamiento de datos de SQL Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="280bd-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="280bd-478">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="280bd-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="280bd-479">**Servicio vinculado del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="280bd-480">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="280bd-481">**Conjunto de datos de entrada del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="280bd-482">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en el almacén de datos de SQL Azure y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="280bd-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="280bd-483">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="280bd-484">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="280bd-485">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="280bd-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="280bd-486">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="280bd-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="280bd-487">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="280bd-488">**Actividad de copia en una canalización con SqlDWSource y BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="280bd-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="280bd-489">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="280bd-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="280bd-490">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlDWSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="280bd-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="280bd-491">consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="280bd-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="280bd-492">En el ejemplo de Hola, **sqlReaderQuery** se especifica para hello SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="280bd-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="280bd-493">Hola actividad de copia ejecuta esta consulta contra Hola datos de almacenamiento de datos de SQL Azure origen tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="280bd-494">Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="280bd-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="280bd-495">Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, columnas de hello definidas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usa una consulta (select column1, column2 de mytable) toorun contra Hola almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="280bd-496">Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="280bd-497">Ejemplo: Copiar los datos de Blob de Azure tooAzure almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="280bd-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="280bd-498">ejemplo de Hola define Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="280bd-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="280bd-499">Un servicio vinculado de tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="280bd-500">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="280bd-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="280bd-501">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="280bd-502">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="280bd-503">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="280bd-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="280bd-504">ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de tabla de tooa de blobs de Azure en la base de datos de almacenamiento de datos de SQL Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="280bd-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="280bd-505">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="280bd-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="280bd-506">**Servicio vinculado del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="280bd-507">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="280bd-508">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="280bd-509">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="280bd-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="280bd-510">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="280bd-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="280bd-511">ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="280bd-512">"externo": "true" configuración informa a servicio de factoría de datos de Hola que esta tabla es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="280bd-513">**Conjunto de datos de salida del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="280bd-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="280bd-514">ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en el almacén de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="280bd-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="280bd-515">Crear tabla de hello en el almacén de datos de SQL Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="280bd-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="280bd-516">Se agregan nuevas filas toohello tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="280bd-516">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="280bd-517">**Actividad de copia en una canalización con BlobSource y SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="280bd-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="280bd-518">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="280bd-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="280bd-519">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="280bd-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="280bd-520">Para obtener un tutorial, vea hello [cargar 1 TB en almacenamiento de datos de SQL Azure en 15 minutos con Data Factory de Azure](data-factory-load-sql-data-warehouse.md) y [carga los datos con Data Factory de Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artículo Hola almacenamiento de datos de SQL Azure documentación.</span><span class="sxs-lookup"><span data-stu-id="280bd-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="280bd-521">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="280bd-521">Performance and Tuning</span></span>
<span data-ttu-id="280bd-522">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="280bd-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
