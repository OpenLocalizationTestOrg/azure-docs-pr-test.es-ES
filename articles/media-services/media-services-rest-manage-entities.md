---
title: entidades de servicios multimedia de aaaManaging con REST | Documentos de Microsoft
description: "Obtenga información acerca de cómo de servicios multimedia de toomanage entidades con API de REST."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="d8cfe-103">Administración de entidades de Media Services con REST</span><span class="sxs-lookup"><span data-stu-id="d8cfe-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8cfe-104">REST</span><span class="sxs-lookup"><span data-stu-id="d8cfe-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="d8cfe-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d8cfe-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="d8cfe-106">Servicios multimedia de Microsoft Azure es un servicio REST basado en OData v3.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="d8cfe-107">Puede agregar, consulta, actualización y eliminar entidades prácticamente Hola misma forma que lo haría en cualquier otro servicio de OData.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="d8cfe-108">Se indicarán las excepciones cuando proceda.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="d8cfe-109">Para obtener más información sobre OData, consulte la [documentación de Open Data Protocol](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="d8cfe-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="d8cfe-110">Este tema muestra cómo las entidades de servicios multimedia de Azure toomanage con REST.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="d8cfe-111">A partir del 1 de abril de 2017, cualquier registro de trabajo en su cuenta de más de 90 días se eliminarán automáticamente, junto con sus registros de tarea asociados, incluso si el número total de Hola de registros está por debajo de la cuota máxima de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="d8cfe-112">Por ejemplo, el 1 de abril de 2017, todos los registros de trabajo de la cuenta que sean anteriores al 31 de diciembre de 2016 se eliminarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="d8cfe-113">Si necesita información de trabajo o tarea hello tooarchive, puede usar código de hello descrito en este tema.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="d8cfe-114">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="d8cfe-114">Considerations</span></span>  

<span data-ttu-id="d8cfe-115">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d8cfe-116">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d8cfe-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="d8cfe-117">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="d8cfe-117">Connect tooMedia Services</span></span>

<span data-ttu-id="d8cfe-118">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d8cfe-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d8cfe-119">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d8cfe-120">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="d8cfe-121">Incorporación de entidades</span><span class="sxs-lookup"><span data-stu-id="d8cfe-121">Adding entities</span></span>
<span data-ttu-id="d8cfe-122">Todas las entidades de servicios multimedia se agregan el conjunto de entidades tooan, por ejemplo, Assets, mediante una solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="d8cfe-123">Hola siguiente ejemplo se muestra cómo toocreate AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="d8cfe-124">Consulta de entidades</span><span class="sxs-lookup"><span data-stu-id="d8cfe-124">Querying entities</span></span>
<span data-ttu-id="d8cfe-125">La consulta y enumeración de entidades es sencilla y solo implica una solicitud HTTP GET y operaciones OData opcionales.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="d8cfe-126">Hello en el ejemplo siguiente se recupera una lista de todas las entidades MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="d8cfe-127">También puede recuperar una entidad específica o todos los conjuntos de entidades asociados con una entidad específica, como en hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d8cfe-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="d8cfe-128">Hello en el ejemplo siguiente se devuelve solo Hola propiedad de estado de todos los trabajos.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="d8cfe-129">Hello en el ejemplo siguiente se devuelve todas las JobTemplates con el nombre de Hola "SampleTemplate".</span><span class="sxs-lookup"><span data-stu-id="d8cfe-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="d8cfe-130">la operación de expansión Hello $ no se admite en los servicios multimedia, así como Hola métodos LINQ incompatibles que se describe en la sección Consideraciones de LINQ (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="d8cfe-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="d8cfe-131">Enumeración de grandes colecciones de entidades</span><span class="sxs-lookup"><span data-stu-id="d8cfe-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="d8cfe-132">Cuando se consultan las entidades, hay un límite de 1000 entidades devueltas al mismo tiempo porque pública v2 REST limita los resultados de too1000 de resultados de consulta.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="d8cfe-133">Use **omitir** y **arriba** tooenumerate a través de la colección de gran tamaño Hola de entidades.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="d8cfe-134">Hola siguiente ejemplo se muestra cómo toouse **omitir** y **arriba** tooskip Hola primero 2000 trabajos y get Hola junto 1000 trabajos.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="d8cfe-135">Actualización de entidades</span><span class="sxs-lookup"><span data-stu-id="d8cfe-135">Updating entities</span></span>
<span data-ttu-id="d8cfe-136">Según el tipo de entidad de Hola y el estado de Hola que se encuentra, puede actualizar propiedades de la entidad a través de una revisión, solicitudes PUT o MERGE HTTP.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="d8cfe-137">Para obtener más información acerca de estas operaciones, vea [PATCH, PUT, MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8cfe-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="d8cfe-138">Hola, ejemplo de código siguiente muestra cómo tooupdate Hola propiedad de nombre de una entidad de activos.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="d8cfe-139">Eliminación de entidades</span><span class="sxs-lookup"><span data-stu-id="d8cfe-139">Deleting entities</span></span>
<span data-ttu-id="d8cfe-140">Las entidades pueden eliminarse en Servicios multimedia mediante una solicitud HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="d8cfe-141">Dependiendo de la entidad de hello, orden de Hola que eliminar entidades sea importante.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="d8cfe-142">Por ejemplo, las entidades como Assets, requieren que revocar (o eliminar) todos los localizadores que hagan referencia a Asset particular antes de eliminar Hola activo.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="d8cfe-143">Hola siguiente ejemplo se muestra cómo toodelete un localizador que estaba tooupload usa un archivo en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d8cfe-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8cfe-144">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="d8cfe-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8cfe-145">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d8cfe-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

