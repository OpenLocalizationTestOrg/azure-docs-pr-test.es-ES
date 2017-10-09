---
title: aaaMove datos de PostgreSQL mediante Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de base de datos PostgreSQL mediante Data Factory de Azure."
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
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="1e37d-103">Movimiento de datos de PostgreSQL mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="1e37d-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="1e37d-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="1e37d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="1e37d-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="1e37d-106">Puede copiar datos desde un almacén de datos local PostgreSQL datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="1e37d-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="1e37d-107">Para obtener una lista de almacenes de datos que se admiten como receptores por actividad de copia de hello, consulte [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1e37d-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1e37d-108">Factoría de datos actualmente permite mover datos desde un PostgreSQL base de datos de almacenes de datos tooother, pero no para mover los datos de otros datos de los almacenes de datos de PostgreSQL tooan.</span><span class="sxs-lookup"><span data-stu-id="1e37d-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1e37d-109">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e37d-109">prerequisites</span></span>

<span data-ttu-id="1e37d-110">Servicio de factoría de datos admite conexión orígenes de PostgreSQL de tooon local mediante Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1e37d-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="1e37d-111">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="1e37d-112">Puerta de enlace es necesario incluso si la base de datos de PostgreSQL Hola se hospeda en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e37d-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="1e37d-113">Puerta de enlace se puede instalar en hello mismo IaaS VM como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="1e37d-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="1e37d-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1e37d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="1e37d-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="1e37d-115">Supported versions and installation</span></span>
<span data-ttu-id="1e37d-116">Para Data Management Gateway tooconnect toohello base de datos PostgreSQL, instale hello [Ngpsql el proveedor de datos de PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 o por encima de Hola mismo sistema como Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1e37d-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="1e37d-117">Se admite la versión 7.4 o posterior de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e37d-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1e37d-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="1e37d-118">Getting started</span></span>
<span data-ttu-id="1e37d-119">Puede crear una canalización con una actividad de copia que mueva datos desde un almacén de datos de PostgreSQL local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="1e37d-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="1e37d-120">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="1e37d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="1e37d-121">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="1e37d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="1e37d-122">También puede usar Hola después herramientas toocreate una canalización:</span><span class="sxs-lookup"><span data-stu-id="1e37d-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="1e37d-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1e37d-123">Azure portal</span></span>
    - <span data-ttu-id="1e37d-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e37d-124">Visual Studio</span></span>
    - <span data-ttu-id="1e37d-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e37d-125">Azure PowerShell</span></span>
    - <span data-ttu-id="1e37d-126">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1e37d-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="1e37d-127">API de .NET</span><span class="sxs-lookup"><span data-stu-id="1e37d-127">.NET API</span></span>
    - <span data-ttu-id="1e37d-128">API de REST</span><span class="sxs-lookup"><span data-stu-id="1e37d-128">REST API</span></span>

     <span data-ttu-id="1e37d-129">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="1e37d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1e37d-130">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="1e37d-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="1e37d-131">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="1e37d-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="1e37d-132">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="1e37d-133">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="1e37d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1e37d-134">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="1e37d-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="1e37d-135">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="1e37d-136">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de PostgreSQL local, vea [ejemplo de JSON: copiar los datos de PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1e37d-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1e37d-137">Hola las secciones siguientes proporciona detalles acerca de propiedades JSON de almacén de datos de PostgreSQL de toodefine usado factoría de datos entidades tooa específica:</span><span class="sxs-lookup"><span data-stu-id="1e37d-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1e37d-138">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="1e37d-138">Linked service properties</span></span>
<span data-ttu-id="1e37d-139">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooPostgreSQL vinculado.</span><span class="sxs-lookup"><span data-stu-id="1e37d-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="1e37d-140">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1e37d-140">Property</span></span> | <span data-ttu-id="1e37d-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e37d-141">Description</span></span> | <span data-ttu-id="1e37d-142">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1e37d-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e37d-143">type</span><span class="sxs-lookup"><span data-stu-id="1e37d-143">type</span></span> |<span data-ttu-id="1e37d-144">propiedad de tipo Hello debe establecerse en: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="1e37d-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="1e37d-145">Sí</span><span class="sxs-lookup"><span data-stu-id="1e37d-145">Yes</span></span> |
| <span data-ttu-id="1e37d-146">Servidor</span><span class="sxs-lookup"><span data-stu-id="1e37d-146">server</span></span> |<span data-ttu-id="1e37d-147">Nombre del servidor de hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e37d-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="1e37d-148">Sí</span><span class="sxs-lookup"><span data-stu-id="1e37d-148">Yes</span></span> |
| <span data-ttu-id="1e37d-149">database</span><span class="sxs-lookup"><span data-stu-id="1e37d-149">database</span></span> |<span data-ttu-id="1e37d-150">Nombre de base de datos de PostgreSQL Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="1e37d-151">Sí</span><span class="sxs-lookup"><span data-stu-id="1e37d-151">Yes</span></span> |
| <span data-ttu-id="1e37d-152">schema</span><span class="sxs-lookup"><span data-stu-id="1e37d-152">schema</span></span> |<span data-ttu-id="1e37d-153">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="1e37d-154">nombre del esquema Hola distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1e37d-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="1e37d-155">No</span><span class="sxs-lookup"><span data-stu-id="1e37d-155">No</span></span> |
| <span data-ttu-id="1e37d-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1e37d-156">authenticationType</span></span> |<span data-ttu-id="1e37d-157">Tipo de autenticación que utiliza la base de datos de PostgreSQL tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1e37d-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="1e37d-158">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="1e37d-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="1e37d-159">Sí</span><span class="sxs-lookup"><span data-stu-id="1e37d-159">Yes</span></span> |
| <span data-ttu-id="1e37d-160">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="1e37d-160">username</span></span> |<span data-ttu-id="1e37d-161">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="1e37d-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="1e37d-162">No</span><span class="sxs-lookup"><span data-stu-id="1e37d-162">No</span></span> |
| <span data-ttu-id="1e37d-163">Contraseña</span><span class="sxs-lookup"><span data-stu-id="1e37d-163">password</span></span> |<span data-ttu-id="1e37d-164">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="1e37d-165">No</span><span class="sxs-lookup"><span data-stu-id="1e37d-165">No</span></span> |
| <span data-ttu-id="1e37d-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1e37d-166">gatewayName</span></span> |<span data-ttu-id="1e37d-167">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de PostgreSQL local de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1e37d-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="1e37d-168">Sí</span><span class="sxs-lookup"><span data-stu-id="1e37d-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="1e37d-169">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="1e37d-169">Dataset properties</span></span>
<span data-ttu-id="1e37d-170">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="1e37d-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1e37d-171">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1e37d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="1e37d-172">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="1e37d-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="1e37d-173">sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de PostgreSQL) tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e37d-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="1e37d-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1e37d-174">Property</span></span> | <span data-ttu-id="1e37d-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e37d-175">Description</span></span> | <span data-ttu-id="1e37d-176">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1e37d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e37d-177">tableName</span><span class="sxs-lookup"><span data-stu-id="1e37d-177">tableName</span></span> |<span data-ttu-id="1e37d-178">Nombre de tabla de Hola Hola instancia de base de datos PostgreSQL que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1e37d-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="1e37d-179">Hola tableName distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1e37d-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="1e37d-180">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="1e37d-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="1e37d-181">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="1e37d-181">Copy activity properties</span></span>
<span data-ttu-id="1e37d-182">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="1e37d-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1e37d-183">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="1e37d-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="1e37d-184">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="1e37d-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="1e37d-185">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="1e37d-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="1e37d-186">Cuando el origen es del tipo **RelationalSource** (que incluye PostgreSQL), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="1e37d-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1e37d-187">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1e37d-187">Property</span></span> | <span data-ttu-id="1e37d-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e37d-188">Description</span></span> | <span data-ttu-id="1e37d-189">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1e37d-189">Allowed values</span></span> | <span data-ttu-id="1e37d-190">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1e37d-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1e37d-191">query</span><span class="sxs-lookup"><span data-stu-id="1e37d-191">query</span></span> |<span data-ttu-id="1e37d-192">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="1e37d-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="1e37d-193">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1e37d-193">SQL query string.</span></span> <span data-ttu-id="1e37d-194">Por ejemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="1e37d-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="1e37d-195">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="1e37d-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="1e37d-196">Los nombres de esquema y tabla distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1e37d-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="1e37d-197">Encerrarlas entre `""` (comillas dobles) en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="1e37d-198">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="1e37d-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="1e37d-199">Ejemplo de JSON: copiar los datos de PostgreSQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="1e37d-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="1e37d-200">Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1e37d-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1e37d-201">Muestra cómo la base de datos toocopy de PostgreSQL datos tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="1e37d-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="1e37d-202">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e37d-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="1e37d-203">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="1e37d-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="1e37d-204">No incluye instrucciones paso a paso para la creación de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="1e37d-205">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="1e37d-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="1e37d-206">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="1e37d-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="1e37d-207">Un servicio vinculado de tipo [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1e37d-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="1e37d-208">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1e37d-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1e37d-209">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1e37d-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="1e37d-210">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1e37d-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1e37d-211">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1e37d-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1e37d-212">ejemplo de Hola copia datos de un resultado de consulta en el blob de tooa de base de datos de PostgreSQL cada hora.</span><span class="sxs-lookup"><span data-stu-id="1e37d-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="1e37d-213">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="1e37d-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="1e37d-214">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="1e37d-215">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="1e37d-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="1e37d-216">**Servicio vinculado de PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="1e37d-216">**PostgreSQL linked service:**</span></span>

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
<span data-ttu-id="1e37d-217">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="1e37d-217">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="1e37d-218">**Conjunto de datos de entrada de PostgreSQL**</span><span class="sxs-lookup"><span data-stu-id="1e37d-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="1e37d-219">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en PostgreSQL y contiene una columna denominada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="1e37d-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="1e37d-220">Establecer `"external": true` informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="1e37d-221">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="1e37d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="1e37d-222">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="1e37d-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1e37d-223">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="1e37d-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="1e37d-224">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="1e37d-225">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="1e37d-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="1e37d-226">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="1e37d-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="1e37d-227">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1e37d-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="1e37d-228">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola de tabla de public.usstates de hello en la base de datos de PostgreSQL Hola.</span><span class="sxs-lookup"><span data-stu-id="1e37d-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

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
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="1e37d-229">Asignación de tipos para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1e37d-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="1e37d-230">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="1e37d-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="1e37d-231">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="1e37d-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="1e37d-232">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="1e37d-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="1e37d-233">Al mover datos tooPostgreSQL, hello asignaciones siguientes sirven de PostgreSQL tipo too.NET.</span><span class="sxs-lookup"><span data-stu-id="1e37d-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="1e37d-234">Tipo de Base de datos de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1e37d-234">PostgreSQL Database type</span></span> | <span data-ttu-id="1e37d-235">Alias de PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="1e37d-235">PostgresSQL aliases</span></span> | <span data-ttu-id="1e37d-236">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="1e37d-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e37d-237">abstime</span><span class="sxs-lookup"><span data-stu-id="1e37d-237">abstime</span></span> | |<span data-ttu-id="1e37d-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="1e37d-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="1e37d-239">bigint</span><span class="sxs-lookup"><span data-stu-id="1e37d-239">bigint</span></span> |<span data-ttu-id="1e37d-240">int8</span><span class="sxs-lookup"><span data-stu-id="1e37d-240">int8</span></span> |<span data-ttu-id="1e37d-241">Int64</span><span class="sxs-lookup"><span data-stu-id="1e37d-241">Int64</span></span> |
| <span data-ttu-id="1e37d-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="1e37d-242">bigserial</span></span> |<span data-ttu-id="1e37d-243">serial8</span><span class="sxs-lookup"><span data-stu-id="1e37d-243">serial8</span></span> |<span data-ttu-id="1e37d-244">Int64</span><span class="sxs-lookup"><span data-stu-id="1e37d-244">Int64</span></span> |
| <span data-ttu-id="1e37d-245">bit</span><span class="sxs-lookup"><span data-stu-id="1e37d-245">bit [ (n) ]</span></span> | |<span data-ttu-id="1e37d-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="1e37d-247">bit variable [(n)]</span><span class="sxs-lookup"><span data-stu-id="1e37d-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="1e37d-248">varbit</span><span class="sxs-lookup"><span data-stu-id="1e37d-248">varbit</span></span> |<span data-ttu-id="1e37d-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-249">Byte[], String</span></span> |
| <span data-ttu-id="1e37d-250">boolean</span><span class="sxs-lookup"><span data-stu-id="1e37d-250">boolean</span></span> |<span data-ttu-id="1e37d-251">booleano</span><span class="sxs-lookup"><span data-stu-id="1e37d-251">bool</span></span> |<span data-ttu-id="1e37d-252">boolean</span><span class="sxs-lookup"><span data-stu-id="1e37d-252">Boolean</span></span> |
| <span data-ttu-id="1e37d-253">Box</span><span class="sxs-lookup"><span data-stu-id="1e37d-253">box</span></span> | |<span data-ttu-id="1e37d-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-255">bytea</span><span class="sxs-lookup"><span data-stu-id="1e37d-255">bytea</span></span> | |<span data-ttu-id="1e37d-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-257">character [ (n) ]</span></span> |<span data-ttu-id="1e37d-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-258">char [ (n) ]</span></span> |<span data-ttu-id="1e37d-259">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-259">String</span></span> |
| <span data-ttu-id="1e37d-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-260">character varying [ (n) ]</span></span> |<span data-ttu-id="1e37d-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-261">varchar [ (n) ]</span></span> |<span data-ttu-id="1e37d-262">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-262">String</span></span> |
| <span data-ttu-id="1e37d-263">cid</span><span class="sxs-lookup"><span data-stu-id="1e37d-263">cid</span></span> | |<span data-ttu-id="1e37d-264">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-264">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-265">cidr</span><span class="sxs-lookup"><span data-stu-id="1e37d-265">cidr</span></span> | |<span data-ttu-id="1e37d-266">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-266">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-267">circle</span><span class="sxs-lookup"><span data-stu-id="1e37d-267">circle</span></span> | |<span data-ttu-id="1e37d-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-269">fecha</span><span class="sxs-lookup"><span data-stu-id="1e37d-269">date</span></span> | |<span data-ttu-id="1e37d-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="1e37d-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="1e37d-271">daterange</span><span class="sxs-lookup"><span data-stu-id="1e37d-271">daterange</span></span> | |<span data-ttu-id="1e37d-272">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-272">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-273">double precision</span><span class="sxs-lookup"><span data-stu-id="1e37d-273">double precision</span></span> |<span data-ttu-id="1e37d-274">float8</span><span class="sxs-lookup"><span data-stu-id="1e37d-274">float8</span></span> |<span data-ttu-id="1e37d-275">Doble</span><span class="sxs-lookup"><span data-stu-id="1e37d-275">Double</span></span> |
| <span data-ttu-id="1e37d-276">inet</span><span class="sxs-lookup"><span data-stu-id="1e37d-276">inet</span></span> | |<span data-ttu-id="1e37d-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-278">intarry</span><span class="sxs-lookup"><span data-stu-id="1e37d-278">intarry</span></span> | |<span data-ttu-id="1e37d-279">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-279">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-280">int4range</span><span class="sxs-lookup"><span data-stu-id="1e37d-280">int4range</span></span> | |<span data-ttu-id="1e37d-281">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-281">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-282">int8range</span><span class="sxs-lookup"><span data-stu-id="1e37d-282">int8range</span></span> | |<span data-ttu-id="1e37d-283">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-283">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-284">integer</span><span class="sxs-lookup"><span data-stu-id="1e37d-284">integer</span></span> |<span data-ttu-id="1e37d-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="1e37d-285">int, int4</span></span> |<span data-ttu-id="1e37d-286">Int32</span><span class="sxs-lookup"><span data-stu-id="1e37d-286">Int32</span></span> |
| <span data-ttu-id="1e37d-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="1e37d-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1e37d-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="1e37d-289">json</span><span class="sxs-lookup"><span data-stu-id="1e37d-289">json</span></span> | |<span data-ttu-id="1e37d-290">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-290">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="1e37d-291">jsonb</span></span> | |<span data-ttu-id="1e37d-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="1e37d-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="1e37d-293">line</span><span class="sxs-lookup"><span data-stu-id="1e37d-293">line</span></span> | |<span data-ttu-id="1e37d-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-295">lseg</span><span class="sxs-lookup"><span data-stu-id="1e37d-295">lseg</span></span> | |<span data-ttu-id="1e37d-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="1e37d-297">macaddr</span></span> | |<span data-ttu-id="1e37d-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-299">money</span><span class="sxs-lookup"><span data-stu-id="1e37d-299">money</span></span> | |<span data-ttu-id="1e37d-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="1e37d-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="1e37d-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="1e37d-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="1e37d-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="1e37d-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="1e37d-303">Decimal</span></span> |
| <span data-ttu-id="1e37d-304">numrange</span><span class="sxs-lookup"><span data-stu-id="1e37d-304">numrange</span></span> | |<span data-ttu-id="1e37d-305">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-305">String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-306">oid</span><span class="sxs-lookup"><span data-stu-id="1e37d-306">oid</span></span> | |<span data-ttu-id="1e37d-307">Int32</span><span class="sxs-lookup"><span data-stu-id="1e37d-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="1e37d-308">path</span><span class="sxs-lookup"><span data-stu-id="1e37d-308">path</span></span> | |<span data-ttu-id="1e37d-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="1e37d-310">pg_lsn</span></span> | |<span data-ttu-id="1e37d-311">Int64</span><span class="sxs-lookup"><span data-stu-id="1e37d-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="1e37d-312">point</span><span class="sxs-lookup"><span data-stu-id="1e37d-312">point</span></span> | |<span data-ttu-id="1e37d-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-314">polygon</span><span class="sxs-lookup"><span data-stu-id="1e37d-314">polygon</span></span> | |<span data-ttu-id="1e37d-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="1e37d-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="1e37d-316">real</span><span class="sxs-lookup"><span data-stu-id="1e37d-316">real</span></span> |<span data-ttu-id="1e37d-317">float4</span><span class="sxs-lookup"><span data-stu-id="1e37d-317">float4</span></span> |<span data-ttu-id="1e37d-318">Single</span><span class="sxs-lookup"><span data-stu-id="1e37d-318">Single</span></span> |
| <span data-ttu-id="1e37d-319">smallint</span><span class="sxs-lookup"><span data-stu-id="1e37d-319">smallint</span></span> |<span data-ttu-id="1e37d-320">int2</span><span class="sxs-lookup"><span data-stu-id="1e37d-320">int2</span></span> |<span data-ttu-id="1e37d-321">Int16</span><span class="sxs-lookup"><span data-stu-id="1e37d-321">Int16</span></span> |
| <span data-ttu-id="1e37d-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="1e37d-322">smallserial</span></span> |<span data-ttu-id="1e37d-323">serial2</span><span class="sxs-lookup"><span data-stu-id="1e37d-323">serial2</span></span> |<span data-ttu-id="1e37d-324">Int16</span><span class="sxs-lookup"><span data-stu-id="1e37d-324">Int16</span></span> |
| <span data-ttu-id="1e37d-325">serial</span><span class="sxs-lookup"><span data-stu-id="1e37d-325">serial</span></span> |<span data-ttu-id="1e37d-326">serial4</span><span class="sxs-lookup"><span data-stu-id="1e37d-326">serial4</span></span> |<span data-ttu-id="1e37d-327">Int32</span><span class="sxs-lookup"><span data-stu-id="1e37d-327">Int32</span></span> |
| <span data-ttu-id="1e37d-328">text</span><span class="sxs-lookup"><span data-stu-id="1e37d-328">text</span></span> | |<span data-ttu-id="1e37d-329">String</span><span class="sxs-lookup"><span data-stu-id="1e37d-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="1e37d-330">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="1e37d-330">Map source toosink columns</span></span>
<span data-ttu-id="1e37d-331">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1e37d-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1e37d-332">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="1e37d-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="1e37d-333">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="1e37d-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="1e37d-334">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="1e37d-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1e37d-335">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="1e37d-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1e37d-336">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="1e37d-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1e37d-337">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="1e37d-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1e37d-338">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="1e37d-338">Performance and Tuning</span></span>
<span data-ttu-id="1e37d-339">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="1e37d-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
