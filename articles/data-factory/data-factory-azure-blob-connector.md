---
title: datos de aaaCopy hacia/desde el almacenamiento de blobs de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy blob datos en Data Factory de Azure. Utilice nuestro ejemplo: cómo toocopy tooand de datos de almacenamiento de blobs de Azure y base de datos de SQL Azure."
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
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="50031-105">Copiar datos tooor de almacenamiento de blobs de Azure mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="50031-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="50031-106">Este artículo explica cómo toouse Hola actividad de copia de Data Factory de Azure toocopy datos tooand desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="50031-107">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="50031-108">Información general</span><span class="sxs-lookup"><span data-stu-id="50031-108">Overview</span></span>
<span data-ttu-id="50031-109">Puede copiar datos desde cualquier origen compatible almacenan tooAzure almacenamiento de blobs de datos o de datos de receptor de almacenamiento de blobs de Azure tooany admitida almacenan.</span><span class="sxs-lookup"><span data-stu-id="50031-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="50031-110">Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes o receptores de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="50031-111">Por ejemplo, puede mover datos **de** una base de datos SQL Server o una base de datos Azure SQL **a** una instancia de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="50031-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="50031-112">Y, puede copiar datos **desde** Azure Blob Storage **hacia** una instancia de Azure SQL Data Warehouse o una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="50031-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="50031-113">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="50031-113">Supported scenarios</span></span>
<span data-ttu-id="50031-114">Puede copiar datos **desde el almacenamiento de blobs de Azure** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="50031-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="50031-115">Puede copiar los datos de hello siguientes almacenes de datos **tooAzure almacenamiento de blobs**:</span><span class="sxs-lookup"><span data-stu-id="50031-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="50031-116">Actividad de copia es compatible con copia de datos de / tooboth cuentas de almacenamiento de Azure general y estrechamente/estupendo almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="50031-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="50031-117">admite la actividad Hello **leyendo de bloque, anexar o blobs en páginas**, pero es compatible con **escritura de blobs en bloques tooonly**.</span><span class="sxs-lookup"><span data-stu-id="50031-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="50031-118">Azure Premium Storage no es compatible como receptor porque está respaldado por blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="50031-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="50031-119">Actividad de copia no elimina datos de origen de hello después Hola datos están correctamente copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="50031-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="50031-120">Si necesita datos de origen de toodelete después de una copia correcta, cree un [actividad personalizada](data-factory-use-custom-activities.md) toodelete Hola datos y usar actividad hello en canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="50031-121">Para obtener un ejemplo, vea hello [ejemplo de Delete blob o una carpeta en GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="50031-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="50031-122">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="50031-122">Get started</span></span>
<span data-ttu-id="50031-123">Puede crear una canalización con actividad de copia que mueva los datos desde Azure Blob Storage o hacia él mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="50031-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="50031-124">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="50031-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="50031-125">Este artículo tiene un [tutorial](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para crear una canalización de datos de toocopy de un tooanother de ubicación de almacenamiento de blobs de Azure ubicación de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="50031-126">Para obtener un tutorial sobre cómo crear un toocopy de datos de canalización desde una base de datos SQL de tooAzure de almacenamiento de blobs de Azure, consulte [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="50031-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="50031-127">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="50031-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="50031-128">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="50031-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="50031-129">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="50031-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="50031-130">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="50031-130">Create a **data factory**.</span></span> <span data-ttu-id="50031-131">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="50031-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="50031-132">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="50031-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="50031-133">Por ejemplo, si va a copiar datos desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="50031-134">Para las propiedades de servicio vinculado que son específico tooAzure almacenamiento de blobs, vea [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="50031-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="50031-135">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="50031-136">En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="50031-137">Y crear tabla de otro conjunto de datos toospecify Hola SQL en la base de datos de SQL Azure de Hola que contiene los datos de hello copiados desde el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="50031-138">Para las propiedades del conjunto de datos que son específico tooAzure almacenamiento de blobs, vea [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="50031-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="50031-139">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="50031-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="50031-140">En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y SqlSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="50031-141">De forma similar, si va a copiar desde la base de datos de SQL Azure tooAzure almacenamiento de blobs, utilice SqlSource y BlobSink en la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="50031-142">Para copiar propiedades de actividad que son específico tooAzure almacenamiento de blobs, vea [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="50031-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="50031-143">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="50031-144">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="50031-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="50031-145">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="50031-146">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde un almacenamiento de blobs de Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="50031-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="50031-147">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="50031-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="50031-148">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="50031-148">Linked service properties</span></span>
<span data-ttu-id="50031-149">Hay dos tipos de servicios vinculados que se puede usar toolink un generador de datos de Azure de tooan de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="50031-150">Se trata del servicio vinculado **AzureStorage** y el servicio vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="50031-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="50031-151">Hola servicio vinculado de almacenamiento de Azure proporciona factoría de datos de hello con acceso global toohello almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="50031-152">Mientras que vinculado hello Azure almacenamiento SAS (firma de acceso compartido) servicio proporciona factoría de datos de hello con acceso restringido tiempo enlazadas toohello almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="50031-153">No existen otras diferencias entre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="50031-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="50031-154">Elegir servicio de hello vinculado que se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="50031-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="50031-155">Hello las secciones siguientes proporcionan más detalles sobre estos dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="50031-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="50031-156">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="50031-156">Dataset properties</span></span>
<span data-ttu-id="50031-157">toospecify un conjunto de datos toorepresent datos de entrada o salidas de un almacenamiento de blobs de Azure, Establece Hola de propiedad de tipo de conjunto de datos de Hola para: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="50031-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="50031-158">Conjunto hello **linkedServiceName** servicio vinculado de propiedad del nombre de toohello de conjunto de datos de Hola de hello almacenamiento de Azure o SAS de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="50031-159">propiedades de tipo Hello del conjunto de datos de hello especifican hello **contenedor de blobs** hello y **carpeta** Hola almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="50031-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="50031-160">Para obtener una lista completa de secciones JSON y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="50031-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="50031-161">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="50031-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="50031-162">Factoría de datos admite Hola después de valores de tipo conforme a CLS .NET según para proporcionar información de tipo en "estructura" para orígenes de datos de lectura de esquema como blobs de Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="50031-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="50031-163">Factoría de datos realiza automáticamente las conversiones de tipos al mover el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="50031-164">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y se proporciona información acerca de la ubicación de hello, etc., formato de datos de hello en el almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="50031-165">sección typeProperties Hello para el conjunto de datos de tipo **AzureBlob** conjunto de datos tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="50031-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="50031-166">Propiedad</span><span class="sxs-lookup"><span data-stu-id="50031-166">Property</span></span> | <span data-ttu-id="50031-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="50031-167">Description</span></span> | <span data-ttu-id="50031-168">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="50031-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50031-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="50031-169">folderPath</span></span> |<span data-ttu-id="50031-170">Contenedor de toohello de ruta de acceso y la carpeta en el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="50031-171">Ejemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="50031-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="50031-172">Sí</span><span class="sxs-lookup"><span data-stu-id="50031-172">Yes</span></span> |
| <span data-ttu-id="50031-173">fileName</span><span class="sxs-lookup"><span data-stu-id="50031-173">fileName</span></span> |<span data-ttu-id="50031-174">Nombre del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-174">Name of hello blob.</span></span> <span data-ttu-id="50031-175">La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="50031-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="50031-176">Si especifica un nombre de archivo, funciona de la actividad (incluida la copia) de hello en Hola Blob en cuestión.</span><span class="sxs-lookup"><span data-stu-id="50031-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="50031-177">Cuando no se especifica el nombre de archivo, copia incluye todos los Blobs en folderPath hello para el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="50031-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="50031-178">Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, nombre de hello del archivo hello genera sería Hola siguiendo este formato: datos.<Guid>. txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="50031-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="50031-179">No</span><span class="sxs-lookup"><span data-stu-id="50031-179">No</span></span> |
| <span data-ttu-id="50031-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="50031-180">partitionedBy</span></span> |<span data-ttu-id="50031-181">partitionedBy es una propiedad opcional.</span><span class="sxs-lookup"><span data-stu-id="50031-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="50031-182">Se pueden usar toospecify un folderPath dinámica y nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="50031-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="50031-183">Por ejemplo, se puede parametrizar folderPath por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="50031-184">Vea hello [mediante partitionedBy propiedad sección](#using-partitionedBy-property) para obtener información detallada y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="50031-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="50031-185">No</span><span class="sxs-lookup"><span data-stu-id="50031-185">No</span></span> |
| <span data-ttu-id="50031-186">formato</span><span class="sxs-lookup"><span data-stu-id="50031-186">format</span></span> | <span data-ttu-id="50031-187">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="50031-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="50031-188">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="50031-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="50031-189">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="50031-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="50031-190">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="50031-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="50031-191">No</span><span class="sxs-lookup"><span data-stu-id="50031-191">No</span></span> |
| <span data-ttu-id="50031-192">compresión</span><span class="sxs-lookup"><span data-stu-id="50031-192">compression</span></span> | <span data-ttu-id="50031-193">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="50031-194">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="50031-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="50031-195">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="50031-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="50031-196">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="50031-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="50031-197">No</span><span class="sxs-lookup"><span data-stu-id="50031-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="50031-198">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="50031-198">Using partitionedBy property</span></span>
<span data-ttu-id="50031-199">Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámica y el nombre de archivo de datos de serie temporal con hello **partitionedBy** propiedad, [funciones de factoría de datos y las variables del sistema hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="50031-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="50031-200">Para más información sobre los conjuntos de datos de series temporales, la programación y los segmentos, consulte los artículos [Creación de conjuntos de datos](data-factory-create-datasets.md) y [Programación y ejecución](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="50031-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="50031-201">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="50031-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="50031-202">En este ejemplo, {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart factoría de datos en formato de hello (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="50031-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="50031-203">Hola SliceStart refiere a tiempo toostart de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="50031-204">Hola folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="50031-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="50031-205">Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="50031-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="50031-206">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="50031-206">Sample 2</span></span>

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

<span data-ttu-id="50031-207">En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.</span><span class="sxs-lookup"><span data-stu-id="50031-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="50031-208">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="50031-208">Copy activity properties</span></span>
<span data-ttu-id="50031-209">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="50031-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="50031-210">Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="50031-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="50031-211">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="50031-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="50031-212">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="50031-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="50031-213">Si va a mover datos desde un almacenamiento de blobs de Azure, configure tipo de origen de hello en la actividad de copia de hello demasiado**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="50031-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="50031-214">De forma similar, si va a mover datos tooan almacenamiento de blobs de Azure, Establece el tipo de receptor de hello en actividad de copia de hello demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="50031-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="50031-215">Esta sección proporciona una lista de propiedades admitidas por BlobSource y BlobSink.</span><span class="sxs-lookup"><span data-stu-id="50031-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="50031-216">**BlobSource** admite Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="50031-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="50031-217">Propiedad</span><span class="sxs-lookup"><span data-stu-id="50031-217">Property</span></span> | <span data-ttu-id="50031-218">Descripción</span><span class="sxs-lookup"><span data-stu-id="50031-218">Description</span></span> | <span data-ttu-id="50031-219">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="50031-219">Allowed values</span></span> | <span data-ttu-id="50031-220">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="50031-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50031-221">recursive</span><span class="sxs-lookup"><span data-stu-id="50031-221">recursive</span></span> |<span data-ttu-id="50031-222">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="50031-223">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="50031-223">True (default value), False</span></span> |<span data-ttu-id="50031-224">No</span><span class="sxs-lookup"><span data-stu-id="50031-224">No</span></span> |

<span data-ttu-id="50031-225">**BlobSink** admite Hola propiedades siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="50031-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="50031-226">Propiedad</span><span class="sxs-lookup"><span data-stu-id="50031-226">Property</span></span> | <span data-ttu-id="50031-227">Descripción</span><span class="sxs-lookup"><span data-stu-id="50031-227">Description</span></span> | <span data-ttu-id="50031-228">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="50031-228">Allowed values</span></span> | <span data-ttu-id="50031-229">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="50031-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50031-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="50031-230">copyBehavior</span></span> |<span data-ttu-id="50031-231">Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="50031-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="50031-232"><b>PreserveHierarchy</b>: conserva Hola jerarquía de archivos en la carpeta de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="50031-233">ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="50031-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="50031-234"><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola están en hello primero niveles de carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="50031-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="50031-235">archivos de destino de Hello tienen nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="50031-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="50031-236"><b>MergeFiles</b>: combina todos los archivos del archivo de tooone de carpeta de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="50031-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="50031-237">Si se especifica Hola nombre de archivo o Blob, nombre de archivo combinado Hola sería Hola especificado de lo contrario, sería el nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="50031-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="50031-238">No</span><span class="sxs-lookup"><span data-stu-id="50031-238">No</span></span> |

<span data-ttu-id="50031-239">**BlobSource** también admite estas dos propiedades para ofrecer compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="50031-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="50031-240">**treatEmptyAsNull**: Especifica si una cadena nula o vacía tootreat como un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="50031-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="50031-241">**skipHeaderLineCount** : especifica cuántas líneas deben omitirse.</span><span class="sxs-lookup"><span data-stu-id="50031-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="50031-242">Es aplicable únicamente cuando el conjunto de datos de entrada usa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="50031-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="50031-243">De forma similar, **BlobSink** admite Hola después de propiedad para la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="50031-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="50031-244">**blobWriterAddHeader**: Especifica si el conjunto de datos de salida de un encabezado de definiciones de columna al escribir tooan tooadd.</span><span class="sxs-lookup"><span data-stu-id="50031-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="50031-245">Hola de conjuntos de datos ahora compatibilidad con propiedades que implementan siguientes Hola misma funcionalidad: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="50031-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="50031-246">Hello tabla siguiente proporciona orientación sobre el uso de propiedades de conjunto de datos nuevo hello en lugar de estas propiedades de origen/receptor de blob.</span><span class="sxs-lookup"><span data-stu-id="50031-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="50031-247">Propiedad de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="50031-247">Copy Activity property</span></span> | <span data-ttu-id="50031-248">Propiedad de conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="50031-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="50031-249">skipHeaderLineCount en BlobSource</span><span class="sxs-lookup"><span data-stu-id="50031-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="50031-250">skipLineCount y firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="50031-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="50031-251">Las líneas se omiten en primer lugar y, a continuación, se lee la primera fila de Hola como un encabezado.</span><span class="sxs-lookup"><span data-stu-id="50031-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="50031-252">treatEmptyAsNull en BlobSource</span><span class="sxs-lookup"><span data-stu-id="50031-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="50031-253">treatEmptyAsNull en el conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="50031-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="50031-254">blobWriterAddHeader en BlobSink</span><span class="sxs-lookup"><span data-stu-id="50031-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="50031-255">firstRowAsHeader en el conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="50031-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="50031-256">Consulte la sección [Especificación de TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) para obtener información detallada acerca de estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="50031-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="50031-257">Ejemplos de recursive y copyBehavior</span><span class="sxs-lookup"><span data-stu-id="50031-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="50031-258">Esta sección describe el comportamiento resultante de Hola de operación de copia de Hola para diferentes combinaciones de valores recursiva y copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="50031-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="50031-259">recursive</span><span class="sxs-lookup"><span data-stu-id="50031-259">recursive</span></span> | <span data-ttu-id="50031-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="50031-260">copyBehavior</span></span> | <span data-ttu-id="50031-261">Comportamiento resultante</span><span class="sxs-lookup"><span data-stu-id="50031-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50031-262">true</span><span class="sxs-lookup"><span data-stu-id="50031-262">true</span></span> |<span data-ttu-id="50031-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="50031-263">preserveHierarchy</span></span> |<span data-ttu-id="50031-264">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="50031-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-265">Folder1</span></span><br/><span data-ttu-id="50031-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="50031-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="50031-272">se crea la carpeta de destino de Hello carpeta1 con hello misma estructura como origen de Hola</span><span class="sxs-lookup"><span data-stu-id="50031-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="50031-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-273">Folder1</span></span><br/><span data-ttu-id="50031-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="50031-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="50031-280">true</span><span class="sxs-lookup"><span data-stu-id="50031-280">true</span></span> |<span data-ttu-id="50031-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="50031-281">flattenHierarchy</span></span> |<span data-ttu-id="50031-282">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="50031-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-283">Folder1</span></span><br/><span data-ttu-id="50031-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="50031-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="50031-290">se crea el destino de Hola carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="50031-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-291">Folder1</span></span><br/><span data-ttu-id="50031-292">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="50031-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="50031-293">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="50031-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="50031-294">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3</span><span class="sxs-lookup"><span data-stu-id="50031-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="50031-295">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4</span><span class="sxs-lookup"><span data-stu-id="50031-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="50031-296">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5</span><span class="sxs-lookup"><span data-stu-id="50031-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="50031-297">true</span><span class="sxs-lookup"><span data-stu-id="50031-297">true</span></span> |<span data-ttu-id="50031-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="50031-298">mergeFiles</span></span> |<span data-ttu-id="50031-299">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="50031-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-300">Folder1</span></span><br/><span data-ttu-id="50031-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="50031-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="50031-307">se crea el destino de Hola carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="50031-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-308">Folder1</span></span><br/><span data-ttu-id="50031-309">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente</span><span class="sxs-lookup"><span data-stu-id="50031-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="50031-310">false</span><span class="sxs-lookup"><span data-stu-id="50031-310">false</span></span> |<span data-ttu-id="50031-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="50031-311">preserveHierarchy</span></span> |<span data-ttu-id="50031-312">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="50031-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-313">Folder1</span></span><br/><span data-ttu-id="50031-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="50031-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="50031-320">se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura</span><span class="sxs-lookup"><span data-stu-id="50031-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="50031-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-321">Folder1</span></span><br/><span data-ttu-id="50031-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="50031-324">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="50031-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="50031-325">false</span><span class="sxs-lookup"><span data-stu-id="50031-325">false</span></span> |<span data-ttu-id="50031-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="50031-326">flattenHierarchy</span></span> |<span data-ttu-id="50031-327">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="50031-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-328">Folder1</span></span><br/><span data-ttu-id="50031-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="50031-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="50031-335">se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura</span><span class="sxs-lookup"><span data-stu-id="50031-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="50031-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-336">Folder1</span></span><br/><span data-ttu-id="50031-337">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="50031-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="50031-338">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="50031-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="50031-339">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="50031-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="50031-340">false</span><span class="sxs-lookup"><span data-stu-id="50031-340">false</span></span> |<span data-ttu-id="50031-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="50031-341">mergeFiles</span></span> |<span data-ttu-id="50031-342">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="50031-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="50031-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-343">Folder1</span></span><br/><span data-ttu-id="50031-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="50031-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="50031-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="50031-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="50031-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="50031-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="50031-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="50031-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="50031-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="50031-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="50031-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="50031-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="50031-350">se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura</span><span class="sxs-lookup"><span data-stu-id="50031-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="50031-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="50031-351">Folder1</span></span><br/><span data-ttu-id="50031-352">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="50031-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="50031-353">Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="50031-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="50031-354">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="50031-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="50031-355">Tutorial: Datos de toocopy usar el Asistente para copia de almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="50031-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="50031-356">Echemos un vistazo a cómo el almacenamiento de blobs tooquickly copiar datos desde un Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="50031-357">En este tutorial, los almacenes de datos de origen y destino son de tipo: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="50031-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="50031-358">Hello canalización en este tutorial copia datos de una carpeta de tooanother en hello mismo contenedor de blob.</span><span class="sxs-lookup"><span data-stu-id="50031-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="50031-359">Este tutorial es deliberadamente simple tooshow valores o propiedades cuando se usa el almacenamiento de blobs como origen o receptor.</span><span class="sxs-lookup"><span data-stu-id="50031-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="50031-360">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="50031-360">Prerequisites</span></span>
1. <span data-ttu-id="50031-361">Si aún no tiene una, cree una **cuenta de Azure Storage** de uso general.</span><span class="sxs-lookup"><span data-stu-id="50031-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="50031-362">Usar el almacenamiento de blobs de hello como **origen** y **destino** almacén de datos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="50031-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="50031-363">Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo para toocreate pasos uno.</span><span class="sxs-lookup"><span data-stu-id="50031-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="50031-364">Crear un contenedor de blobs denominado **adfblobconnector** en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="50031-365">Cree una carpeta denominada **entrada** en hello **adfblobconnector** contenedor.</span><span class="sxs-lookup"><span data-stu-id="50031-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="50031-366">Cree un archivo denominado **emp.txt** con hello después de contenido y cargarlo toohello **entrada** carpeta mediante herramientas como [Explorador de almacenamiento de Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="50031-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="50031-367">Crear Hola factoría de datos</span><span class="sxs-lookup"><span data-stu-id="50031-367">Create hello data factory</span></span>
1. <span data-ttu-id="50031-368">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50031-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="50031-369">Haga clic en **+ nuevo** desde la esquina superior izquierda de hello, haga clic en **Intelligence + análisis**y haga clic en **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="50031-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="50031-370">Hola **factoría de datos** hoja:</span><span class="sxs-lookup"><span data-stu-id="50031-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="50031-371">Escriba **ADFBlobConnectorDF** para hello **nombre**.</span><span class="sxs-lookup"><span data-stu-id="50031-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="50031-372">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="50031-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="50031-373">Si recibe el error hello: `*Data factory name “ADFBlobConnectorDF” is not available`, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameADFBlobConnectorDF) y pruebe a crear de nuevo.</span><span class="sxs-lookup"><span data-stu-id="50031-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="50031-374">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="50031-375">Selección la **suscripción**de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="50031-376">Para el grupo de recursos, seleccione **usar existente** tooselect una existente recursos grupo (o) seleccione **crear nuevo** tooenter un nombre para un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="50031-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="50031-377">Seleccione un **ubicación** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="50031-378">Seleccione **toodashboard Pin** casilla situada en la parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="50031-379">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="50031-379">Click **Create**.</span></span>
3. <span data-ttu-id="50031-380">Una vez completada la creación de hello, vea hello **factoría de datos** hoja como se muestra en hello después de imagen: ![página principal de generador de datos](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="50031-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="50031-381">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="50031-381">Copy Wizard</span></span>
1. <span data-ttu-id="50031-382">En la página de inicio de la factoría de datos de hello, haga clic en hello **copiar datos [vista previa]** icono toolaunch **Asistente para copia de datos** en una pestaña independiente.</span><span class="sxs-lookup"><span data-stu-id="50031-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="50031-383">Si ve ese explorador web de hello está atascado en "Autorizar …", deshabilite o desactive **bloquear las cookies de terceros y datos de sitio** configuración (o) manténgala habilitada y cree una excepción para **login.microsoftonline.com**y, a continuación, intente iniciar Asistente de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="50031-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="50031-384">Hola **propiedades** página:</span><span class="sxs-lookup"><span data-stu-id="50031-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="50031-385">Escriba **CopyPipeline** en **Task name** (Nombre de tarea).</span><span class="sxs-lookup"><span data-stu-id="50031-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="50031-386">nombre de la tarea de Hello es Hola de canalización de saludo de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="50031-387">Escriba un **descripción** para la tarea de hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="50031-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="50031-388">Para **cadencia de tarea o la programación de tareas**, mantener hello **ejecute con regularidad en programación** opción.</span><span class="sxs-lookup"><span data-stu-id="50031-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="50031-389">Si desea que toorun esta tarea solo una vez en lugar de ejecutar repetidamente según una programación, seleccione **ejecutar una vez ahora**.</span><span class="sxs-lookup"><span data-stu-id="50031-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="50031-390">Si selecciona la opción **Run once now** (Ejecutar una vez ahora), se crea una [canalización única](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="50031-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="50031-391">Mantener valores de hello para **periódica patrón**.</span><span class="sxs-lookup"><span data-stu-id="50031-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="50031-392">Esta tarea se ejecuta diariamente entre Hola empezar y terminar horas se especifique en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="50031-393">Hola de cambio **fecha hora de inicio** demasiado**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="50031-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="50031-394">Hola de cambio **fecha hora de finalización** demasiado**04/25/2017**.</span><span class="sxs-lookup"><span data-stu-id="50031-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="50031-395">Puede que desee fecha de hello tootype en lugar de examinar calendario Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="50031-396">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-396">Click **Next**.</span></span>
      <span data-ttu-id="50031-397">![Herramienta de copia: Página de propiedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="50031-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="50031-398">En hello **almacén de datos de origen** página, haga clic en **almacenamiento de blobs de Azure** icono.</span><span class="sxs-lookup"><span data-stu-id="50031-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="50031-399">Utilice este almacén de datos de origen de página toospecify hello para la tarea de copia de hello.</span><span class="sxs-lookup"><span data-stu-id="50031-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="50031-400">Puede usar un servicio vinculado del almacén de datos existente, o bien especificar un almacén de datos nuevo.</span><span class="sxs-lookup"><span data-stu-id="50031-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="50031-401">servicio vinculado de toouse existente, se debe seleccionar **de existente servicios vinculados** y seleccione Hola derecho servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="50031-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="50031-402">![Herramienta de copia: Página de almacén de datos de origen](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="50031-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="50031-403">En hello **especificar cuenta de almacenamiento de blobs de Azure de hello** página:</span><span class="sxs-lookup"><span data-stu-id="50031-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="50031-404">Mantener el nombre generado automáticamente Hola para **nombre de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="50031-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="50031-405">nombre de la conexión de Hello es el nombre de hello del servicio de hello vinculado del tipo: el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="50031-406">Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="50031-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="50031-407">Seleccione la suscripción de Azure o mantenga **Seleccionar todo** para **Suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="50031-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="50031-408">Seleccione un **cuenta de almacenamiento de Azure** de hello cuentas disponible en la suscripción de hello seleccionado lista de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="50031-409">También puede elegir tooenter configuración de la cuenta de almacenamiento manualmente mediante la selección **escribir manualmente** opción para hello **método de selección de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="50031-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="50031-410">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-410">Click **Next**.</span></span> 
      <span data-ttu-id="50031-411">![Herramienta Copiar: especificar la cuenta de almacenamiento de blobs de Azure Hola](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="50031-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="50031-412">En **Elegir archivo de entrada de Hola o una carpeta** página:</span><span class="sxs-lookup"><span data-stu-id="50031-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="50031-413">Haga doble clic en **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="50031-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="50031-414">Seleccione **entrada** y haga clic en **Elegir**.</span><span class="sxs-lookup"><span data-stu-id="50031-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="50031-415">En este tutorial, se selecciona la carpeta de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="50031-416">También podría seleccionar archivo de hello emp.txt en la carpeta de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="50031-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="50031-417">![Herramienta Copiar: elegir el archivo de entrada de Hola o una carpeta](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="50031-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="50031-418">En hello **Elegir archivo de entrada de Hola o una carpeta** página:</span><span class="sxs-lookup"><span data-stu-id="50031-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="50031-419">Confirme que hello **archivo o carpeta** se establece demasiado**adfblobconnector/entrada**.</span><span class="sxs-lookup"><span data-stu-id="50031-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="50031-420">Si hay archivos de hello en subcarpetas, por ejemplo, de 2017/04/01, 2017/04/02 y así sucesivamente, escriba adfblobconnector/entrada / {year} / {month} / {day} para archivo o carpeta.</span><span class="sxs-lookup"><span data-stu-id="50031-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="50031-421">Al presionar TAB fuera del cuadro de texto hello, verá tres formatos de tooselect listas desplegables para year (aaaa), month (MM) y día (dd).</span><span class="sxs-lookup"><span data-stu-id="50031-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="50031-422">No marque la casilla **Copy file recursively** (Copiar archivo de forma recursiva).</span><span class="sxs-lookup"><span data-stu-id="50031-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="50031-423">Seleccione este recorrido de toorecursively opción a través de las carpetas de destino de archivos toobe toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="50031-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="50031-424">Hola no **copia binaria** opción.</span><span class="sxs-lookup"><span data-stu-id="50031-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="50031-425">Seleccione este tooperform opción una copia binaria del destino de toohello del archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="50031-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="50031-426">No seleccione para este tutorial para que puedan ver más opciones para páginas siguientes del saludo.</span><span class="sxs-lookup"><span data-stu-id="50031-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="50031-427">Confirme que hello **el tipo de compresión** se establece demasiado**ninguno**.</span><span class="sxs-lookup"><span data-stu-id="50031-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="50031-428">Seleccione un valor para esta opción si los archivos de origen están comprimidos en uno de los formatos de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="50031-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="50031-429">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-429">Click **Next**.</span></span>
    <span data-ttu-id="50031-430">![Herramienta Copiar: elegir el archivo de entrada de Hola o una carpeta](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="50031-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="50031-431">En hello **configuración de formato de archivo** página, verá los delimitadores de Hola y Hola esquema detecta automáticamente por el Asistente de hello bien analizando el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="50031-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="50031-432">Confirmar Hola siguientes opciones: una.</span><span class="sxs-lookup"><span data-stu-id="50031-432">Confirm hello following options: a.</span></span> <span data-ttu-id="50031-433">Hola **formato de archivo** se establece demasiado**formato de texto**.</span><span class="sxs-lookup"><span data-stu-id="50031-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="50031-434">Puede ver todos los formatos de hello compatibles en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="50031-435">Por ejemplo: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="50031-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="50031-436">b.</span><span class="sxs-lookup"><span data-stu-id="50031-436">b.</span></span> <span data-ttu-id="50031-437">Hola **delimitador de columna** se establece demasiado`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="50031-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="50031-438">Puede ver Hola otros delimitadores de columna admitidos por factoría de datos en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="50031-439">También puede especificar un delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="50031-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="50031-440">c.</span><span class="sxs-lookup"><span data-stu-id="50031-440">c.</span></span> <span data-ttu-id="50031-441">Hola **delimitador de filas** se establece demasiado`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="50031-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="50031-442">Puede ver Hola otros delimitadores de fila admitidos por factoría de datos en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="50031-443">También puede especificar un delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="50031-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="50031-444">d.</span><span class="sxs-lookup"><span data-stu-id="50031-444">d.</span></span> <span data-ttu-id="50031-445">Hola **omitir recuento de líneas** se establece demasiado**0**.</span><span class="sxs-lookup"><span data-stu-id="50031-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="50031-446">Si desea que unos toobe líneas omiten en la parte superior de hello del archivo hello, escriba aquí el número de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="50031-447">e.</span><span class="sxs-lookup"><span data-stu-id="50031-447">e.</span></span>  <span data-ttu-id="50031-448">Hola **primera fila de datos contiene nombres de columna** no se ha establecido.</span><span class="sxs-lookup"><span data-stu-id="50031-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="50031-449">Si los archivos de origen de hello contienen nombres de columna en la primera fila de hello, seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="50031-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="50031-450">f.</span><span class="sxs-lookup"><span data-stu-id="50031-450">f.</span></span> <span data-ttu-id="50031-451">Hola **tratar el valor de la columna vacía como null** opción está establecida.</span><span class="sxs-lookup"><span data-stu-id="50031-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="50031-452">Expanda **configuración avanzada** toosee avanzada opción disponible.</span><span class="sxs-lookup"><span data-stu-id="50031-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="50031-453">En parte inferior de Hola de página de hello, vea hello **vista previa** de datos de archivo de hello emp.txt.</span><span class="sxs-lookup"><span data-stu-id="50031-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="50031-454">Haga clic en **esquema** pestaña en el esquema de hello inferior toosee Hola ese asistente para copiar de hello inferida examinando datos hello en el archivo de código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="50031-455">Haga clic en **siguiente** después de revisar los delimitadores de Hola y obtener una vista previa de los datos.</span><span class="sxs-lookup"><span data-stu-id="50031-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="50031-456">![Herramienta de copia: Configuración de formato de archivo](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="50031-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="50031-457">En hello **página de almacén de datos de destino**, seleccione **almacenamiento de blobs de Azure**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="50031-458">Hola almacenamiento de blobs de Azure que usa como ambos almacenes de datos de origen y destino de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="50031-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="50031-459">![Herramienta de copia: Selección del almacén de datos de destino](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="50031-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="50031-460">En **especificar cuenta de almacenamiento de blobs de Azure de hello** página:</span><span class="sxs-lookup"><span data-stu-id="50031-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="50031-461">Escriba **AzureStorageLinkedService** para hello **nombre de la conexión** campo.</span><span class="sxs-lookup"><span data-stu-id="50031-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="50031-462">Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="50031-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="50031-463">Selección la **suscripción**de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="50031-464">Seleccione su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="50031-465">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-465">Click **Next**.</span></span>     
10. <span data-ttu-id="50031-466">En hello **Hola Elegir archivo o carpeta de salida** página:</span><span class="sxs-lookup"><span data-stu-id="50031-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="50031-467">Especifique la **ruta de acceso de carpeta** como **adfblobconnector/output/{year}/{month}/{day}**.</span><span class="sxs-lookup"><span data-stu-id="50031-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="50031-468">Escriba **TAB**.</span><span class="sxs-lookup"><span data-stu-id="50031-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="50031-469">Para hello **año**, seleccione **aaaa**.</span><span class="sxs-lookup"><span data-stu-id="50031-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="50031-470">Para hello **mes**, confirme que está establecido demasiado**MM**.</span><span class="sxs-lookup"><span data-stu-id="50031-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="50031-471">Para hello **día**, confirme que está establecido demasiado**dd**.</span><span class="sxs-lookup"><span data-stu-id="50031-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="50031-472">Confirme que hello **el tipo de compresión** se establece demasiado**ninguno**.</span><span class="sxs-lookup"><span data-stu-id="50031-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="50031-473">Confirme que hello **Copiar comportamiento** se establece demasiado**combinar archivos**.</span><span class="sxs-lookup"><span data-stu-id="50031-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="50031-474">Si el archivo con hello ya existe el mismo nombre de salida de hello, hello contenido nuevo es agregado toohello mismo archivo al final de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="50031-475">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-475">Click **Next**.</span></span>
    <span data-ttu-id="50031-476">![Herramienta de copia: Selección del archivo o la carpeta de salida](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="50031-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="50031-477">En hello **configuración de formato de archivo** página, revise la configuración de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="50031-478">Una de estas opciones adicionales de hello es tooadd un archivo de salida de encabezado toohello.</span><span class="sxs-lookup"><span data-stu-id="50031-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="50031-479">Si selecciona esta opción, se agrega una fila de encabezado con nombres de columnas de hello del esquema de Hola de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="50031-480">Puede cambiar los nombres de columna predeterminados de hello al ver el esquema de hello para el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="50031-481">Por ejemplo, puede cambiar Hola primera columna tooFirst nombre y la segunda columna tooLast nombre.</span><span class="sxs-lookup"><span data-stu-id="50031-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="50031-482">A continuación, archivo de salida de hello se genera con un encabezado con estos nombres como nombres de columna.</span><span class="sxs-lookup"><span data-stu-id="50031-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="50031-483">![Herramienta de copia: Configuración del formato de archivo de destino](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="50031-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="50031-484">En hello **configuración de rendimiento** página, confirme que **unidades en la nube** y **copias en paralelo** se establecen demasiado**automática**y haga clic en siguiente.</span><span class="sxs-lookup"><span data-stu-id="50031-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="50031-485">Para más información sobre esta configuración, consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="50031-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="50031-486">![Herramienta de copia: Configuración de rendimiento](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="50031-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="50031-487">En hello **resumen** página, revise todas las configuraciones (propiedades de la tarea, configuración de origen y de destino y Copiar configuración) y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="50031-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="50031-488">![Herramienta de copia: Página de resumen](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="50031-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="50031-489">Revise la información en hello **resumen** página y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="50031-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="50031-490">Asistente de Hello crea dos servicios vinculados, dos conjuntos de datos (entrada y salida) y una canalización de factoría de datos de hello (desde donde se haya iniciado Hola Asistente para copiar).</span><span class="sxs-lookup"><span data-stu-id="50031-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="50031-491">![Herramienta de copia: Página de implementación](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="50031-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="50031-492">Supervisar la canalización de hello (tarea de copia)</span><span class="sxs-lookup"><span data-stu-id="50031-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="50031-493">Haga clic en el vínculo de hello `Click here toomonitor copy pipeline` en hello **implementación** página.</span><span class="sxs-lookup"><span data-stu-id="50031-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="50031-494">Debería ver Hola **supervisar y administrar aplicaciones** en una pestaña independiente.  ![Supervisar y administrar la aplicación](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="50031-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="50031-495">Hola de cambio **iniciar** de demasiado tiempo en la parte superior de hello`04/19/2017` y **final** demasiado tiempo`04/27/2017`y, a continuación, haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="50031-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="50031-496">Debería ver cinco ventanas de la actividad en hello **WINDOWS actividad** lista.</span><span class="sxs-lookup"><span data-stu-id="50031-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="50031-497">Hola **WindowStart** veces deben cubrir todos los días de horas de finalización de toopipeline de inicio de canalización.</span><span class="sxs-lookup"><span data-stu-id="50031-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="50031-498">Haga clic en **actualizar** botón para hello **WINDOWS actividad** lista varias veces hasta que vea Estado Hola de todas las ventanas de la actividad de Hola se establece tooReady.</span><span class="sxs-lookup"><span data-stu-id="50031-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="50031-499">Ahora, compruebe que se generan archivos de salida de hello en carpeta de salida de hello de contenedor adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="50031-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="50031-500">Debería ver Hola siguiendo la estructura de carpetas en la carpeta de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="50031-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="50031-501">Para más información sobre la supervisión y administración de factorías de datos, consulte el artículo [Supervisión y administración de canalizaciones de Data Factory](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="50031-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="50031-502">Entidades de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="50031-502">Data Factory entities</span></span>
<span data-ttu-id="50031-503">Ahora, cambie toohello back-pestaña con la página principal de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="50031-504">Observe que ahora hay en su factoría de datos dos servicios vinculados, dos conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="50031-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Página principal de Data Factory con entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="50031-506">Haga clic en **autor e implementar** toolaunch Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Editor de la Factoría de datos](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="50031-508">Debería ver Hola siguiendo las entidades de la factoría de datos de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="50031-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="50031-509">Dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="50031-509">Two linked services.</span></span> <span data-ttu-id="50031-510">Uno para el origen de Hola y Hola otro destino Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="50031-511">Ambos servicios Hola vinculado que hacen referencia toohello misma cuenta de almacenamiento de Azure en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="50031-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="50031-512">Dos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="50031-512">Two datasets.</span></span> <span data-ttu-id="50031-513">Un conjunto de datos de entrada y un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="50031-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="50031-514">En este tutorial, ambos usan Hola mismo contenedor de blob, pero hacen referencia a las carpetas de toodifferent (entrada y salida).</span><span class="sxs-lookup"><span data-stu-id="50031-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="50031-515">Una canalización.</span><span class="sxs-lookup"><span data-stu-id="50031-515">A pipeline.</span></span> <span data-ttu-id="50031-516">canalización de Hello contiene una actividad de copia que utiliza un origen de blobs y una blob receptor toocopy de datos de un tooanother de ubicación de blob de Azure ubicación del blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="50031-517">Hello las secciones siguientes proporcionan más información acerca de estas entidades.</span><span class="sxs-lookup"><span data-stu-id="50031-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="50031-518">Servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="50031-518">Linked services</span></span>
<span data-ttu-id="50031-519">Verá dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="50031-519">You should see two linked services.</span></span> <span data-ttu-id="50031-520">Uno para el origen de Hola y Hola otro destino Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="50031-521">En este tutorial, ambos buscar definiciones Hola mismo salvo para los nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="50031-522">Hola **tipo** de hello servicio vinculado se establece demasiado**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="50031-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="50031-523">Propiedad más importante de la definición del servicio vinculado de hello es hello **connectionString**, que se usa por factoría de datos tooconnect tooyour cuenta de almacenamiento de Azure en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="50031-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="50031-524">Caso omiso hello hubName propiedad en la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="50031-525">Servicio vinculado de almacenamiento de blobs de origen</span><span class="sxs-lookup"><span data-stu-id="50031-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="50031-526">Servicio vinculado de almacenamiento de blobs de destino</span><span class="sxs-lookup"><span data-stu-id="50031-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="50031-527">Para más información sobre el servicio vinculado Azure Storage, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="50031-528">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="50031-528">Datasets</span></span>
<span data-ttu-id="50031-529">Hay dos conjuntos de datos: un conjunto de datos de entrada y un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="50031-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="50031-530">tipo de Hello del conjunto de datos de Hola se establece demasiado**AzureBlob** para ambos.</span><span class="sxs-lookup"><span data-stu-id="50031-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="50031-531">conjunto de datos de entrada de Hello señala toohello **entrada** carpeta de hello **adfblobconnector** contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="50031-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="50031-532">Hola **externo** propiedad se establece demasiado**true** para este conjunto de datos como Hola datos no se crea por canalización Hola con la actividad de copia de Hola que toma este conjunto de datos como entrada.</span><span class="sxs-lookup"><span data-stu-id="50031-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="50031-533">Hola toohello de puntos del conjunto de datos de salida **salida** carpeta de hello mismo contenedor de blob.</span><span class="sxs-lookup"><span data-stu-id="50031-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="50031-534">Hello conjunto de datos de salida también utiliza Hola año, mes y día de hello **SliceStart** toodynamically variable del sistema evaluar la ruta de acceso de hello para el archivo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="50031-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="50031-535">Para ver la lista de funciones y variables del sistema que admite Data Factory, consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="50031-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="50031-536">Hola **externo** propiedad se establece demasiado**false** (valor predeterminado) porque este conjunto de datos generado por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="50031-537">Para más información sobre las propiedades admitidas por el conjunto de datos de blob de Azure, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="50031-538">Conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="50031-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="50031-539">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="50031-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="50031-540">Canalización</span><span class="sxs-lookup"><span data-stu-id="50031-540">Pipeline</span></span>
<span data-ttu-id="50031-541">canalización de Hello tiene solo una actividad.</span><span class="sxs-lookup"><span data-stu-id="50031-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="50031-542">Hola **tipo** de hello actividad se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="50031-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="50031-543">En Propiedades de tipos de Hola de actividad hello, hay dos secciones, una para el origen y hello otro para el receptor.</span><span class="sxs-lookup"><span data-stu-id="50031-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="50031-544">tipo de origen de Hola se establece demasiado**BlobSource** como actividad hello es copiar datos desde un almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="50031-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="50031-545">Hello el tipo de receptor se establece demasiado**BlobSink** como actividad hello copiando el almacenamiento de blobs de datos tooa.</span><span class="sxs-lookup"><span data-stu-id="50031-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="50031-546">actividad de copia de Hello toma InputDataset z4y como entrada de Hola y OutputDataset z4y como salida de hello.</span><span class="sxs-lookup"><span data-stu-id="50031-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="50031-547">Para más información sobre las propiedades admitidas por BlobSource y BlobSink, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="50031-548">Ejemplos JSON para copiar datos tooand del almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="50031-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="50031-549">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="50031-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="50031-550">Muestran cómo toocopy tooand de datos de almacenamiento de blobs de Azure y base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="50031-551">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="50031-552">Ejemplo JSON: Copiar los datos de almacenamiento de blobs tooSQL base de datos</span><span class="sxs-lookup"><span data-stu-id="50031-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="50031-553">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="50031-553">hello following sample shows:</span></span>

1. <span data-ttu-id="50031-554">Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="50031-555">Un servicio vinculado de tipo [AzureStorage](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="50031-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="50031-556">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="50031-557">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="50031-558">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [BlobSource](#copy-activity-properties) y [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="50031-559">ejemplo de Hola copia datos de serie temporal de una tabla de SQL Azure tooan de blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="50031-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="50031-560">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="50031-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="50031-561">**Servicio vinculado SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="50031-562">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="50031-563">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="50031-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="50031-564">Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="50031-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="50031-565">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="50031-566">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="50031-567">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="50031-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="50031-568">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="50031-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="50031-569">ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="50031-570">"externo": "true" configuración indica factoría de datos de esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="50031-571">**Conjunto de datos de salida SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="50031-572">ejemplo de Hola copia la tabla de tooa de datos denominado "MyTable" en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="50031-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="50031-573">Crear tabla de hello en la base de datos de SQL Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="50031-574">Se agregan nuevas filas toohello tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="50031-574">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="50031-575">**Una actividad de copia en una canalización con el origen de blob y el receptor SQL:**</span><span class="sxs-lookup"><span data-stu-id="50031-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="50031-576">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="50031-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="50031-577">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="50031-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="50031-578">Ejemplo JSON: Copiar los datos de SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="50031-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="50031-579">Hola el siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="50031-579">hello following sample shows:</span></span>

1. <span data-ttu-id="50031-580">Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="50031-581">Un servicio vinculado de tipo [AzureStorage](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="50031-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="50031-582">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="50031-583">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="50031-584">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) y [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="50031-585">ejemplo Hello copia datos de serie temporal de un tooan de tabla de SQL Azure blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="50031-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="50031-586">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="50031-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="50031-587">**Servicio vinculado SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="50031-588">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="50031-589">Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="50031-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="50031-590">Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="50031-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="50031-591">Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50031-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="50031-592">**Conjunto de datos de entrada SQL de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="50031-593">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Azure y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="50031-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="50031-594">Establecer "externo": "true" informa a servicio Data Factory esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="50031-595">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="50031-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="50031-596">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="50031-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="50031-597">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="50031-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="50031-598">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="50031-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="50031-599">**Actividad de copia en una canalización con el origen SQL y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="50031-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="50031-600">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="50031-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="50031-601">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="50031-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="50031-602">consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="50031-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="50031-603">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="50031-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="50031-604">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="50031-604">Performance and Tuning</span></span>
<span data-ttu-id="50031-605">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="50031-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
