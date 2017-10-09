---
title: "aaaToken (HTTP/2) la autenticación de APNS en centros de notificaciones de Azure | Documentos de Microsoft"
description: "Este tema explica cómo tooleverage Hola nueva autenticación de token para APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="1335c-103">Autenticación basada en token (HTTP/2) para APNs</span><span class="sxs-lookup"><span data-stu-id="1335c-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="1335c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1335c-104">Overview</span></span>
<span data-ttu-id="1335c-105">Este artículo detalla cómo toouse Hola nuevo APN HTTP/2 protocolo con el token de la autenticación basada en.</span><span class="sxs-lookup"><span data-stu-id="1335c-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="1335c-106">Hola ventajas principales de usar el nuevo protocolo de hello incluyen:</span><span class="sxs-lookup"><span data-stu-id="1335c-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="1335c-107">Generación de tokens es relativamente complicaciones libre (comparados toocertificates)</span><span class="sxs-lookup"><span data-stu-id="1335c-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="1335c-108">Ya no hay fechas de expiración: es usted quien controla los tokens de autenticación y su revocación.</span><span class="sxs-lookup"><span data-stu-id="1335c-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="1335c-109">Ahora pueden estar cargas too4 KB</span><span class="sxs-lookup"><span data-stu-id="1335c-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="1335c-110">Los comentarios son sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="1335c-110">Synchronous feedback</span></span>
-   <span data-ttu-id="1335c-111">Está en el protocolo más reciente de Apple: certificados seguir usan el protocolo binario de hello, que es marcadas como obsoletas</span><span class="sxs-lookup"><span data-stu-id="1335c-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="1335c-112">Para usar este mecanismo nuevo, basta con que realice dos pasos que le llevarán un par de minutos:</span><span class="sxs-lookup"><span data-stu-id="1335c-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="1335c-113">Obtener la información necesaria de Hola desde el portal de cuenta de desarrollador de Apple Hola</span><span class="sxs-lookup"><span data-stu-id="1335c-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="1335c-114">Configurar el centro de notificaciones con nueva información de Hola</span><span class="sxs-lookup"><span data-stu-id="1335c-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="1335c-115">Los centros de notificaciones es ahora todos los conjunto toouse Hola nueva autenticación sistema con APNS.</span><span class="sxs-lookup"><span data-stu-id="1335c-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="1335c-116">Tenga en cuenta que si antes usaba credenciales de certificado para APNs y ha realizado la migración:</span><span class="sxs-lookup"><span data-stu-id="1335c-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="1335c-117">propiedades de símbolo (token) de Hello sobrescriben el certificado en el sistema</span><span class="sxs-lookup"><span data-stu-id="1335c-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="1335c-118">pero la aplicación continúa tooreceive notificaciones sin problemas.</span><span class="sxs-lookup"><span data-stu-id="1335c-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="1335c-119">Obtener información de autenticación de Apple</span><span class="sxs-lookup"><span data-stu-id="1335c-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="1335c-120">autenticación basada en token tooenable, necesita Hola siguientes propiedades de la cuenta de desarrollador de Apple:</span><span class="sxs-lookup"><span data-stu-id="1335c-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="1335c-121">Identificador de clave</span><span class="sxs-lookup"><span data-stu-id="1335c-121">Key Identifier</span></span>
<span data-ttu-id="1335c-122">identificador de clave de Hello puede obtenerse de la página de "Claves" hello en la cuenta de desarrollador de Apple</span><span class="sxs-lookup"><span data-stu-id="1335c-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="1335c-123">Identificador y nombre de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1335c-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="1335c-124">nombre de la aplicación Hello está disponible a través de la página de identificadores de aplicación Hola Hola cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="1335c-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="1335c-125">identificador de la aplicación Hello está disponible a través de la página de detalles de pertenencia de Hola Hola cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="1335c-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="1335c-126">Token de autenticación</span><span class="sxs-lookup"><span data-stu-id="1335c-126">Authentication token</span></span>
<span data-ttu-id="1335c-127">token de autenticación de Hola se puede descargar después de generar un token para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1335c-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="1335c-128">Para obtener más información sobre cómo toogenerate este símbolo (token), consulte demasiado[la documentación para desarrolladores de Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="1335c-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="1335c-129">Configurar la autenticación basada en autorización token de notificación concentrador toouse</span><span class="sxs-lookup"><span data-stu-id="1335c-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="1335c-130">Configurar a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1335c-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="1335c-131">símbolo (token) de tooenable en función de la autenticación en el portal de hello, inicio de sesión toohello portal de Azure y vaya tooyour centro de notificaciones > Servicios de notificación de > panel APNS.</span><span class="sxs-lookup"><span data-stu-id="1335c-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="1335c-132">Hay una nueva propiedad: *Modo de autenticación*.</span><span class="sxs-lookup"><span data-stu-id="1335c-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="1335c-133">Si selecciona el símbolo (token), podrá tooupdate el concentrador con todas las propiedades token pertinentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="1335c-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="1335c-134">Especifique las propiedades de hello que recupera de la cuenta de desarrollador de Apple</span><span class="sxs-lookup"><span data-stu-id="1335c-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="1335c-135">Elija el modo de aplicación (producción o espacio aislado).</span><span class="sxs-lookup"><span data-stu-id="1335c-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="1335c-136">Haga clic en Guardar tooupdate sus credenciales APNS.</span><span class="sxs-lookup"><span data-stu-id="1335c-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="1335c-137">Configurar mediante la API de administración (REST)</span><span class="sxs-lookup"><span data-stu-id="1335c-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="1335c-138">Puede usar nuestro [API de administración de](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate la autenticación basada en autorización token de notificación concentrador toouse.</span><span class="sxs-lookup"><span data-stu-id="1335c-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="1335c-139">Dependiendo de si la aplicación hello que está configurando es una aplicación de producción o de espacio aislado (especificada en la cuenta de desarrollador de Apple), utilice uno de los puntos de conexión correspondiente de hello:</span><span class="sxs-lookup"><span data-stu-id="1335c-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="1335c-140">Punto de conexión de espacio aislado: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="1335c-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="1335c-141">Punto de conexión de producción: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="1335c-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1335c-142">La autenticación basada en token requiere una versión de API de **04-2017 o posterior**.</span><span class="sxs-lookup"><span data-stu-id="1335c-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="1335c-143">Este es un ejemplo de un tooupdate de solicitud PUT un concentrador con autenticación basada en token:</span><span class="sxs-lookup"><span data-stu-id="1335c-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="1335c-144">Configurar a través de hello SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="1335c-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="1335c-145">Puede configurar la autenticación basada en tokens de toouse concentrador mediante nuestro [SDK más reciente del cliente](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="1335c-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="1335c-146">Este es un ejemplo de código que ilustra el uso correcto de hello:</span><span class="sxs-lookup"><span data-stu-id="1335c-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="1335c-147">Autenticación basada en certificados toousing reversión</span><span class="sxs-lookup"><span data-stu-id="1335c-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="1335c-148">Puede recuperar en cualquier autenticación basada en certificados toousing mediante cualquier certificado de Hola de método y pasar anterior en lugar de propiedades de símbolo (token) de Hola.</span><span class="sxs-lookup"><span data-stu-id="1335c-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="1335c-149">Que acción sobrescribe hello las credenciales almacenadas previamente.</span><span class="sxs-lookup"><span data-stu-id="1335c-149">That action overwrites hello previously stored credentials.</span></span>
