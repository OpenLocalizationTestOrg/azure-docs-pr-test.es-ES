---
title: datos de aaaMove de fuentes de OData | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure de orígenes de datos de toomove de OData."
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
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="a088a-103">Movimiento de datos de un origen de OData mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="a088a-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="a088a-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un origen de OData.</span><span class="sxs-lookup"><span data-stu-id="a088a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="a088a-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a088a-106">Puede copiar datos desde un almacén de datos de OData origen tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="a088a-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="a088a-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="a088a-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a088a-108">Factoría de datos admite actualmente solo mover almacenes de datos desde una fuente de OData tooother datos, pero no para mover los datos de otros datos almacena el código fuente de OData de tooan.</span><span class="sxs-lookup"><span data-stu-id="a088a-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="a088a-109">Versiones admitidas y tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="a088a-109">Supported versions and authentication types</span></span>
<span data-ttu-id="a088a-110">Este conector OData admite la versión de OData 3.0 y 4.0, y puede copiar datos de orígenes OData locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="a088a-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="a088a-111">Para Hola este último debe tooinstall Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a088a-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="a088a-112">Consulte el artículo [Mover datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a088a-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="a088a-113">Estos son los tipos de autenticación admitidos:</span><span class="sxs-lookup"><span data-stu-id="a088a-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="a088a-114">tooaccess **nube** fuente de OData, puede usar anónima, básica (nombre de usuario y contraseña) o Azure Active Directory en la función de autenticación de OAuth.</span><span class="sxs-lookup"><span data-stu-id="a088a-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="a088a-115">tooaccess **local** fuente de OData, puede usar anónima, básica (nombre de usuario y contraseña) o la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="a088a-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a088a-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="a088a-116">Getting started</span></span>
<span data-ttu-id="a088a-117">Puede crear una canalización con una actividad de copia que mueva datos desde un origen OData mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="a088a-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="a088a-118">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="a088a-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a088a-119">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="a088a-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="a088a-120">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="a088a-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a088a-121">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="a088a-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a088a-122">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="a088a-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="a088a-123">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="a088a-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a088a-124">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="a088a-125">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="a088a-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a088a-126">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="a088a-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a088a-127">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a088a-128">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un origen OData, vea [ejemplo de JSON: copiar los datos de código fuente de OData tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a088a-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a088a-129">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son origen de tooOData específicos de entidades de toodefine usado factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="a088a-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a088a-130">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="a088a-130">Linked Service properties</span></span>
<span data-ttu-id="a088a-131">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooOData vinculado.</span><span class="sxs-lookup"><span data-stu-id="a088a-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="a088a-132">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a088a-132">Property</span></span> | <span data-ttu-id="a088a-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="a088a-133">Description</span></span> | <span data-ttu-id="a088a-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a088a-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a088a-135">type</span><span class="sxs-lookup"><span data-stu-id="a088a-135">type</span></span> |<span data-ttu-id="a088a-136">propiedad de tipo Hello debe establecerse en: **OData**</span><span class="sxs-lookup"><span data-stu-id="a088a-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="a088a-137">Sí</span><span class="sxs-lookup"><span data-stu-id="a088a-137">Yes</span></span> |
| <span data-ttu-id="a088a-138">url</span><span class="sxs-lookup"><span data-stu-id="a088a-138">url</span></span> |<span data-ttu-id="a088a-139">Dirección URL del servicio OData Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-139">Url of hello OData service.</span></span> |<span data-ttu-id="a088a-140">Sí</span><span class="sxs-lookup"><span data-stu-id="a088a-140">Yes</span></span> |
| <span data-ttu-id="a088a-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a088a-141">authenticationType</span></span> |<span data-ttu-id="a088a-142">Tipo de autenticación usa tooconnect toohello OData origen.</span><span class="sxs-lookup"><span data-stu-id="a088a-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="a088a-143">Para OData en la nube, los valores posibles son Anonymous, Basic y OAuth (tenga en cuenta que Azure Data Factory en estos momentos solo admite la autenticación OAuth basada en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a088a-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="a088a-144">Para OData local, los valores posibles son: Anonymous, Basic y Windows.</span><span class="sxs-lookup"><span data-stu-id="a088a-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="a088a-145">Sí</span><span class="sxs-lookup"><span data-stu-id="a088a-145">Yes</span></span> |
| <span data-ttu-id="a088a-146">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="a088a-146">username</span></span> |<span data-ttu-id="a088a-147">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="a088a-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="a088a-148">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="a088a-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="a088a-149">Contraseña</span><span class="sxs-lookup"><span data-stu-id="a088a-149">password</span></span> |<span data-ttu-id="a088a-150">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="a088a-151">Sí (solo si usa la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="a088a-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="a088a-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="a088a-152">authorizedCredential</span></span> |<span data-ttu-id="a088a-153">Si usa OAuth, haga clic en **Authorize** botón en hello Asistente para copiar de factoría de datos o el Editor y escriba sus credenciales, valor de Hola de esta propiedad será generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a088a-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="a088a-154">Sí (solo si usa la autenticación OAuth)</span><span class="sxs-lookup"><span data-stu-id="a088a-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="a088a-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a088a-155">gatewayName</span></span> |<span data-ttu-id="a088a-156">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el servicio de OData de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="a088a-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="a088a-157">Especifique solo si va a copiar datos del origen de OData local.</span><span class="sxs-lookup"><span data-stu-id="a088a-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="a088a-158">No</span><span class="sxs-lookup"><span data-stu-id="a088a-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="a088a-159">Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="a088a-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a088a-160">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="a088a-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="a088a-161">Uso de la autenticación de Windows para acceder al origen de OData local</span><span class="sxs-lookup"><span data-stu-id="a088a-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="a088a-162">Uso de la autenticación OAuth para tener acceso al origen de OData en la nube</span><span class="sxs-lookup"><span data-stu-id="a088a-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a088a-163">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="a088a-163">Dataset properties</span></span>
<span data-ttu-id="a088a-164">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a088a-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a088a-165">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="a088a-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a088a-166">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="a088a-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a088a-167">sección typeProperties Hello para el conjunto de datos de tipo **ODataResource** (que incluye el conjunto de datos de OData) tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="a088a-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="a088a-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a088a-168">Property</span></span> | <span data-ttu-id="a088a-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="a088a-169">Description</span></span> | <span data-ttu-id="a088a-170">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a088a-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a088a-171">path</span><span class="sxs-lookup"><span data-stu-id="a088a-171">path</span></span> |<span data-ttu-id="a088a-172">Ruta de acceso toohello recurso de OData</span><span class="sxs-lookup"><span data-stu-id="a088a-172">Path toohello OData resource</span></span> |<span data-ttu-id="a088a-173">No</span><span class="sxs-lookup"><span data-stu-id="a088a-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a088a-174">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="a088a-174">Copy activity properties</span></span>
<span data-ttu-id="a088a-175">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a088a-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a088a-176">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="a088a-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a088a-177">Propiedades disponibles en la sección de typeProperties Hola de actividad de hello en hello otra parte varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="a088a-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="a088a-178">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="a088a-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a088a-179">Cuando el origen es del tipo **RelationalSource** (que incluye OData) Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="a088a-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a088a-180">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a088a-180">Property</span></span> | <span data-ttu-id="a088a-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="a088a-181">Description</span></span> | <span data-ttu-id="a088a-182">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a088a-182">Example</span></span> | <span data-ttu-id="a088a-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a088a-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a088a-184">query</span><span class="sxs-lookup"><span data-stu-id="a088a-184">query</span></span> |<span data-ttu-id="a088a-185">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="a088a-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="a088a-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="a088a-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="a088a-187">No</span><span class="sxs-lookup"><span data-stu-id="a088a-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="a088a-188">Asignación de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="a088a-188">Type Mapping for OData</span></span>
<span data-ttu-id="a088a-189">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="a088a-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="a088a-190">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="a088a-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="a088a-191">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a088a-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="a088a-192">Al mover los datos de OData, hello siguientes usan las asignaciones son de tipo de too.NET de tipos de OData.</span><span class="sxs-lookup"><span data-stu-id="a088a-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="a088a-193">Tipo de datos OData</span><span class="sxs-lookup"><span data-stu-id="a088a-193">OData Data Type</span></span> | <span data-ttu-id="a088a-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a088a-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="a088a-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="a088a-195">Edm.Binary</span></span> |<span data-ttu-id="a088a-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a088a-196">Byte[]</span></span> |
| <span data-ttu-id="a088a-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="a088a-197">Edm.Boolean</span></span> |<span data-ttu-id="a088a-198">Booleano</span><span class="sxs-lookup"><span data-stu-id="a088a-198">Bool</span></span> |
| <span data-ttu-id="a088a-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="a088a-199">Edm.Byte</span></span> |<span data-ttu-id="a088a-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a088a-200">Byte[]</span></span> |
| <span data-ttu-id="a088a-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="a088a-201">Edm.DateTime</span></span> |<span data-ttu-id="a088a-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="a088a-202">DateTime</span></span> |
| <span data-ttu-id="a088a-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="a088a-203">Edm.Decimal</span></span> |<span data-ttu-id="a088a-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="a088a-204">Decimal</span></span> |
| <span data-ttu-id="a088a-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="a088a-205">Edm.Double</span></span> |<span data-ttu-id="a088a-206">Doble</span><span class="sxs-lookup"><span data-stu-id="a088a-206">Double</span></span> |
| <span data-ttu-id="a088a-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="a088a-207">Edm.Single</span></span> |<span data-ttu-id="a088a-208">Single</span><span class="sxs-lookup"><span data-stu-id="a088a-208">Single</span></span> |
| <span data-ttu-id="a088a-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="a088a-209">Edm.Guid</span></span> |<span data-ttu-id="a088a-210">Guid</span><span class="sxs-lookup"><span data-stu-id="a088a-210">Guid</span></span> |
| <span data-ttu-id="a088a-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="a088a-211">Edm.Int16</span></span> |<span data-ttu-id="a088a-212">Int16</span><span class="sxs-lookup"><span data-stu-id="a088a-212">Int16</span></span> |
| <span data-ttu-id="a088a-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="a088a-213">Edm.Int32</span></span> |<span data-ttu-id="a088a-214">Int32</span><span class="sxs-lookup"><span data-stu-id="a088a-214">Int32</span></span> |
| <span data-ttu-id="a088a-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="a088a-215">Edm.Int64</span></span> |<span data-ttu-id="a088a-216">Int64</span><span class="sxs-lookup"><span data-stu-id="a088a-216">Int64</span></span> |
| <span data-ttu-id="a088a-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="a088a-217">Edm.SByte</span></span> |<span data-ttu-id="a088a-218">Int16</span><span class="sxs-lookup"><span data-stu-id="a088a-218">Int16</span></span> |
| <span data-ttu-id="a088a-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="a088a-219">Edm.String</span></span> |<span data-ttu-id="a088a-220">String</span><span class="sxs-lookup"><span data-stu-id="a088a-220">String</span></span> |
| <span data-ttu-id="a088a-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="a088a-221">Edm.Time</span></span> |<span data-ttu-id="a088a-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a088a-222">TimeSpan</span></span> |
| <span data-ttu-id="a088a-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a088a-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="a088a-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a088a-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="a088a-225">Los tipos de datos complejos de OData, como por ejemplo, Object no se admiten.</span><span class="sxs-lookup"><span data-stu-id="a088a-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="a088a-226">Ejemplo de JSON: copiar los datos de código fuente de OData tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="a088a-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="a088a-227">Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a088a-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a088a-228">Muestra cómo tooan almacenamiento de blobs de Azure del origen de datos de toocopy desde una de OData.</span><span class="sxs-lookup"><span data-stu-id="a088a-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="a088a-229">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a088a-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="a088a-230">ejemplo de Hola tiene Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="a088a-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="a088a-231">Un servicio vinculado de tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a088a-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="a088a-232">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="a088a-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a088a-233">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a088a-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="a088a-234">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a088a-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a088a-235">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a088a-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a088a-236">ejemplo de Hola copia datos de realizar una consulta en un tooan de origen OData blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="a088a-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="a088a-237">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="a088a-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a088a-238">**Servicio vinculado de OData:** en este ejemplo usa Hola autenticación anónima.</span><span class="sxs-lookup"><span data-stu-id="a088a-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="a088a-239">Consulte la sección [Propiedades del servicio vinculado de OData](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="a088a-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="a088a-240">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="a088a-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="a088a-241">**Conjunto de datos de entrada de OData:**</span><span class="sxs-lookup"><span data-stu-id="a088a-241">**OData input dataset:**</span></span>

<span data-ttu-id="a088a-242">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="a088a-243">Especificar **ruta de acceso** en el conjunto de datos de hello definición es opcional.</span><span class="sxs-lookup"><span data-stu-id="a088a-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="a088a-244">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="a088a-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a088a-245">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a088a-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a088a-246">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="a088a-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a088a-247">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="a088a-248">**Actividad de copia en una canalización con origen OData y receptor blob:**</span><span class="sxs-lookup"><span data-stu-id="a088a-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="a088a-249">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="a088a-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a088a-250">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a088a-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a088a-251">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos de (más recientes) más recientes de Hola de código fuente de OData de Hola.</span><span class="sxs-lookup"><span data-stu-id="a088a-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

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

<span data-ttu-id="a088a-252">Especificar **consulta** en canalización Hola definición es opcional.</span><span class="sxs-lookup"><span data-stu-id="a088a-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="a088a-253">Hola **URL** es que el servicio de factoría de datos de hello utiliza datos tooretrieve: dirección URL especificada en Hola servicios vinculados (obligatorio) + ruta de acceso especificada en el conjunto de datos de hello (opcional) + consultar en la canalización de hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="a088a-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="a088a-254">Asignación de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="a088a-254">Type mapping for OData</span></span>
<span data-ttu-id="a088a-255">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="a088a-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="a088a-256">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="a088a-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="a088a-257">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a088a-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="a088a-258">Al mover los datos de almacenes de datos de OData, tipos de datos de OData son tipos de too.NET asignado.</span><span class="sxs-lookup"><span data-stu-id="a088a-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="a088a-259">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="a088a-259">Map source toosink columns</span></span>
<span data-ttu-id="a088a-260">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a088a-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a088a-261">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="a088a-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="a088a-262">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="a088a-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="a088a-263">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="a088a-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a088a-264">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="a088a-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a088a-265">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="a088a-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a088a-266">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a088a-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a088a-267">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="a088a-267">Performance and Tuning</span></span>
<span data-ttu-id="a088a-268">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="a088a-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
