---
title: "Autenticación basada en token (HTTP/2) para APNs en Azure Notification Hubs | Microsoft Docs"
description: "En este tema se explica cómo aprovechar la nueva autenticación de token para APNs."
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="b34a4-103">Autenticación basada en token (HTTP/2) para APNs</span><span class="sxs-lookup"><span data-stu-id="b34a4-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="b34a4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b34a4-104">Overview</span></span>
<span data-ttu-id="b34a4-105">En este artículo se detalla cómo usar el nuevo protocolo HTTP/2 de APNs con la autenticación basada en token.</span><span class="sxs-lookup"><span data-stu-id="b34a4-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="b34a4-106">Entre las ventajas principales de usar el nuevo protocolo destacan las siguientes:</span><span class="sxs-lookup"><span data-stu-id="b34a4-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="b34a4-107">La generación de tokens es relativamente fácil (comparada con los certificados).</span><span class="sxs-lookup"><span data-stu-id="b34a4-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="b34a4-108">Ya no hay fechas de expiración: es usted quien controla los tokens de autenticación y su revocación.</span><span class="sxs-lookup"><span data-stu-id="b34a4-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="b34a4-109">Ahora las cargas pueden ser de hasta 4 KB.</span><span class="sxs-lookup"><span data-stu-id="b34a4-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="b34a4-110">Los comentarios son sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="b34a4-110">Synchronous feedback</span></span>
-   <span data-ttu-id="b34a4-111">Está en el protocolo más reciente de Apple: los certificados siguen usando el protocolo binario, que está marcado como en desuso.</span><span class="sxs-lookup"><span data-stu-id="b34a4-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="b34a4-112">Para usar este mecanismo nuevo, basta con que realice dos pasos que le llevarán un par de minutos:</span><span class="sxs-lookup"><span data-stu-id="b34a4-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="b34a4-113">Obtenga la información necesaria en el portal de la cuenta de desarrollador de Apple.</span><span class="sxs-lookup"><span data-stu-id="b34a4-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="b34a4-114">Configure el centro de notificaciones con la nueva información.</span><span class="sxs-lookup"><span data-stu-id="b34a4-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="b34a4-115">Ahora, todos los Notification Hubs están configurados para usar el nuevo sistema de autenticación con APNs.</span><span class="sxs-lookup"><span data-stu-id="b34a4-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="b34a4-116">Tenga en cuenta que si antes usaba credenciales de certificado para APNs y ha realizado la migración:</span><span class="sxs-lookup"><span data-stu-id="b34a4-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="b34a4-117">las propiedades de token sobrescriben su certificado en nuestro sistema,</span><span class="sxs-lookup"><span data-stu-id="b34a4-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="b34a4-118">pero la aplicación sigue recibiendo notificaciones sin problemas.</span><span class="sxs-lookup"><span data-stu-id="b34a4-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="b34a4-119">Obtener información de autenticación de Apple</span><span class="sxs-lookup"><span data-stu-id="b34a4-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="b34a4-120">Para habilitar la autenticación basada en token, necesita las siguientes propiedades de la cuenta de desarrollador de Apple:</span><span class="sxs-lookup"><span data-stu-id="b34a4-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="b34a4-121">Identificador de clave</span><span class="sxs-lookup"><span data-stu-id="b34a4-121">Key Identifier</span></span>
<span data-ttu-id="b34a4-122">Puede obtener el identificador de clave en la página "Claves" de la cuenta de desarrollador de Apple.</span><span class="sxs-lookup"><span data-stu-id="b34a4-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="b34a4-123">Identificador y nombre de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b34a4-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="b34a4-124">El nombre de la aplicación está disponible a través de la página de identificadores de aplicaciones en la cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="b34a4-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="b34a4-125">El identificador de la aplicación está disponible a través de la página de detalles de la pertenencia en la cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="b34a4-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="b34a4-126">Token de autenticación</span><span class="sxs-lookup"><span data-stu-id="b34a4-126">Authentication token</span></span>
<span data-ttu-id="b34a4-127">Puede descargar el token de autenticación después de generar un token para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b34a4-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="b34a4-128">Para obtener más información sobre cómo generar este token, vea la [documentación para desarrolladores de Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="b34a4-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="b34a4-129">Configurar el centro de notificaciones para usar la autenticación basada en token</span><span class="sxs-lookup"><span data-stu-id="b34a4-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="b34a4-130">Configurar mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b34a4-130">Configure via the Azure portal</span></span>
<span data-ttu-id="b34a4-131">Para habilitar la autenticación basada en token en el portal, inicie sesión en Azure Portal y vaya al Centro de notificaciones > Servicios de notificación > Panel APNs.</span><span class="sxs-lookup"><span data-stu-id="b34a4-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="b34a4-132">Hay una nueva propiedad: *Modo de autenticación*.</span><span class="sxs-lookup"><span data-stu-id="b34a4-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="b34a4-133">La selección de tokens le permite actualizar el centro con todas las propiedades de token pertinentes.</span><span class="sxs-lookup"><span data-stu-id="b34a4-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="b34a4-134">Escriba las propiedades que ha recuperado de la cuenta de desarrollador de Apple.</span><span class="sxs-lookup"><span data-stu-id="b34a4-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="b34a4-135">Elija el modo de aplicación (producción o espacio aislado).</span><span class="sxs-lookup"><span data-stu-id="b34a4-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="b34a4-136">Haga clic en Guardar para actualizar las credenciales de APNs.</span><span class="sxs-lookup"><span data-stu-id="b34a4-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="b34a4-137">Configurar mediante la API de administración (REST)</span><span class="sxs-lookup"><span data-stu-id="b34a4-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="b34a4-138">Puede usar nuestras [API de administración](https://msdn.microsoft.com/library/azure/dn495827.aspx) para actualizar el centro de notificaciones de modo que use la autenticación basada en token.</span><span class="sxs-lookup"><span data-stu-id="b34a4-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="b34a4-139">Use uno de los puntos de conexión correspondientes, en función de si la aplicación que está configurando es una aplicación de espacio aislado o de producción (según se especifique en la cuenta de desarrollador de Apple):</span><span class="sxs-lookup"><span data-stu-id="b34a4-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="b34a4-140">Punto de conexión de espacio aislado: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="b34a4-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="b34a4-141">Punto de conexión de producción: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="b34a4-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b34a4-142">La autenticación basada en token requiere una versión de API de **04-2017 o posterior**.</span><span class="sxs-lookup"><span data-stu-id="b34a4-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="b34a4-143">A continuación se muestra un ejemplo de una solicitud PUT para actualizar un centro con autenticación basada en token:</span><span class="sxs-lookup"><span data-stu-id="b34a4-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="b34a4-144">Configurar mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="b34a4-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="b34a4-145">Puede configurar el centro para que use la autenticación basada en token mediante nuestro [SDK de cliente más reciente](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="b34a4-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="b34a4-146">A continuación se muestra un ejemplo de código que ilustra el uso correcto:</span><span class="sxs-lookup"><span data-stu-id="b34a4-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="b34a4-147">Volver a usar la autenticación basada en certificados</span><span class="sxs-lookup"><span data-stu-id="b34a4-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="b34a4-148">Puede volver a usar en cualquier momento la autenticación basada en certificados. Para ello, use cualquiera de los métodos anteriores y pase las propiedades del certificado en lugar de las propiedades del token.</span><span class="sxs-lookup"><span data-stu-id="b34a4-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="b34a4-149">Esta acción sobrescribe las credenciales almacenadas previamente.</span><span class="sxs-lookup"><span data-stu-id="b34a4-149">That action overwrites the previously stored credentials.</span></span>
