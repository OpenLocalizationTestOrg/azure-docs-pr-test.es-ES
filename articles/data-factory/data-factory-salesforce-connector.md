---
title: Movimiento de datos de Salesforce mediante el uso de Data Factory | Microsoft Docs
description: Aprenda a mover datos de Salesforce usando Data Factory de Azure.
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
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="c5deb-103">Movimiento de datos de Salesforce mediante el uso de Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="c5deb-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="c5deb-104">En este artículo se describe cómo puede usar la actividad de copia en Data Factory de Azure para copiar datos de Salesforce en cualquier almacén de datos que aparezca en la columna Receptores en la tabla de [orígenes y receptores admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="c5deb-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c5deb-105">Este artículo se basa en el artículo sobre [movimiento de datos y actividad de copia](data-factory-data-movement-activities.md) que presenta una introducción general del movimiento de datos con la actividad de copia y las combinaciones de almacén de datos admitidas.</span><span class="sxs-lookup"><span data-stu-id="c5deb-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="c5deb-106">Actualmente, Data Factory de Azure solo admite mover datos de Salesforce a [almacenes de datos receptores compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats), pero no de otros almacenes de datos a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c5deb-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="c5deb-107">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="c5deb-107">Supported versions</span></span>
<span data-ttu-id="c5deb-108">Este conector es compatible con las siguientes ediciones de Salesforce: Developer Edition, Professional Edition, Enterprise Edition o Unlimited Edition.</span><span class="sxs-lookup"><span data-stu-id="c5deb-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="c5deb-109">Y admite la copia del dominio personalizado, producción y espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c5deb-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5deb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c5deb-110">Prerequisites</span></span>
* <span data-ttu-id="c5deb-111">Debe estar habilitado el permiso API.</span><span class="sxs-lookup"><span data-stu-id="c5deb-111">API permission must be enabled.</span></span> <span data-ttu-id="c5deb-112">Consulte [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="c5deb-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="c5deb-113">Para copiar datos de Salesforce en almacenes de datos locales, tiene que tener Data Management Gateway versión 2.0 o posterior instalado en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="c5deb-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="c5deb-114">Límites de solicitudes de Salesforce</span><span class="sxs-lookup"><span data-stu-id="c5deb-114">Salesforce request limits</span></span>
<span data-ttu-id="c5deb-115">Salesforce tiene límites para el número total de solicitudes de API y el de solicitudes de API simultáneas.</span><span class="sxs-lookup"><span data-stu-id="c5deb-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="c5deb-116">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="c5deb-116">Note the following points:</span></span>

- <span data-ttu-id="c5deb-117">Si el número de solicitudes simultáneas supera el límite, se produce la limitación y verá errores aleatorios.</span><span class="sxs-lookup"><span data-stu-id="c5deb-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="c5deb-118">Si el número total de solicitudes supera el límite, la cuenta de Salesforce se bloqueará durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="c5deb-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="c5deb-119">También podría recibir el error "REQUEST_LIMIT_EXCEEDED" en ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="c5deb-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="c5deb-120">Consulte la sección API Request Limits (Límites de solicitudes de API) del artículo [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) (Límites de desarrollador de Salesforce) para más información.</span><span class="sxs-lookup"><span data-stu-id="c5deb-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c5deb-121">Introducción</span><span class="sxs-lookup"><span data-stu-id="c5deb-121">Getting started</span></span>
<span data-ttu-id="c5deb-122">Puede crear una canalización con actividad de copia que mueva datos desde Salesforce mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="c5deb-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="c5deb-123">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c5deb-124">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="c5deb-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="c5deb-125">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c5deb-126">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="c5deb-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c5deb-127">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="c5deb-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="c5deb-128">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c5deb-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c5deb-129">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="c5deb-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c5deb-130">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="c5deb-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c5deb-131">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="c5deb-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c5deb-132">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c5deb-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c5deb-133">Si desea obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan con el fin de copiar los datos de Salesforce, consulte la sección [Ejemplo de JSON: Copia de datos de Salesforce a un blob de Azure](#json-example-copy-data-from-salesforce-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="c5deb-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c5deb-134">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Salesforce:</span><span class="sxs-lookup"><span data-stu-id="c5deb-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="c5deb-135">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="c5deb-135">Linked service properties</span></span>
<span data-ttu-id="c5deb-136">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c5deb-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="c5deb-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c5deb-137">Property</span></span> | <span data-ttu-id="c5deb-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="c5deb-138">Description</span></span> | <span data-ttu-id="c5deb-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c5deb-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5deb-140">type</span><span class="sxs-lookup"><span data-stu-id="c5deb-140">type</span></span> |<span data-ttu-id="c5deb-141">La propiedad type debe establecerse en: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="c5deb-142">Sí</span><span class="sxs-lookup"><span data-stu-id="c5deb-142">Yes</span></span> |
| <span data-ttu-id="c5deb-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="c5deb-143">environmentUrl</span></span> | <span data-ttu-id="c5deb-144">Especifique la URL de la instancia de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c5deb-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="c5deb-145">- La dirección predeterminada es "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="c5deb-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="c5deb-146">- Para copiar los datos desde el espacio aislado, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="c5deb-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="c5deb-147">- Para copiar datos del dominio personalizado, especifique, por ejemplo, "https://[dominio].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="c5deb-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="c5deb-148">No</span><span class="sxs-lookup"><span data-stu-id="c5deb-148">No</span></span> |
| <span data-ttu-id="c5deb-149">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="c5deb-149">username</span></span> |<span data-ttu-id="c5deb-150">Especifique el nombre de usuario de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="c5deb-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="c5deb-151">Sí</span><span class="sxs-lookup"><span data-stu-id="c5deb-151">Yes</span></span> |
| <span data-ttu-id="c5deb-152">contraseña</span><span class="sxs-lookup"><span data-stu-id="c5deb-152">password</span></span> |<span data-ttu-id="c5deb-153">Especifique la contraseña para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="c5deb-153">Specify a password for the user account.</span></span> |<span data-ttu-id="c5deb-154">Sí</span><span class="sxs-lookup"><span data-stu-id="c5deb-154">Yes</span></span> |
| <span data-ttu-id="c5deb-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="c5deb-155">securityToken</span></span> |<span data-ttu-id="c5deb-156">Especifique el token de seguridad para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="c5deb-156">Specify a security token for the user account.</span></span> <span data-ttu-id="c5deb-157">Consulte [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Obtención de un token de seguridad) para ver instrucciones sobre cómo restablecer u obtener un token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c5deb-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="c5deb-158">Para más información acerca de los tokens de seguridad en general, consulte [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Seguridad y la API).</span><span class="sxs-lookup"><span data-stu-id="c5deb-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="c5deb-159">Sí</span><span class="sxs-lookup"><span data-stu-id="c5deb-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c5deb-160">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="c5deb-160">Dataset properties</span></span>
<span data-ttu-id="c5deb-161">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo sobre [creación de conjuntos de datos](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="c5deb-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c5deb-162">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="c5deb-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="c5deb-163">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="c5deb-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c5deb-164">La sección typeProperties del conjunto de datos del tipo **RelationalTable** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="c5deb-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="c5deb-165">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c5deb-165">Property</span></span> | <span data-ttu-id="c5deb-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="c5deb-166">Description</span></span> | <span data-ttu-id="c5deb-167">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c5deb-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5deb-168">tableName</span><span class="sxs-lookup"><span data-stu-id="c5deb-168">tableName</span></span> |<span data-ttu-id="c5deb-169">Nombre de la tabla de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c5deb-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="c5deb-170">No (si se especifica una **consulta** de **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="c5deb-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c5deb-171">La parte "__c" del nombre de la API es necesaria para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="c5deb-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="c5deb-173">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="c5deb-173">Copy activity properties</span></span>
<span data-ttu-id="c5deb-174">Para obtener una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo sobre [creación de canalizaciones](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="c5deb-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c5deb-175">Propiedades como name, description, tablas input y output y varias directivas están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="c5deb-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="c5deb-176">Las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="c5deb-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="c5deb-177">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="c5deb-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c5deb-178">En la actividad de copia cuando el origen es del tipo **RelationalSource** (lo que incluye Salesforce), en la sección typeProperties, están disponibles las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="c5deb-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c5deb-179">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c5deb-179">Property</span></span> | <span data-ttu-id="c5deb-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="c5deb-180">Description</span></span> | <span data-ttu-id="c5deb-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="c5deb-181">Allowed values</span></span> | <span data-ttu-id="c5deb-182">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c5deb-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c5deb-183">query</span><span class="sxs-lookup"><span data-stu-id="c5deb-183">query</span></span> |<span data-ttu-id="c5deb-184">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="c5deb-184">Use the custom query to read data.</span></span> |<span data-ttu-id="c5deb-185">Consulta de SQL-92 o de [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="c5deb-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="c5deb-186">Por ejemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="c5deb-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="c5deb-187">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="c5deb-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c5deb-188">La parte "__c" del nombre de la API es necesaria para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="c5deb-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="c5deb-190">Sugerencias de consulta</span><span class="sxs-lookup"><span data-stu-id="c5deb-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="c5deb-191">Recuperación de datos mediante la cláusula WHERE en la columna DateTime</span><span class="sxs-lookup"><span data-stu-id="c5deb-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="c5deb-192">Cuando se especifica la consulta SQL o SOQL, preste atención a la diferencia del formato de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="c5deb-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="c5deb-193">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c5deb-193">For example:</span></span>

* <span data-ttu-id="c5deb-194">**Ejemplo SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c5deb-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="c5deb-195">**Ejemplo de SQL**:</span><span class="sxs-lookup"><span data-stu-id="c5deb-195">**SQL sample**:</span></span>
    * <span data-ttu-id="c5deb-196">**Uso del Asistente para copia para especificar la consulta:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c5deb-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="c5deb-197">**Uso de la edición JSON para especificar la consulta (carácter de escape adecuado):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c5deb-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="c5deb-198">Recuperación de datos de informes de Salesforce</span><span class="sxs-lookup"><span data-stu-id="c5deb-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="c5deb-199">Puede recuperar datos de informes de Salesforce especificando las consultas como `{call "<report name>"}`; por ejemplo,.</span><span class="sxs-lookup"><span data-stu-id="c5deb-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="c5deb-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="c5deb-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="c5deb-201">Recuperación de los registros eliminados desde la papelera de reciclaje de Salesforce</span><span class="sxs-lookup"><span data-stu-id="c5deb-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="c5deb-202">Para consultar los registros eliminados temporalmente de papelera de reciclaje de Salesforce, puede especificar **"IsDeleted = 1"** en la consulta.</span><span class="sxs-lookup"><span data-stu-id="c5deb-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="c5deb-203">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="c5deb-203">For example,</span></span>

* <span data-ttu-id="c5deb-204">Para consultar solo los registros eliminados, especifique "select * from MyTable__c **where IsDeleted= 1**"</span><span class="sxs-lookup"><span data-stu-id="c5deb-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="c5deb-205">Para consultar todos los registros, tanto existentes como eliminados, especifique "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="c5deb-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="c5deb-206">Ejemplo de JSON: Copia de datos de Salesforce a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="c5deb-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="c5deb-207">En el siguiente ejemplo, se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización usando [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c5deb-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c5deb-208">Se muestra cómo copiar datos desde la base de datos Salesforce al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5deb-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="c5deb-209">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5deb-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="c5deb-210">Aquí tiene los artefactos de Data Factory que necesita crear para implementar el escenario.</span><span class="sxs-lookup"><span data-stu-id="c5deb-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="c5deb-211">Las secciones que siguen a la lista proporcionan detalles acerca de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c5deb-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="c5deb-212">Un servicio vinculado del tipo [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c5deb-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="c5deb-213">Un servicio vinculado del tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c5deb-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="c5deb-214">Un [conjunto de datos](data-factory-create-datasets.md) de entrada del tipo [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c5deb-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="c5deb-215">Un [conjunto de datos](data-factory-create-datasets.md) de salida del tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c5deb-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="c5deb-216">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="c5deb-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="c5deb-217">**Servicio vinculado de Salesforce**</span><span class="sxs-lookup"><span data-stu-id="c5deb-217">**Salesforce linked service**</span></span>

<span data-ttu-id="c5deb-218">Este ejemplo usa el servicio vinculado de **Salesforce** .</span><span class="sxs-lookup"><span data-stu-id="c5deb-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="c5deb-219">Consulte la sección sobre el [servicio vinculado de Salesforce](#linked-service-properties) para ver las propiedades que admite este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="c5deb-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="c5deb-220">Consulte [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Obtención de un token de seguridad) para ver instrucciones sobre cómo restablecer u obtener un token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c5deb-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

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
<span data-ttu-id="c5deb-221">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="c5deb-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="c5deb-222">**Conjunto de datos de entrada de Salesforce**</span><span class="sxs-lookup"><span data-stu-id="c5deb-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="c5deb-223">Si se establece **external** en **true**, se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c5deb-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5deb-224">La parte "__c" del nombre de la API es necesaria para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="c5deb-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="c5deb-226">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="c5deb-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="c5deb-227">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="c5deb-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="c5deb-228">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="c5deb-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="c5deb-229">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="c5deb-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="c5deb-230">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c5deb-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="c5deb-231">Consulte [Propiedades del tipo RelationalSource](#copy-activity-properties) para obtener la lista de propiedades admitidas por RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="c5deb-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

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
            "description": "Copy from Salesforce to an Azure blob",
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
> <span data-ttu-id="c5deb-232">La parte "__c" del nombre de la API es necesaria para cualquier objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="c5deb-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="c5deb-234">Asignación de tipos para Salesforce</span><span class="sxs-lookup"><span data-stu-id="c5deb-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="c5deb-235">Tipo de Salesforce</span><span class="sxs-lookup"><span data-stu-id="c5deb-235">Salesforce type</span></span> | <span data-ttu-id="c5deb-236">Tipo basado en .NET</span><span class="sxs-lookup"><span data-stu-id="c5deb-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="c5deb-237">Numeración automática</span><span class="sxs-lookup"><span data-stu-id="c5deb-237">Auto Number</span></span> |<span data-ttu-id="c5deb-238">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-238">String</span></span> |
| <span data-ttu-id="c5deb-239">Casilla de verificación</span><span class="sxs-lookup"><span data-stu-id="c5deb-239">Checkbox</span></span> |<span data-ttu-id="c5deb-240">Booleano</span><span class="sxs-lookup"><span data-stu-id="c5deb-240">Boolean</span></span> |
| <span data-ttu-id="c5deb-241">Moneda</span><span class="sxs-lookup"><span data-stu-id="c5deb-241">Currency</span></span> |<span data-ttu-id="c5deb-242">Doble</span><span class="sxs-lookup"><span data-stu-id="c5deb-242">Double</span></span> |
| <span data-ttu-id="c5deb-243">Date</span><span class="sxs-lookup"><span data-stu-id="c5deb-243">Date</span></span> |<span data-ttu-id="c5deb-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="c5deb-244">DateTime</span></span> |
| <span data-ttu-id="c5deb-245">Fecha y hora</span><span class="sxs-lookup"><span data-stu-id="c5deb-245">Date/Time</span></span> |<span data-ttu-id="c5deb-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="c5deb-246">DateTime</span></span> |
| <span data-ttu-id="c5deb-247">Email</span><span class="sxs-lookup"><span data-stu-id="c5deb-247">Email</span></span> |<span data-ttu-id="c5deb-248">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-248">String</span></span> |
| <span data-ttu-id="c5deb-249">Id</span><span class="sxs-lookup"><span data-stu-id="c5deb-249">Id</span></span> |<span data-ttu-id="c5deb-250">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-250">String</span></span> |
| <span data-ttu-id="c5deb-251">Relación de búsqueda</span><span class="sxs-lookup"><span data-stu-id="c5deb-251">Lookup Relationship</span></span> |<span data-ttu-id="c5deb-252">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-252">String</span></span> |
| <span data-ttu-id="c5deb-253">Lista desplegable de selección múltiple</span><span class="sxs-lookup"><span data-stu-id="c5deb-253">Multi-Select Picklist</span></span> |<span data-ttu-id="c5deb-254">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-254">String</span></span> |
| <span data-ttu-id="c5deb-255">Number</span><span class="sxs-lookup"><span data-stu-id="c5deb-255">Number</span></span> |<span data-ttu-id="c5deb-256">Doble</span><span class="sxs-lookup"><span data-stu-id="c5deb-256">Double</span></span> |
| <span data-ttu-id="c5deb-257">Percent</span><span class="sxs-lookup"><span data-stu-id="c5deb-257">Percent</span></span> |<span data-ttu-id="c5deb-258">Doble</span><span class="sxs-lookup"><span data-stu-id="c5deb-258">Double</span></span> |
| <span data-ttu-id="c5deb-259">Teléfono</span><span class="sxs-lookup"><span data-stu-id="c5deb-259">Phone</span></span> |<span data-ttu-id="c5deb-260">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-260">String</span></span> |
| <span data-ttu-id="c5deb-261">Lista desplegable</span><span class="sxs-lookup"><span data-stu-id="c5deb-261">Picklist</span></span> |<span data-ttu-id="c5deb-262">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-262">String</span></span> |
| <span data-ttu-id="c5deb-263">Texto</span><span class="sxs-lookup"><span data-stu-id="c5deb-263">Text</span></span> |<span data-ttu-id="c5deb-264">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-264">String</span></span> |
| <span data-ttu-id="c5deb-265">Área de texto</span><span class="sxs-lookup"><span data-stu-id="c5deb-265">Text Area</span></span> |<span data-ttu-id="c5deb-266">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-266">String</span></span> |
| <span data-ttu-id="c5deb-267">Área de texto (largo)</span><span class="sxs-lookup"><span data-stu-id="c5deb-267">Text Area (Long)</span></span> |<span data-ttu-id="c5deb-268">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-268">String</span></span> |
| <span data-ttu-id="c5deb-269">Área de texto (enriquecido)</span><span class="sxs-lookup"><span data-stu-id="c5deb-269">Text Area (Rich)</span></span> |<span data-ttu-id="c5deb-270">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-270">String</span></span> |
| <span data-ttu-id="c5deb-271">Texto (cifrado)</span><span class="sxs-lookup"><span data-stu-id="c5deb-271">Text (Encrypted)</span></span> |<span data-ttu-id="c5deb-272">String</span><span class="sxs-lookup"><span data-stu-id="c5deb-272">String</span></span> |
| <span data-ttu-id="c5deb-273">URL</span><span class="sxs-lookup"><span data-stu-id="c5deb-273">URL</span></span> |<span data-ttu-id="c5deb-274">string</span><span class="sxs-lookup"><span data-stu-id="c5deb-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="c5deb-275">Para asignar columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte el artículo [Asignación de columnas de conjuntos de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c5deb-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="c5deb-276">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="c5deb-276">Performance and tuning</span></span>
<span data-ttu-id="c5deb-277">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Data Factory de Azure y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="c5deb-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
