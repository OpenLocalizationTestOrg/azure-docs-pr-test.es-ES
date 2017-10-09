---
title: aaaMove datos de Sybase con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de base de datos de Sybase con Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="5179f-103">Movimiento de datos de Sybase mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="5179f-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="5179f-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de Sybase local.</span><span class="sxs-lookup"><span data-stu-id="5179f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="5179f-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="5179f-106">Puede copiar datos desde un almacén de datos local Sybase datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="5179f-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="5179f-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="5179f-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5179f-108">Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos de datos de Sybase, pero no para mover los datos de otro almacén de datos de Sybase tooa de datos almacenes.</span><span class="sxs-lookup"><span data-stu-id="5179f-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5179f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5179f-109">Prerequisites</span></span>
<span data-ttu-id="5179f-110">Servicio de factoría de datos admite conexión orígenes de Sybase local tooon con hello Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="5179f-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="5179f-111">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="5179f-112">Puerta de enlace es necesario incluso si la base de datos de Sybase Hola se hospeda en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="5179f-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="5179f-113">Puede instalar la puerta de enlace de hello en Hola mismo IaaS VM como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="5179f-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="5179f-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="5179f-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="5179f-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="5179f-115">Supported versions and installation</span></span>
<span data-ttu-id="5179f-116">Para Data Management Gateway tooconnect toohello base de datos de Sybase, necesita hello tooinstall [proveedor de datos de Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 o por encima de Hola mismo sistema como Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="5179f-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="5179f-117">Se admite la versión 16 de Sybase o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="5179f-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5179f-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="5179f-118">Getting started</span></span>
<span data-ttu-id="5179f-119">Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="5179f-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="5179f-120">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="5179f-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5179f-121">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="5179f-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="5179f-122">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="5179f-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5179f-123">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="5179f-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5179f-124">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="5179f-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5179f-125">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="5179f-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5179f-126">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5179f-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="5179f-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5179f-128">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="5179f-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5179f-129">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5179f-130">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de Sybase local, vea [ejemplo de JSON: copiar los datos de Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="5179f-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5179f-131">Hola las secciones siguientes proporciona detalles acerca de propiedades JSON que forman el almacén de datos de Sybase de toodefine usado factoría de datos entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="5179f-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5179f-132">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="5179f-132">Linked service properties</span></span>
<span data-ttu-id="5179f-133">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooSybase vinculado.</span><span class="sxs-lookup"><span data-stu-id="5179f-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="5179f-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5179f-134">Property</span></span> | <span data-ttu-id="5179f-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="5179f-135">Description</span></span> | <span data-ttu-id="5179f-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5179f-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5179f-137">type</span><span class="sxs-lookup"><span data-stu-id="5179f-137">type</span></span> |<span data-ttu-id="5179f-138">propiedad de tipo Hello debe establecerse en: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="5179f-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="5179f-139">Sí</span><span class="sxs-lookup"><span data-stu-id="5179f-139">Yes</span></span> |
| <span data-ttu-id="5179f-140">Servidor</span><span class="sxs-lookup"><span data-stu-id="5179f-140">server</span></span> |<span data-ttu-id="5179f-141">Nombre del servidor de Sybase Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="5179f-142">Sí</span><span class="sxs-lookup"><span data-stu-id="5179f-142">Yes</span></span> |
| <span data-ttu-id="5179f-143">database</span><span class="sxs-lookup"><span data-stu-id="5179f-143">database</span></span> |<span data-ttu-id="5179f-144">Nombre de base de datos de Sybase Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="5179f-145">Sí</span><span class="sxs-lookup"><span data-stu-id="5179f-145">Yes</span></span> |
| <span data-ttu-id="5179f-146">schema</span><span class="sxs-lookup"><span data-stu-id="5179f-146">schema</span></span> |<span data-ttu-id="5179f-147">Nombre del esquema de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="5179f-148">No</span><span class="sxs-lookup"><span data-stu-id="5179f-148">No</span></span> |
| <span data-ttu-id="5179f-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="5179f-149">authenticationType</span></span> |<span data-ttu-id="5179f-150">Tipo de autenticación usa tooconnect toohello bases de datos Sybase.</span><span class="sxs-lookup"><span data-stu-id="5179f-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="5179f-151">Los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="5179f-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="5179f-152">Sí</span><span class="sxs-lookup"><span data-stu-id="5179f-152">Yes</span></span> |
| <span data-ttu-id="5179f-153">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="5179f-153">username</span></span> |<span data-ttu-id="5179f-154">Especifique el nombre de usuario si usa la autenticación Basic o Windows.</span><span class="sxs-lookup"><span data-stu-id="5179f-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="5179f-155">No</span><span class="sxs-lookup"><span data-stu-id="5179f-155">No</span></span> |
| <span data-ttu-id="5179f-156">Contraseña</span><span class="sxs-lookup"><span data-stu-id="5179f-156">password</span></span> |<span data-ttu-id="5179f-157">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="5179f-158">No</span><span class="sxs-lookup"><span data-stu-id="5179f-158">No</span></span> |
| <span data-ttu-id="5179f-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="5179f-159">gatewayName</span></span> |<span data-ttu-id="5179f-160">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de Sybase local de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="5179f-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="5179f-161">Sí</span><span class="sxs-lookup"><span data-stu-id="5179f-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5179f-162">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="5179f-162">Dataset properties</span></span>
<span data-ttu-id="5179f-163">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="5179f-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5179f-164">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="5179f-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5179f-165">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="5179f-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5179f-166">Hola **typeProperties** sección para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de Sybase) tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="5179f-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="5179f-167">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5179f-167">Property</span></span> | <span data-ttu-id="5179f-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="5179f-168">Description</span></span> | <span data-ttu-id="5179f-169">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5179f-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5179f-170">tableName</span><span class="sxs-lookup"><span data-stu-id="5179f-170">tableName</span></span> |<span data-ttu-id="5179f-171">Nombre de tabla de Hola Hola instancia de base de datos de Sybase que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="5179f-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="5179f-172">No (si se especifica **query** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="5179f-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="5179f-173">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="5179f-173">Copy activity properties</span></span>
<span data-ttu-id="5179f-174">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5179f-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5179f-175">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="5179f-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="5179f-176">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="5179f-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="5179f-177">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="5179f-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5179f-178">Cuando el origen de hello es del tipo **RelationalSource** (que incluye Sybase), Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="5179f-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="5179f-179">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5179f-179">Property</span></span> | <span data-ttu-id="5179f-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="5179f-180">Description</span></span> | <span data-ttu-id="5179f-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="5179f-181">Allowed values</span></span> | <span data-ttu-id="5179f-182">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5179f-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5179f-183">query</span><span class="sxs-lookup"><span data-stu-id="5179f-183">query</span></span> |<span data-ttu-id="5179f-184">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="5179f-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="5179f-185">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="5179f-185">SQL query string.</span></span> <span data-ttu-id="5179f-186">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="5179f-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="5179f-187">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="5179f-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="5179f-188">Ejemplo de JSON: copiar los datos de Sybase tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="5179f-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="5179f-189">Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5179f-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5179f-190">Muestra cómo la base de datos toocopy de Sybase datos tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="5179f-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="5179f-191">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5179f-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="5179f-192">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="5179f-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="5179f-193">Un servicio vinculado de tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5179f-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="5179f-194">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5179f-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="5179f-195">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5179f-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="5179f-196">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5179f-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="5179f-197">Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5179f-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5179f-198">ejemplo de Hola copia datos de un resultado de consulta en el blob de tooa de base de datos de Sybase cada hora.</span><span class="sxs-lookup"><span data-stu-id="5179f-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="5179f-199">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="5179f-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="5179f-200">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="5179f-201">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="5179f-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="5179f-202">**Servicio vinculado de Sybase:**</span><span class="sxs-lookup"><span data-stu-id="5179f-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="5179f-203">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="5179f-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="5179f-204">**Conjunto de datos de entrada de Sybase:**</span><span class="sxs-lookup"><span data-stu-id="5179f-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="5179f-205">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" de Sybase y contiene una columna denominada "timestamp" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="5179f-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="5179f-206">Establecer "externo": true informa a servicio de factoría de datos de Hola que este conjunto de datos es externo toohello factoría de datos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="5179f-207">Tenga en cuenta que hello **tipo** de hello servicio vinculado se establece en: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="5179f-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="5179f-208">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="5179f-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5179f-209">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="5179f-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5179f-210">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="5179f-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5179f-211">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="5179f-212">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="5179f-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="5179f-213">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="5179f-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="5179f-214">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5179f-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="5179f-215">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos de Hola de hello DBA. Tabla Orders en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5179f-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="5179f-216">Asignación de tipos para Sybase</span><span class="sxs-lookup"><span data-stu-id="5179f-216">Type mapping for Sybase</span></span>
<span data-ttu-id="5179f-217">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, Hola actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="5179f-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="5179f-218">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="5179f-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="5179f-219">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="5179f-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="5179f-220">Sybase admite T-SQL y tipos de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="5179f-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="5179f-221">Para una tabla de asignación de tipo de too.NET de tipos de sql, vea [conector de SQL Azure](data-factory-azure-sql-connector.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="5179f-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="5179f-222">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="5179f-222">Map source toosink columns</span></span>
<span data-ttu-id="5179f-223">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5179f-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5179f-224">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="5179f-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="5179f-225">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="5179f-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="5179f-226">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="5179f-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5179f-227">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="5179f-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5179f-228">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="5179f-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="5179f-229">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="5179f-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5179f-230">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="5179f-230">Performance and Tuning</span></span>
<span data-ttu-id="5179f-231">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="5179f-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
