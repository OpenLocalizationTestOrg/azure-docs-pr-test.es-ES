---
title: "Conexión con la cuenta de Media Services mediante la API de REST | Microsoft Azure"
description: "En este tema se muestra cómo conectarse a Servicios multimedia con la API de REST."
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
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="11ead-103">Conexión con la cuenta de Servicios multimedia mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="11ead-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11ead-104">.NET</span><span class="sxs-lookup"><span data-stu-id="11ead-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="11ead-105">REST</span><span class="sxs-lookup"><span data-stu-id="11ead-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="11ead-106">En este tema se describe cómo obtener una conexión mediante programación a Microsoft Azure Media Services al programar con la API de REST de Media Services.</span><span class="sxs-lookup"><span data-stu-id="11ead-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="11ead-107">Hay dos elementos necesarios al obtener acceso a Servicios multimedia de Microsoft Azure: un token de acceso proporcionado por los Servicios de control de acceso (ACS) de Azure y el propio URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="11ead-108">Puede usar los métodos que desee para crear estas solicitudes siempre que especifique los valores de encabezado adecuados y pase el token de acceso correctamente al llamar a Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="11ead-109">En los pasos siguientes se describe el flujo de trabajo más común al usar la API de REST de Servicios multimedia para conectarse a Servicios multimedia:</span><span class="sxs-lookup"><span data-stu-id="11ead-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="11ead-110">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="11ead-110">Getting an access token</span></span> 
2. <span data-ttu-id="11ead-111">Conexión al URI de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="11ead-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="11ead-112">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="11ead-113">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="11ead-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="11ead-114">Es posible que también reciba una respuesta HTTP/1.1 200 que contenga la descripción de metadatos de la API de ODATA.</span><span class="sxs-lookup"><span data-stu-id="11ead-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="11ead-115">Registre las llamadas de API posteriores en la nueva dirección URL.</span><span class="sxs-lookup"><span data-stu-id="11ead-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="11ead-116">Por ejemplo, si después de intentar conectarse, obtiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="11ead-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="11ead-117">Debe registrar las llamadas posteriores de API en https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="11ead-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="11ead-118">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="11ead-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="11ead-119">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="11ead-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="11ead-120">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="11ead-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="11ead-121">Dirección de control de acceso</span><span class="sxs-lookup"><span data-stu-id="11ead-121">Access control address</span></span>
<span data-ttu-id="11ead-122">La dirección de control de acceso de Media Services es https://wamsprodglobal001acs.accesscontrol.windows.net, excepto para la región del Norte de China, que es https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="11ead-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="11ead-123">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="11ead-123">Getting an access token</span></span>
<span data-ttu-id="11ead-124">Para obtener acceso a Servicios multimedia directamente a través de la API de REST, recupere un token de acceso de ACS y úselo en todas las solicitudes HTTP que realice en el servicio.</span><span class="sxs-lookup"><span data-stu-id="11ead-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="11ead-125">Este token es similar a otros tokens proporcionados por ACS basados en notificaciones de acceso proporcionadas en el encabezado de una solicitud HTTP y que usan el protocolo OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="11ead-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="11ead-126">No es necesario ningún otro requisito previo antes de conectarse directamente a Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="11ead-127">En el ejemplo siguiente se muestra el encabezado y el cuerpo de solicitud HTTP que se usan para recuperar un token.</span><span class="sxs-lookup"><span data-stu-id="11ead-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="11ead-128">**Encabezado**:</span><span class="sxs-lookup"><span data-stu-id="11ead-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="11ead-129">**Cuerpo**:</span><span class="sxs-lookup"><span data-stu-id="11ead-129">**Body**:</span></span>

<span data-ttu-id="11ead-130">Debe probar los valores client_id y client_secret en el cuerpo de esta solicitud; client_id y client_secret se corresponden con los valores AccountName y AccountKey, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="11ead-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="11ead-131">Servicios multimedia le proporciona estos valores al configurar su cuenta.</span><span class="sxs-lookup"><span data-stu-id="11ead-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="11ead-132">Tenga en cuenta que el valor AccountKey de su cuenta de Media Services debe tener codificación URL (consulte [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) cuando se usa como el valor client_secret en la solicitud de token de acceso.</span><span class="sxs-lookup"><span data-stu-id="11ead-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="11ead-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="11ead-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="11ead-134">En el ejemplo siguiente se muestra la respuesta HTTP que contiene el token de acceso en el cuerpo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="11ead-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

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
> <span data-ttu-id="11ead-135">Se recomienda almacenar en memoria caché los valores "access_token" y "expires_in" en un almacenamiento externo.</span><span class="sxs-lookup"><span data-stu-id="11ead-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="11ead-136">Los datos del token se pueden recuperar más tarde desde el almacenamiento y se pueden reutilizar en las llamadas de API de REST de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="11ead-137">Esto es especialmente útil para escenarios en que el token se puede compartir de forma segura entre varios procesos o equipos.</span><span class="sxs-lookup"><span data-stu-id="11ead-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="11ead-138">Asegúrese de supervisar el valor "expires_in" del token de acceso y actualice las llamadas de API de REST con nuevos tokens según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="11ead-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="11ead-139">Conexión al URI de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="11ead-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="11ead-140">El URI raíz de Servicios multimedia es https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="11ead-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="11ead-141">Inicialmente, debe conectarse a este URI y, si obtiene una redirección 301 como respuesta, debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="11ead-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="11ead-142">Además, no use ninguna lógica de redirección automática/seguimiento en las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="11ead-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="11ead-143">Los verbos HTTP y los cuerpos de solicitud no se enviarán al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="11ead-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="11ead-144">Tenga en cuenta que el URI raíz para cargar y descargar archivos de recursos es https://yourstorageaccount.blob.core.windows.net/, donde el nombre de la cuenta de almacenamiento es el mismo que usó al configurar la cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="11ead-145">En el ejemplo siguiente se muestra la solicitud HTTP al URI raíz de Media Services (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="11ead-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="11ead-146">La solicitud obtiene una redirección 301 como respuesta.</span><span class="sxs-lookup"><span data-stu-id="11ead-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="11ead-147">La solicitud siguiente usa el nuevo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="11ead-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="11ead-148">**Solicitud HTTP**:</span><span class="sxs-lookup"><span data-stu-id="11ead-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="11ead-149">**Respuesta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="11ead-149">**HTTP Response**:</span></span>

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
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="11ead-150">**Solicitud HTTP** (con el nuevo URI):</span><span class="sxs-lookup"><span data-stu-id="11ead-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="11ead-151">**Respuesta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="11ead-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="11ead-152">Una vez que obtenga el nuevo URI, ese será el URI que debe usarse para comunicarse con Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="11ead-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="11ead-153">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="11ead-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11ead-154">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="11ead-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

