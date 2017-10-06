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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Conexión tooMedia cuenta de servicios mediante la API de REST de servicios multimedia
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Este tema describe cómo tooobtain una tooMicrosoft de conexión mediante programación los servicios de multimedia de Azure cuando se programa con Hola API de REST de servicios multimedia.

Se necesitan dos cosas al obtener acceso a servicios de multimedia de Microsoft Azure: un token de acceso proporcionado por servicios de Control de acceso (ACS) de Azure y Hola URI de los servicios de multimedia propio. Puede usar los métodos que quiera para crear estas solicitudes, siempre que especifique los valores de encabezado adecuados de Hola y pasar en el token de acceso de hello correctamente al llamar a en los servicios multimedia.

Hola pasos describe el flujo de trabajo de más comunes de hello al usar Hola API de REST de servicios multimedia tooconnect tooMedia Services:

1. Obtención de un token de acceso 
2. Toohello conexión URI de servicios multimedia 
   
   > [!NOTE]
   > Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI.
   > También puede recibir una respuesta HTTP/1.1 200 que contiene Hola descripción de metadatos de API de ODATA.
   > 
   > 
3. Registrar su posterior llamadas a la API toohello nueva dirección URL. 
   
    Por ejemplo, si después de intentar tooconnect, obtuvo siguiente hello:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Debe publicar los siguientes API llamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.

    >[!NOTE]
    >Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .

## <a name="access-control-address"></a>Dirección de control de acceso
La dirección de control de acceso de Media Services es https://wamsprodglobal001acs.accesscontrol.windows.net, excepto para la región del Norte de China, que es https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Obtención de un token de acceso
Servicios de multimedia de tooaccess directamente a través de la API de REST de hello, recuperar un token de acceso de ACS y úselo durante todas las solicitudes HTTP que realice en el servicio de Hola. Este token es similar tokens tooother proporcionados por ACS basado en notificaciones de acceso proporcionadas en el encabezado de Hola de una solicitud HTTP y el uso de protocolo de hello OAuth v2. No es necesario ningún otro requisito previo antes de conectarse directamente tooMedia servicios.

Hello en el ejemplo siguiente se muestra encabezado de solicitud HTTP de Hola y tooretrieve cuerpo usa un token.

**Encabezado**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Cuerpo**:

Necesita los valores de client_id y client_secret de hello tooprove en el cuerpo de Hola de esta solicitud; client_id y client_secret corresponden toohello AccountName y AccountKey valores, respectivamente. Estos valores se proporcionan tooyou con servicios multimedia al configurar la cuenta. 

Tenga en cuenta que hello AccountKey para su cuenta de servicios multimedia debe codificarse para URL (vea [codificación porcentual](http://tools.ietf.org/html/rfc3986#section-2.1) cuando se usa como valor de client_secret hello en la solicitud de token de acceso.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Por ejemplo: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Hello en el ejemplo siguiente se muestra hello HTTP respuesta que contiene el acceso de hello token en el cuerpo de la respuesta de Hola.

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
> Se recomienda toocache Hola "access_token" y "expires_in" valores tooan almacenamiento externo. datos de token de Hello más adelante pudieron recuperar desde el almacenamiento de Hola o volver a utilizar en las llamadas de API de REST de servicios multimedia. Esto es especialmente útil para escenarios donde el token de hello puede compartirse de forma segura entre varios procesos o equipos.
> 
> 

Asegúrese de que toomonitor Hola "expires_in" el valor de acceso de hello token y actualice las llamadas de API de REST con nuevos tokens según sea necesario.

### <a name="connecting-toohello-media-services-uri"></a>Toohello conexión URI de servicios multimedia
Hola URI raíz para los servicios multimedia es https://media.windows.net/. Debe conectarse inicialmente toothis URI y, si recibe una redirección 301 en respuesta, debe realizar las llamadas subsiguientes toohello nuevo URI. Además, no use ninguna lógica de redirección automática/seguimiento en las solicitudes. Verbos HTTP y los cuerpos de solicitud no se reenviarán toohello nuevo URI.

Tenga en cuenta que root Hola URI para cargar y descargar archivos de recursos es https://yourstorageaccount.blob.core.windows.net/ donde nombre de cuenta de almacenamiento de Hola Hola uno mismo que usó durante la configuración de la cuenta de servicios multimedia.

Hola de ejemplo siguiente se muestra cómo HTTP solicitud toohello servicios multimedia raíz URI (https://media.windows.net/). solicitud de Hello Obtiene una redirección 301 en respuesta. Hello solicitud subsiguiente usa Hola nuevo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**Solicitud HTTP**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**Respuesta HTTP**:

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


**Solicitud HTTP** (usando Hola nuevo URI):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**Respuesta HTTP**:

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
> Cuando obtenga Hola nuevo URI, que es hello URI que se debe toocommunicate utilizado con servicios multimedia. 
> 
> 

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

