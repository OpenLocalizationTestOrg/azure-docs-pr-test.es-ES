---
title: "aaaMove datos de Salesforce con factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de Salesforce con Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="9b9ac-103">Movimiento de datos de Salesforce mediante el uso de Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="9b9ac-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="9b9ac-104">En este artículo se describe cómo puede usar actividad de copia en un Azure generador toocopy datos de almacén de datos de Salesforce tooany que aparece en la columna de receptor de Hola Hola [admite orígenes y receptores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="9b9ac-105">En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia y combinaciones de almacén de datos admitidos.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="9b9ac-106">Factoría de datos de Azure admite actualmente solo mover datos de Salesforce demasiado[admite almacenes de datos del receptor](data-factory-data-movement-activities.md#supported-data-stores-and-formats), pero no admite la migración de datos de otro tooSalesforce de almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="9b9ac-107">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="9b9ac-107">Supported versions</span></span>
<span data-ttu-id="9b9ac-108">Este conector es compatible con hello siguientes ediciones de Salesforce: Developer Edition, Professional Edition, Enterprise Edition o edición ilimitado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="9b9ac-109">Y admite la copia del dominio personalizado, producción y espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b9ac-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b9ac-110">Prerequisites</span></span>
* <span data-ttu-id="9b9ac-111">Debe estar habilitado el permiso API.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-111">API permission must be enabled.</span></span> <span data-ttu-id="9b9ac-112">Consulte [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="9b9ac-113">toocopy datos de almacenes de datos de Salesforce tooon local, debe tener al menos 2.0 de puerta de enlace de administración de datos instalados en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="9b9ac-114">Límites de solicitudes de Salesforce</span><span class="sxs-lookup"><span data-stu-id="9b9ac-114">Salesforce request limits</span></span>
<span data-ttu-id="9b9ac-115">Salesforce tiene límites para el número total de solicitudes de API y el de solicitudes de API simultáneas.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="9b9ac-116">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-116">Note hello following points:</span></span>

- <span data-ttu-id="9b9ac-117">Si el número de Hola de solicitudes simultáneas supera el límite de hello, se produce una limitación y verá errores aleatorios.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="9b9ac-118">Si el número total de Hola de solicitudes supera el límite de hello, Hola cuenta de Salesforce se bloqueará durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="9b9ac-119">También puede recibir errores de "REQUEST_LIMIT_EXCEEDED" hello en ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="9b9ac-120">Consulte la sección Hola "API límites de solicitudes" Hola [límites de desarrollador de Salesforce](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9b9ac-121">Introducción</span><span class="sxs-lookup"><span data-stu-id="9b9ac-121">Getting started</span></span>
<span data-ttu-id="9b9ac-122">Puede crear una canalización con actividad de copia que mueva datos desde Salesforce mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="9b9ac-123">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="9b9ac-124">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="9b9ac-125">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9b9ac-126">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9b9ac-127">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="9b9ac-128">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="9b9ac-129">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="9b9ac-130">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9b9ac-131">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="9b9ac-132">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="9b9ac-133">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son toocopy usa datos de Salesforce, consulte [ejemplo de JSON: copiar los datos de Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="9b9ac-134">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos usado toodefine tooSalesforce específico:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="9b9ac-135">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="9b9ac-135">Linked service properties</span></span>
<span data-ttu-id="9b9ac-136">Hello en la tabla siguiente proporciona descripciones para los elementos JSON que son toohello específico del servicio vinculado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="9b9ac-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9b9ac-137">Property</span></span> | <span data-ttu-id="9b9ac-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="9b9ac-138">Description</span></span> | <span data-ttu-id="9b9ac-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9b9ac-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b9ac-140">type</span><span class="sxs-lookup"><span data-stu-id="9b9ac-140">type</span></span> |<span data-ttu-id="9b9ac-141">propiedad de tipo Hello debe establecerse en: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="9b9ac-142">Sí</span><span class="sxs-lookup"><span data-stu-id="9b9ac-142">Yes</span></span> |
| <span data-ttu-id="9b9ac-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="9b9ac-143">environmentUrl</span></span> | <span data-ttu-id="9b9ac-144">Especifique la instancia de la dirección URL de Salesforce de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="9b9ac-145">- La dirección predeterminada es "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="9b9ac-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="9b9ac-146">-toocopy datos de espacio aislado, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="9b9ac-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="9b9ac-147">-toocopy datos de dominio personalizado, especifique, por ejemplo, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="9b9ac-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="9b9ac-148">No</span><span class="sxs-lookup"><span data-stu-id="9b9ac-148">No</span></span> |
| <span data-ttu-id="9b9ac-149">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="9b9ac-149">username</span></span> |<span data-ttu-id="9b9ac-150">Especifique un nombre de usuario de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="9b9ac-151">Sí</span><span class="sxs-lookup"><span data-stu-id="9b9ac-151">Yes</span></span> |
| <span data-ttu-id="9b9ac-152">Contraseña</span><span class="sxs-lookup"><span data-stu-id="9b9ac-152">password</span></span> |<span data-ttu-id="9b9ac-153">Especifique una contraseña para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="9b9ac-154">Sí</span><span class="sxs-lookup"><span data-stu-id="9b9ac-154">Yes</span></span> |
| <span data-ttu-id="9b9ac-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="9b9ac-155">securityToken</span></span> |<span data-ttu-id="9b9ac-156">Especifique un token de seguridad para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="9b9ac-157">Vea [obtener token de seguridad](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obtener instrucciones sobre cómo tooreset/obtener un token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="9b9ac-158">en general, vea toolearn acerca de los tokens de seguridad [API hello y seguridad](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="9b9ac-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="9b9ac-159">Sí</span><span class="sxs-lookup"><span data-stu-id="9b9ac-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="9b9ac-160">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="9b9ac-160">Dataset properties</span></span>
<span data-ttu-id="9b9ac-161">Para obtener una lista completa de secciones y propiedades que están disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9b9ac-162">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="9b9ac-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="9b9ac-163">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="9b9ac-164">Hola typeProperties sección un conjunto de datos de tipo hello **RelationalTable** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="9b9ac-165">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9b9ac-165">Property</span></span> | <span data-ttu-id="9b9ac-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="9b9ac-166">Description</span></span> | <span data-ttu-id="9b9ac-167">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9b9ac-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b9ac-168">tableName</span><span class="sxs-lookup"><span data-stu-id="9b9ac-168">tableName</span></span> |<span data-ttu-id="9b9ac-169">Nombre de tabla de hello en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="9b9ac-170">No (si se especifica una **consulta** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9b9ac-171">parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="9b9ac-173">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="9b9ac-173">Copy activity properties</span></span>
<span data-ttu-id="9b9ac-174">Para obtener una lista completa de secciones y propiedades que están disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9b9ac-175">Propiedades como name, description, tablas input y output y varias directivas están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="9b9ac-176">propiedades de Hola que están disponibles en Hola typeProperties sección de actividad de hello, en hello en otra parte, varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="9b9ac-177">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="9b9ac-178">En la actividad de copia, al origen de hello es del tipo hello **RelationalSource** (que incluye Salesforce), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="9b9ac-179">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9b9ac-179">Property</span></span> | <span data-ttu-id="9b9ac-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="9b9ac-180">Description</span></span> | <span data-ttu-id="9b9ac-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="9b9ac-181">Allowed values</span></span> | <span data-ttu-id="9b9ac-182">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9b9ac-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9b9ac-183">query</span><span class="sxs-lookup"><span data-stu-id="9b9ac-183">query</span></span> |<span data-ttu-id="9b9ac-184">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="9b9ac-185">Consulta de SQL-92 o de [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="9b9ac-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="9b9ac-186">Por ejemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="9b9ac-187">No (si hello **tableName** de hello **conjunto de datos** se especifica)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9b9ac-188">parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="9b9ac-190">Sugerencias de consulta</span><span class="sxs-lookup"><span data-stu-id="9b9ac-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="9b9ac-191">Recuperación de datos mediante la cláusula WHERE en la columna DateTime</span><span class="sxs-lookup"><span data-stu-id="9b9ac-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="9b9ac-192">Cuando especifique consultas SQL o SOQL de hello, preste atención toohello diferencia de formato de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="9b9ac-193">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-193">For example:</span></span>

* <span data-ttu-id="9b9ac-194">**Ejemplo SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="9b9ac-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="9b9ac-195">**Ejemplo de SQL**:</span><span class="sxs-lookup"><span data-stu-id="9b9ac-195">**SQL sample**:</span></span>
    * <span data-ttu-id="9b9ac-196">**Mediante copia Asistente toospecify Hola consulta:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="9b9ac-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="9b9ac-197">**Usar JSON editar toospecify Hola consulta (carácter de escape correctamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="9b9ac-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="9b9ac-198">Recuperación de datos de informes de Salesforce</span><span class="sxs-lookup"><span data-stu-id="9b9ac-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="9b9ac-199">Puede recuperar datos de informes de Salesforce especificando las consultas como `{call "<report name>"}`; por ejemplo,.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="9b9ac-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="9b9ac-201">Recuperación de los registros eliminados desde la papelera de reciclaje de Salesforce</span><span class="sxs-lookup"><span data-stu-id="9b9ac-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="9b9ac-202">tooquery Hola suave elimina registros de Papelera de reciclaje de Salesforce, puede especificar **"IsDeleted = 1"** en la consulta.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="9b9ac-203">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="9b9ac-203">For example,</span></span>

* <span data-ttu-id="9b9ac-204">Especifique tooquery sólo los registros eliminado de hello, "Seleccione * de MyTable__c **donde IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="9b9ac-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="9b9ac-205">especificar tooquery todos Hola registros incluso existente de Hola y Hola eliminado, "Seleccione * de MyTable__c **donde IsDeleted = 0 o IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="9b9ac-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="9b9ac-206">Ejemplo de JSON: copiar los datos de Salesforce tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="9b9ac-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="9b9ac-207">Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9b9ac-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9b9ac-208">Muestran cómo toocopy datos de Salesforce tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="9b9ac-209">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="9b9ac-210">Estos son artefactos de la factoría de datos de Hola que necesitará escenario de toocreate tooimplement Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="9b9ac-211">secciones de Hola que siguen la lista de hello proporcionan detalles acerca de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="9b9ac-212">Un servicio vinculado de tipo hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="9b9ac-213">Un servicio vinculado de tipo hello [azurestorage.](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="9b9ac-214">Una entrada [conjunto de datos](data-factory-create-datasets.md) de tipo hello [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="9b9ac-215">Una salida [conjunto de datos](data-factory-create-datasets.md) de tipo hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="9b9ac-216">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="9b9ac-217">**Servicio vinculado de Salesforce**</span><span class="sxs-lookup"><span data-stu-id="9b9ac-217">**Salesforce linked service**</span></span>

<span data-ttu-id="9b9ac-218">Este ejemplo utiliza hello **Salesforce** servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="9b9ac-219">Vea hello [servicio vinculado de Salesforce](#linked-service-properties) sección de propiedades de Hola que son compatibles con este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="9b9ac-220">Vea [obtener token de seguridad](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obtener instrucciones sobre cómo tooreset/get Hola token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="9b9ac-221">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="9b9ac-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="9b9ac-222">**Conjunto de datos de entrada de Salesforce**</span><span class="sxs-lookup"><span data-stu-id="9b9ac-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

<span data-ttu-id="9b9ac-223">Establecer **externo** demasiado**true** informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b9ac-224">parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="9b9ac-226">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="9b9ac-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="9b9ac-227">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="9b9ac-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9b9ac-228">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="9b9ac-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="9b9ac-229">canalización Hello contiene actividad de copia, que se configura toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="9b9ac-230">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource**, hello y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="9b9ac-231">Vea [propiedades de tipo RelationalSource](#copy-activity-properties) para lista de Hola de propiedades que son compatibles con hello RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="9b9ac-232">parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="9b9ac-234">Asignación de tipos para Salesforce</span><span class="sxs-lookup"><span data-stu-id="9b9ac-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="9b9ac-235">Tipo de Salesforce</span><span class="sxs-lookup"><span data-stu-id="9b9ac-235">Salesforce type</span></span> | <span data-ttu-id="9b9ac-236">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="9b9ac-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="9b9ac-237">Numeración automática</span><span class="sxs-lookup"><span data-stu-id="9b9ac-237">Auto Number</span></span> |<span data-ttu-id="9b9ac-238">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-238">String</span></span> |
| <span data-ttu-id="9b9ac-239">Casilla de verificación</span><span class="sxs-lookup"><span data-stu-id="9b9ac-239">Checkbox</span></span> |<span data-ttu-id="9b9ac-240">Booleano</span><span class="sxs-lookup"><span data-stu-id="9b9ac-240">Boolean</span></span> |
| <span data-ttu-id="9b9ac-241">Moneda</span><span class="sxs-lookup"><span data-stu-id="9b9ac-241">Currency</span></span> |<span data-ttu-id="9b9ac-242">Doble</span><span class="sxs-lookup"><span data-stu-id="9b9ac-242">Double</span></span> |
| <span data-ttu-id="9b9ac-243">Date</span><span class="sxs-lookup"><span data-stu-id="9b9ac-243">Date</span></span> |<span data-ttu-id="9b9ac-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b9ac-244">DateTime</span></span> |
| <span data-ttu-id="9b9ac-245">Fecha y hora</span><span class="sxs-lookup"><span data-stu-id="9b9ac-245">Date/Time</span></span> |<span data-ttu-id="9b9ac-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b9ac-246">DateTime</span></span> |
| <span data-ttu-id="9b9ac-247">Email</span><span class="sxs-lookup"><span data-stu-id="9b9ac-247">Email</span></span> |<span data-ttu-id="9b9ac-248">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-248">String</span></span> |
| <span data-ttu-id="9b9ac-249">Id</span><span class="sxs-lookup"><span data-stu-id="9b9ac-249">Id</span></span> |<span data-ttu-id="9b9ac-250">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-250">String</span></span> |
| <span data-ttu-id="9b9ac-251">Relación de búsqueda</span><span class="sxs-lookup"><span data-stu-id="9b9ac-251">Lookup Relationship</span></span> |<span data-ttu-id="9b9ac-252">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-252">String</span></span> |
| <span data-ttu-id="9b9ac-253">Lista desplegable de selección múltiple</span><span class="sxs-lookup"><span data-stu-id="9b9ac-253">Multi-Select Picklist</span></span> |<span data-ttu-id="9b9ac-254">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-254">String</span></span> |
| <span data-ttu-id="9b9ac-255">Number</span><span class="sxs-lookup"><span data-stu-id="9b9ac-255">Number</span></span> |<span data-ttu-id="9b9ac-256">Doble</span><span class="sxs-lookup"><span data-stu-id="9b9ac-256">Double</span></span> |
| <span data-ttu-id="9b9ac-257">Percent</span><span class="sxs-lookup"><span data-stu-id="9b9ac-257">Percent</span></span> |<span data-ttu-id="9b9ac-258">Doble</span><span class="sxs-lookup"><span data-stu-id="9b9ac-258">Double</span></span> |
| <span data-ttu-id="9b9ac-259">Teléfono</span><span class="sxs-lookup"><span data-stu-id="9b9ac-259">Phone</span></span> |<span data-ttu-id="9b9ac-260">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-260">String</span></span> |
| <span data-ttu-id="9b9ac-261">Lista desplegable</span><span class="sxs-lookup"><span data-stu-id="9b9ac-261">Picklist</span></span> |<span data-ttu-id="9b9ac-262">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-262">String</span></span> |
| <span data-ttu-id="9b9ac-263">Texto</span><span class="sxs-lookup"><span data-stu-id="9b9ac-263">Text</span></span> |<span data-ttu-id="9b9ac-264">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-264">String</span></span> |
| <span data-ttu-id="9b9ac-265">Área de texto</span><span class="sxs-lookup"><span data-stu-id="9b9ac-265">Text Area</span></span> |<span data-ttu-id="9b9ac-266">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-266">String</span></span> |
| <span data-ttu-id="9b9ac-267">Área de texto (largo)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-267">Text Area (Long)</span></span> |<span data-ttu-id="9b9ac-268">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-268">String</span></span> |
| <span data-ttu-id="9b9ac-269">Área de texto (enriquecido)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-269">Text Area (Rich)</span></span> |<span data-ttu-id="9b9ac-270">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-270">String</span></span> |
| <span data-ttu-id="9b9ac-271">Texto (cifrado)</span><span class="sxs-lookup"><span data-stu-id="9b9ac-271">Text (Encrypted)</span></span> |<span data-ttu-id="9b9ac-272">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-272">String</span></span> |
| <span data-ttu-id="9b9ac-273">URL</span><span class="sxs-lookup"><span data-stu-id="9b9ac-273">URL</span></span> |<span data-ttu-id="9b9ac-274">String</span><span class="sxs-lookup"><span data-stu-id="9b9ac-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="9b9ac-275">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9b9ac-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="9b9ac-276">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="9b9ac-276">Performance and tuning</span></span>
<span data-ttu-id="9b9ac-277">Vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="9b9ac-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
