---
title: Movimiento de datos de PostgreSQL mediante Azure Data Factory | Microsoft Docs
description: "Obtenga información acerca de cómo mover los datos de la base de datos de PostgreSQL mediante Factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: fd26f0d03f8b0b352a6544a81ad952d2e2a1b7a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="8066d-103">Movimiento de datos de PostgreSQL mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="8066d-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="8066d-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos desde una base de datos de PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="8066d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="8066d-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8066d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="8066d-106">Puede copiar datos de un almacén de datos de PostgreSQL local a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="8066d-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="8066d-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como receptores.</span><span class="sxs-lookup"><span data-stu-id="8066d-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="8066d-108">Data Factory solo admite actualmente el movimiento de datos de una base de datos de PostgreSQL a otros almacenes de datos, pero no viceversa.</span><span class="sxs-lookup"><span data-stu-id="8066d-108">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8066d-109">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8066d-109">prerequisites</span></span>

<span data-ttu-id="8066d-110">El servicio Factoría de datos admite la conexión a orígenes de PostgreSQL locales mediante Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="8066d-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="8066d-111">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8066d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="8066d-112">La puerta de enlace es necesaria incluso si la base de datos PostgreSQL está hospedada en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="8066d-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="8066d-113">Puede instalar la puerta de enlace en la misma máquina virtual de IaaS como almacén de datos o en una máquina virtual diferente, siempre y cuando la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-113">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="8066d-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8066d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="8066d-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="8066d-115">Supported versions and installation</span></span>
<span data-ttu-id="8066d-116">Para que la puerta de enlace de administración de datos se conecte a la base de datos de PostgreSQL, instale la versión 2.0.12 o posterior del [proveedor de datos Ngpsql para PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) en el mismo sistema que Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="8066d-116">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="8066d-117">Se admite la versión 7.4 o posterior de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8066d-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="8066d-118">Getting started</span></span>
<span data-ttu-id="8066d-119">Puede crear una canalización con una actividad de copia que mueva datos desde un almacén de datos de PostgreSQL local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="8066d-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="8066d-120">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="8066d-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8066d-121">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="8066d-122">Puede usar las siguientes herramientas para crear una canalización:</span><span class="sxs-lookup"><span data-stu-id="8066d-122">You can also use the following tools to create a pipeline:</span></span> 
    - <span data-ttu-id="8066d-123">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8066d-123">Azure portal</span></span>
    - <span data-ttu-id="8066d-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8066d-124">Visual Studio</span></span>
    - <span data-ttu-id="8066d-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8066d-125">Azure PowerShell</span></span>
    - <span data-ttu-id="8066d-126">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8066d-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="8066d-127">API de .NET</span><span class="sxs-lookup"><span data-stu-id="8066d-127">.NET API</span></span>
    - <span data-ttu-id="8066d-128">API de REST</span><span class="sxs-lookup"><span data-stu-id="8066d-128">REST API</span></span>

     <span data-ttu-id="8066d-129">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="8066d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8066d-130">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="8066d-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="8066d-131">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8066d-132">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="8066d-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8066d-133">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="8066d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8066d-134">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="8066d-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8066d-135">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="8066d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8066d-136">Si desea obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan con el fin de copiar los datos desde un almacén de datos de PostgreSQL local, consulte la sección [Ejemplo de JSON: Copia de datos de PostgreSQL a un blob de Azure](#json-example-copy-data-from-postgresql-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8066d-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="8066d-137">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos de PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="8066d-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8066d-138">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="8066d-138">Linked service properties</span></span>
<span data-ttu-id="8066d-139">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-139">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="8066d-140">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8066d-140">Property</span></span> | <span data-ttu-id="8066d-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="8066d-141">Description</span></span> | <span data-ttu-id="8066d-142">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8066d-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8066d-143">type</span><span class="sxs-lookup"><span data-stu-id="8066d-143">type</span></span> |<span data-ttu-id="8066d-144">La propiedad type debe establecerse en: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="8066d-144">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="8066d-145">Sí</span><span class="sxs-lookup"><span data-stu-id="8066d-145">Yes</span></span> |
| <span data-ttu-id="8066d-146">server</span><span class="sxs-lookup"><span data-stu-id="8066d-146">server</span></span> |<span data-ttu-id="8066d-147">Nombre del servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-147">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="8066d-148">Sí</span><span class="sxs-lookup"><span data-stu-id="8066d-148">Yes</span></span> |
| <span data-ttu-id="8066d-149">database</span><span class="sxs-lookup"><span data-stu-id="8066d-149">database</span></span> |<span data-ttu-id="8066d-150">Nombre de la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-150">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="8066d-151">Sí</span><span class="sxs-lookup"><span data-stu-id="8066d-151">Yes</span></span> |
| <span data-ttu-id="8066d-152">schema</span><span class="sxs-lookup"><span data-stu-id="8066d-152">schema</span></span> |<span data-ttu-id="8066d-153">Nombre del esquema de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-153">Name of the schema in the database.</span></span> <span data-ttu-id="8066d-154">El nombre del esquema distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8066d-154">The schema name is case-sensitive.</span></span> |<span data-ttu-id="8066d-155">No</span><span class="sxs-lookup"><span data-stu-id="8066d-155">No</span></span> |
| <span data-ttu-id="8066d-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8066d-156">authenticationType</span></span> |<span data-ttu-id="8066d-157">Tipo de autenticación usado para conectarse a la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-157">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="8066d-158">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="8066d-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8066d-159">Sí</span><span class="sxs-lookup"><span data-stu-id="8066d-159">Yes</span></span> |
| <span data-ttu-id="8066d-160">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="8066d-160">username</span></span> |<span data-ttu-id="8066d-161">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="8066d-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="8066d-162">No</span><span class="sxs-lookup"><span data-stu-id="8066d-162">No</span></span> |
| <span data-ttu-id="8066d-163">contraseña</span><span class="sxs-lookup"><span data-stu-id="8066d-163">password</span></span> |<span data-ttu-id="8066d-164">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="8066d-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8066d-165">No</span><span class="sxs-lookup"><span data-stu-id="8066d-165">No</span></span> |
| <span data-ttu-id="8066d-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8066d-166">gatewayName</span></span> |<span data-ttu-id="8066d-167">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse a la base de datos de PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="8066d-167">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="8066d-168">Sí</span><span class="sxs-lookup"><span data-stu-id="8066d-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="8066d-169">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="8066d-169">Dataset properties</span></span>
<span data-ttu-id="8066d-170">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="8066d-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8066d-171">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="8066d-172">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-172">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8066d-173">La sección typeProperties del conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de PostgreSQL) tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="8066d-173">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="8066d-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8066d-174">Property</span></span> | <span data-ttu-id="8066d-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="8066d-175">Description</span></span> | <span data-ttu-id="8066d-176">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8066d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8066d-177">tableName</span><span class="sxs-lookup"><span data-stu-id="8066d-177">tableName</span></span> |<span data-ttu-id="8066d-178">Nombre de la tabla en la instancia de Base de datos de PostgreSQL a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="8066d-178">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="8066d-179">tableName distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8066d-179">The tableName is case-sensitive.</span></span> |<span data-ttu-id="8066d-180">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="8066d-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8066d-181">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="8066d-181">Copy activity properties</span></span>
<span data-ttu-id="8066d-182">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8066d-182">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8066d-183">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="8066d-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="8066d-184">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="8066d-184">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="8066d-185">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="8066d-185">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8066d-186">Cuando el origen es de tipo **RelationalSource** (lo que incluye PostgreSQL), están disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="8066d-186">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="8066d-187">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8066d-187">Property</span></span> | <span data-ttu-id="8066d-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="8066d-188">Description</span></span> | <span data-ttu-id="8066d-189">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8066d-189">Allowed values</span></span> | <span data-ttu-id="8066d-190">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8066d-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8066d-191">query</span><span class="sxs-lookup"><span data-stu-id="8066d-191">query</span></span> |<span data-ttu-id="8066d-192">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-192">Use the custom query to read data.</span></span> |<span data-ttu-id="8066d-193">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-193">SQL query string.</span></span> <span data-ttu-id="8066d-194">Por ejemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="8066d-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="8066d-195">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="8066d-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="8066d-196">Los nombres de esquema y tabla distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8066d-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="8066d-197">Incluya los nombres entre comillas dobles `""` en la consulta.</span><span class="sxs-lookup"><span data-stu-id="8066d-197">Enclose them in `""` (double quotes) in the query.</span></span>  

<span data-ttu-id="8066d-198">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8066d-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="8066d-199">Ejemplo de JSON: Copia de datos de PostgreSQL a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="8066d-199">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="8066d-200">Este ejemplo proporciona definiciones de JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8066d-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8066d-201">Se muestra cómo copiar datos desde la base de datos PostgreSQL al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="8066d-201">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="8066d-202">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="8066d-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="8066d-203">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="8066d-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="8066d-204">No incluye instrucciones paso a paso para crear la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8066d-204">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="8066d-205">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="8066d-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="8066d-206">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="8066d-206">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="8066d-207">Un servicio vinculado de tipo [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8066d-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8066d-208">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="8066d-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8066d-209">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8066d-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8066d-210">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8066d-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8066d-211">La [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8066d-211">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8066d-212">El ejemplo copia cada hora los datos de un resultado de consulta de la base de datos PostgreSQL en un blob.</span><span class="sxs-lookup"><span data-stu-id="8066d-212">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="8066d-213">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="8066d-213">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8066d-214">En primer lugar, configure Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="8066d-214">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="8066d-215">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="8066d-215">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8066d-216">**Servicio vinculado de PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="8066d-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="8066d-217">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="8066d-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="8066d-218">**Conjunto de datos de entrada de PostgreSQL**</span><span class="sxs-lookup"><span data-stu-id="8066d-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="8066d-219">El ejemplo supone que ha creado una tabla "MyTable" en PostgreSQL y que contiene una columna denominada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="8066d-219">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="8066d-220">La opción `"external": true` informa al servicio Data Factory de que el conjunto de datos es externo a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="8066d-220">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="8066d-221">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="8066d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8066d-222">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="8066d-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8066d-223">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="8066d-223">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8066d-224">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="8066d-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="8066d-225">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="8066d-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="8066d-226">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="8066d-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="8066d-227">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8066d-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="8066d-228">La consulta SQL especificada para la propiedad **query** selecciona los datos de la tabla public.usstates de la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8066d-228">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="8066d-229">Asignación de tipos para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8066d-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="8066d-230">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="8066d-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="8066d-231">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="8066d-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="8066d-232">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="8066d-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="8066d-233">Al mover datos a PostgreSQL, se usan las asignaciones siguientes de tipo PostgreSQL a tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="8066d-233">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="8066d-234">Tipo de Base de datos de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8066d-234">PostgreSQL Database type</span></span> | <span data-ttu-id="8066d-235">Alias de PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="8066d-235">PostgresSQL aliases</span></span> | <span data-ttu-id="8066d-236">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8066d-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8066d-237">abstime</span><span class="sxs-lookup"><span data-stu-id="8066d-237">abstime</span></span> | |<span data-ttu-id="8066d-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="8066d-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="8066d-239">bigint</span><span class="sxs-lookup"><span data-stu-id="8066d-239">bigint</span></span> |<span data-ttu-id="8066d-240">int8</span><span class="sxs-lookup"><span data-stu-id="8066d-240">int8</span></span> |<span data-ttu-id="8066d-241">Int64</span><span class="sxs-lookup"><span data-stu-id="8066d-241">Int64</span></span> |
| <span data-ttu-id="8066d-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="8066d-242">bigserial</span></span> |<span data-ttu-id="8066d-243">serial8</span><span class="sxs-lookup"><span data-stu-id="8066d-243">serial8</span></span> |<span data-ttu-id="8066d-244">Int64</span><span class="sxs-lookup"><span data-stu-id="8066d-244">Int64</span></span> |
| <span data-ttu-id="8066d-245">bit</span><span class="sxs-lookup"><span data-stu-id="8066d-245">bit [ (n) ]</span></span> | |<span data-ttu-id="8066d-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="8066d-247">bit variable [(n)]</span><span class="sxs-lookup"><span data-stu-id="8066d-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="8066d-248">varbit</span><span class="sxs-lookup"><span data-stu-id="8066d-248">varbit</span></span> |<span data-ttu-id="8066d-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-249">Byte[], String</span></span> |
| <span data-ttu-id="8066d-250">boolean</span><span class="sxs-lookup"><span data-stu-id="8066d-250">boolean</span></span> |<span data-ttu-id="8066d-251">booleano</span><span class="sxs-lookup"><span data-stu-id="8066d-251">bool</span></span> |<span data-ttu-id="8066d-252">boolean</span><span class="sxs-lookup"><span data-stu-id="8066d-252">Boolean</span></span> |
| <span data-ttu-id="8066d-253">Box</span><span class="sxs-lookup"><span data-stu-id="8066d-253">box</span></span> | |<span data-ttu-id="8066d-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-255">bytea</span><span class="sxs-lookup"><span data-stu-id="8066d-255">bytea</span></span> | |<span data-ttu-id="8066d-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-257">character [ (n) ]</span></span> |<span data-ttu-id="8066d-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-258">char [ (n) ]</span></span> |<span data-ttu-id="8066d-259">String</span><span class="sxs-lookup"><span data-stu-id="8066d-259">String</span></span> |
| <span data-ttu-id="8066d-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-260">character varying [ (n) ]</span></span> |<span data-ttu-id="8066d-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-261">varchar [ (n) ]</span></span> |<span data-ttu-id="8066d-262">String</span><span class="sxs-lookup"><span data-stu-id="8066d-262">String</span></span> |
| <span data-ttu-id="8066d-263">cid</span><span class="sxs-lookup"><span data-stu-id="8066d-263">cid</span></span> | |<span data-ttu-id="8066d-264">String</span><span class="sxs-lookup"><span data-stu-id="8066d-264">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-265">cidr</span><span class="sxs-lookup"><span data-stu-id="8066d-265">cidr</span></span> | |<span data-ttu-id="8066d-266">String</span><span class="sxs-lookup"><span data-stu-id="8066d-266">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-267">circle</span><span class="sxs-lookup"><span data-stu-id="8066d-267">circle</span></span> | |<span data-ttu-id="8066d-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-269">fecha</span><span class="sxs-lookup"><span data-stu-id="8066d-269">date</span></span> | |<span data-ttu-id="8066d-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="8066d-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="8066d-271">daterange</span><span class="sxs-lookup"><span data-stu-id="8066d-271">daterange</span></span> | |<span data-ttu-id="8066d-272">String</span><span class="sxs-lookup"><span data-stu-id="8066d-272">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-273">double precision</span><span class="sxs-lookup"><span data-stu-id="8066d-273">double precision</span></span> |<span data-ttu-id="8066d-274">float8</span><span class="sxs-lookup"><span data-stu-id="8066d-274">float8</span></span> |<span data-ttu-id="8066d-275">Doble</span><span class="sxs-lookup"><span data-stu-id="8066d-275">Double</span></span> |
| <span data-ttu-id="8066d-276">inet</span><span class="sxs-lookup"><span data-stu-id="8066d-276">inet</span></span> | |<span data-ttu-id="8066d-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-278">intarry</span><span class="sxs-lookup"><span data-stu-id="8066d-278">intarry</span></span> | |<span data-ttu-id="8066d-279">String</span><span class="sxs-lookup"><span data-stu-id="8066d-279">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-280">int4range</span><span class="sxs-lookup"><span data-stu-id="8066d-280">int4range</span></span> | |<span data-ttu-id="8066d-281">String</span><span class="sxs-lookup"><span data-stu-id="8066d-281">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-282">int8range</span><span class="sxs-lookup"><span data-stu-id="8066d-282">int8range</span></span> | |<span data-ttu-id="8066d-283">String</span><span class="sxs-lookup"><span data-stu-id="8066d-283">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-284">integer</span><span class="sxs-lookup"><span data-stu-id="8066d-284">integer</span></span> |<span data-ttu-id="8066d-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="8066d-285">int, int4</span></span> |<span data-ttu-id="8066d-286">Int32</span><span class="sxs-lookup"><span data-stu-id="8066d-286">Int32</span></span> |
| <span data-ttu-id="8066d-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="8066d-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8066d-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="8066d-289">json</span><span class="sxs-lookup"><span data-stu-id="8066d-289">json</span></span> | |<span data-ttu-id="8066d-290">String</span><span class="sxs-lookup"><span data-stu-id="8066d-290">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="8066d-291">jsonb</span></span> | |<span data-ttu-id="8066d-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8066d-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="8066d-293">line</span><span class="sxs-lookup"><span data-stu-id="8066d-293">line</span></span> | |<span data-ttu-id="8066d-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-295">lseg</span><span class="sxs-lookup"><span data-stu-id="8066d-295">lseg</span></span> | |<span data-ttu-id="8066d-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="8066d-297">macaddr</span></span> | |<span data-ttu-id="8066d-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-299">money</span><span class="sxs-lookup"><span data-stu-id="8066d-299">money</span></span> | |<span data-ttu-id="8066d-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="8066d-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="8066d-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="8066d-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="8066d-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="8066d-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="8066d-303">Decimal</span></span> |
| <span data-ttu-id="8066d-304">numrange</span><span class="sxs-lookup"><span data-stu-id="8066d-304">numrange</span></span> | |<span data-ttu-id="8066d-305">String</span><span class="sxs-lookup"><span data-stu-id="8066d-305">String</span></span> |&nbsp;
| <span data-ttu-id="8066d-306">oid</span><span class="sxs-lookup"><span data-stu-id="8066d-306">oid</span></span> | |<span data-ttu-id="8066d-307">Int32</span><span class="sxs-lookup"><span data-stu-id="8066d-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="8066d-308">path</span><span class="sxs-lookup"><span data-stu-id="8066d-308">path</span></span> | |<span data-ttu-id="8066d-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="8066d-310">pg_lsn</span></span> | |<span data-ttu-id="8066d-311">Int64</span><span class="sxs-lookup"><span data-stu-id="8066d-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="8066d-312">point</span><span class="sxs-lookup"><span data-stu-id="8066d-312">point</span></span> | |<span data-ttu-id="8066d-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-314">polygon</span><span class="sxs-lookup"><span data-stu-id="8066d-314">polygon</span></span> | |<span data-ttu-id="8066d-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8066d-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8066d-316">real</span><span class="sxs-lookup"><span data-stu-id="8066d-316">real</span></span> |<span data-ttu-id="8066d-317">float4</span><span class="sxs-lookup"><span data-stu-id="8066d-317">float4</span></span> |<span data-ttu-id="8066d-318">Single</span><span class="sxs-lookup"><span data-stu-id="8066d-318">Single</span></span> |
| <span data-ttu-id="8066d-319">smallint</span><span class="sxs-lookup"><span data-stu-id="8066d-319">smallint</span></span> |<span data-ttu-id="8066d-320">int2</span><span class="sxs-lookup"><span data-stu-id="8066d-320">int2</span></span> |<span data-ttu-id="8066d-321">Int16</span><span class="sxs-lookup"><span data-stu-id="8066d-321">Int16</span></span> |
| <span data-ttu-id="8066d-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="8066d-322">smallserial</span></span> |<span data-ttu-id="8066d-323">serial2</span><span class="sxs-lookup"><span data-stu-id="8066d-323">serial2</span></span> |<span data-ttu-id="8066d-324">Int16</span><span class="sxs-lookup"><span data-stu-id="8066d-324">Int16</span></span> |
| <span data-ttu-id="8066d-325">serial</span><span class="sxs-lookup"><span data-stu-id="8066d-325">serial</span></span> |<span data-ttu-id="8066d-326">serial4</span><span class="sxs-lookup"><span data-stu-id="8066d-326">serial4</span></span> |<span data-ttu-id="8066d-327">Int32</span><span class="sxs-lookup"><span data-stu-id="8066d-327">Int32</span></span> |
| <span data-ttu-id="8066d-328">text</span><span class="sxs-lookup"><span data-stu-id="8066d-328">text</span></span> | |<span data-ttu-id="8066d-329">string</span><span class="sxs-lookup"><span data-stu-id="8066d-329">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="8066d-330">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="8066d-330">Map source to sink columns</span></span>
<span data-ttu-id="8066d-331">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8066d-331">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8066d-332">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="8066d-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="8066d-333">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="8066d-333">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="8066d-334">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="8066d-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8066d-335">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8066d-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8066d-336">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="8066d-336">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="8066d-337">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8066d-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8066d-338">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="8066d-338">Performance and Tuning</span></span>
<span data-ttu-id="8066d-339">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="8066d-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
