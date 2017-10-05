---
title: Movimiento de datos de Amazon Redshift mediante Data Factory | Microsoft Docs
description: "Obtenga información sobre cómo mover datos desde Amazon Redshift mediante Azure Data Factory."
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
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="5b729-103">Movimiento de datos de Amazon Redshift mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5b729-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="5b729-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="5b729-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="5b729-105">El artículo se basa en la información general sobre el movimiento de datos con la actividad de copia que ofrece el artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="5b729-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="5b729-106">Puede copiar datos de Amazon Redshift en cualquier almacén de datos de receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="5b729-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="5b729-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como receptores.</span><span class="sxs-lookup"><span data-stu-id="5b729-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="5b729-108">Data Factory solo admite actualmente el movimiento de datos de Amazon Redshift a otros almacenes de datos, pero no de otros almacenes de datos a Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="5b729-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b729-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5b729-109">Prerequisites</span></span>
* <span data-ttu-id="5b729-110">Si mueve datos a un almacén de datos local, instale [Data Management Gateway](data-factory-data-management-gateway.md) en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="5b729-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="5b729-111">Conceda a Data Management Gateway (use la dirección IP del equipo) el acceso al clúster de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="5b729-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="5b729-112">Consulte [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) (Autorización para acceder al clúster) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="5b729-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="5b729-113">Si va a mover datos a un almacén de datos de Azure, consulte [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) (Intervalos de direcciones IP de Azure Data Center) para ver los intervalos de direcciones IP de Compute y los intervalos SQL que se utilizan en los centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b729-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5b729-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="5b729-114">Getting started</span></span>
<span data-ttu-id="5b729-115">Puede crear una canalización con actividad de copia que mueva los datos desde un origen de Amazon Redshift mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="5b729-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="5b729-116">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="5b729-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5b729-117">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="5b729-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="5b729-118">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="5b729-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5b729-119">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="5b729-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5b729-120">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="5b729-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="5b729-121">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5b729-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="5b729-122">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="5b729-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="5b729-123">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="5b729-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5b729-124">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="5b729-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="5b729-125">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="5b729-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="5b729-126">Para obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan para copiar los datos de un almacén de datos de Amazon Redshift, consulte la sección [Ejemplo de JSON: Copiar datos de Amazon Redshift a un blob de Azure](#json-example-copy-data-from-amazon-redshift-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="5b729-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5b729-127">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Amazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="5b729-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="5b729-128">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="5b729-128">Linked service properties</span></span>
<span data-ttu-id="5b729-129">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="5b729-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="5b729-130">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b729-130">Property</span></span> | <span data-ttu-id="5b729-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="5b729-131">Description</span></span> | <span data-ttu-id="5b729-132">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5b729-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b729-133">type</span><span class="sxs-lookup"><span data-stu-id="5b729-133">type</span></span> |<span data-ttu-id="5b729-134">La propiedad type debe establecerse en: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="5b729-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="5b729-135">Sí</span><span class="sxs-lookup"><span data-stu-id="5b729-135">Yes</span></span> |
| <span data-ttu-id="5b729-136">server</span><span class="sxs-lookup"><span data-stu-id="5b729-136">server</span></span> |<span data-ttu-id="5b729-137">Dirección IP o nombre de host del servidor de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="5b729-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="5b729-138">Sí</span><span class="sxs-lookup"><span data-stu-id="5b729-138">Yes</span></span> |
| <span data-ttu-id="5b729-139">puerto</span><span class="sxs-lookup"><span data-stu-id="5b729-139">port</span></span> |<span data-ttu-id="5b729-140">El número del puerto TCP que el servidor de Amazon Redshift utiliza para escuchar las conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="5b729-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="5b729-141">No, valor predeterminado: 5439</span><span class="sxs-lookup"><span data-stu-id="5b729-141">No, default value: 5439</span></span> |
| <span data-ttu-id="5b729-142">database</span><span class="sxs-lookup"><span data-stu-id="5b729-142">database</span></span> |<span data-ttu-id="5b729-143">Nombre de la base de datos de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="5b729-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="5b729-144">Sí</span><span class="sxs-lookup"><span data-stu-id="5b729-144">Yes</span></span> |
| <span data-ttu-id="5b729-145">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="5b729-145">username</span></span> |<span data-ttu-id="5b729-146">Nombre del usuario que tiene acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="5b729-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="5b729-147">Sí</span><span class="sxs-lookup"><span data-stu-id="5b729-147">Yes</span></span> |
| <span data-ttu-id="5b729-148">contraseña</span><span class="sxs-lookup"><span data-stu-id="5b729-148">password</span></span> |<span data-ttu-id="5b729-149">Contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="5b729-149">Password for the user account.</span></span> |<span data-ttu-id="5b729-150">Sí</span><span class="sxs-lookup"><span data-stu-id="5b729-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5b729-151">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="5b729-151">Dataset properties</span></span>
<span data-ttu-id="5b729-152">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="5b729-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5b729-153">Las secciones como structure, availability y policy son similares para todos los tipos de conjunto de datos (Azure SQL, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="5b729-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5b729-154">La sección **typeProperties** es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="5b729-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="5b729-155">Proporciona información acerca de la ubicación de los datos del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="5b729-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="5b729-156">La sección typeProperties del conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de Amazon Redshift) tiene las propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="5b729-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="5b729-157">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b729-157">Property</span></span> | <span data-ttu-id="5b729-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="5b729-158">Description</span></span> | <span data-ttu-id="5b729-159">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5b729-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b729-160">tableName</span><span class="sxs-lookup"><span data-stu-id="5b729-160">tableName</span></span> |<span data-ttu-id="5b729-161">Nombre de la tabla en la base de datos de Amazon Redshift a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="5b729-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="5b729-162">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="5b729-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="5b729-163">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="5b729-163">Copy activity properties</span></span>
<span data-ttu-id="5b729-164">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5b729-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5b729-165">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="5b729-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="5b729-166">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="5b729-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="5b729-167">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="5b729-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="5b729-168">Si el origen de la actividad de copia es del tipo **RelationalSource** (que incluye Amazon Redshift), las propiedades siguientes están disponibles en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="5b729-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="5b729-169">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5b729-169">Property</span></span> | <span data-ttu-id="5b729-170">Descripción</span><span class="sxs-lookup"><span data-stu-id="5b729-170">Description</span></span> | <span data-ttu-id="5b729-171">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="5b729-171">Allowed values</span></span> | <span data-ttu-id="5b729-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5b729-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b729-173">query</span><span class="sxs-lookup"><span data-stu-id="5b729-173">query</span></span> |<span data-ttu-id="5b729-174">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="5b729-174">Use the custom query to read data.</span></span> |<span data-ttu-id="5b729-175">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="5b729-175">SQL query string.</span></span> <span data-ttu-id="5b729-176">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="5b729-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="5b729-177">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="5b729-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="5b729-178">Ejemplo de JSON: Copiar datos de Amazon Redshift a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="5b729-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="5b729-179">En este ejemplo, se muestra cómo copiar datos de una base de datos de Amazon Redshift a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="5b729-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="5b729-180">Sin embargo, se pueden copiar datos **directamente** a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b729-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="5b729-181">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="5b729-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="5b729-182">Un servicio vinculado de tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5b729-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="5b729-183">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="5b729-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5b729-184">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5b729-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="5b729-185">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5b729-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5b729-186">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5b729-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="5b729-187">El ejemplo copia cada hora los datos de un resultado de consulta de Amazon Redshift en un blob.</span><span class="sxs-lookup"><span data-stu-id="5b729-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="5b729-188">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="5b729-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5b729-189">**Servicio vinculado de Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="5b729-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="5b729-190">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="5b729-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="5b729-191">**Conjunto de datos de entrada de Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="5b729-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="5b729-192">La opción `"external": true` informa al servicio Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="5b729-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="5b729-193">Establezca esta propiedad en true en un conjunto de datos de entrada no generado por una actividad en la canalización.</span><span class="sxs-lookup"><span data-stu-id="5b729-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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

<span data-ttu-id="5b729-194">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="5b729-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5b729-195">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="5b729-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5b729-196">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="5b729-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5b729-197">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="5b729-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="5b729-198">**Actividad de copia en una canalización con el origen de Azure Redshift (RelationalSource) y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="5b729-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="5b729-199">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="5b729-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="5b729-200">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5b729-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="5b729-201">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="5b729-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="5b729-202">Asignación de tipos para Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="5b729-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="5b729-203">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b729-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="5b729-204">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="5b729-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="5b729-205">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="5b729-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="5b729-206">Al mover datos a Amazon Redshift, se usan las asignaciones siguientes de los tipos Amazon Redshift a los tipos .NET.</span><span class="sxs-lookup"><span data-stu-id="5b729-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="5b729-207">Tipo Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="5b729-207">Amazon Redshift Type</span></span> | <span data-ttu-id="5b729-208">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="5b729-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="5b729-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="5b729-209">SMALLINT</span></span> |<span data-ttu-id="5b729-210">Int16</span><span class="sxs-lookup"><span data-stu-id="5b729-210">Int16</span></span> |
| <span data-ttu-id="5b729-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="5b729-211">INTEGER</span></span> |<span data-ttu-id="5b729-212">Int32</span><span class="sxs-lookup"><span data-stu-id="5b729-212">Int32</span></span> |
| <span data-ttu-id="5b729-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="5b729-213">BIGINT</span></span> |<span data-ttu-id="5b729-214">Int64</span><span class="sxs-lookup"><span data-stu-id="5b729-214">Int64</span></span> |
| <span data-ttu-id="5b729-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="5b729-215">DECIMAL</span></span> |<span data-ttu-id="5b729-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="5b729-216">Decimal</span></span> |
| <span data-ttu-id="5b729-217">REAL</span><span class="sxs-lookup"><span data-stu-id="5b729-217">REAL</span></span> |<span data-ttu-id="5b729-218">Single</span><span class="sxs-lookup"><span data-stu-id="5b729-218">Single</span></span> |
| <span data-ttu-id="5b729-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="5b729-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="5b729-220">Doble</span><span class="sxs-lookup"><span data-stu-id="5b729-220">Double</span></span> |
| <span data-ttu-id="5b729-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="5b729-221">BOOLEAN</span></span> |<span data-ttu-id="5b729-222">String</span><span class="sxs-lookup"><span data-stu-id="5b729-222">String</span></span> |
| <span data-ttu-id="5b729-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="5b729-223">CHAR</span></span> |<span data-ttu-id="5b729-224">String</span><span class="sxs-lookup"><span data-stu-id="5b729-224">String</span></span> |
| <span data-ttu-id="5b729-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="5b729-225">VARCHAR</span></span> |<span data-ttu-id="5b729-226">String</span><span class="sxs-lookup"><span data-stu-id="5b729-226">String</span></span> |
| <span data-ttu-id="5b729-227">DATE</span><span class="sxs-lookup"><span data-stu-id="5b729-227">DATE</span></span> |<span data-ttu-id="5b729-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="5b729-228">DateTime</span></span> |
| <span data-ttu-id="5b729-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="5b729-229">TIMESTAMP</span></span> |<span data-ttu-id="5b729-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="5b729-230">DateTime</span></span> |
| <span data-ttu-id="5b729-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="5b729-231">TEXT</span></span> |<span data-ttu-id="5b729-232">string</span><span class="sxs-lookup"><span data-stu-id="5b729-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="5b729-233">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="5b729-233">Map source to sink columns</span></span>
<span data-ttu-id="5b729-234">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5b729-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5b729-235">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="5b729-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="5b729-236">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="5b729-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="5b729-237">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="5b729-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5b729-238">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="5b729-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5b729-239">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="5b729-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="5b729-240">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="5b729-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5b729-241">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="5b729-241">Performance and Tuning</span></span>
<span data-ttu-id="5b729-242">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="5b729-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b729-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b729-243">Next Steps</span></span>
<span data-ttu-id="5b729-244">Consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b729-244">See the following articles:</span></span>

* <span data-ttu-id="5b729-245">[Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="5b729-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
