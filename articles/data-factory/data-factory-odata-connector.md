---
title: "Movimiento de datos desde orígenes OData | Microsoft Docs"
description: "Obtenga información sobre cómo mover datos desde orígenes de OData mediante Factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="bd380-103">Movimiento de datos de un origen de OData mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="bd380-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="bd380-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos desde un origen OData.</span><span class="sxs-lookup"><span data-stu-id="bd380-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="bd380-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bd380-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="bd380-106">Puede copiar datos de un origen OData a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="bd380-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="bd380-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como receptores.</span><span class="sxs-lookup"><span data-stu-id="bd380-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="bd380-108">Data Factory solo admite actualmente la transferencia de datos de un origen OData a otros almacenes de datos, pero no viceversa.</span><span class="sxs-lookup"><span data-stu-id="bd380-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="bd380-109">Versiones admitidas y tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="bd380-109">Supported versions and authentication types</span></span>
<span data-ttu-id="bd380-110">Este conector OData admite la versión de OData 3.0 y 4.0, y puede copiar datos de orígenes OData locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="bd380-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="bd380-111">Por último, debe instalar Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="bd380-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="bd380-112">Consulte el artículo [Mover datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="bd380-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="bd380-113">Estos son los tipos de autenticación admitidos:</span><span class="sxs-lookup"><span data-stu-id="bd380-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="bd380-114">Para acceder a la fuente OData **en la nube**, puede usar la autenticación anónima y básica (nombre de usuario y contraseña), o la autenticación OAuth basada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd380-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="bd380-115">Para acceder a la fuente OData **local**, puede usar la autenticación anónima y básica (nombre de usuario y contraseña), o la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="bd380-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bd380-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="bd380-116">Getting started</span></span>
<span data-ttu-id="bd380-117">Puede crear una canalización con una actividad de copia que mueva datos desde un origen OData mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="bd380-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="bd380-118">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="bd380-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="bd380-119">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="bd380-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="bd380-120">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="bd380-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bd380-121">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="bd380-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="bd380-122">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="bd380-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="bd380-123">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="bd380-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="bd380-124">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="bd380-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="bd380-125">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="bd380-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="bd380-126">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="bd380-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="bd380-127">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="bd380-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="bd380-128">Si desea obtener un ejemplo con definiciones de JSON para entidades de Data Factory utilizadas con el fin de copiar los datos desde un origen OData, consulte la sección [Ejemplo de JSON: Copia de datos de un origen OData a un blob de Azure](#json-example-copy-data-from-odata-source-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="bd380-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="bd380-129">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de los orígenes OData:</span><span class="sxs-lookup"><span data-stu-id="bd380-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bd380-130">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="bd380-130">Linked Service properties</span></span>
<span data-ttu-id="bd380-131">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de OData.</span><span class="sxs-lookup"><span data-stu-id="bd380-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="bd380-132">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bd380-132">Property</span></span> | <span data-ttu-id="bd380-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="bd380-133">Description</span></span> | <span data-ttu-id="bd380-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bd380-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd380-135">type</span><span class="sxs-lookup"><span data-stu-id="bd380-135">type</span></span> |<span data-ttu-id="bd380-136">La propiedad type debe establecerse en **OData**</span><span class="sxs-lookup"><span data-stu-id="bd380-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="bd380-137">Sí</span><span class="sxs-lookup"><span data-stu-id="bd380-137">Yes</span></span> |
| <span data-ttu-id="bd380-138">URL</span><span class="sxs-lookup"><span data-stu-id="bd380-138">url</span></span> |<span data-ttu-id="bd380-139">Dirección URL del servicio de OData.</span><span class="sxs-lookup"><span data-stu-id="bd380-139">Url of the OData service.</span></span> |<span data-ttu-id="bd380-140">Sí</span><span class="sxs-lookup"><span data-stu-id="bd380-140">Yes</span></span> |
| <span data-ttu-id="bd380-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="bd380-141">authenticationType</span></span> |<span data-ttu-id="bd380-142">Tipo de autenticación que se usa para conectarse al origen de OData.</span><span class="sxs-lookup"><span data-stu-id="bd380-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="bd380-143">Para OData en la nube, los valores posibles son Anonymous, Basic y OAuth (tenga en cuenta que Azure Data Factory en estos momentos solo admite la autenticación OAuth basada en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="bd380-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="bd380-144">Para OData local, los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="bd380-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="bd380-145">Sí</span><span class="sxs-lookup"><span data-stu-id="bd380-145">Yes</span></span> |
| <span data-ttu-id="bd380-146">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="bd380-146">username</span></span> |<span data-ttu-id="bd380-147">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="bd380-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="bd380-148">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="bd380-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="bd380-149">contraseña</span><span class="sxs-lookup"><span data-stu-id="bd380-149">password</span></span> |<span data-ttu-id="bd380-150">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="bd380-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="bd380-151">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="bd380-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="bd380-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="bd380-152">authorizedCredential</span></span> |<span data-ttu-id="bd380-153">Si está usando OAuth, haga clic en el botón **Autorizar** del Editor o el Asistente para copiar de Data Factory y escriba su credencial. Después, el valor de esta propiedad se generará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bd380-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="bd380-154">Sí (solo si usa la autenticación OAuth)</span><span class="sxs-lookup"><span data-stu-id="bd380-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="bd380-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="bd380-155">gatewayName</span></span> |<span data-ttu-id="bd380-156">Nombre de la puerta de enlace que debe usar el servicio Factoría de datos para conectarse al servicio de OData local.</span><span class="sxs-lookup"><span data-stu-id="bd380-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="bd380-157">Especifique solo si va a copiar datos del origen de OData local.</span><span class="sxs-lookup"><span data-stu-id="bd380-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="bd380-158">No</span><span class="sxs-lookup"><span data-stu-id="bd380-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="bd380-159">Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="bd380-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="bd380-160">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="bd380-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="bd380-161">Uso de la autenticación de Windows para acceder al origen de OData local</span><span class="sxs-lookup"><span data-stu-id="bd380-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="bd380-162">Uso de la autenticación OAuth para tener acceso al origen de OData en la nube</span><span class="sxs-lookup"><span data-stu-id="bd380-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="bd380-163">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="bd380-163">Dataset properties</span></span>
<span data-ttu-id="bd380-164">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="bd380-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bd380-165">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="bd380-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bd380-166">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="bd380-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="bd380-167">La sección typeProperties del conjunto de datos del tipo **ODataResource** (que incluye el conjunto de datos de OData) tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd380-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="bd380-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bd380-168">Property</span></span> | <span data-ttu-id="bd380-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="bd380-169">Description</span></span> | <span data-ttu-id="bd380-170">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bd380-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd380-171">path</span><span class="sxs-lookup"><span data-stu-id="bd380-171">path</span></span> |<span data-ttu-id="bd380-172">Ruta de acceso al recurso de OData</span><span class="sxs-lookup"><span data-stu-id="bd380-172">Path to the OData resource</span></span> |<span data-ttu-id="bd380-173">No</span><span class="sxs-lookup"><span data-stu-id="bd380-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="bd380-174">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="bd380-174">Copy activity properties</span></span>
<span data-ttu-id="bd380-175">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="bd380-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bd380-176">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="bd380-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="bd380-177">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="bd380-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="bd380-178">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="bd380-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="bd380-179">Cuando la actividad de copia es de tipo **RelationalSource** (lo que incluye OData), están disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="bd380-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="bd380-180">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bd380-180">Property</span></span> | <span data-ttu-id="bd380-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="bd380-181">Description</span></span> | <span data-ttu-id="bd380-182">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd380-182">Example</span></span> | <span data-ttu-id="bd380-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bd380-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bd380-184">query</span><span class="sxs-lookup"><span data-stu-id="bd380-184">query</span></span> |<span data-ttu-id="bd380-185">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="bd380-185">Use the custom query to read data.</span></span> |<span data-ttu-id="bd380-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="bd380-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="bd380-187">No</span><span class="sxs-lookup"><span data-stu-id="bd380-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="bd380-188">Asignación de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="bd380-188">Type Mapping for OData</span></span>
<span data-ttu-id="bd380-189">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="bd380-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="bd380-190">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="bd380-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="bd380-191">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="bd380-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="bd380-192">Al mover datos desde OData, se usan las asignaciones siguientes de tipos de OData al tipo de .NET.</span><span class="sxs-lookup"><span data-stu-id="bd380-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="bd380-193">Tipo de datos OData</span><span class="sxs-lookup"><span data-stu-id="bd380-193">OData Data Type</span></span> | <span data-ttu-id="bd380-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="bd380-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="bd380-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="bd380-195">Edm.Binary</span></span> |<span data-ttu-id="bd380-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd380-196">Byte[]</span></span> |
| <span data-ttu-id="bd380-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="bd380-197">Edm.Boolean</span></span> |<span data-ttu-id="bd380-198">Booleano</span><span class="sxs-lookup"><span data-stu-id="bd380-198">Bool</span></span> |
| <span data-ttu-id="bd380-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="bd380-199">Edm.Byte</span></span> |<span data-ttu-id="bd380-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd380-200">Byte[]</span></span> |
| <span data-ttu-id="bd380-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="bd380-201">Edm.DateTime</span></span> |<span data-ttu-id="bd380-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd380-202">DateTime</span></span> |
| <span data-ttu-id="bd380-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="bd380-203">Edm.Decimal</span></span> |<span data-ttu-id="bd380-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="bd380-204">Decimal</span></span> |
| <span data-ttu-id="bd380-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="bd380-205">Edm.Double</span></span> |<span data-ttu-id="bd380-206">Doble</span><span class="sxs-lookup"><span data-stu-id="bd380-206">Double</span></span> |
| <span data-ttu-id="bd380-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="bd380-207">Edm.Single</span></span> |<span data-ttu-id="bd380-208">Single</span><span class="sxs-lookup"><span data-stu-id="bd380-208">Single</span></span> |
| <span data-ttu-id="bd380-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="bd380-209">Edm.Guid</span></span> |<span data-ttu-id="bd380-210">Guid</span><span class="sxs-lookup"><span data-stu-id="bd380-210">Guid</span></span> |
| <span data-ttu-id="bd380-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="bd380-211">Edm.Int16</span></span> |<span data-ttu-id="bd380-212">Int16</span><span class="sxs-lookup"><span data-stu-id="bd380-212">Int16</span></span> |
| <span data-ttu-id="bd380-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="bd380-213">Edm.Int32</span></span> |<span data-ttu-id="bd380-214">Int32</span><span class="sxs-lookup"><span data-stu-id="bd380-214">Int32</span></span> |
| <span data-ttu-id="bd380-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="bd380-215">Edm.Int64</span></span> |<span data-ttu-id="bd380-216">Int64</span><span class="sxs-lookup"><span data-stu-id="bd380-216">Int64</span></span> |
| <span data-ttu-id="bd380-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="bd380-217">Edm.SByte</span></span> |<span data-ttu-id="bd380-218">Int16</span><span class="sxs-lookup"><span data-stu-id="bd380-218">Int16</span></span> |
| <span data-ttu-id="bd380-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="bd380-219">Edm.String</span></span> |<span data-ttu-id="bd380-220">String</span><span class="sxs-lookup"><span data-stu-id="bd380-220">String</span></span> |
| <span data-ttu-id="bd380-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="bd380-221">Edm.Time</span></span> |<span data-ttu-id="bd380-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="bd380-222">TimeSpan</span></span> |
| <span data-ttu-id="bd380-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="bd380-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="bd380-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bd380-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="bd380-225">Los tipos de datos complejos de OData, como por ejemplo, Object no se admiten.</span><span class="sxs-lookup"><span data-stu-id="bd380-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="bd380-226">Ejemplo de JSON: Copia de datos de un origen OData a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="bd380-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="bd380-227">Este ejemplo proporciona definiciones de JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd380-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bd380-228">En ellos se muestra cómo copiar datos de un origen de OData en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd380-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="bd380-229">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd380-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="bd380-230">El ejemplo consta de las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="bd380-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="bd380-231">Un servicio vinculado de tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd380-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="bd380-232">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="bd380-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bd380-233">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd380-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="bd380-234">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd380-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bd380-235">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bd380-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bd380-236">En el ejemplo se copian los datos de la consulta en un origen de OData a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="bd380-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="bd380-237">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="bd380-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="bd380-238">**Servicio vinculado de OData:** En este ejemplo se usa la autenticación anónima.</span><span class="sxs-lookup"><span data-stu-id="bd380-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="bd380-239">Consulte la sección [Propiedades del servicio vinculado de OData](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="bd380-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="bd380-240">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="bd380-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="bd380-241">**Conjunto de datos de entrada de OData:**</span><span class="sxs-lookup"><span data-stu-id="bd380-241">**OData input dataset:**</span></span>

<span data-ttu-id="bd380-242">Si se establece "external": "true", se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="bd380-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="bd380-243">La especificación de **path** en la definición del conjunto de datos es opcional.</span><span class="sxs-lookup"><span data-stu-id="bd380-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="bd380-244">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="bd380-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bd380-245">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="bd380-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bd380-246">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="bd380-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bd380-247">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="bd380-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="bd380-248">**Actividad de copia en una canalización con origen OData y receptor blob:**</span><span class="sxs-lookup"><span data-stu-id="bd380-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="bd380-249">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="bd380-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="bd380-250">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bd380-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="bd380-251">La consulta SQL especificada para la propiedad **query** selecciona los últimos datos (los más recientes) del origen de OData.</span><span class="sxs-lookup"><span data-stu-id="bd380-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="bd380-252">La especificación de **query** en la definición de la canalización es opcional.</span><span class="sxs-lookup"><span data-stu-id="bd380-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="bd380-253">Dirección **URL** que el servicio Data Factory usa para recuperar los datos: dirección URL especificada en el servicio vinculado (obligatorio) + ruta de acceso especificada en el conjunto de datos (opcional) + consulta en la canalización (opcional).</span><span class="sxs-lookup"><span data-stu-id="bd380-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="bd380-254">Asignación de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="bd380-254">Type mapping for OData</span></span>
<span data-ttu-id="bd380-255">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="bd380-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="bd380-256">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="bd380-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="bd380-257">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="bd380-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="bd380-258">Cuando se mueven datos desde almacenes de datos de OData, los tipos de datos de OData se asignan a tipos. NET.</span><span class="sxs-lookup"><span data-stu-id="bd380-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="bd380-259">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="bd380-259">Map source to sink columns</span></span>
<span data-ttu-id="bd380-260">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bd380-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="bd380-261">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="bd380-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="bd380-262">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="bd380-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="bd380-263">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="bd380-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="bd380-264">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="bd380-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="bd380-265">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="bd380-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="bd380-266">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="bd380-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bd380-267">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="bd380-267">Performance and Tuning</span></span>
<span data-ttu-id="bd380-268">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="bd380-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
