---
title: Copia de datos hacia la instancia de Azure SQL Database y desde ella | Microsoft Docs
description: "Información acerca de cómo copiar datos hacia una instancia de Azure SQL Database y desde ella con Azure Data Factory."
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
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="ccf38-103">Copia de datos hacia una instancia de Azure SQL Database y desde ella con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ccf38-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="ccf38-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos hacia y desde Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ccf38-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="ccf38-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ccf38-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="ccf38-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="ccf38-106">Supported scenarios</span></span>
<span data-ttu-id="ccf38-107">Puede copiar datos **de Azure SQL Database** a los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="ccf38-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ccf38-108">Puede copiar datos de los siguientes almacenes de datos **a Azure SQL Database**:</span><span class="sxs-lookup"><span data-stu-id="ccf38-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="ccf38-109">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="ccf38-109">Supported authentication type</span></span>
<span data-ttu-id="ccf38-110">El conector de Azure SQL Database admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="ccf38-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ccf38-111">Introducción</span><span class="sxs-lookup"><span data-stu-id="ccf38-111">Getting started</span></span>
<span data-ttu-id="ccf38-112">Puede crear una canalización con actividad de copia que mueva los datos hacia Azure SQL Database y desde esta base de datos mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="ccf38-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="ccf38-113">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ccf38-114">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="ccf38-115">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ccf38-116">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="ccf38-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ccf38-117">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="ccf38-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="ccf38-118">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-118">Create a **data factory**.</span></span> <span data-ttu-id="ccf38-119">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="ccf38-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ccf38-120">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="ccf38-121">Por ejemplo, si va a copiar datos desde una instancia de Azure Blob Storage hacia una instancia de Azure SQL Database, creará dos servicios vinculados para vincular la cuenta de Azure Storage y la instancia de Azure SQL Database a su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="ccf38-122">Para información sobre las propiedades de los servicios vinculados que son específicas de Azure SQL Database, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ccf38-123">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="ccf38-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="ccf38-124">En el ejemplo mencionado en el último paso, se crea un conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="ccf38-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="ccf38-125">Además, se crea otro conjunto de datos para especificar la tabla SQL en la instancia de Azure SQL Database que contiene los datos copiados del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="ccf38-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="ccf38-126">Para información sobre las propiedades del conjunto de datos que son específicas de Azure Data Lake Store, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ccf38-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="ccf38-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ccf38-128">En el ejemplo que se ha mencionado anteriormente, se usa BlobSource como origen y SqlSink como receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="ccf38-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="ccf38-129">De igual forma, si va a copiar desde Azure SQL Database hacia Azure Blob Storage, usará SqlSource y BlobSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="ccf38-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="ccf38-130">Para información sobre las propiedades de actividad de copia que son específicas de Azure SQL Database, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ccf38-131">Para más información sobre cómo usar un almacén de datos como origen o receptor, haga clic en el vínculo de la sección anterior para su almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="ccf38-132">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="ccf38-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ccf38-133">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ccf38-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ccf38-134">Para obtener ejemplos con definiciones de JSON para entidades de Data Factory que se utilizan para copiar datos a Azure SQL Database y desde esta base de datos, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-to-and-from-sql-database) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="ccf38-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="ccf38-135">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="ccf38-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ccf38-136">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="ccf38-136">Linked service properties</span></span>
<span data-ttu-id="ccf38-137">Un servicio vinculado SQL de Azure vincula una base de datos SQL de Azure a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="ccf38-138">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf38-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="ccf38-139">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ccf38-139">Property</span></span> | <span data-ttu-id="ccf38-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="ccf38-140">Description</span></span> | <span data-ttu-id="ccf38-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ccf38-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccf38-142">type</span><span class="sxs-lookup"><span data-stu-id="ccf38-142">type</span></span> |<span data-ttu-id="ccf38-143">La propiedad type debe establecerse en: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="ccf38-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="ccf38-144">Sí</span><span class="sxs-lookup"><span data-stu-id="ccf38-144">Yes</span></span> |
| <span data-ttu-id="ccf38-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="ccf38-145">connectionString</span></span> |<span data-ttu-id="ccf38-146">Especifique la información necesaria para conectarse a la instancia de Base de datos SQL de Azure para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="ccf38-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="ccf38-147">Solo se admite la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="ccf38-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="ccf38-148">Sí</span><span class="sxs-lookup"><span data-stu-id="ccf38-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ccf38-149">Configure el [firewall de Azure SQL Database](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) y el servidor de bases de datos para [permitir que los servicios de Azure accedan al servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="ccf38-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="ccf38-150">Además, si va a copiar datos a Azure SQL Database desde fuera de Azure, incluidos orígenes de datos locales con puerta de enlace de la factoría de datos, configure el intervalo de direcciones IP adecuado para el equipo que envía datos a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ccf38-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ccf38-151">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="ccf38-151">Dataset properties</span></span>
<span data-ttu-id="ccf38-152">Para especificar un conjunto de datos para representar datos de entrada o salida en una base de datos SQL de Azure, establezca la propiedad de tipo del conjunto de datos en **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="ccf38-153">Establezca la propiedad **linkedServiceName** del conjunto de datos en el nombre del servicio vinculado SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf38-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="ccf38-154">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="ccf38-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ccf38-155">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="ccf38-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ccf38-156">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ccf38-157">La sección **typeProperties** del conjunto de datos de tipo **AzureSqlTable** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="ccf38-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="ccf38-158">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ccf38-158">Property</span></span> | <span data-ttu-id="ccf38-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="ccf38-159">Description</span></span> | <span data-ttu-id="ccf38-160">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ccf38-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccf38-161">tableName</span><span class="sxs-lookup"><span data-stu-id="ccf38-161">tableName</span></span> |<span data-ttu-id="ccf38-162">Nombre de la tabla o vista en la instancia de Azure SQL Database a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ccf38-163">Sí</span><span class="sxs-lookup"><span data-stu-id="ccf38-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ccf38-164">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="ccf38-164">Copy activity properties</span></span>
<span data-ttu-id="ccf38-165">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ccf38-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ccf38-166">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="ccf38-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ccf38-167">La actividad de copia toma solo una entrada y genera una única salida.</span><span class="sxs-lookup"><span data-stu-id="ccf38-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ccf38-168">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="ccf38-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="ccf38-169">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="ccf38-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="ccf38-170">Si va a mover datos desde una Azure SQL Database, establezca el tipo de origen en la actividad de copia en **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="ccf38-171">De igual forma, si va a mover datos a una Azure SQL Database, establezca el tipo de receptor en la actividad de copia en **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="ccf38-172">Esta sección proporciona una lista de propiedades admitidas por SqlSource y SqlSink.</span><span class="sxs-lookup"><span data-stu-id="ccf38-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="ccf38-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="ccf38-173">SqlSource</span></span>
<span data-ttu-id="ccf38-174">En la actividad de copia, si el origen es de tipo **SqlSource**, están disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="ccf38-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ccf38-175">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ccf38-175">Property</span></span> | <span data-ttu-id="ccf38-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="ccf38-176">Description</span></span> | <span data-ttu-id="ccf38-177">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ccf38-177">Allowed values</span></span> | <span data-ttu-id="ccf38-178">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ccf38-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ccf38-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ccf38-179">sqlReaderQuery</span></span> |<span data-ttu-id="ccf38-180">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-180">Use the custom query to read data.</span></span> |<span data-ttu-id="ccf38-181">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ccf38-181">SQL query string.</span></span> <span data-ttu-id="ccf38-182">Ejemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ccf38-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="ccf38-183">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-183">No</span></span> |
| <span data-ttu-id="ccf38-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ccf38-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ccf38-185">Nombre del procedimiento almacenado que lee datos de la tabla de origen.</span><span class="sxs-lookup"><span data-stu-id="ccf38-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="ccf38-186">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-186">Name of the stored procedure.</span></span> <span data-ttu-id="ccf38-187">La última instrucción SQL debe ser una instrucción SELECT del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="ccf38-188">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-188">No</span></span> |
| <span data-ttu-id="ccf38-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ccf38-189">storedProcedureParameters</span></span> |<span data-ttu-id="ccf38-190">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ccf38-191">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="ccf38-191">Name/value pairs.</span></span> <span data-ttu-id="ccf38-192">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ccf38-193">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-193">No</span></span> |

<span data-ttu-id="ccf38-194">Si se especifica **sqlReaderQuery** para SqlSource, la actividad de copia ejecuta la consulta en el origen de Base de datos SQL de Azure para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="ccf38-195">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="ccf38-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ccf38-196">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura del conjunto de datos JSON se usan para crear una consulta (`select column1, column2 from mytable`) y ejecutarla en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ccf38-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="ccf38-197">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="ccf38-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="ccf38-198">Cuando use **sqlReaderStoredProcedureName**, necesitará especificar un valor para la propiedad **tableName** del conjunto de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="ccf38-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="ccf38-199">Pero no se ha realizado ninguna validación en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="ccf38-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="ccf38-200">Ejemplo de SqlSource</span><span class="sxs-lookup"><span data-stu-id="ccf38-200">SqlSource example</span></span>

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

<span data-ttu-id="ccf38-201">**Definición del procedimiento almacenado:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="ccf38-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="ccf38-202">SqlSink</span></span>
<span data-ttu-id="ccf38-203">**SqlSink** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="ccf38-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="ccf38-204">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ccf38-204">Property</span></span> | <span data-ttu-id="ccf38-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="ccf38-205">Description</span></span> | <span data-ttu-id="ccf38-206">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ccf38-206">Allowed values</span></span> | <span data-ttu-id="ccf38-207">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ccf38-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ccf38-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ccf38-208">writeBatchTimeout</span></span> |<span data-ttu-id="ccf38-209">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="ccf38-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="ccf38-210">timespan</span><span class="sxs-lookup"><span data-stu-id="ccf38-210">timespan</span></span><br/><br/> <span data-ttu-id="ccf38-211">Ejemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ccf38-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ccf38-212">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-212">No</span></span> |
| <span data-ttu-id="ccf38-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ccf38-213">writeBatchSize</span></span> |<span data-ttu-id="ccf38-214">Inserta datos en la tabla SQL cuando el tamaño del búfer alcanza el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ccf38-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ccf38-215">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="ccf38-215">Integer (number of rows)</span></span> |<span data-ttu-id="ccf38-216">No (valor predeterminado = 10000)</span><span class="sxs-lookup"><span data-stu-id="ccf38-216">No (default: 10000)</span></span> |
| <span data-ttu-id="ccf38-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ccf38-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ccf38-218">Especifique una consulta para que se ejecute la actividad de copia de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="ccf38-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ccf38-219">Para más información, consulte [Copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ccf38-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ccf38-220">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="ccf38-220">A query statement.</span></span> |<span data-ttu-id="ccf38-221">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-221">No</span></span> |
| <span data-ttu-id="ccf38-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ccf38-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ccf38-223">Especifique el nombre de columna para que la rellene la actividad de copia con un identificador de segmentos generado automáticamente, que se usará para limpiar los datos de un segmento específico cuando se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="ccf38-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ccf38-224">Para más información, consulte [Copia repetible](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ccf38-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ccf38-225">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="ccf38-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ccf38-226">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-226">No</span></span> |
| <span data-ttu-id="ccf38-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ccf38-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ccf38-228">Nombre del procedimiento almacenado que actualiza e inserta (operación de upsert) datos en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="ccf38-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="ccf38-229">Nombre del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-229">Name of the stored procedure.</span></span> |<span data-ttu-id="ccf38-230">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-230">No</span></span> |
| <span data-ttu-id="ccf38-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ccf38-231">storedProcedureParameters</span></span> |<span data-ttu-id="ccf38-232">Parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ccf38-233">Pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="ccf38-233">Name/value pairs.</span></span> <span data-ttu-id="ccf38-234">Los nombres y las mayúsculas y minúsculas de los parámetros deben coincidir con las mismas características de los parámetros de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ccf38-235">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-235">No</span></span> |
| <span data-ttu-id="ccf38-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ccf38-236">sqlWriterTableType</span></span> |<span data-ttu-id="ccf38-237">Especifique el nombre del tipo de tabla que se usará en el procedimiento almacenado anterior.</span><span class="sxs-lookup"><span data-stu-id="ccf38-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="ccf38-238">La actividad de copia dispone que los datos que se mueven estén disponibles en una tabla temporal con este tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="ccf38-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ccf38-239">El código de procedimiento almacenado puede combinar los datos copiados con datos existentes.</span><span class="sxs-lookup"><span data-stu-id="ccf38-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="ccf38-240">Un nombre de tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="ccf38-240">A table type name.</span></span> |<span data-ttu-id="ccf38-241">No</span><span class="sxs-lookup"><span data-stu-id="ccf38-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="ccf38-242">Ejemplo de SqlSink</span><span class="sxs-lookup"><span data-stu-id="ccf38-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="ccf38-243">Ejemplos JSON para copiar datos hacia y desde SQL Database</span><span class="sxs-lookup"><span data-stu-id="ccf38-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="ccf38-244">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ccf38-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ccf38-245">Muestran cómo copiar datos entre el Almacenamiento de blobs de Azure y la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf38-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="ccf38-246">Sin embargo, los datos se pueden copiar **directamente** de cualquiera de los orígenes a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf38-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="ccf38-247">Ejemplo: copia de datos de Azure SQL Database a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="ccf38-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="ccf38-248">El ejemplo define las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="ccf38-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="ccf38-249">Un servicio vinculado de tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ccf38-250">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="ccf38-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ccf38-251">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ccf38-252">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ccf38-253">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [SqlSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ccf38-254">El ejemplo copia los datos de la serie temporal (por horas, días, etc.) de una tabla de Azure SQL Database en un blob cada hora.</span><span class="sxs-lookup"><span data-stu-id="ccf38-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="ccf38-255">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="ccf38-256">**Servicio vinculado a Azure SQL Database:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="ccf38-257">Consulte la sección [Servicio vinculado SQL de Azure](#linked-service) para obtener la lista de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="ccf38-258">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ccf38-259">Vea el artículo [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener la lista de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="ccf38-260">**Conjunto de datos de entrada SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="ccf38-261">El ejemplo supone que ha creado una tabla "MyTable" en SQL de Azure y que contiene una columna denominada "timestampcolumn" para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="ccf38-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ccf38-262">Si se establece "external": "true", se informa al servicio Azure Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="ccf38-263">Consulte la sección [Propiedades de tipo de conjunto de datos SQL de Azure](#dataset) para obtener la lista de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ccf38-264">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ccf38-265">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ccf38-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ccf38-266">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="ccf38-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ccf38-267">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="ccf38-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="ccf38-268">Consulte la sección [Propiedades de tipo de conjunto de datos Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener la lista de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ccf38-269">**Actividad de copia en una canalización con el origen SQL y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="ccf38-270">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="ccf38-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ccf38-271">En la definición de la canalización JSON, el tipo **source** se establece en **SqlSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ccf38-272">La consulta SQL especificada para la propiedad **SqlReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="ccf38-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="ccf38-273">En el ejemplo, **sqlReaderQuery** se especifica para SqlSource.</span><span class="sxs-lookup"><span data-stu-id="ccf38-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="ccf38-274">La actividad de copia ejecuta esta consulta en el origen de Base de datos SQL de Azure para obtener los datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="ccf38-275">Como alternativa, puede indicar un procedimiento almacenado mediante la especificación de **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si el procedimiento almacenado toma parámetros).</span><span class="sxs-lookup"><span data-stu-id="ccf38-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ccf38-276">Si no especifica sqlReaderQuery ni sqlReaderStoredProcedureName, las columnas definidas en la sección sobre la estructura del conjunto de datos JSON se usan para crear una consulta y ejecutarla en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ccf38-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="ccf38-277">Por ejemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="ccf38-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="ccf38-278">Si la definición del conjunto de datos no tiene la estructura, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="ccf38-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="ccf38-279">Vea la sección [Sql Source](#sqlsource) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para obtener la lista de propiedades admitidas por SqlSource y BlobSink.</span><span class="sxs-lookup"><span data-stu-id="ccf38-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="ccf38-280">Ejemplo: copia de datos de un blob de Azure a SQL Database</span><span class="sxs-lookup"><span data-stu-id="ccf38-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="ccf38-281">El ejemplo define las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="ccf38-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="ccf38-282">Un servicio vinculado de tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ccf38-283">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="ccf38-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ccf38-284">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ccf38-285">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="ccf38-286">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf38-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ccf38-287">El ejemplo copia los datos de la serie temporal (por horas, días, etc.) de un blob de Azure a una tabla de Azure SQL Database cada hora.</span><span class="sxs-lookup"><span data-stu-id="ccf38-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="ccf38-288">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ccf38-289">**Servicio vinculado SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="ccf38-290">Consulte la sección [Servicio vinculado SQL de Azure](#linked-service) para obtener la lista de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="ccf38-291">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ccf38-292">Vea el artículo [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener la lista de propiedades admitidas por este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ccf38-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="ccf38-293">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ccf38-294">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ccf38-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ccf38-295">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="ccf38-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ccf38-296">La ruta de acceso de la carpeta usa la parte year, month y day de la hora de inicio y el nombre de archivo, la parte hour.</span><span class="sxs-lookup"><span data-stu-id="ccf38-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="ccf38-297">El valor "external": "true" informa al servicio Data Factory que esta tabla es externa a la factoría y no la produce una actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="ccf38-298">Consulte la sección [Propiedades de tipo de conjunto de datos Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener la lista de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ccf38-299">**Conjunto de datos de salida de Azure SQL Database:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="ccf38-300">El ejemplo copia los datos a una tabla denominada "MyTable" en SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf38-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="ccf38-301">Cree la tabla en SQL de Azure con el mismo número de columnas que espera que contenga el archivo CSV de blob.</span><span class="sxs-lookup"><span data-stu-id="ccf38-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="ccf38-302">Se agregan nuevas filas a la tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="ccf38-302">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="ccf38-303">Consulte la sección [Propiedades de tipo de conjunto de datos SQL de Azure](#dataset) para obtener la lista de propiedades admitidas por este tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ccf38-304">**Una actividad de copia en una canalización con el origen de blob y el receptor SQL:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="ccf38-305">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="ccf38-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ccf38-306">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ccf38-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
<span data-ttu-id="ccf38-307">Vea la sección [Sql Sink](#sqlsink) y [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) para obtener la lista de propiedades admitidas por SqlSink y BlobSource.</span><span class="sxs-lookup"><span data-stu-id="ccf38-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="ccf38-308">Columnas de identidad en la base de datos de destino</span><span class="sxs-lookup"><span data-stu-id="ccf38-308">Identity columns in the target database</span></span>
<span data-ttu-id="ccf38-309">En esta sección se proporciona un ejemplo para copiar datos de una tabla de origen sin una columna de identidad en una tabla de destino con una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="ccf38-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="ccf38-310">**Tabla de origen:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="ccf38-311">**Tabla de destino:**</span><span class="sxs-lookup"><span data-stu-id="ccf38-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="ccf38-312">Observe que la tabla de destino tiene una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="ccf38-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="ccf38-313">**Definición de JSON del conjunto de datos de origen**</span><span class="sxs-lookup"><span data-stu-id="ccf38-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="ccf38-314">**Definición de JSON del conjunto de datos de destino**</span><span class="sxs-lookup"><span data-stu-id="ccf38-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="ccf38-315">Tenga en cuenta que la tabla de origen y de destino tienen un esquema diferente (el destino tiene una columna adicional con identidad).</span><span class="sxs-lookup"><span data-stu-id="ccf38-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="ccf38-316">En este escenario, debe especificar la propiedad **structure** de la definición del conjunto de datos de destino, que no incluye la columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="ccf38-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="ccf38-317">Invocación del procedimiento almacenado desde el receptor de SQL</span><span class="sxs-lookup"><span data-stu-id="ccf38-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="ccf38-318">Para obtener un ejemplo de invocación a un procedimiento almacenado de receptor SQL en una actividad de copia de una canalización, consulte el artículo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocación de un procedimiento almacenado para el receptor SQL en la actividad de copia).</span><span class="sxs-lookup"><span data-stu-id="ccf38-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="ccf38-319">Asignación de tipos para Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ccf38-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="ccf38-320">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md), la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="ccf38-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="ccf38-321">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="ccf38-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ccf38-322">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="ccf38-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ccf38-323">Al migrar datos a Azure SQL Database y en sentido contrario, se usarán las siguientes asignaciones del tipo SQL al tipo .NET, y viceversa.</span><span class="sxs-lookup"><span data-stu-id="ccf38-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="ccf38-324">La asignación es igual que la asignación de tipo de datos de SQL Server para ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="ccf38-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="ccf38-325">Tipo de motor de base de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="ccf38-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="ccf38-326">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ccf38-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ccf38-327">bigint</span><span class="sxs-lookup"><span data-stu-id="ccf38-327">bigint</span></span> |<span data-ttu-id="ccf38-328">Int64</span><span class="sxs-lookup"><span data-stu-id="ccf38-328">Int64</span></span> |
| <span data-ttu-id="ccf38-329">binary</span><span class="sxs-lookup"><span data-stu-id="ccf38-329">binary</span></span> |<span data-ttu-id="ccf38-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-330">Byte[]</span></span> |
| <span data-ttu-id="ccf38-331">bit</span><span class="sxs-lookup"><span data-stu-id="ccf38-331">bit</span></span> |<span data-ttu-id="ccf38-332">Booleano</span><span class="sxs-lookup"><span data-stu-id="ccf38-332">Boolean</span></span> |
| <span data-ttu-id="ccf38-333">char</span><span class="sxs-lookup"><span data-stu-id="ccf38-333">char</span></span> |<span data-ttu-id="ccf38-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-334">String, Char[]</span></span> |
| <span data-ttu-id="ccf38-335">fecha</span><span class="sxs-lookup"><span data-stu-id="ccf38-335">date</span></span> |<span data-ttu-id="ccf38-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="ccf38-336">DateTime</span></span> |
| <span data-ttu-id="ccf38-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="ccf38-337">Datetime</span></span> |<span data-ttu-id="ccf38-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="ccf38-338">DateTime</span></span> |
| <span data-ttu-id="ccf38-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="ccf38-339">datetime2</span></span> |<span data-ttu-id="ccf38-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="ccf38-340">DateTime</span></span> |
| <span data-ttu-id="ccf38-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ccf38-341">Datetimeoffset</span></span> |<span data-ttu-id="ccf38-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ccf38-342">DateTimeOffset</span></span> |
| <span data-ttu-id="ccf38-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="ccf38-343">Decimal</span></span> |<span data-ttu-id="ccf38-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="ccf38-344">Decimal</span></span> |
| <span data-ttu-id="ccf38-345">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ccf38-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ccf38-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-346">Byte[]</span></span> |
| <span data-ttu-id="ccf38-347">Float</span><span class="sxs-lookup"><span data-stu-id="ccf38-347">Float</span></span> |<span data-ttu-id="ccf38-348">Doble</span><span class="sxs-lookup"><span data-stu-id="ccf38-348">Double</span></span> |
| <span data-ttu-id="ccf38-349">imagen</span><span class="sxs-lookup"><span data-stu-id="ccf38-349">image</span></span> |<span data-ttu-id="ccf38-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-350">Byte[]</span></span> |
| <span data-ttu-id="ccf38-351">int</span><span class="sxs-lookup"><span data-stu-id="ccf38-351">int</span></span> |<span data-ttu-id="ccf38-352">Int32</span><span class="sxs-lookup"><span data-stu-id="ccf38-352">Int32</span></span> |
| <span data-ttu-id="ccf38-353">money</span><span class="sxs-lookup"><span data-stu-id="ccf38-353">money</span></span> |<span data-ttu-id="ccf38-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="ccf38-354">Decimal</span></span> |
| <span data-ttu-id="ccf38-355">nchar</span><span class="sxs-lookup"><span data-stu-id="ccf38-355">nchar</span></span> |<span data-ttu-id="ccf38-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-356">String, Char[]</span></span> |
| <span data-ttu-id="ccf38-357">ntext</span><span class="sxs-lookup"><span data-stu-id="ccf38-357">ntext</span></span> |<span data-ttu-id="ccf38-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-358">String, Char[]</span></span> |
| <span data-ttu-id="ccf38-359">numeric</span><span class="sxs-lookup"><span data-stu-id="ccf38-359">numeric</span></span> |<span data-ttu-id="ccf38-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="ccf38-360">Decimal</span></span> |
| <span data-ttu-id="ccf38-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ccf38-361">nvarchar</span></span> |<span data-ttu-id="ccf38-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-362">String, Char[]</span></span> |
| <span data-ttu-id="ccf38-363">real</span><span class="sxs-lookup"><span data-stu-id="ccf38-363">real</span></span> |<span data-ttu-id="ccf38-364">Single</span><span class="sxs-lookup"><span data-stu-id="ccf38-364">Single</span></span> |
| <span data-ttu-id="ccf38-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="ccf38-365">rowversion</span></span> |<span data-ttu-id="ccf38-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-366">Byte[]</span></span> |
| <span data-ttu-id="ccf38-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ccf38-367">smalldatetime</span></span> |<span data-ttu-id="ccf38-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="ccf38-368">DateTime</span></span> |
| <span data-ttu-id="ccf38-369">smallint</span><span class="sxs-lookup"><span data-stu-id="ccf38-369">smallint</span></span> |<span data-ttu-id="ccf38-370">Int16</span><span class="sxs-lookup"><span data-stu-id="ccf38-370">Int16</span></span> |
| <span data-ttu-id="ccf38-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="ccf38-371">smallmoney</span></span> |<span data-ttu-id="ccf38-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="ccf38-372">Decimal</span></span> |
| <span data-ttu-id="ccf38-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ccf38-373">sql_variant</span></span> |<span data-ttu-id="ccf38-374">Object *</span><span class="sxs-lookup"><span data-stu-id="ccf38-374">Object *</span></span> |
| <span data-ttu-id="ccf38-375">text</span><span class="sxs-lookup"><span data-stu-id="ccf38-375">text</span></span> |<span data-ttu-id="ccf38-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-376">String, Char[]</span></span> |
| <span data-ttu-id="ccf38-377">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="ccf38-377">time</span></span> |<span data-ttu-id="ccf38-378">timespan</span><span class="sxs-lookup"><span data-stu-id="ccf38-378">TimeSpan</span></span> |
| <span data-ttu-id="ccf38-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="ccf38-379">timestamp</span></span> |<span data-ttu-id="ccf38-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-380">Byte[]</span></span> |
| <span data-ttu-id="ccf38-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="ccf38-381">tinyint</span></span> |<span data-ttu-id="ccf38-382">Byte</span><span class="sxs-lookup"><span data-stu-id="ccf38-382">Byte</span></span> |
| <span data-ttu-id="ccf38-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="ccf38-383">uniqueidentifier</span></span> |<span data-ttu-id="ccf38-384">Guid</span><span class="sxs-lookup"><span data-stu-id="ccf38-384">Guid</span></span> |
| <span data-ttu-id="ccf38-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="ccf38-385">varbinary</span></span> |<span data-ttu-id="ccf38-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-386">Byte[]</span></span> |
| <span data-ttu-id="ccf38-387">varchar</span><span class="sxs-lookup"><span data-stu-id="ccf38-387">varchar</span></span> |<span data-ttu-id="ccf38-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ccf38-388">String, Char[]</span></span> |
| <span data-ttu-id="ccf38-389">xml</span><span class="sxs-lookup"><span data-stu-id="ccf38-389">xml</span></span> |<span data-ttu-id="ccf38-390">xml</span><span class="sxs-lookup"><span data-stu-id="ccf38-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="ccf38-391">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="ccf38-391">Map source to sink columns</span></span>
<span data-ttu-id="ccf38-392">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ccf38-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="ccf38-393">Copia repetible</span><span class="sxs-lookup"><span data-stu-id="ccf38-393">Repeatable copy</span></span>
<span data-ttu-id="ccf38-394">Cuando se copian datos en SQL Server Database, la actividad de copia anexa datos a la tabla receptora de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ccf38-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="ccf38-395">Para ejecutar una semántica UPSERT en su lugar, consulte el artículo [Escritura repetible en SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="ccf38-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="ccf38-396">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="ccf38-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="ccf38-397">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="ccf38-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ccf38-398">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="ccf38-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ccf38-399">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="ccf38-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ccf38-400">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ccf38-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ccf38-401">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="ccf38-401">Performance and Tuning</span></span>
<span data-ttu-id="ccf38-402">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="ccf38-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
