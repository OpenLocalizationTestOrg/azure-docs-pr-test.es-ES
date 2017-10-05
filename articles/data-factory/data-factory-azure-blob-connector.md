---
title: Copiar datos hacia y desde Azure Blob Storage | Microsoft Docs
description: 'Aprenda a copiar datos de blob en Data Factory de Azure. Use nuestro ejemplo: Copia de datos entre Almacenamiento de blobs de Azure y Base de datos SQL de Azure.'
keywords: datos de blob, copia de blobs de azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="b968a-105">Copia de datos hacia Azure Blob Storage o desde él con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b968a-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="b968a-106">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para copiar datos hacia Azure Blob Storage y desde este servicio.</span><span class="sxs-lookup"><span data-stu-id="b968a-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="b968a-107">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="b968a-108">Información general</span><span class="sxs-lookup"><span data-stu-id="b968a-108">Overview</span></span>
<span data-ttu-id="b968a-109">Puede copiar datos de cualquier almacén de datos de origen compatible a Azure Blob Storage o de Azure Blob Storage a cualquier almacén de datos del receptor compatible.</span><span class="sxs-lookup"><span data-stu-id="b968a-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="b968a-110">En la tabla siguiente se proporciona una lista de almacenes de datos que se admiten como orígenes o receptores de la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b968a-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="b968a-111">Por ejemplo, puede mover datos **de** una base de datos SQL Server o una base de datos Azure SQL **a** una instancia de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="b968a-112">Y, puede copiar datos **desde** Azure Blob Storage **hacia** una instancia de Azure SQL Data Warehouse o una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b968a-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="b968a-113">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="b968a-113">Supported scenarios</span></span>
<span data-ttu-id="b968a-114">Puede copiar datos **desde Azure Blob Storage** hacia los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="b968a-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b968a-115">Puede copiar datos desde los siguientes almacenes de datos **hacia Azure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="b968a-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="b968a-116">La actividad de copia es compatible con la copia de datos desde y hacia cuentas de Azure Storage de propósito general y el almacenamiento de blobs en frío y en caliente.</span><span class="sxs-lookup"><span data-stu-id="b968a-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="b968a-117">La actividad admite **leer desde blobs en bloques, en anexos o en páginas**, pero solo permite **escribir en blobs en bloques**.</span><span class="sxs-lookup"><span data-stu-id="b968a-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="b968a-118">Azure Premium Storage no es compatible como receptor porque está respaldado por blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="b968a-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="b968a-119">La actividad de copia no elimina datos del origen una vez copiados los datos correctamente en el destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="b968a-120">Si necesita eliminar datos de origen tras una copia correcta, cree una [actividad personalizada](data-factory-use-custom-activities.md) para tal fin y úsela en la canalización.</span><span class="sxs-lookup"><span data-stu-id="b968a-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="b968a-121">Para más información, consulte el [ejemplo de eliminación de un blob o una carpeta en GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="b968a-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="b968a-122">Introducción</span><span class="sxs-lookup"><span data-stu-id="b968a-122">Get started</span></span>
<span data-ttu-id="b968a-123">Puede crear una canalización con actividad de copia que mueva los datos desde Azure Blob Storage o hacia él mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="b968a-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="b968a-124">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="b968a-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b968a-125">Este artículo tiene un [tutorial](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para crear una canalización para copiar datos entre ubicaciones de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="b968a-126">Para ver un tutorial sobre la creación de una canalización para copiar datos desde una instancia de Azure Blob Storage hacia una instancia de Azure SQL Database, consulte [Tutorial: crear una canalización mediante el Asistente para copia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="b968a-127">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="b968a-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b968a-128">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b968a-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="b968a-129">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="b968a-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b968a-130">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="b968a-130">Create a **data factory**.</span></span> <span data-ttu-id="b968a-131">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="b968a-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b968a-132">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="b968a-133">Por ejemplo, si va a copiar datos desde una instancia de Azure Blob Storage hacia una instancia de Azure SQL Database, creará dos servicios vinculados para vincular la cuenta de Azure Storage y la instancia de Azure SQL Database a su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="b968a-134">Para información sobre las propiedades de los servicios vinculados que son específicas de Azure Blob Storage, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="b968a-135">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="b968a-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="b968a-136">En el ejemplo mencionado en el último paso, se crea un conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="b968a-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="b968a-137">Además, se crea otro conjunto de datos para especificar la tabla SQL en la instancia de Azure SQL Database que contiene los datos copiados del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b968a-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="b968a-138">Para información sobre las propiedades del conjunto de datos que son específicas de Azure Blob Storage, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="b968a-139">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b968a-140">En el ejemplo que se ha mencionado anteriormente, se usa BlobSource como origen y SqlSink como receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b968a-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="b968a-141">De igual forma, si va a copiar desde Azure SQL Database hacia Azure Blob Storage, se usa SqlSource y BlobSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="b968a-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="b968a-142">Para información sobre las propiedades de la actividad de copia que son específicas de Azure Blob Storage, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b968a-143">Para más información sobre cómo usar un almacén de datos como origen o como receptor, haga clic en el vínculo de la sección anterior para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="b968a-144">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="b968a-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b968a-145">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b968a-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b968a-146">Para obtener ejemplos con definiciones de JSON para entidades de Data Factory que se utilizan para copiar datos con Azure Blob Storage como origen y destino, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="b968a-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="b968a-147">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b968a-148">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="b968a-148">Linked service properties</span></span>
<span data-ttu-id="b968a-149">Hay dos tipos de servicios vinculados que puede usar para vincular una instancia de Azure Storage a una instancia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b968a-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="b968a-150">Se trata del servicio vinculado **AzureStorage** y el servicio vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="b968a-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="b968a-151">El servicio vinculado de Almacenamiento de Azure proporciona a la factoría de datos acceso global al Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="b968a-152">Mientras que el servicio vinculado de SAS (firma de acceso compartido) de Almacenamiento de Azure proporciona a la factoría de datos acceso restringido/controlado por tiempo al Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="b968a-153">No existen otras diferencias entre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="b968a-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="b968a-154">Elija el servicio vinculado que se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="b968a-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="b968a-155">En las siguientes secciones se ofrecen más detalles sobre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="b968a-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="b968a-156">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="b968a-156">Dataset properties</span></span>
<span data-ttu-id="b968a-157">Para especificar un conjunto de datos para representar datos de entrada o salida en Azure Blob Storage, establezca la propiedad de tipo del conjunto de datos en **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="b968a-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="b968a-158">Establezca la propiedad **linkedServiceName** del conjunto de datos en el nombre del servicio vinculado Azure Storage o SAS de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="b968a-159">Las propiedades de tipo del conjunto de datos especifican el **contenedor de blobs** y la **carpeta** en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="b968a-160">Para obtener una lista completa de las secciones y propiedades JSON disponibles para definir conjuntos de datos, consulte el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b968a-161">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="b968a-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b968a-162">Data factory admite los siguientes valores de tipo basados en .NET compatible con CLS con el fin de proporcionar información de tipos en la sección "structure" del esquema de los orígenes de datos de lectura como un blob de Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset y Timespan.</span><span class="sxs-lookup"><span data-stu-id="b968a-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="b968a-163">Data Factory realiza automáticamente las conversiones de tipo al mover datos desde un almacén de datos de origen a un almacén de datos de receptor.</span><span class="sxs-lookup"><span data-stu-id="b968a-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="b968a-164">La sección **typeProperties** es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación, el formato, etc. de los datos del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="b968a-165">La sección typeProperties del conjunto de datos de tipo **AzureBlob** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="b968a-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="b968a-166">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b968a-166">Property</span></span> | <span data-ttu-id="b968a-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="b968a-167">Description</span></span> | <span data-ttu-id="b968a-168">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b968a-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b968a-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="b968a-169">folderPath</span></span> |<span data-ttu-id="b968a-170">Ruta de acceso para el contenedor y la carpeta en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b968a-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="b968a-171">Ejemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="b968a-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="b968a-172">Sí</span><span class="sxs-lookup"><span data-stu-id="b968a-172">Yes</span></span> |
| <span data-ttu-id="b968a-173">fileName</span><span class="sxs-lookup"><span data-stu-id="b968a-173">fileName</span></span> |<span data-ttu-id="b968a-174">Nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="b968a-174">Name of the blob.</span></span> <span data-ttu-id="b968a-175">La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b968a-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="b968a-176">Si especifica fileName, la actividad (incluida la copia) funciona en el blob específico.</span><span class="sxs-lookup"><span data-stu-id="b968a-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="b968a-177">Cuando no se especifica fileName, la copia incluirá todos los blobs de folderPath para el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="b968a-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="b968a-178">Si no se especifica **fileName** para un conjunto de datos de salida y no se especifica **preserveHierarchy** en el receptor de actividad, el nombre del archivo generado tendrá el siguiente formato: Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="b968a-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="b968a-179">No</span><span class="sxs-lookup"><span data-stu-id="b968a-179">No</span></span> |
| <span data-ttu-id="b968a-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="b968a-180">partitionedBy</span></span> |<span data-ttu-id="b968a-181">partitionedBy es una propiedad opcional.</span><span class="sxs-lookup"><span data-stu-id="b968a-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="b968a-182">Puede usarla para especificar un folderPath dinámico y un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="b968a-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="b968a-183">Por ejemplo, se puede parametrizar folderPath por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="b968a-184">Consulte la sección [Uso de la propiedad partitionedBy](#using-partitionedBy-property) para ver información detallada y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="b968a-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="b968a-185">No</span><span class="sxs-lookup"><span data-stu-id="b968a-185">No</span></span> |
| <span data-ttu-id="b968a-186">formato</span><span class="sxs-lookup"><span data-stu-id="b968a-186">format</span></span> | <span data-ttu-id="b968a-187">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="b968a-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b968a-188">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="b968a-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="b968a-189">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="b968a-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="b968a-190">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="b968a-191">No</span><span class="sxs-lookup"><span data-stu-id="b968a-191">No</span></span> |
| <span data-ttu-id="b968a-192">compresión</span><span class="sxs-lookup"><span data-stu-id="b968a-192">compression</span></span> | <span data-ttu-id="b968a-193">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="b968a-194">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="b968a-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b968a-195">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="b968a-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b968a-196">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="b968a-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b968a-197">No</span><span class="sxs-lookup"><span data-stu-id="b968a-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="b968a-198">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="b968a-198">Using partitionedBy property</span></span>
<span data-ttu-id="b968a-199">Como ya se ha indicado en la sección anterior, se puede especificar un valor dinámico de folderPath y filename para datos de series temporales con la propiedad **partitionedBy**, [funciones de Data Factory y las variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="b968a-200">Para más información sobre los conjuntos de datos de series temporales, la programación y los segmentos, consulte los artículos [Creación de conjuntos de datos](data-factory-create-datasets.md) y [Programación y ejecución](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="b968a-201">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="b968a-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="b968a-202">En este ejemplo, {Slice} se reemplaza por el valor de la variable del sistema SliceStart de Data Factory en el formato (YYYYMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="b968a-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="b968a-203">SliceStart hace referencia a la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="b968a-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="b968a-204">folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="b968a-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="b968a-205">Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="b968a-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="b968a-206">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="b968a-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="b968a-207">En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.</span><span class="sxs-lookup"><span data-stu-id="b968a-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b968a-208">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="b968a-208">Copy activity properties</span></span>
<span data-ttu-id="b968a-209">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b968a-210">Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="b968a-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="b968a-211">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="b968a-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="b968a-212">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="b968a-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="b968a-213">Si va a mover datos desde un Azure Blob Storage, establezca el tipo de origen en la actividad de copia en **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="b968a-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="b968a-214">De igual forma, si va a mover datos desde un Azure Blob Storage, establezca el tipo de receptor en la actividad de copia en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b968a-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="b968a-215">Esta sección proporciona una lista de propiedades admitidas por BlobSource y BlobSink.</span><span class="sxs-lookup"><span data-stu-id="b968a-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="b968a-216">**BlobSource** admite las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="b968a-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="b968a-217">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b968a-217">Property</span></span> | <span data-ttu-id="b968a-218">Descripción</span><span class="sxs-lookup"><span data-stu-id="b968a-218">Description</span></span> | <span data-ttu-id="b968a-219">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b968a-219">Allowed values</span></span> | <span data-ttu-id="b968a-220">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b968a-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b968a-221">recursive</span><span class="sxs-lookup"><span data-stu-id="b968a-221">recursive</span></span> |<span data-ttu-id="b968a-222">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="b968a-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="b968a-223">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="b968a-223">True (default value), False</span></span> |<span data-ttu-id="b968a-224">No</span><span class="sxs-lookup"><span data-stu-id="b968a-224">No</span></span> |

<span data-ttu-id="b968a-225">**BlobSink** admite las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="b968a-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="b968a-226">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b968a-226">Property</span></span> | <span data-ttu-id="b968a-227">Descripción</span><span class="sxs-lookup"><span data-stu-id="b968a-227">Description</span></span> | <span data-ttu-id="b968a-228">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b968a-228">Allowed values</span></span> | <span data-ttu-id="b968a-229">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b968a-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b968a-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b968a-230">copyBehavior</span></span> |<span data-ttu-id="b968a-231">Define el comportamiento de copia cuando el origen es BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="b968a-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="b968a-232"><b>PreserveHierarchy:</b> conserva la jerarquía de archivos en la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="b968a-233">La ruta de acceso relativa del archivo de origen que apunta a la carpeta de origen es idéntica a la ruta de acceso relativa del archivo de destino que apunta a la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="b968a-234"><b>FlattenHierarchy:</b> todos los archivos de la carpeta de origen están en el primer nivel de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="b968a-235">Los archivos de destino tienen un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b968a-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="b968a-236"><b>MergeFiles:</b> combina todos los archivos de la carpeta de origen en un archivo.</span><span class="sxs-lookup"><span data-stu-id="b968a-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="b968a-237">Si se especifica el nombre de archivo/blob, el nombre de archivo combinado sería el nombre especificado; de lo contrario, sería el nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b968a-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="b968a-238">No</span><span class="sxs-lookup"><span data-stu-id="b968a-238">No</span></span> |

<span data-ttu-id="b968a-239">**BlobSource** también admite estas dos propiedades para ofrecer compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="b968a-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="b968a-240">**treatEmptyAsNull**: especifica si se debe tratar una cadena nula o vacía como un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="b968a-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="b968a-241">**skipHeaderLineCount** : especifica cuántas líneas deben omitirse.</span><span class="sxs-lookup"><span data-stu-id="b968a-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="b968a-242">Es aplicable únicamente cuando el conjunto de datos de entrada usa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="b968a-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="b968a-243">De forma similar, **BlobSink** admite la siguiente propiedad para ofrecer compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="b968a-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="b968a-244">**blobWriterAddHeader**: especifica si se debe agregar un encabezado de definiciones de columna al escribir en un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="b968a-245">Los conjuntos de datos ahora son compatibles con las siguientes propiedades que implementan la misma funcionalidad: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="b968a-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="b968a-246">En la tabla siguiente se proporciona orientación sobre cómo utilizar las nuevas propiedades de conjunto de datos en lugar de estas propiedades de origen/receptor de blob.</span><span class="sxs-lookup"><span data-stu-id="b968a-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="b968a-247">Propiedad de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="b968a-247">Copy Activity property</span></span> | <span data-ttu-id="b968a-248">Propiedad de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="b968a-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="b968a-249">skipHeaderLineCount en BlobSource</span><span class="sxs-lookup"><span data-stu-id="b968a-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="b968a-250">skipLineCount y firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="b968a-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="b968a-251">Las líneas se omiten en primer lugar y, a continuación, se lee la primera fila como encabezado.</span><span class="sxs-lookup"><span data-stu-id="b968a-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="b968a-252">treatEmptyAsNull en BlobSource</span><span class="sxs-lookup"><span data-stu-id="b968a-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="b968a-253">treatEmptyAsNull en el conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="b968a-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="b968a-254">blobWriterAddHeader en BlobSink</span><span class="sxs-lookup"><span data-stu-id="b968a-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="b968a-255">firstRowAsHeader en el conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="b968a-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="b968a-256">Consulte la sección [Especificación de TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) para obtener información detallada acerca de estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="b968a-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="b968a-257">Ejemplos de recursive y copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b968a-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="b968a-258">En esta sección se describe el comportamiento resultante de la operación de copia para diferentes combinaciones de valores recursive y copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="b968a-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="b968a-259">recursive</span><span class="sxs-lookup"><span data-stu-id="b968a-259">recursive</span></span> | <span data-ttu-id="b968a-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b968a-260">copyBehavior</span></span> | <span data-ttu-id="b968a-261">Comportamiento resultante</span><span class="sxs-lookup"><span data-stu-id="b968a-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b968a-262">true</span><span class="sxs-lookup"><span data-stu-id="b968a-262">true</span></span> |<span data-ttu-id="b968a-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b968a-263">preserveHierarchy</span></span> |<span data-ttu-id="b968a-264">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="b968a-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b968a-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-265">Folder1</span></span><br/><span data-ttu-id="b968a-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b968a-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b968a-272">la carpeta de destino Folder1 se crea con la misma estructura que la de origen</span><span class="sxs-lookup"><span data-stu-id="b968a-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="b968a-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-273">Folder1</span></span><br/><span data-ttu-id="b968a-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="b968a-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="b968a-280">true</span><span class="sxs-lookup"><span data-stu-id="b968a-280">true</span></span> |<span data-ttu-id="b968a-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b968a-281">flattenHierarchy</span></span> |<span data-ttu-id="b968a-282">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="b968a-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b968a-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-283">Folder1</span></span><br/><span data-ttu-id="b968a-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b968a-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b968a-290">la carpeta de destino Folder1 se crea con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="b968a-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="b968a-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-291">Folder1</span></span><br/><span data-ttu-id="b968a-292">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="b968a-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b968a-293">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="b968a-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="b968a-294">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3</span><span class="sxs-lookup"><span data-stu-id="b968a-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="b968a-295">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4</span><span class="sxs-lookup"><span data-stu-id="b968a-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="b968a-296">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5</span><span class="sxs-lookup"><span data-stu-id="b968a-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="b968a-297">true</span><span class="sxs-lookup"><span data-stu-id="b968a-297">true</span></span> |<span data-ttu-id="b968a-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b968a-298">mergeFiles</span></span> |<span data-ttu-id="b968a-299">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="b968a-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b968a-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-300">Folder1</span></span><br/><span data-ttu-id="b968a-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b968a-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b968a-307">la carpeta de destino Folder1 se crea con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="b968a-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="b968a-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-308">Folder1</span></span><br/><span data-ttu-id="b968a-309">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente</span><span class="sxs-lookup"><span data-stu-id="b968a-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="b968a-310">false</span><span class="sxs-lookup"><span data-stu-id="b968a-310">false</span></span> |<span data-ttu-id="b968a-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b968a-311">preserveHierarchy</span></span> |<span data-ttu-id="b968a-312">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="b968a-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b968a-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-313">Folder1</span></span><br/><span data-ttu-id="b968a-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b968a-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b968a-320">la carpeta de destino Folder1 se crea con la estructura siguiente</span><span class="sxs-lookup"><span data-stu-id="b968a-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b968a-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-321">Folder1</span></span><br/><span data-ttu-id="b968a-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="b968a-324">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="b968a-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="b968a-325">false</span><span class="sxs-lookup"><span data-stu-id="b968a-325">false</span></span> |<span data-ttu-id="b968a-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b968a-326">flattenHierarchy</span></span> |<span data-ttu-id="b968a-327">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="b968a-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="b968a-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-328">Folder1</span></span><br/><span data-ttu-id="b968a-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b968a-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b968a-335">la carpeta de destino Folder1 se crea con la estructura siguiente</span><span class="sxs-lookup"><span data-stu-id="b968a-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b968a-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-336">Folder1</span></span><br/><span data-ttu-id="b968a-337">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="b968a-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b968a-338">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="b968a-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="b968a-339">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="b968a-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="b968a-340">false</span><span class="sxs-lookup"><span data-stu-id="b968a-340">false</span></span> |<span data-ttu-id="b968a-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b968a-341">mergeFiles</span></span> |<span data-ttu-id="b968a-342">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="b968a-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="b968a-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-343">Folder1</span></span><br/><span data-ttu-id="b968a-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b968a-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b968a-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b968a-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b968a-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b968a-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b968a-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b968a-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b968a-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b968a-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b968a-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b968a-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b968a-350">la carpeta de destino Folder1 se crea con la estructura siguiente</span><span class="sxs-lookup"><span data-stu-id="b968a-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b968a-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="b968a-351">Folder1</span></span><br/><span data-ttu-id="b968a-352">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b968a-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="b968a-353">Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="b968a-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="b968a-354">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="b968a-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="b968a-355">Tutorial: Uso del Asistente para copia para copiar datos a y desde Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b968a-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="b968a-356">Vamos a ver cómo copiar rápidamente datos a y desde una instancia de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="b968a-357">En este tutorial, los almacenes de datos de origen y destino son de tipo: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="b968a-358">La canalización en este tutorial copia datos de una carpeta a otra carpeta en el mismo contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="b968a-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="b968a-359">Este tutorial es sencillo a propósito para mostrar sus valores de configuración o propiedades al usar Blob Storage como origen o receptor.</span><span class="sxs-lookup"><span data-stu-id="b968a-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="b968a-360">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b968a-360">Prerequisites</span></span>
1. <span data-ttu-id="b968a-361">Si aún no tiene una, cree una **cuenta de Azure Storage** de uso general.</span><span class="sxs-lookup"><span data-stu-id="b968a-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="b968a-362">En este tutorial usará el almacenamiento de blobs como almacén de datos de **origen** y **destino**.</span><span class="sxs-lookup"><span data-stu-id="b968a-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="b968a-363">Si no tiene una cuenta de Almacenamiento de Azure, consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para ver los pasos para su creación.</span><span class="sxs-lookup"><span data-stu-id="b968a-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="b968a-364">Cree un contenedor de blobs denominado **adfblobconnector** en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b968a-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="b968a-365">Cree una carpeta denominada **entrada** en el contenedor **adfblobconnector**.</span><span class="sxs-lookup"><span data-stu-id="b968a-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="b968a-366">Cree un archivo denominado **emp.txt** con el siguiente contenido y cárguelo en la carpeta **entrada** mediante herramientas como el [Explorador de Azure Storage](https://azurestorageexplorer.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="b968a-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="b968a-367">Creación de la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="b968a-367">Create the data factory</span></span>
1. <span data-ttu-id="b968a-368">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b968a-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b968a-369">Haga clic en **+ NUEVO** en la esquina superior izquierda, después en **Inteligencia y análisis** y en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="b968a-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="b968a-370">En la hoja **Nueva factoría de datos** :</span><span class="sxs-lookup"><span data-stu-id="b968a-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="b968a-371">Escriba **ADFBlobConnectorDF** como **nombre**.</span><span class="sxs-lookup"><span data-stu-id="b968a-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="b968a-372">El nombre del generador de datos de Azure debe ser único global.</span><span class="sxs-lookup"><span data-stu-id="b968a-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="b968a-373">Si recibe el siguiente error: `*Data factory name “ADFBlobConnectorDF” is not available`, cambie el nombre de la factoría de datos (por ejemplo, yournameADFBlobConnectorDF) e intente crearla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b968a-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="b968a-374">Consulte el tema [Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para conocer las reglas de nomenclatura para los artefactos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b968a-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="b968a-375">Selección la **suscripción**de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="b968a-376">Para Grupo de recursos, seleccione **Usar el existente** para seleccionar un grupo de recursos existente (o) seleccione **Crear nuevo** para escribir un nombre para un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b968a-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="b968a-377">Seleccione una **ubicación** para la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="b968a-378">Seleccione la casilla **Anclar al panel** en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="b968a-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="b968a-379">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b968a-379">Click **Create**.</span></span>
3. <span data-ttu-id="b968a-380">Una vez finalizada la creación, puede ver la hoja **Data Factory** como se muestra en la siguiente imagen: ![página principal de Data Factory](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="b968a-381">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="b968a-381">Copy Wizard</span></span>
1. <span data-ttu-id="b968a-382">En la página principal de Data Factory, haga clic en el icono **Copy data [PREVIEW]** (Copiar datos) [versión preliminar] para iniciar el **Asistente para copia de datos** en una pestaña aparte.</span><span class="sxs-lookup"><span data-stu-id="b968a-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="b968a-383">Si ve que el explorador web está atascado en "Autorizando...", deshabilite o desactive la opción **Block third-party cookies and site data** (Bloquear cookies y datos de sitios de terceros) o déjela habilitada y cree una excepción para **login.microsoftonline.com** e intente volver a iniciar el asistente.</span><span class="sxs-lookup"><span data-stu-id="b968a-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="b968a-384">En la página **Propiedades** :</span><span class="sxs-lookup"><span data-stu-id="b968a-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="b968a-385">Escriba **CopyPipeline** en **Task name** (Nombre de tarea).</span><span class="sxs-lookup"><span data-stu-id="b968a-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="b968a-386">El nombre de la tarea es el nombre de la canalización de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="b968a-387">Escriba una **descripción** para la tarea (opcional).</span><span class="sxs-lookup"><span data-stu-id="b968a-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="b968a-388">En **Task cadence or Task schedule** (Cadencia de tareas o programación de tareas), mantenga la opción **Run regularly on schedule** (Copiar datos periódicamente según programación).</span><span class="sxs-lookup"><span data-stu-id="b968a-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="b968a-389">Si quiere ejecutar esta tarea solo una vez en lugar de ejecutarla varias veces según una programación, seleccione **Run once now** (Ejecutar una vez ahora).</span><span class="sxs-lookup"><span data-stu-id="b968a-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="b968a-390">Si selecciona la opción **Run once now** (Ejecutar una vez ahora), se crea una [canalización única](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b968a-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="b968a-391">Conserve el valor de configuración de **Recurring pattern** (Patrón de repetición).</span><span class="sxs-lookup"><span data-stu-id="b968a-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="b968a-392">Esta tarea se ejecuta diariamente entre las horas de inicio y finalización que especifique en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="b968a-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="b968a-393">Cambie la **fecha y hora de inicio** a **04/21/2017**.</span><span class="sxs-lookup"><span data-stu-id="b968a-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="b968a-394">Cambie la **fecha y hora de finalización** a **04/25/2017**.</span><span class="sxs-lookup"><span data-stu-id="b968a-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="b968a-395">Puede escribir la fecha en lugar de buscarla en el calendario.</span><span class="sxs-lookup"><span data-stu-id="b968a-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="b968a-396">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b968a-396">Click **Next**.</span></span>
      <span data-ttu-id="b968a-397">![Herramienta de copia: Página de propiedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="b968a-398">En la página **Almacén de datos de origen**, haga clic en el icono **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="b968a-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="b968a-399">Use esta página para especificar el almacén de datos de origen para la tarea de copia.</span><span class="sxs-lookup"><span data-stu-id="b968a-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="b968a-400">Puede usar un servicio vinculado del almacén de datos existente, o bien especificar un almacén de datos nuevo.</span><span class="sxs-lookup"><span data-stu-id="b968a-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="b968a-401">Para usar un servicio vinculado existente, seleccionaría **FROM EXISTING LINKED SERVICES** (DE SERVICIOS VINCULADOS EXISTENTES) y luego el servicio vinculado correcto.</span><span class="sxs-lookup"><span data-stu-id="b968a-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="b968a-402">![Herramienta de copia: Página de almacén de datos de origen](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="b968a-403">En la página **Especificar cuenta de Almacenamiento de blobs de Azure** :</span><span class="sxs-lookup"><span data-stu-id="b968a-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="b968a-404">En **Nombre de la conexión**, mantenga el nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b968a-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="b968a-405">El nombre de conexión es el nombre del servicio vinculado de tipo: Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b968a-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="b968a-406">Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="b968a-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="b968a-407">Seleccione la suscripción de Azure o mantenga **Seleccionar todo** para **Suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b968a-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="b968a-408">Seleccione una **cuenta de Azure Storage** en la lista de cuentas de Azure Storage disponibles en la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b968a-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="b968a-409">También puede elegir especificar la configuración de la cuenta de almacenamiento manualmente, para lo que debe seleccionar la opción **Enter manually** (Especificar manualmente) en **Account selection method** (Método de selección de cuenta).</span><span class="sxs-lookup"><span data-stu-id="b968a-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="b968a-410">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="b968a-410">Click **Next**.</span></span> 
      <span data-ttu-id="b968a-411">![Herramienta de copia: Especificación de la cuenta de Azure Blob Storage](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="b968a-412">En la página **Elegir el archivo o la carpeta de entrada** :</span><span class="sxs-lookup"><span data-stu-id="b968a-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="b968a-413">Haga doble clic en **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="b968a-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="b968a-414">Seleccione **entrada** y haga clic en **Elegir**.</span><span class="sxs-lookup"><span data-stu-id="b968a-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="b968a-415">En este tutorial, seleccionará la carpeta de entrada.</span><span class="sxs-lookup"><span data-stu-id="b968a-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="b968a-416">También podría seleccionar en su lugar el archivo emp.txt de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="b968a-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="b968a-417">![Herramienta de copia: Selección del archivo o la carpeta de entrada](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="b968a-418">En la página **Choose the input file or folder** (Elegir el archivo o la carpeta de entrada):</span><span class="sxs-lookup"><span data-stu-id="b968a-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="b968a-419">Confirme que el **archivo o la carpeta** están establecidos en **adfblobconnector/entrada**.</span><span class="sxs-lookup"><span data-stu-id="b968a-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="b968a-420">Si los archivos se encuentran en subcarpetas, por ejemplo, 2017/04/01, 2017/04/02, etc., escriba adfblobconnector/entrada/{año}/{mes}/{día} para el archivo o la carpeta.</span><span class="sxs-lookup"><span data-stu-id="b968a-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="b968a-421">Al presionar la tecla de tabulación fuera del cuadro de texto, verá tres listas desplegables para seleccionar el formato de año (aaaa), meso (MM) y día (dd).</span><span class="sxs-lookup"><span data-stu-id="b968a-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="b968a-422">No marque la casilla **Copy file recursively** (Copiar archivo de forma recursiva).</span><span class="sxs-lookup"><span data-stu-id="b968a-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="b968a-423">Seleccione esta opción para recorrer las carpetas de forma recursiva para encontrar los archivos que se van a copiar en el destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="b968a-424">No marque la opción **Binary copy** (Copia binaria).</span><span class="sxs-lookup"><span data-stu-id="b968a-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="b968a-425">Seleccione esta opción para realizar una copia binaria del archivo de origen en el destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="b968a-426">No la seleccione para este tutorial, así podrá ver más opciones en las páginas siguientes.</span><span class="sxs-lookup"><span data-stu-id="b968a-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="b968a-427">Confirme que **Compression type** (Tipo de compresión) está establecido en **Ninguno**.</span><span class="sxs-lookup"><span data-stu-id="b968a-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="b968a-428">Seleccione un valor para esta opción si sus archivos de origen están comprimidos en uno de los formatos admitidos.</span><span class="sxs-lookup"><span data-stu-id="b968a-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="b968a-429">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="b968a-429">Click **Next**.</span></span>
    <span data-ttu-id="b968a-430">![Herramienta de copia: Selección del archivo o la carpeta de entrada](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="b968a-431">En la página **Configuración de formato de archivo**, verá los delimitadores y el esquema que el asistente detecta automáticamente al analizar el archivo.</span><span class="sxs-lookup"><span data-stu-id="b968a-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="b968a-432">Confirme las siguientes opciones: a.</span><span class="sxs-lookup"><span data-stu-id="b968a-432">Confirm the following options: a.</span></span> <span data-ttu-id="b968a-433">El **formato de archivo** está establecido en **Formato de texto**.</span><span class="sxs-lookup"><span data-stu-id="b968a-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="b968a-434">Puede ver todos los formatos admitidos en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b968a-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="b968a-435">Por ejemplo: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="b968a-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="b968a-436">b.</span><span class="sxs-lookup"><span data-stu-id="b968a-436">b.</span></span> <span data-ttu-id="b968a-437">El **delimitador de columnas** está establecido en `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="b968a-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="b968a-438">Puede ver los demás delimitadores de columna compatibles Data Factory en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b968a-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="b968a-439">También puede especificar un delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="b968a-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="b968a-440">c.</span><span class="sxs-lookup"><span data-stu-id="b968a-440">c.</span></span> <span data-ttu-id="b968a-441">El **delimitador de filas** está establecido en `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="b968a-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="b968a-442">Puede ver los otros delimitadores de fila admitidos por Data Factory en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b968a-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="b968a-443">También puede especificar un delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="b968a-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="b968a-444">d.</span><span class="sxs-lookup"><span data-stu-id="b968a-444">d.</span></span> <span data-ttu-id="b968a-445">El **número de líneas que se omiten** está establecido en **0**.</span><span class="sxs-lookup"><span data-stu-id="b968a-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="b968a-446">Si quiere que se omitan algunas líneas al principio del archivo, escriba aquí el número.</span><span class="sxs-lookup"><span data-stu-id="b968a-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="b968a-447">e.</span><span class="sxs-lookup"><span data-stu-id="b968a-447">e.</span></span>  <span data-ttu-id="b968a-448">La casilla **first data row contains column names** (La primera fila de datos contiene nombres de columna) no esta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b968a-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="b968a-449">Si los archivos de origen contienen nombres de columna en la primera fila, seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="b968a-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="b968a-450">f.</span><span class="sxs-lookup"><span data-stu-id="b968a-450">f.</span></span> <span data-ttu-id="b968a-451">La opción **treat empty column value as null** (Tratar el valor de columna vacío como null) está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b968a-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="b968a-452">Expanda **Configuración avanzada** para ver las opciones avanzadas disponibles.</span><span class="sxs-lookup"><span data-stu-id="b968a-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="b968a-453">En la parte inferior de la página, obtenga la **vista previa** de datos del archivo emp.txt.</span><span class="sxs-lookup"><span data-stu-id="b968a-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="b968a-454">Haga clic en la pestaña **ESQUEMA** en la parte inferior para ver el esquema que dedujo el Asistente para copia examinando los datos del archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="b968a-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="b968a-455">Haga clic en **Siguiente** después de revisar los delimitadores y obtener una vista previa de los datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="b968a-456">![Herramienta de copia: Configuración de formato de archivo](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="b968a-457">En la página **Destination data store** (Almacén de datos de destino), seleccione **Azure Blob Storage** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b968a-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="b968a-458">En este tutorial usará Azure Blob Storage como almacén de datos de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="b968a-459">![Herramienta de copia: Selección del almacén de datos de destino](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="b968a-460">En la página **Specify the Azure Blob storage account** (Especificar cuenta de Azure Blob Storage):</span><span class="sxs-lookup"><span data-stu-id="b968a-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="b968a-461">Escriba **AzureStorageLinkedService** en el campo **Nombre de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="b968a-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="b968a-462">Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="b968a-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="b968a-463">Selección la **suscripción**de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="b968a-464">Seleccione su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="b968a-465">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="b968a-465">Click **Next**.</span></span>     
10. <span data-ttu-id="b968a-466">En la página **Choose the output file or folder** (Elegir el archivo o la carpeta de salida):</span><span class="sxs-lookup"><span data-stu-id="b968a-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="b968a-467">Especifique la **ruta de acceso de carpeta** como **adfblobconnector/output/{year}/{month}/{day}**.</span><span class="sxs-lookup"><span data-stu-id="b968a-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="b968a-468">Escriba **TAB**.</span><span class="sxs-lookup"><span data-stu-id="b968a-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="b968a-469">Para el **año**, seleccione **aaaa**.</span><span class="sxs-lookup"><span data-stu-id="b968a-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="b968a-470">Para el **mes**, confirme que está configurado como **MM**.</span><span class="sxs-lookup"><span data-stu-id="b968a-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="b968a-471">Para el **día**, confirme que está configurado como **dd**.</span><span class="sxs-lookup"><span data-stu-id="b968a-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="b968a-472">Confirme que **Compression type** (Tipo de compresión) está establecido en **Ninguno**.</span><span class="sxs-lookup"><span data-stu-id="b968a-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="b968a-473">Confirme que el **comportamiento de copia** está establecido en **Merge files** (Combinar archivos).</span><span class="sxs-lookup"><span data-stu-id="b968a-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="b968a-474">Si ya existe un archivo de salida con el mismo nombre, el nuevo contenido se agrega al final al mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="b968a-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="b968a-475">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b968a-475">Click **Next**.</span></span>
    <span data-ttu-id="b968a-476">![Herramienta de copia: Selección del archivo o la carpeta de salida](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="b968a-477">En la página **File format settings** (Configuración de formato de archivo), revise la configuración y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b968a-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="b968a-478">Una de las opciones adicionales aquí es agregar un encabezado al archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="b968a-479">Si selecciona esta opción, se agrega una fila de encabezado con nombres de las columnas del esquema de origen.</span><span class="sxs-lookup"><span data-stu-id="b968a-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="b968a-480">Puede cambiar los nombres de columna predeterminados al visualizar el esquema para el origen.</span><span class="sxs-lookup"><span data-stu-id="b968a-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="b968a-481">Por ejemplo, podría cambiar la primera columna a Nombre y la segunda columna a Apellido.</span><span class="sxs-lookup"><span data-stu-id="b968a-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="b968a-482">El archivo de salida se genera entonces con un encabezado con estos nombres como nombres de columna.</span><span class="sxs-lookup"><span data-stu-id="b968a-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="b968a-483">![Herramienta de copia: Configuración del formato de archivo de destino](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="b968a-484">En la página **Performance settings** (Configuración de rendimiento), confirme que **cloud units** (Unidades de nube) y **parallel copies** (Copias paralelas) están establecidas en **Auto** y haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="b968a-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="b968a-485">Para más información sobre esta configuración, consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="b968a-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="b968a-486">![Herramienta de copia: Configuración de rendimiento](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="b968a-487">En la página **Resumen**, revise toda la configuración (propiedades de tareas, configuración de origen y destino y configuración de copia) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b968a-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="b968a-488">![Herramienta de copia: Página de resumen](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="b968a-489">Revise la información de la página **Resumen** y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="b968a-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="b968a-490">El asistente crea dos servicios vinculados, dos conjuntos de datos (entrada y salida) y una canalización en la factoría de datos (desde donde se inició al Asistente para copia).</span><span class="sxs-lookup"><span data-stu-id="b968a-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="b968a-491">![Herramienta de copia: Página de implementación](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="b968a-492">Supervisión de la canalización (tarea de copia)</span><span class="sxs-lookup"><span data-stu-id="b968a-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="b968a-493">Haga clic en el vínculo `Click here to monitor copy pipeline` de la página **Implementación**.</span><span class="sxs-lookup"><span data-stu-id="b968a-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="b968a-494">Verá la opción **Monitor and Manage application** (Supervisar y administrar la aplicación) en una pestaña aparte.  ![Supervisar y administrar la aplicación](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="b968a-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="b968a-495">Cambie la hora de **inicio** de la parte superior a `04/19/2017` y la hora de **finalización** a `04/27/2017`; a continuación, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b968a-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="b968a-496">Verá cinco ventanas de actividad en la lista **ACTIVITY WINDOWS** (VENTANAS DE ACTIVIDAD).</span><span class="sxs-lookup"><span data-stu-id="b968a-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="b968a-497">Las horas de **WindowStart** deben abarcar todos los días desde las horas de inicio hasta las horas de finalización de la canalización.</span><span class="sxs-lookup"><span data-stu-id="b968a-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="b968a-498">Haga clic en el botón **Actualizar** de la lista **ACTIVITY WINDOWS** (VENTANAS DE ACTIVIDAD) unas cuantas veces hasta que vea el estado de todas las ventanas de actividad establecido en Listo.</span><span class="sxs-lookup"><span data-stu-id="b968a-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="b968a-499">Ahora, compruebe que los archivos de salida se generan en la carpeta de salida del contenedor adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="b968a-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="b968a-500">Verá la siguiente estructura de carpetas en la carpeta de salida:</span><span class="sxs-lookup"><span data-stu-id="b968a-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="b968a-501">Para más información sobre la supervisión y administración de factorías de datos, consulte el artículo [Supervisión y administración de canalizaciones de Data Factory](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="b968a-502">Entidades de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="b968a-502">Data Factory entities</span></span>
<span data-ttu-id="b968a-503">Ahora, vuelva a la pestaña con la página principal de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b968a-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="b968a-504">Observe que ahora hay en su factoría de datos dos servicios vinculados, dos conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="b968a-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Página principal de Data Factory con entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="b968a-506">Haga clic en **Author and deploy** (Crear e implementar) para iniciar Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="b968a-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Editor de la Factoría de datos](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="b968a-508">Verá las siguientes entidades de Data Factory en su factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="b968a-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="b968a-509">Dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="b968a-509">Two linked services.</span></span> <span data-ttu-id="b968a-510">Uno para el origen y el otro para el destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="b968a-511">Ambos servicios vinculados hacen referencia a la misma cuenta de Azure Storage de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b968a-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="b968a-512">Dos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="b968a-512">Two datasets.</span></span> <span data-ttu-id="b968a-513">Un conjunto de datos de entrada y un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="b968a-514">En este tutorial, ambos usan el mismo contenedor de blobs, pero hacen referencia a carpetas diferentes (entrada y salida).</span><span class="sxs-lookup"><span data-stu-id="b968a-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="b968a-515">Una canalización.</span><span class="sxs-lookup"><span data-stu-id="b968a-515">A pipeline.</span></span> <span data-ttu-id="b968a-516">La canalización contiene una actividad de copia que usa un origen de blob y un receptor de blob para copiar datos entre ubicaciones de blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="b968a-517">En las secciones siguientes se proporciona más información sobre estas entidades.</span><span class="sxs-lookup"><span data-stu-id="b968a-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="b968a-518">Servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="b968a-518">Linked services</span></span>
<span data-ttu-id="b968a-519">Verá dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="b968a-519">You should see two linked services.</span></span> <span data-ttu-id="b968a-520">Uno para el origen y el otro para el destino.</span><span class="sxs-lookup"><span data-stu-id="b968a-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="b968a-521">En este tutorial, ambas definiciones parecen las mismas, si exceptuamos los nombres.</span><span class="sxs-lookup"><span data-stu-id="b968a-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="b968a-522">El **tipo** del servicio vinculado se establece en **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="b968a-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="b968a-523">La propiedad más importante de la definición del servicio vinculado es **connectionString**, que se usa en Data Factory para la conexión a la cuenta de Azure Storage en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b968a-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="b968a-524">Omita la propiedad hubName en la definición.</span><span class="sxs-lookup"><span data-stu-id="b968a-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="b968a-525">Servicio vinculado de almacenamiento de blobs de origen</span><span class="sxs-lookup"><span data-stu-id="b968a-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="b968a-526">Servicio vinculado de almacenamiento de blobs de destino</span><span class="sxs-lookup"><span data-stu-id="b968a-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="b968a-527">Para más información sobre el servicio vinculado Azure Storage, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="b968a-528">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="b968a-528">Datasets</span></span>
<span data-ttu-id="b968a-529">Hay dos conjuntos de datos: un conjunto de datos de entrada y un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="b968a-530">El tipo del conjunto de datos está establecido en **AzureBlob** para ambos.</span><span class="sxs-lookup"><span data-stu-id="b968a-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="b968a-531">El conjunto de datos de entrada apunta a la carpeta **entrada** del contenedor de blobs **adfblobconnector**.</span><span class="sxs-lookup"><span data-stu-id="b968a-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="b968a-532">La propiedad **external** está establecida en **true** para este conjunto de datos ya que los datos no se generan mediante la canalización con la actividad de copia que toma este conjunto de datos como entrada.</span><span class="sxs-lookup"><span data-stu-id="b968a-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="b968a-533">El conjunto de datos de salida apunta a la carpeta **salida** del mismo contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="b968a-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="b968a-534">También usa el año, mes y día de la variable del sistema **SliceStart** para evaluar de forma dinámica la ruta de acceso del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="b968a-535">Para ver la lista de funciones y variables del sistema que admite Data Factory, consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="b968a-536">La propiedad **external** está establecida en **false** (valor predeterminado) porque este conjunto de datos lo genera la canalización.</span><span class="sxs-lookup"><span data-stu-id="b968a-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="b968a-537">Para más información sobre las propiedades admitidas por el conjunto de datos de blob de Azure, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="b968a-538">Conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="b968a-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="b968a-539">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="b968a-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="b968a-540">Canalización</span><span class="sxs-lookup"><span data-stu-id="b968a-540">Pipeline</span></span>
<span data-ttu-id="b968a-541">La canalización tiene una sola actividad.</span><span class="sxs-lookup"><span data-stu-id="b968a-541">The pipeline has just one activity.</span></span> <span data-ttu-id="b968a-542">El **tipo** de la actividad se establece en **Copia**.</span><span class="sxs-lookup"><span data-stu-id="b968a-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="b968a-543">En las propiedades de tipo de la actividad, hay dos secciones, una para el origen y otra para el receptor.</span><span class="sxs-lookup"><span data-stu-id="b968a-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="b968a-544">El tipo de origen se establece en **BlobSource** ya que la actividad es copiar datos de un almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b968a-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="b968a-545">El tipo de receptor se establece en **BlobSink** ya que la actividad es copiar datos en un almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b968a-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="b968a-546">La actividad de copia toma InputDataset z4y como entrada y OutputDataset-z4y como salida.</span><span class="sxs-lookup"><span data-stu-id="b968a-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="b968a-547">Para más información sobre las propiedades admitidas por BlobSource y BlobSink, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="b968a-548">Ejemplos de JSON para copiar datos hacia y desde Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b968a-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="b968a-549">En los siguientes ejemplos se proporcionan definiciones JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b968a-550">Muestran cómo copiar datos entre el Almacenamiento de blobs de Azure y la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="b968a-551">Sin embargo, los datos se pueden copiar **directamente** de cualquiera de los orígenes a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="b968a-552">Ejemplo de JSON: Copia de datos de Blob Storage a SQL Database</span><span class="sxs-lookup"><span data-stu-id="b968a-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="b968a-553">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="b968a-553">The following sample shows:</span></span>

1. <span data-ttu-id="b968a-554">Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="b968a-555">Un servicio vinculado de tipo [AzureStorage](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b968a-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="b968a-556">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="b968a-557">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b968a-558">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [BlobSource](#copy-activity-properties) y [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b968a-559">El ejemplo copia los datos de la serie temporal desde un blob de Azure a una tabla de SQL de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="b968a-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="b968a-560">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="b968a-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b968a-561">**Servicio vinculado SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-561">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="b968a-562">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="b968a-563">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="b968a-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="b968a-564">En el primer caso, especifique la cadena de conexión que incluye la clave de cuenta. En el segundo, especifique el Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="b968a-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="b968a-565">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="b968a-566">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="b968a-567">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="b968a-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b968a-568">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="b968a-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b968a-569">La ruta de acceso de la carpeta usa la parte year, month y day de la hora de inicio y el nombre de archivo, la parte hour.</span><span class="sxs-lookup"><span data-stu-id="b968a-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="b968a-570">El valor "external": "true" informa a Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="b968a-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="b968a-571">**Conjunto de datos de salida SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="b968a-572">El ejemplo copia los datos a una tabla denominada "MyTable" en una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="b968a-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="b968a-573">Cree la tabla en la Base de datos SQL de Azure con el mismo número de columnas que espera que contenga el archivo CSV de blob.</span><span class="sxs-lookup"><span data-stu-id="b968a-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="b968a-574">Se agregan nuevas filas a la tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="b968a-574">New rows are added to the table every hour.</span></span>

```json
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
<span data-ttu-id="b968a-575">**Una actividad de copia en una canalización con el origen de blob y el receptor SQL:**</span><span class="sxs-lookup"><span data-stu-id="b968a-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="b968a-576">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="b968a-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b968a-577">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="b968a-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
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
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="b968a-578">Ejemplo de JSON: Copia de datos de Azure SQL a Azure Blob</span><span class="sxs-lookup"><span data-stu-id="b968a-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="b968a-579">El ejemplo siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="b968a-579">The following sample shows:</span></span>

1. <span data-ttu-id="b968a-580">Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="b968a-581">Un servicio vinculado de tipo [AzureStorage](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b968a-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="b968a-582">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b968a-583">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="b968a-584">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) y [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b968a-585">El ejemplo copia los datos de la serie temporal desde una tabla de SQL de Azure a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="b968a-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="b968a-586">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="b968a-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b968a-587">**Servicio vinculado SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-587">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="b968a-588">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="b968a-589">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="b968a-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="b968a-590">En el primer caso, especifique la cadena de conexión que incluye la clave de cuenta. En el segundo, especifique el Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="b968a-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="b968a-591">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b968a-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="b968a-592">**Conjunto de datos de entrada SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="b968a-593">El ejemplo supone que ha creado una tabla "MyTable" en SQL de Azure y que contiene una columna denominada "timestampcolumn" para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="b968a-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="b968a-594">Si se establece "external": "true", se informa al servicio Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="b968a-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
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

<span data-ttu-id="b968a-595">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="b968a-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b968a-596">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="b968a-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b968a-597">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="b968a-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b968a-598">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="b968a-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="b968a-599">**Actividad de copia en una canalización con el origen SQL y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="b968a-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="b968a-600">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="b968a-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b968a-601">En la definición de la canalización JSON, el tipo **source** se establece en **SqlSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b968a-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b968a-602">La consulta SQL especificada para la propiedad **SqlReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="b968a-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
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

> [!NOTE]
> <span data-ttu-id="b968a-603">Para asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte el artículo sobre la [asignación de columnas de conjuntos de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b968a-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b968a-604">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="b968a-604">Performance and Tuning</span></span>
<span data-ttu-id="b968a-605">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="b968a-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
