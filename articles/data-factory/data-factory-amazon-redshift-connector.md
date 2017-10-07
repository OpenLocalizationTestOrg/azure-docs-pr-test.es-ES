---
title: "datos de aaaMove de Amazon Redshift con factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de Amazon Redshift con Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="77867-103">Movimiento de datos de Amazon Redshift mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="77867-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="77867-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove de Data Factory de Azure de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="77867-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="77867-105">artículo de Hola se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="77867-106">Puede copiar datos de almacén de datos de Amazon Redshift tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="77867-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="77867-107">Para obtener una lista de almacenes de datos que se admiten como receptores por actividad de copia de hello, consulte [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="77867-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="77867-108">Factoría de datos actualmente admite la migración de datos de almacenes de datos de Amazon Redshift tooother, pero no para mover datos desde otro tooAmazon de almacenes de datos Redshift.</span><span class="sxs-lookup"><span data-stu-id="77867-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77867-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="77867-109">Prerequisites</span></span>
* <span data-ttu-id="77867-110">Si va a mover datos tooan un almacén de datos local, instale [Data Management Gateway](data-factory-data-management-gateway.md) en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="77867-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="77867-111">A continuación, conceder Data Management Gateway (usar una dirección IP de la máquina de hello) hello tooAmazon Redshift clúster de acceso.</span><span class="sxs-lookup"><span data-stu-id="77867-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="77867-112">Vea [clúster de autorizar acceso toohello](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="77867-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="77867-113">Si va a mover el almacén de datos tooan datos de Azure, consulte [intervalos de IP de centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653) para los intervalos SQL utilizados por los centros de datos de Azure de Hola y dirección IP de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="77867-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="77867-114">Getting started</span></span>
<span data-ttu-id="77867-115">Puede crear una canalización con actividad de copia que mueva los datos desde un origen de Amazon Redshift mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="77867-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="77867-116">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="77867-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="77867-117">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="77867-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="77867-118">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="77867-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="77867-119">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="77867-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="77867-120">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="77867-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="77867-121">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="77867-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="77867-122">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="77867-123">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="77867-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="77867-124">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="77867-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="77867-125">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="77867-126">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de Amazon Redshift, consulte [ejemplo de JSON: copiar los datos de Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="77867-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="77867-127">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAmazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="77867-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="77867-128">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="77867-128">Linked service properties</span></span>
<span data-ttu-id="77867-129">Hello en la tabla siguiente proporciona la descripción de JSON elementos específico tooAmazon servicio Redshift vinculado.</span><span class="sxs-lookup"><span data-stu-id="77867-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="77867-130">Propiedad</span><span class="sxs-lookup"><span data-stu-id="77867-130">Property</span></span> | <span data-ttu-id="77867-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="77867-131">Description</span></span> | <span data-ttu-id="77867-132">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="77867-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77867-133">type</span><span class="sxs-lookup"><span data-stu-id="77867-133">type</span></span> |<span data-ttu-id="77867-134">propiedad de tipo Hello debe establecerse en: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="77867-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="77867-135">Sí</span><span class="sxs-lookup"><span data-stu-id="77867-135">Yes</span></span> |
| <span data-ttu-id="77867-136">Servidor</span><span class="sxs-lookup"><span data-stu-id="77867-136">server</span></span> |<span data-ttu-id="77867-137">IP dirección o nombre de host del servidor de Amazon Redshift Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="77867-138">Sí</span><span class="sxs-lookup"><span data-stu-id="77867-138">Yes</span></span> |
| <span data-ttu-id="77867-139">puerto</span><span class="sxs-lookup"><span data-stu-id="77867-139">port</span></span> |<span data-ttu-id="77867-140">número de Hola de puerto TCP Hola Hola Amazon Redshift server usa toolisten para las conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="77867-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="77867-141">No, valor predeterminado: 5439</span><span class="sxs-lookup"><span data-stu-id="77867-141">No, default value: 5439</span></span> |
| <span data-ttu-id="77867-142">database</span><span class="sxs-lookup"><span data-stu-id="77867-142">database</span></span> |<span data-ttu-id="77867-143">Nombre de base de datos de Amazon Redshift Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="77867-144">Sí</span><span class="sxs-lookup"><span data-stu-id="77867-144">Yes</span></span> |
| <span data-ttu-id="77867-145">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="77867-145">username</span></span> |<span data-ttu-id="77867-146">Nombre de usuario que tenga la base de datos de access toohello.</span><span class="sxs-lookup"><span data-stu-id="77867-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="77867-147">Sí</span><span class="sxs-lookup"><span data-stu-id="77867-147">Yes</span></span> |
| <span data-ttu-id="77867-148">Contraseña</span><span class="sxs-lookup"><span data-stu-id="77867-148">password</span></span> |<span data-ttu-id="77867-149">Contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-149">Password for hello user account.</span></span> |<span data-ttu-id="77867-150">Sí</span><span class="sxs-lookup"><span data-stu-id="77867-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="77867-151">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="77867-151">Dataset properties</span></span>
<span data-ttu-id="77867-152">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="77867-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="77867-153">Las secciones como structure, availability y policy son similares para todos los tipos de conjunto de datos (Azure SQL, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="77867-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="77867-154">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="77867-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="77867-155">Proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="77867-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="77867-156">sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de Amazon Redshift) tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="77867-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="77867-157">Propiedad</span><span class="sxs-lookup"><span data-stu-id="77867-157">Property</span></span> | <span data-ttu-id="77867-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="77867-158">Description</span></span> | <span data-ttu-id="77867-159">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="77867-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77867-160">tableName</span><span class="sxs-lookup"><span data-stu-id="77867-160">tableName</span></span> |<span data-ttu-id="77867-161">Nombre de tabla de hello en base de datos de Amazon Redshift de hello servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="77867-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="77867-162">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="77867-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="77867-163">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="77867-163">Copy activity properties</span></span>
<span data-ttu-id="77867-164">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="77867-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="77867-165">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="77867-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="77867-166">Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="77867-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="77867-167">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="77867-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="77867-168">Cuando el origen de la actividad de copia es del tipo **RelationalSource** (que incluye Amazon Redshift), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="77867-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="77867-169">Propiedad</span><span class="sxs-lookup"><span data-stu-id="77867-169">Property</span></span> | <span data-ttu-id="77867-170">Descripción</span><span class="sxs-lookup"><span data-stu-id="77867-170">Description</span></span> | <span data-ttu-id="77867-171">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="77867-171">Allowed values</span></span> | <span data-ttu-id="77867-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="77867-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="77867-173">query</span><span class="sxs-lookup"><span data-stu-id="77867-173">query</span></span> |<span data-ttu-id="77867-174">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="77867-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="77867-175">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="77867-175">SQL query string.</span></span> <span data-ttu-id="77867-176">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="77867-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="77867-177">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="77867-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="77867-178">Ejemplo de JSON: copiar los datos de Amazon Redshift tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="77867-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="77867-179">Este ejemplo muestra cómo la base de datos toocopy desde un Amazon Redshift datos tooan almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="77867-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="77867-180">Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="77867-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="77867-181">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="77867-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="77867-182">Un servicio vinculado de tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="77867-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="77867-183">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="77867-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="77867-184">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="77867-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="77867-185">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="77867-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="77867-186">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="77867-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="77867-187">ejemplo de Hola copia datos de un resultado de consulta en el blob de Amazon Redshift tooa cada hora.</span><span class="sxs-lookup"><span data-stu-id="77867-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="77867-188">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="77867-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="77867-189">**Servicio vinculado de Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="77867-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="77867-190">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="77867-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="77867-191">**Conjunto de datos de entrada de Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="77867-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="77867-192">Establecer `"external": true` informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="77867-193">Establecer esta propiedad tootrue en un conjunto de datos de entrada que no se crea una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="77867-194">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="77867-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="77867-195">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="77867-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="77867-196">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="77867-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="77867-197">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="77867-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="77867-198">**Actividad de copia en una canalización con el origen de Azure Redshift (RelationalSource) y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="77867-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="77867-199">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="77867-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="77867-200">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="77867-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="77867-201">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="77867-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="77867-202">Asignación de tipos para Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="77867-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="77867-203">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="77867-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="77867-204">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="77867-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="77867-205">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="77867-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="77867-206">Al mover datos tooAmazon Redshift, Hola siguiendo las asignaciones se usa desde tipos de Amazon Redshift too.NET tipos.</span><span class="sxs-lookup"><span data-stu-id="77867-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="77867-207">Tipo Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="77867-207">Amazon Redshift Type</span></span> | <span data-ttu-id="77867-208">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="77867-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="77867-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="77867-209">SMALLINT</span></span> |<span data-ttu-id="77867-210">Int16</span><span class="sxs-lookup"><span data-stu-id="77867-210">Int16</span></span> |
| <span data-ttu-id="77867-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="77867-211">INTEGER</span></span> |<span data-ttu-id="77867-212">Int32</span><span class="sxs-lookup"><span data-stu-id="77867-212">Int32</span></span> |
| <span data-ttu-id="77867-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="77867-213">BIGINT</span></span> |<span data-ttu-id="77867-214">Int64</span><span class="sxs-lookup"><span data-stu-id="77867-214">Int64</span></span> |
| <span data-ttu-id="77867-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="77867-215">DECIMAL</span></span> |<span data-ttu-id="77867-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="77867-216">Decimal</span></span> |
| <span data-ttu-id="77867-217">REAL</span><span class="sxs-lookup"><span data-stu-id="77867-217">REAL</span></span> |<span data-ttu-id="77867-218">Single</span><span class="sxs-lookup"><span data-stu-id="77867-218">Single</span></span> |
| <span data-ttu-id="77867-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="77867-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="77867-220">Doble</span><span class="sxs-lookup"><span data-stu-id="77867-220">Double</span></span> |
| <span data-ttu-id="77867-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="77867-221">BOOLEAN</span></span> |<span data-ttu-id="77867-222">String</span><span class="sxs-lookup"><span data-stu-id="77867-222">String</span></span> |
| <span data-ttu-id="77867-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="77867-223">CHAR</span></span> |<span data-ttu-id="77867-224">String</span><span class="sxs-lookup"><span data-stu-id="77867-224">String</span></span> |
| <span data-ttu-id="77867-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="77867-225">VARCHAR</span></span> |<span data-ttu-id="77867-226">String</span><span class="sxs-lookup"><span data-stu-id="77867-226">String</span></span> |
| <span data-ttu-id="77867-227">DATE</span><span class="sxs-lookup"><span data-stu-id="77867-227">DATE</span></span> |<span data-ttu-id="77867-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="77867-228">DateTime</span></span> |
| <span data-ttu-id="77867-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="77867-229">TIMESTAMP</span></span> |<span data-ttu-id="77867-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="77867-230">DateTime</span></span> |
| <span data-ttu-id="77867-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="77867-231">TEXT</span></span> |<span data-ttu-id="77867-232">String</span><span class="sxs-lookup"><span data-stu-id="77867-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="77867-233">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="77867-233">Map source toosink columns</span></span>
<span data-ttu-id="77867-234">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="77867-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="77867-235">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="77867-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="77867-236">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="77867-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="77867-237">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="77867-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="77867-238">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="77867-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="77867-239">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="77867-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="77867-240">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="77867-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="77867-241">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="77867-241">Performance and Tuning</span></span>
<span data-ttu-id="77867-242">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="77867-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77867-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77867-243">Next Steps</span></span>
<span data-ttu-id="77867-244">Vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="77867-244">See hello following articles:</span></span>

* <span data-ttu-id="77867-245">[Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="77867-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
