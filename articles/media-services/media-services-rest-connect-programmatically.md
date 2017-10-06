---
title: aaaConnecting tooMedia cuenta de servicios mediante API de REST | Documentos de Microsoft
description: "Este tema muestra cómo usar servicios de tooconnect tooMedia REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="01a7f-103">Conexión tooMedia cuenta de servicios mediante la API de REST de servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="01a7f-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01a7f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="01a7f-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="01a7f-105">REST</span><span class="sxs-lookup"><span data-stu-id="01a7f-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="01a7f-106">Este tema describe cómo tooobtain una tooMicrosoft de conexión mediante programación los servicios de multimedia de Azure cuando se programa con Hola API de REST de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="01a7f-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="01a7f-107">Se necesitan dos cosas al obtener acceso a servicios de multimedia de Microsoft Azure: un token de acceso proporcionado por servicios de Control de acceso (ACS) de Azure y Hola URI de los servicios de multimedia propio.</span><span class="sxs-lookup"><span data-stu-id="01a7f-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="01a7f-108">Puede usar los métodos que quiera para crear estas solicitudes, siempre que especifique los valores de encabezado adecuados de Hola y pasar en el token de acceso de hello correctamente al llamar a en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="01a7f-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="01a7f-109">Hola pasos describe el flujo de trabajo de más comunes de hello al usar Hola API de REST de servicios multimedia tooconnect tooMedia Services:</span><span class="sxs-lookup"><span data-stu-id="01a7f-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="01a7f-110">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="01a7f-110">Getting an access token</span></span> 
2. <span data-ttu-id="01a7f-111">Toohello conexión URI de servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="01a7f-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="01a7f-112">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="01a7f-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="01a7f-113">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="01a7f-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="01a7f-114">También puede recibir una respuesta HTTP/1.1 200 que contiene Hola descripción de metadatos de API de ODATA.</span><span class="sxs-lookup"><span data-stu-id="01a7f-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="01a7f-115">Registrar su posterior llamadas a la API toohello nueva dirección URL.</span><span class="sxs-lookup"><span data-stu-id="01a7f-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="01a7f-116">Por ejemplo, si después de intentar tooconnect, obtuvo siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="01a7f-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="01a7f-117">Debe publicar los siguientes API llamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="01a7f-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="01a7f-118">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="01a7f-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="01a7f-119">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="01a7f-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="01a7f-120">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="01a7f-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="01a7f-121">Dirección de control de acceso</span><span class="sxs-lookup"><span data-stu-id="01a7f-121">Access control address</span></span>
<span data-ttu-id="01a7f-122">La dirección de control de acceso de Media Services es https://wamsprodglobal001acs.accesscontrol.windows.net, excepto para la región del Norte de China, que es https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="01a7f-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="01a7f-123">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="01a7f-123">Getting an access token</span></span>
<span data-ttu-id="01a7f-124">Servicios de multimedia de tooaccess directamente a través de la API de REST de hello, recuperar un token de acceso de ACS y úselo durante todas las solicitudes HTTP que realice en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a7f-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="01a7f-125">Este token es similar tokens tooother proporcionados por ACS basado en notificaciones de acceso proporcionadas en el encabezado de Hola de una solicitud HTTP y el uso de protocolo de hello OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="01a7f-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="01a7f-126">No es necesario ningún otro requisito previo antes de conectarse directamente tooMedia servicios.</span><span class="sxs-lookup"><span data-stu-id="01a7f-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="01a7f-127">Hello en el ejemplo siguiente se muestra encabezado de solicitud HTTP de Hola y tooretrieve cuerpo usa un token.</span><span class="sxs-lookup"><span data-stu-id="01a7f-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="01a7f-128">**Encabezado**:</span><span class="sxs-lookup"><span data-stu-id="01a7f-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="01a7f-129">**Cuerpo**:</span><span class="sxs-lookup"><span data-stu-id="01a7f-129">**Body**:</span></span>

<span data-ttu-id="01a7f-130">Necesita los valores de client_id y client_secret de hello tooprove en el cuerpo de Hola de esta solicitud; client_id y client_secret corresponden toohello AccountName y AccountKey valores, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="01a7f-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="01a7f-131">Estos valores se proporcionan tooyou con servicios multimedia al configurar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="01a7f-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="01a7f-132">Tenga en cuenta que hello AccountKey para su cuenta de servicios multimedia debe codificarse para URL (vea [codificación porcentual](http://tools.ietf.org/html/rfc3986#section-2.1) cuando se usa como valor de client_secret hello en la solicitud de token de acceso.</span><span class="sxs-lookup"><span data-stu-id="01a7f-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="01a7f-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="01a7f-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="01a7f-134">Hello en el ejemplo siguiente se muestra hello HTTP respuesta que contiene el acceso de hello token en el cuerpo de la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a7f-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="01a7f-135">Se recomienda toocache Hola "access_token" y "expires_in" valores tooan almacenamiento externo.</span><span class="sxs-lookup"><span data-stu-id="01a7f-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="01a7f-136">datos de token de Hello más adelante pudieron recuperar desde el almacenamiento de Hola o volver a utilizar en las llamadas de API de REST de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="01a7f-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="01a7f-137">Esto es especialmente útil para escenarios donde el token de hello puede compartirse de forma segura entre varios procesos o equipos.</span><span class="sxs-lookup"><span data-stu-id="01a7f-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="01a7f-138">Asegúrese de que toomonitor Hola "expires_in" el valor de acceso de hello token y actualice las llamadas de API de REST con nuevos tokens según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="01a7f-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="01a7f-139">Toohello conexión URI de servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="01a7f-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="01a7f-140">Hola URI raíz para los servicios multimedia es https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="01a7f-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="01a7f-141">Debe conectarse inicialmente toothis URI y, si recibe una redirección 301 en respuesta, debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="01a7f-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="01a7f-142">Además, no use ninguna lógica de redirección automática/seguimiento en las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="01a7f-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="01a7f-143">Verbos HTTP y los cuerpos de solicitud no se reenviarán toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="01a7f-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="01a7f-144">Tenga en cuenta que root Hola URI para cargar y descargar archivos de recursos es https://yourstorageaccount.blob.core.windows.net/ donde nombre de cuenta de almacenamiento de Hola Hola uno mismo que usó durante la configuración de la cuenta de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="01a7f-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="01a7f-145">Hola de ejemplo siguiente se muestra cómo HTTP solicitud toohello servicios multimedia raíz URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="01a7f-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="01a7f-146">solicitud de Hello Obtiene una redirección 301 en respuesta.</span><span class="sxs-lookup"><span data-stu-id="01a7f-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="01a7f-147">Hello solicitud subsiguiente usa Hola nuevo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="01a7f-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="01a7f-148">**Solicitud HTTP**:</span><span class="sxs-lookup"><span data-stu-id="01a7f-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="01a7f-149">**Respuesta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="01a7f-149">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="01a7f-150">**Solicitud HTTP** (usando Hola nuevo URI):</span><span class="sxs-lookup"><span data-stu-id="01a7f-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="01a7f-151">**Respuesta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="01a7f-151">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="01a7f-152">Cuando obtenga Hola nuevo URI, que es hello URI que se debe toocommunicate utilizado con servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="01a7f-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="01a7f-153">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="01a7f-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="01a7f-154">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="01a7f-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

