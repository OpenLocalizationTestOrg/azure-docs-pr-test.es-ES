---
title: "Copia de datos hacia Azure SQL Data Warehouse y desde él | Microsoft Docs"
description: Aprenda a copiar datos hacia y desde Azure SQL Data Warehouse mediante Azure Data Factory
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
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="d4306-103">Copia de datos hacia y desde SQL Data Warehouse mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d4306-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="d4306-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos con Azure SQL Data Warehouse como origen o destino.</span><span class="sxs-lookup"><span data-stu-id="d4306-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4306-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d4306-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="d4306-106">Para obtener el mejor rendimiento posible, use PolyBase para cargar datos en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4306-107">Consulte [Movimiento de datos hacia y desde Almacenamiento de datos SQL de Azure mediante Factoría de datos de Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d4306-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="d4306-108">Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="d4306-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d4306-109">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="d4306-109">Supported scenarios</span></span>
<span data-ttu-id="d4306-110">Puede copiar datos **de Azure SQL Data Warehouse** a los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="d4306-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d4306-111">Puede copiar datos de los siguientes almacenes de datos **a Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="d4306-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="d4306-112">Al copiar datos desde SQL Server o Azure SQL Database en Azure SQL Data Warehouse, si la tabla no se encuentra en el almacén de destino, Data Factory puede crear la tabla automáticamente en SQL Data Warehouse mediante el esquema de la tabla en el almacén de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="d4306-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="d4306-113">Vea [Creación automática de tablas](#auto-table-creation) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d4306-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="d4306-114">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="d4306-114">Supported authentication type</span></span>
<span data-ttu-id="d4306-115">El conector de Azure SQL Data Warehouse admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="d4306-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d4306-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="d4306-116">Getting started</span></span>
<span data-ttu-id="d4306-117">Puede crear una canalización con una actividad de copia que mueva datos con Azure SQL Data Warehouse como origen o destino mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="d4306-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="d4306-118">La manera más sencilla de crear una canalización que copie datos hacia y desde Almacenamiento de datos SQL es usar el Asistente para copia de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="d4306-119">Vea [Tutorial: cargar datos en almacenamiento de datos de SQL con factoría de datos](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) para una rápida visita guiada sobre la creación de una canalización mediante el Asistente para copia de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d4306-120">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="d4306-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d4306-121">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d4306-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="d4306-122">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="d4306-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="d4306-123">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="d4306-123">Create a **data factory**.</span></span> <span data-ttu-id="d4306-124">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="d4306-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d4306-125">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="d4306-126">Por ejemplo, si va a copiar datos desde una instancia de Azure Blob Storage hacia una instancia de Azure SQL Data Warehouse, creará dos servicios vinculados para vincular la cuenta de Azure Storage y la instancia de Azure SQL Data Warehouse a su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="d4306-127">Para información sobre las propiedades de los servicios vinculados que son específicas de Azure SQL Data Warehouse, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="d4306-128">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="d4306-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="d4306-129">En el ejemplo mencionado en el último paso, se crea un conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="d4306-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="d4306-130">Además, se crea otro conjunto de datos para especificar la tabla SQL en la instancia de Azure SQL Data Warehouse que contiene los datos copiados del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d4306-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="d4306-131">Para información sobre las propiedades del conjunto de datos que son específicas de Azure SQL Data Warehouse, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="d4306-132">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="d4306-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d4306-133">En el ejemplo que se ha mencionado anteriormente, se usa BlobSource como origen y SqlSink como receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d4306-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="d4306-134">De igual forma, si va a copiar desde Azure SQL Data Warehouse hacia Azure Blob Storage, usará SqlSource y BlobSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d4306-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="d4306-135">Para información sobre las propiedades de actividad de copia que son específicas de Azure SQL Data Warehouse, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d4306-136">Para más información sobre cómo usar un almacén de datos como origen o receptor, haga clic en el vínculo de la sección anterior para su almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="d4306-137">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="d4306-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d4306-138">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d4306-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d4306-139">Si desea obtener ejemplos con definiciones de JSON para entidades de Data Factory que se utilizan con el fin de copiar datos con Azure SQL Data Warehouse como origen o destino, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d4306-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="d4306-140">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="d4306-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d4306-141">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="d4306-141">Linked service properties</span></span>
<span data-ttu-id="d4306-142">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado del almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4306-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="d4306-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d4306-143">Property</span></span> | <span data-ttu-id="d4306-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4306-144">Description</span></span> | <span data-ttu-id="d4306-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d4306-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4306-146">type</span><span class="sxs-lookup"><span data-stu-id="d4306-146">type</span></span> |<span data-ttu-id="d4306-147">La propiedad type debe establecerse en: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="d4306-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="d4306-148">Sí</span><span class="sxs-lookup"><span data-stu-id="d4306-148">Yes</span></span> |
| <span data-ttu-id="d4306-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="d4306-149">connectionString</span></span> |<span data-ttu-id="d4306-150">Especifique la información necesaria para conectarse a la instancia de Almacenamiento de datos SQL de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="d4306-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="d4306-151">Solo se admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="d4306-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="d4306-152">Sí</span><span class="sxs-lookup"><span data-stu-id="d4306-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d4306-153">Configure el [firewall de Azure SQL Database](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) y el servidor de bases de datos para [permitir que los servicios de Azure tengan acceso al servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="d4306-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="d4306-154">Además, si va a copiar datos a Azure SQL Data Warehouse desde fuera de Azure, incluidos orígenes de datos locales con puerta de enlace de la factoría de datos, debe configurar el intervalo de direcciones IP adecuado para el equipo que envía datos a Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="d4306-155">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="d4306-155">Dataset properties</span></span>
<span data-ttu-id="d4306-156">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d4306-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d4306-157">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="d4306-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d4306-158">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d4306-159">La sección **typeProperties** del conjunto de datos de tipo **AzureSqlDWTable** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="d4306-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="d4306-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d4306-160">Property</span></span> | <span data-ttu-id="d4306-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4306-161">Description</span></span> | <span data-ttu-id="d4306-162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d4306-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4306-163">tableName</span><span class="sxs-lookup"><span data-stu-id="d4306-163">tableName</span></span> |<span data-ttu-id="d4306-164">Nombre de la tabla o vista en la base de datos de Azure SQL Data Warehouse a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="d4306-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="d4306-165">Sí</span><span class="sxs-lookup"><span data-stu-id="d4306-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d4306-166">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="d4306-166">Copy activity properties</span></span>
<span data-ttu-id="d4306-167">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d4306-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d4306-168">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="d4306-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="d4306-169">La actividad de copia toma solo una entrada y genera una única salida.</span><span class="sxs-lookup"><span data-stu-id="d4306-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="d4306-170">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="d4306-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="d4306-171">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="d4306-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="d4306-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="d4306-172">SqlDWSource</span></span>
<span data-ttu-id="d4306-173">Si el origen es de tipo **SqlDWSource**, estarán disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="d4306-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="d4306-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d4306-174">Property</span></span> | <span data-ttu-id="d4306-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4306-175">Description</span></span> | <span data-ttu-id="d4306-176">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="d4306-176">Allowed values</span></span> | <span data-ttu-id="d4306-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d4306-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4306-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d4306-178">sqlReaderQuery</span></span> |<span data-ttu-id="d4306-179">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-179">Use the custom query to read data.</span></span> |<span data-ttu-id="d4306-180">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="d4306-180">SQL query string.</span></span> <span data-ttu-id="d4306-181">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="d4306-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="d4306-182">No</span><span class="sxs-lookup"><span data-stu-id="d4306-182">No</span></span> |
| <span data-ttu-id="d4306-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d4306-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d4306-184">Nombre del procedimiento almacenado que lee datos de la tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="d4306-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="d4306-185">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="d4306-185">Name of the stored procedure.</span></span> <span data-ttu-id="d4306-186">La última instrucción SQL debe ser una instrucción SELECT del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="d4306-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="d4306-187">No</span><span class="sxs-lookup"><span data-stu-id="d4306-187">No</span></span> |
| <span data-ttu-id="d4306-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d4306-188">storedProcedureParameters</span></span> |<span data-ttu-id="d4306-189">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="d4306-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="d4306-190">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="d4306-190">Name/value pairs.</span></span> <span data-ttu-id="d4306-191">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="d4306-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="d4306-192">No</span><span class="sxs-lookup"><span data-stu-id="d4306-192">No</span></span> |

<span data-ttu-id="d4306-193">Si se especifica **sqlReaderQuery** para SqlDWSource, la actividad de copia ejecuta la consulta en el origen de Almacenamiento de datos SQL de Azure para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="d4306-194">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="d4306-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="d4306-195">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura del conjunto de datos JSON se usan para crear una consulta y ejecutarla en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4306-196">Ejemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="d4306-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="d4306-197">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="d4306-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="d4306-198">Ejemplo de SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="d4306-198">SqlDWSource example</span></span>

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
<span data-ttu-id="d4306-199">**Definición del procedimiento almacenado:**</span><span class="sxs-lookup"><span data-stu-id="d4306-199">**The stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="d4306-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="d4306-200">SqlDWSink</span></span>
<span data-ttu-id="d4306-201">**SqlDWSink** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="d4306-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="d4306-202">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d4306-202">Property</span></span> | <span data-ttu-id="d4306-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4306-203">Description</span></span> | <span data-ttu-id="d4306-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="d4306-204">Allowed values</span></span> | <span data-ttu-id="d4306-205">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d4306-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4306-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d4306-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d4306-207">Especifique una consulta para que se ejecute la actividad de copia de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="d4306-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="d4306-208">Consulte la [sección sobre repetibilidad](#repeatability-during-copy)para más información.</span><span class="sxs-lookup"><span data-stu-id="d4306-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="d4306-209">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="d4306-209">A query statement.</span></span> |<span data-ttu-id="d4306-210">No</span><span class="sxs-lookup"><span data-stu-id="d4306-210">No</span></span> |
| <span data-ttu-id="d4306-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="d4306-211">allowPolyBase</span></span> |<span data-ttu-id="d4306-212">Indica si se usa PolyBase (si procede) en lugar del mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="d4306-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="d4306-213">**El uso de PolyBase es el método recomendado para cargar datos en SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="d4306-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="d4306-214">Consulte [Uso de PolyBase para cargar datos en Almacenamiento de datos SQL](#use-polybase-to-load-data-into-azure-sql-data-warehouse) para ver restricciones y más información.</span><span class="sxs-lookup"><span data-stu-id="d4306-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="d4306-215">True </span><span class="sxs-lookup"><span data-stu-id="d4306-215">True</span></span> <br/><span data-ttu-id="d4306-216">False (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="d4306-216">False (default)</span></span> |<span data-ttu-id="d4306-217">No</span><span class="sxs-lookup"><span data-stu-id="d4306-217">No</span></span> |
| <span data-ttu-id="d4306-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="d4306-218">polyBaseSettings</span></span> |<span data-ttu-id="d4306-219">Un grupo de propiedades que se pueden especificar si el valor de la propiedad **allowPolybase** está establecido en **true**.</span><span class="sxs-lookup"><span data-stu-id="d4306-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="d4306-220">No</span><span class="sxs-lookup"><span data-stu-id="d4306-220">No</span></span> |
| <span data-ttu-id="d4306-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="d4306-221">rejectValue</span></span> |<span data-ttu-id="d4306-222">Especifica el número o porcentaje de filas que se pueden rechazar antes de que se produzca un error en la consulta.</span><span class="sxs-lookup"><span data-stu-id="d4306-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="d4306-223">Más información sobre las opciones de rechazo de PolyBase en la sección **Argumentos** del tema [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) [CREAR UNA TABLA EXTERNA (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="d4306-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="d4306-224">0 (predeterminado), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="d4306-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="d4306-225">No</span><span class="sxs-lookup"><span data-stu-id="d4306-225">No</span></span> |
| <span data-ttu-id="d4306-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="d4306-226">rejectType</span></span> |<span data-ttu-id="d4306-227">Especifica si se indica la opción rejectValue como un valor literal o un porcentaje.</span><span class="sxs-lookup"><span data-stu-id="d4306-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="d4306-228">Valor (predeterminado), Porcentaje</span><span class="sxs-lookup"><span data-stu-id="d4306-228">Value (default), Percentage</span></span> |<span data-ttu-id="d4306-229">No</span><span class="sxs-lookup"><span data-stu-id="d4306-229">No</span></span> |
| <span data-ttu-id="d4306-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="d4306-230">rejectSampleValue</span></span> |<span data-ttu-id="d4306-231">Determina el número de filas que se van a recuperar antes de que PolyBase vuelva a calcular el porcentaje de filas rechazadas.</span><span class="sxs-lookup"><span data-stu-id="d4306-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="d4306-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="d4306-232">1, 2, …</span></span> |<span data-ttu-id="d4306-233">Sí, si el valor de **rejectType** es **percentage**</span><span class="sxs-lookup"><span data-stu-id="d4306-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="d4306-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="d4306-234">useTypeDefault</span></span> |<span data-ttu-id="d4306-235">Especifica cómo administrar los valores que faltan en archivos de texto delimitados cuando PolyBase recupera datos del archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="d4306-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="d4306-236">Más información sobre esta propiedad en la sección de argumentos de [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4306-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="d4306-237">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="d4306-237">True, False (default)</span></span> |<span data-ttu-id="d4306-238">No</span><span class="sxs-lookup"><span data-stu-id="d4306-238">No</span></span> |
| <span data-ttu-id="d4306-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d4306-239">writeBatchSize</span></span> |<span data-ttu-id="d4306-240">Inserta datos en la tabla SQL cuando el tamaño del búfer alcance writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d4306-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="d4306-241">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="d4306-241">Integer (number of rows)</span></span> |<span data-ttu-id="d4306-242">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="d4306-242">No (default: 10000)</span></span> |
| <span data-ttu-id="d4306-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d4306-243">writeBatchTimeout</span></span> |<span data-ttu-id="d4306-244">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="d4306-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="d4306-245">timespan</span><span class="sxs-lookup"><span data-stu-id="d4306-245">timespan</span></span><br/><br/> <span data-ttu-id="d4306-246">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="d4306-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d4306-247">No</span><span class="sxs-lookup"><span data-stu-id="d4306-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="d4306-248">Ejemplo de SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="d4306-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="d4306-249">Movimiento de datos hacia y desde Almacenamiento de datos SQL de Azure mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="d4306-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4306-250">Usar **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** es una manera eficaz de cargar grandes cantidades de datos en Azure SQL Data Warehouse con un alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d4306-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="d4306-251">Puede ver una gran mejora en el rendimiento mediante el uso de PolyBase en lugar del mecanismo BULKINSERT predeterminado.</span><span class="sxs-lookup"><span data-stu-id="d4306-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="d4306-252">Vea la [copia del número de referencia de rendimiento](data-factory-copy-activity-performance.md#performance-reference) con una comparación detallada.</span><span class="sxs-lookup"><span data-stu-id="d4306-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="d4306-253">Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="d4306-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="d4306-254">Si los datos de origen están en **Azure Blob o Azure Data Lake Store**, y el formato es compatible con PolyBase, puede realizar las copias directamente desde Azure SQL Data Warehouse mediante PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d4306-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="d4306-255">Consulte **[Copias directas con PolyBase](#direct-copy-using-polybase)** para detalles.</span><span class="sxs-lookup"><span data-stu-id="d4306-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="d4306-256">Si el formato y el almacenamiento de datos de origen no es compatible originalmente con PolyBase, puede usar en su lugar la característica **[Copias almacenadas provisionalmente con PolyBase](#staged-copy-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="d4306-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="d4306-257">También proporciona un mejor rendimiento al convertir automáticamente los datos en formato compatible con PolyBase y almacenarlos en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d4306-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="d4306-258">Luego los carga en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="d4306-259">En la propiedad `allowPolyBase` elija **true**, como se muestra en el ejemplo siguiente de Azure Data Factory para usar PolyBase con el fin de copiar datos en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4306-260">Cuando se establece allowPolyBase en true, se puede especificar las propiedades específicas de PolyBase mediante el grupo de propiedades `polyBaseSettings`.</span><span class="sxs-lookup"><span data-stu-id="d4306-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="d4306-261">Consulte la sección [SqlDWSink](#SqlDWSink) para más información acerca de las propiedades que puede utilizar con polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="d4306-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="d4306-262">Copias directas con PolyBase</span><span class="sxs-lookup"><span data-stu-id="d4306-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="d4306-263">PolyBase de SQL Data Warehouse admite directamente Azure Blob y Azure Data Lake Store (con la entidad de servicio) como origen y con los requisitos de formato de archivo específico.</span><span class="sxs-lookup"><span data-stu-id="d4306-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="d4306-264">Si el origen de datos cumple los criterios descritos en esta sección, puede realizar las copias directamente desde el almacén de datos de origen a Azure SQL Data Warehouse mediante PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d4306-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="d4306-265">De lo contrario, puede usar [Copias almacenadas provisionalmente con PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="d4306-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="d4306-266">Para copiar datos desde Data Lake Store a SQL Data Warehouse de forma más eficiente, obtenga más información en [Azure Data Factory hace incluso más fácil y cómodo el descubrimiento de información de datos cuando se usa Data Lake Store con SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="d4306-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="d4306-267">Si no se cumplen los requisitos, Azure Data Factory comprobará la configuración y volverá automáticamente al mecanismo BULKINSERT para realizar el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="d4306-268">El **servicio de origen vinculado** es de tipo **AzureStorage** o **AzureDataLakeStore con autenticación de la entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="d4306-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="d4306-269">El **conjunto de datos de entrada** es del tipo **AzureBlob** o **AzureDataLakeStore**, y el tipo de formato de las propiedades `type` es **OrcFormat** o **TextFormat** con las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="d4306-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="d4306-270">`rowDelimiter` debe ser **\n**.</span><span class="sxs-lookup"><span data-stu-id="d4306-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="d4306-271">`nullValue` se establece en **una cadena vacía** ("") o `treatEmptyAsNull` se establece en **true**.</span><span class="sxs-lookup"><span data-stu-id="d4306-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="d4306-272">`encodingName` se establece en **utf-8**, que es el valor **predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="d4306-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="d4306-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` y `skipLineCount` no se especifican.</span><span class="sxs-lookup"><span data-stu-id="d4306-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="d4306-274">`compression` puede ser **no compression**, **GZip** o **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="d4306-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="d4306-275">No hay ningún valor `skipHeaderLineCount` en **BlobSource** o **AzureDataLakeStore** para la actividad de copia en la canalización.</span><span class="sxs-lookup"><span data-stu-id="d4306-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="d4306-276">No hay ningún valor `sliceIdentifierColumnName` en **SqlDWSink** para la actividad de copia en la canalización.</span><span class="sxs-lookup"><span data-stu-id="d4306-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="d4306-277">(PolyBase garantiza que todos los datos se actualizan o que no se actualiza ninguno en una única ejecución.</span><span class="sxs-lookup"><span data-stu-id="d4306-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="d4306-278">Para lograr la **capacidad de repetición**, se puede usar `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="d4306-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="d4306-279">No se usa `columnMapping` en la actividad de copia asociada.</span><span class="sxs-lookup"><span data-stu-id="d4306-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="d4306-280">Copias almacenadas provisionalmente con PolyBase</span><span class="sxs-lookup"><span data-stu-id="d4306-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="d4306-281">Si los datos de origen no cumplen los criterios especificados en la sección anterior, puede habilitar la copia de datos a través de un almacenamiento provisional de Azure Blob Storage (no puede ser Premium Storage).</span><span class="sxs-lookup"><span data-stu-id="d4306-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="d4306-282">En este caso, Azure Data Factory realiza transformaciones automáticamente en los datos para que cumplan con los requisitos de formato de datos de PolyBase, luego usa PolyBase para cargar datos en SQL Data Warehouse y, por último, borra los datos temporales de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d4306-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="d4306-283">Consulte [Copias almacenadas provisionalmente](data-factory-copy-activity-performance.md#staged-copy) para más información sobre cómo funciona en general la copia de datos por medio de un blob de Azure de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="d4306-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="d4306-284">Cuando copie datos de un almacén de datos local a Azure SQL Data Warehouse mediante PolyBase y almacenamiento provisional, si la versión de Data Management Gateway es inferior a 2.4, se necesita JRE (Java Runtime Environment) en la máquina de puerta de enlace que se usa para transformar los datos de origen en un formato correcto.</span><span class="sxs-lookup"><span data-stu-id="d4306-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="d4306-285">Se recomienda actualizar la puerta de enlace a la versión más reciente para evitar esta dependencia.</span><span class="sxs-lookup"><span data-stu-id="d4306-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="d4306-286">Para usar esta característica, cree un [servicio vinculado de Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) que haga referencia a la cuenta de Azure Storage que tenga el almacenamiento de blobs provisional y, después, especifique las propiedades `enableStaging` y `stagingSettings` de la actividad de copia como se muestra en el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d4306-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="d4306-287">Procedimientos recomendados al usar PolyBase</span><span class="sxs-lookup"><span data-stu-id="d4306-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="d4306-288">En las secciones siguientes se proporcionan procedimientos recomendados adicionales a los que se mencionan en [Procedimientos recomendados para Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="d4306-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="d4306-289">Permiso de base de datos necesario</span><span class="sxs-lookup"><span data-stu-id="d4306-289">Required database permission</span></span>
<span data-ttu-id="d4306-290">El uso de PolyBase requiere que el usuario que se usa para cargar datos en SQL Data Warehouse tenga [permiso "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) en la base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="d4306-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="d4306-291">Una manera de conseguirlo es agregar ese usuario como miembro del rol "db_owner".</span><span class="sxs-lookup"><span data-stu-id="d4306-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="d4306-292">Obtenga información sobre cómo hacerlo siguiendo [esta sección](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="d4306-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="d4306-293">Limitación del tipo de datos y del tamaño de fila</span><span class="sxs-lookup"><span data-stu-id="d4306-293">Row size and data type limitation</span></span>
<span data-ttu-id="d4306-294">Las cargas de PolyBase se limitan a la carga de filas más pequeñas que **1 MB** y no pueden cargar en VARCHR(MAX), NVARCHAR(MAX) ni VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="d4306-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="d4306-295">O haga clic [aquí](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="d4306-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="d4306-296">Si tiene datos de origen con filas mayores de 1 MB, puede dividir las tablas de origen verticalmente en varias más pequeñas, donde el tamaño de fila mayor de cada una de ellas no supere el límite.</span><span class="sxs-lookup"><span data-stu-id="d4306-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="d4306-297">Las tablas más pequeñas se pueden cargadas con PolyBase y se combinan en el Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4306-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="d4306-298">Clase de recursos de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d4306-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="d4306-299">Para obtener el mejor rendimiento posible, considere la posibilidad de asignar una clase SQL Data Warehouse a través de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d4306-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="d4306-300">Infórmese acerca de cómo hacerlo siguiendo las instrucciones en [Cambio de ejemplo de clase de recursos de usuario](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d4306-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="d4306-301">tableName en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="d4306-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4306-302">En la tabla siguiente se proporcionan ejemplos sobre cómo especificar la propiedad **tableName** en el conjunto de datos JSON para diversas combinaciones de nombre de tabla y esquema.</span><span class="sxs-lookup"><span data-stu-id="d4306-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="d4306-303">Esquema de base de datos</span><span class="sxs-lookup"><span data-stu-id="d4306-303">DB Schema</span></span> | <span data-ttu-id="d4306-304">Nombre de tabla</span><span class="sxs-lookup"><span data-stu-id="d4306-304">Table name</span></span> | <span data-ttu-id="d4306-305">Propiedad JSON tableName</span><span class="sxs-lookup"><span data-stu-id="d4306-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4306-306">dbo</span><span class="sxs-lookup"><span data-stu-id="d4306-306">dbo</span></span> |<span data-ttu-id="d4306-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="d4306-307">MyTable</span></span> |<span data-ttu-id="d4306-308">MyTable o dbo.MyTable o [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="d4306-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="d4306-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="d4306-309">dbo1</span></span> |<span data-ttu-id="d4306-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="d4306-310">MyTable</span></span> |<span data-ttu-id="d4306-311">dbo1.MyTable o [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="d4306-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="d4306-312">dbo</span><span class="sxs-lookup"><span data-stu-id="d4306-312">dbo</span></span> |<span data-ttu-id="d4306-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="d4306-313">My.Table</span></span> |<span data-ttu-id="d4306-314">[My.Table] o [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="d4306-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="d4306-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="d4306-315">dbo1</span></span> |<span data-ttu-id="d4306-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="d4306-316">My.Table</span></span> |<span data-ttu-id="d4306-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="d4306-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="d4306-318">Si ve el siguiente error, podría deberse a un problema con el valor especificado para la propiedad tableName.</span><span class="sxs-lookup"><span data-stu-id="d4306-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="d4306-319">Consulte en la tabla la forma correcta de especificar los valores para la propiedad tableName de JSON.</span><span class="sxs-lookup"><span data-stu-id="d4306-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="d4306-320">Columnas con valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="d4306-320">Columns with default values</span></span>
<span data-ttu-id="d4306-321">Actualmente, la característica PolyBase en Data Factory solo acepta el mismo número de columnas que la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="d4306-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="d4306-322">Supongamos que tiene una tabla con cuatro columnas y una de ellas está definida con un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="d4306-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="d4306-323">Los datos de entrada deberían seguir conteniendo cuatro columnas.</span><span class="sxs-lookup"><span data-stu-id="d4306-323">The input data should still contain four columns.</span></span> <span data-ttu-id="d4306-324">Si se proporciona un conjunto de datos de entrada de tres columnas, se producirá un error parecido al siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="d4306-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="d4306-325">El valor NULL es una forma especial de valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="d4306-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="d4306-326">Si la columna admite valores NULL, los datos de entrada (en el blob) para esa columna pueden estar vacíos (no pueden faltar en el conjunto de datos de entrada).</span><span class="sxs-lookup"><span data-stu-id="d4306-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="d4306-327">PolyBase insertará valores NULL para ellos en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="d4306-328">Creación automáticamente de tablas</span><span class="sxs-lookup"><span data-stu-id="d4306-328">Auto table creation</span></span>
<span data-ttu-id="d4306-329">Si usa el Asistente para copia para copiar datos desde SQL Server o Azure SQL Database en Azure SQL Data Warehouse y la tabla que corresponde a la tabla de origen no existe en el almacén de destino, Data Factory puede crear la tabla automáticamente en el almacenamiento de datos mediante el esquema de tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="d4306-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="d4306-330">Data Factory crea la tabla en el almacén de destino con el mismo nombre de tabla del almacén de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="d4306-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="d4306-331">Los tipos de datos de columnas se eligen en función de la siguiente asignación de tipo.</span><span class="sxs-lookup"><span data-stu-id="d4306-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="d4306-332">Si es necesario, realiza conversiones de tipos para corregir las incompatibilidades entre los almacenes de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="d4306-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="d4306-333">También se utiliza la distribución Round Robin.</span><span class="sxs-lookup"><span data-stu-id="d4306-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="d4306-334">Tipo de columna de SQL Database de origen</span><span class="sxs-lookup"><span data-stu-id="d4306-334">Source SQL Database column type</span></span> | <span data-ttu-id="d4306-335">Tipo de columna de SQL DataWarehouse de destino (limitación de tamaño)</span><span class="sxs-lookup"><span data-stu-id="d4306-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="d4306-336">int</span><span class="sxs-lookup"><span data-stu-id="d4306-336">Int</span></span> | <span data-ttu-id="d4306-337">int</span><span class="sxs-lookup"><span data-stu-id="d4306-337">Int</span></span> |
| <span data-ttu-id="d4306-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="d4306-338">BigInt</span></span> | <span data-ttu-id="d4306-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="d4306-339">BigInt</span></span> |
| <span data-ttu-id="d4306-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="d4306-340">SmallInt</span></span> | <span data-ttu-id="d4306-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="d4306-341">SmallInt</span></span> |
| <span data-ttu-id="d4306-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="d4306-342">TinyInt</span></span> | <span data-ttu-id="d4306-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="d4306-343">TinyInt</span></span> |
| <span data-ttu-id="d4306-344">Bit</span><span class="sxs-lookup"><span data-stu-id="d4306-344">Bit</span></span> | <span data-ttu-id="d4306-345">Bit</span><span class="sxs-lookup"><span data-stu-id="d4306-345">Bit</span></span> |
| <span data-ttu-id="d4306-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-346">Decimal</span></span> | <span data-ttu-id="d4306-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-347">Decimal</span></span> |
| <span data-ttu-id="d4306-348">Numeric</span><span class="sxs-lookup"><span data-stu-id="d4306-348">Numeric</span></span> | <span data-ttu-id="d4306-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-349">Decimal</span></span> |
| <span data-ttu-id="d4306-350">Float</span><span class="sxs-lookup"><span data-stu-id="d4306-350">Float</span></span> | <span data-ttu-id="d4306-351">Float</span><span class="sxs-lookup"><span data-stu-id="d4306-351">Float</span></span> |
| <span data-ttu-id="d4306-352">Money</span><span class="sxs-lookup"><span data-stu-id="d4306-352">Money</span></span> | <span data-ttu-id="d4306-353">Money</span><span class="sxs-lookup"><span data-stu-id="d4306-353">Money</span></span> |
| <span data-ttu-id="d4306-354">Real</span><span class="sxs-lookup"><span data-stu-id="d4306-354">Real</span></span> | <span data-ttu-id="d4306-355">Real</span><span class="sxs-lookup"><span data-stu-id="d4306-355">Real</span></span> |
| <span data-ttu-id="d4306-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="d4306-356">SmallMoney</span></span> | <span data-ttu-id="d4306-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="d4306-357">SmallMoney</span></span> |
| <span data-ttu-id="d4306-358">Binary</span><span class="sxs-lookup"><span data-stu-id="d4306-358">Binary</span></span> | <span data-ttu-id="d4306-359">Binary</span><span class="sxs-lookup"><span data-stu-id="d4306-359">Binary</span></span> |
| <span data-ttu-id="d4306-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="d4306-360">Varbinary</span></span> | <span data-ttu-id="d4306-361">Varbinary (hasta 8000)</span><span class="sxs-lookup"><span data-stu-id="d4306-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="d4306-362">Date</span><span class="sxs-lookup"><span data-stu-id="d4306-362">Date</span></span> | <span data-ttu-id="d4306-363">Date</span><span class="sxs-lookup"><span data-stu-id="d4306-363">Date</span></span> |
| <span data-ttu-id="d4306-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-364">DateTime</span></span> | <span data-ttu-id="d4306-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-365">DateTime</span></span> |
| <span data-ttu-id="d4306-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="d4306-366">DateTime2</span></span> | <span data-ttu-id="d4306-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="d4306-367">DateTime2</span></span> |
| <span data-ttu-id="d4306-368">Hora</span><span class="sxs-lookup"><span data-stu-id="d4306-368">Time</span></span> | <span data-ttu-id="d4306-369">Hora</span><span class="sxs-lookup"><span data-stu-id="d4306-369">Time</span></span> |
| <span data-ttu-id="d4306-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d4306-370">DateTimeOffset</span></span> | <span data-ttu-id="d4306-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d4306-371">DateTimeOffset</span></span> |
| <span data-ttu-id="d4306-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-372">SmallDateTime</span></span> | <span data-ttu-id="d4306-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-373">SmallDateTime</span></span> |
| <span data-ttu-id="d4306-374">Texto</span><span class="sxs-lookup"><span data-stu-id="d4306-374">Text</span></span> | <span data-ttu-id="d4306-375">Varchar (hasta 8000)</span><span class="sxs-lookup"><span data-stu-id="d4306-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="d4306-376">NText</span><span class="sxs-lookup"><span data-stu-id="d4306-376">NText</span></span> | <span data-ttu-id="d4306-377">NVarChar (hasta 4000)</span><span class="sxs-lookup"><span data-stu-id="d4306-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="d4306-378">Imagen</span><span class="sxs-lookup"><span data-stu-id="d4306-378">Image</span></span> | <span data-ttu-id="d4306-379">VarBinary (hasta 8000)</span><span class="sxs-lookup"><span data-stu-id="d4306-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="d4306-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="d4306-380">UniqueIdentifier</span></span> | <span data-ttu-id="d4306-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="d4306-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="d4306-382">Char</span><span class="sxs-lookup"><span data-stu-id="d4306-382">Char</span></span> | <span data-ttu-id="d4306-383">Char</span><span class="sxs-lookup"><span data-stu-id="d4306-383">Char</span></span> |
| <span data-ttu-id="d4306-384">NChar</span><span class="sxs-lookup"><span data-stu-id="d4306-384">NChar</span></span> | <span data-ttu-id="d4306-385">NChar</span><span class="sxs-lookup"><span data-stu-id="d4306-385">NChar</span></span> |
| <span data-ttu-id="d4306-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="d4306-386">VarChar</span></span> | <span data-ttu-id="d4306-387">VarChar (hasta 8000)</span><span class="sxs-lookup"><span data-stu-id="d4306-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="d4306-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="d4306-388">NVarChar</span></span> | <span data-ttu-id="d4306-389">NVarChar (hasta 4000)</span><span class="sxs-lookup"><span data-stu-id="d4306-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="d4306-390">Xml</span><span class="sxs-lookup"><span data-stu-id="d4306-390">Xml</span></span> | <span data-ttu-id="d4306-391">Varchar (hasta 8000)</span><span class="sxs-lookup"><span data-stu-id="d4306-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="d4306-392">Asignación de tipos para Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="d4306-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4306-393">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="d4306-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="d4306-394">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d4306-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d4306-395">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="d4306-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d4306-396">Al migrar datos a Azure SQL Data Warehouse y en sentido contrario, se usarán las siguientes asignaciones del tipo SQL al tipo .NET, y viceversa.</span><span class="sxs-lookup"><span data-stu-id="d4306-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="d4306-397">La asignación es igual que la asignación de [tipo de datos de SQL Server para ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4306-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="d4306-398">Tipo de motor de base de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4306-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="d4306-399">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d4306-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="d4306-400">bigint</span><span class="sxs-lookup"><span data-stu-id="d4306-400">bigint</span></span> |<span data-ttu-id="d4306-401">Int64</span><span class="sxs-lookup"><span data-stu-id="d4306-401">Int64</span></span> |
| <span data-ttu-id="d4306-402">binary</span><span class="sxs-lookup"><span data-stu-id="d4306-402">binary</span></span> |<span data-ttu-id="d4306-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4306-403">Byte[]</span></span> |
| <span data-ttu-id="d4306-404">bit</span><span class="sxs-lookup"><span data-stu-id="d4306-404">bit</span></span> |<span data-ttu-id="d4306-405">Booleano</span><span class="sxs-lookup"><span data-stu-id="d4306-405">Boolean</span></span> |
| <span data-ttu-id="d4306-406">char</span><span class="sxs-lookup"><span data-stu-id="d4306-406">char</span></span> |<span data-ttu-id="d4306-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4306-407">String, Char[]</span></span> |
| <span data-ttu-id="d4306-408">fecha</span><span class="sxs-lookup"><span data-stu-id="d4306-408">date</span></span> |<span data-ttu-id="d4306-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-409">DateTime</span></span> |
| <span data-ttu-id="d4306-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-410">Datetime</span></span> |<span data-ttu-id="d4306-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-411">DateTime</span></span> |
| <span data-ttu-id="d4306-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="d4306-412">datetime2</span></span> |<span data-ttu-id="d4306-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-413">DateTime</span></span> |
| <span data-ttu-id="d4306-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d4306-414">Datetimeoffset</span></span> |<span data-ttu-id="d4306-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d4306-415">DateTimeOffset</span></span> |
| <span data-ttu-id="d4306-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-416">Decimal</span></span> |<span data-ttu-id="d4306-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-417">Decimal</span></span> |
| <span data-ttu-id="d4306-418">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="d4306-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="d4306-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4306-419">Byte[]</span></span> |
| <span data-ttu-id="d4306-420">Float</span><span class="sxs-lookup"><span data-stu-id="d4306-420">Float</span></span> |<span data-ttu-id="d4306-421">Doble</span><span class="sxs-lookup"><span data-stu-id="d4306-421">Double</span></span> |
| <span data-ttu-id="d4306-422">imagen</span><span class="sxs-lookup"><span data-stu-id="d4306-422">image</span></span> |<span data-ttu-id="d4306-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4306-423">Byte[]</span></span> |
| <span data-ttu-id="d4306-424">int</span><span class="sxs-lookup"><span data-stu-id="d4306-424">int</span></span> |<span data-ttu-id="d4306-425">Int32</span><span class="sxs-lookup"><span data-stu-id="d4306-425">Int32</span></span> |
| <span data-ttu-id="d4306-426">money</span><span class="sxs-lookup"><span data-stu-id="d4306-426">money</span></span> |<span data-ttu-id="d4306-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-427">Decimal</span></span> |
| <span data-ttu-id="d4306-428">nchar</span><span class="sxs-lookup"><span data-stu-id="d4306-428">nchar</span></span> |<span data-ttu-id="d4306-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4306-429">String, Char[]</span></span> |
| <span data-ttu-id="d4306-430">ntext</span><span class="sxs-lookup"><span data-stu-id="d4306-430">ntext</span></span> |<span data-ttu-id="d4306-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4306-431">String, Char[]</span></span> |
| <span data-ttu-id="d4306-432">numeric</span><span class="sxs-lookup"><span data-stu-id="d4306-432">numeric</span></span> |<span data-ttu-id="d4306-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-433">Decimal</span></span> |
| <span data-ttu-id="d4306-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="d4306-434">nvarchar</span></span> |<span data-ttu-id="d4306-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4306-435">String, Char[]</span></span> |
| <span data-ttu-id="d4306-436">real</span><span class="sxs-lookup"><span data-stu-id="d4306-436">real</span></span> |<span data-ttu-id="d4306-437">Single</span><span class="sxs-lookup"><span data-stu-id="d4306-437">Single</span></span> |
| <span data-ttu-id="d4306-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="d4306-438">rowversion</span></span> |<span data-ttu-id="d4306-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4306-439">Byte[]</span></span> |
| <span data-ttu-id="d4306-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="d4306-440">smalldatetime</span></span> |<span data-ttu-id="d4306-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="d4306-441">DateTime</span></span> |
| <span data-ttu-id="d4306-442">smallint</span><span class="sxs-lookup"><span data-stu-id="d4306-442">smallint</span></span> |<span data-ttu-id="d4306-443">Int16</span><span class="sxs-lookup"><span data-stu-id="d4306-443">Int16</span></span> |
| <span data-ttu-id="d4306-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="d4306-444">smallmoney</span></span> |<span data-ttu-id="d4306-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="d4306-445">Decimal</span></span> |
| <span data-ttu-id="d4306-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="d4306-446">sql_variant</span></span> |<span data-ttu-id="d4306-447">Object *</span><span class="sxs-lookup"><span data-stu-id="d4306-447">Object *</span></span> |
| <span data-ttu-id="d4306-448">text</span><span class="sxs-lookup"><span data-stu-id="d4306-448">text</span></span> |<span data-ttu-id="d4306-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4306-449">String, Char[]</span></span> |
| <span data-ttu-id="d4306-450">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="d4306-450">time</span></span> |<span data-ttu-id="d4306-451">timespan</span><span class="sxs-lookup"><span data-stu-id="d4306-451">TimeSpan</span></span> |
| <span data-ttu-id="d4306-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="d4306-452">timestamp</span></span> |<span data-ttu-id="d4306-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4306-453">Byte[]</span></span> |
| <span data-ttu-id="d4306-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="d4306-454">tinyint</span></span> |<span data-ttu-id="d4306-455">Byte</span><span class="sxs-lookup"><span data-stu-id="d4306-455">Byte</span></span> |
| <span data-ttu-id="d4306-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="d4306-456">uniqueidentifier</span></span> |<span data-ttu-id="d4306-457">Guid</span><span class="sxs-lookup"><span data-stu-id="d4306-457">Guid</span></span> |
| <span data-ttu-id="d4306-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="d4306-458">varbinary</span></span> |<span data-ttu-id="d4306-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d4306-459">Byte[]</span></span> |
| <span data-ttu-id="d4306-460">varchar</span><span class="sxs-lookup"><span data-stu-id="d4306-460">varchar</span></span> |<span data-ttu-id="d4306-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d4306-461">String, Char[]</span></span> |
| <span data-ttu-id="d4306-462">xml</span><span class="sxs-lookup"><span data-stu-id="d4306-462">xml</span></span> |<span data-ttu-id="d4306-463">xml</span><span class="sxs-lookup"><span data-stu-id="d4306-463">Xml</span></span> |

<span data-ttu-id="d4306-464">También puede asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor en la definición de actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d4306-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="d4306-465">Para más información, consulte [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Asignación de columnas de conjunto de datos de Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="d4306-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="d4306-466">Ejemplos JSON para copiar datos hacia y desde SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d4306-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="d4306-467">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4306-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d4306-468">En ellos se muestra cómo copiar datos entre Almacenamiento de datos SQL y Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4306-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="d4306-469">Sin embargo, los datos se pueden copiar **directamente** de cualquiera de los orígenes a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4306-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="d4306-470">Ejemplo: Copia de datos de Azure SQL Data Warehouse a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="d4306-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="d4306-471">El ejemplo define las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="d4306-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="d4306-472">Un servicio vinculado de tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="d4306-473">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="d4306-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d4306-474">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d4306-475">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d4306-476">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlDWSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d4306-477">El ejemplo copia los datos que pertenecen a una serie temporal (por horas, días, etc.) desde una tabla de una base de datos de Azure SQL Data Warehouse a un blob cada hora.</span><span class="sxs-lookup"><span data-stu-id="d4306-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="d4306-478">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="d4306-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d4306-479">**Servicio vinculado del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="d4306-480">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d4306-481">**Conjunto de datos de entrada del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="d4306-482">El ejemplo supone que ha creado una tabla "MyTable" en el almacenamiento de datos SQL de Azure y que contiene una columna denominada "timestampcolumn" para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="d4306-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d4306-483">Si se establece "external": "true", se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="d4306-484">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d4306-485">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="d4306-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d4306-486">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="d4306-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d4306-487">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="d4306-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="d4306-488">**Actividad de copia en una canalización con SqlDWSource y BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="d4306-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="d4306-489">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="d4306-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d4306-490">En la definición de JSON de canalización, el tipo **source** se establece en **SqlDWSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d4306-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d4306-491">La consulta SQL especificada para la propiedad **SqlReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="d4306-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="d4306-492">En el ejemplo, **sqlReaderQuery** se especifica para SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="d4306-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="d4306-493">La actividad de copia ejecuta esta consulta en el origen de Almacenamiento de datos SQL de Azure para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="d4306-494">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="d4306-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="d4306-495">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura del conjunto de datos JSON se usan para crear una consulta (seleccione column1, column2 en mytable) y ejecutarla en Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4306-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4306-496">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="d4306-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="d4306-497">Ejemplo: Copia de datos de un blob de Azure a Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d4306-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4306-498">El ejemplo define las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="d4306-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="d4306-499">Un servicio vinculado de tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="d4306-500">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="d4306-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d4306-501">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d4306-502">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="d4306-503">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d4306-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d4306-504">El ejemplo copia los datos de la serie temporal (por horas, días, etc.) de un blob de Azure a una tabla de una base de datos de Azure SQL Data Warehouse cada hora.</span><span class="sxs-lookup"><span data-stu-id="d4306-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="d4306-505">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="d4306-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d4306-506">**Servicio vinculado del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="d4306-507">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d4306-508">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="d4306-509">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="d4306-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d4306-510">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="d4306-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d4306-511">La ruta de acceso de la carpeta usa la parte year, month y day de la hora de inicio y el nombre de archivo, la parte hour.</span><span class="sxs-lookup"><span data-stu-id="d4306-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="d4306-512">El valor "external": "true" informa al servicio Data Factory que esta tabla es externa a la factoría y no la produce una actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d4306-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="d4306-513">**Conjunto de datos de salida del almacenamiento de datos SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4306-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="d4306-514">El ejemplo copia los datos a una tabla denominada "MyTable" en el almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4306-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4306-515">Cree la tabla en Azure SQL Data Warehouse con el mismo número de columnas que espera que contenga el archivo CSV de blob.</span><span class="sxs-lookup"><span data-stu-id="d4306-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="d4306-516">Se agregan nuevas filas a la tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="d4306-516">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="d4306-517">**Actividad de copia en una canalización con BlobSource y SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="d4306-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="d4306-518">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="d4306-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d4306-519">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="d4306-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

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
<span data-ttu-id="d4306-520">Para ver un tutorial, consulte los artículos [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en menos de 15 minutos con Azure Data Factory) y [Carga de datos en SQL Data Warehouse con Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) en la documentación de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4306-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d4306-521">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="d4306-521">Performance and Tuning</span></span>
<span data-ttu-id="d4306-522">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="d4306-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
