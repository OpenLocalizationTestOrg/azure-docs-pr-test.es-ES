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
# <a name="token-based-http2-authentication-for-apns"></a>Autenticación basada en token (HTTP/2) para APNs
## <a name="overview"></a>Información general
Este artículo detalla cómo toouse Hola nuevo APN HTTP/2 protocolo con el token de la autenticación basada en.

Hola ventajas principales de usar el nuevo protocolo de hello incluyen:
-   Generación de tokens es relativamente complicaciones libre (comparados toocertificates)
-   Ya no hay fechas de expiración: es usted quien controla los tokens de autenticación y su revocación.
-   Ahora pueden estar cargas too4 KB
- Los comentarios son sincrónicos.
-   Está en el protocolo más reciente de Apple: certificados seguir usan el protocolo binario de hello, que es marcadas como obsoletas

Para usar este mecanismo nuevo, basta con que realice dos pasos que le llevarán un par de minutos:
1.  Obtener la información necesaria de Hola desde el portal de cuenta de desarrollador de Apple Hola
2.  Configurar el centro de notificaciones con nueva información de Hola

Los centros de notificaciones es ahora todos los conjunto toouse Hola nueva autenticación sistema con APNS. 

Tenga en cuenta que si antes usaba credenciales de certificado para APNs y ha realizado la migración:
- propiedades de símbolo (token) de Hello sobrescriben el certificado en el sistema
- pero la aplicación continúa tooreceive notificaciones sin problemas.

## <a name="obtaining-authentication-information-from-apple"></a>Obtener información de autenticación de Apple
autenticación basada en token tooenable, necesita Hola siguientes propiedades de la cuenta de desarrollador de Apple:
### <a name="key-identifier"></a>Identificador de clave
identificador de clave de Hello puede obtenerse de la página de "Claves" hello en la cuenta de desarrollador de Apple

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Identificador y nombre de la aplicación
nombre de la aplicación Hello está disponible a través de la página de identificadores de aplicación Hola Hola cuenta de desarrollador. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

identificador de la aplicación Hello está disponible a través de la página de detalles de pertenencia de Hola Hola cuenta de desarrollador.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Token de autenticación
token de autenticación de Hola se puede descargar después de generar un token para la aplicación. Para obtener más información sobre cómo toogenerate este símbolo (token), consulte demasiado[la documentación para desarrolladores de Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Configurar la autenticación basada en autorización token de notificación concentrador toouse
### <a name="configure-via-hello-azure-portal"></a>Configurar a través de hello portal de Azure
símbolo (token) de tooenable en función de la autenticación en el portal de hello, inicio de sesión toohello portal de Azure y vaya tooyour centro de notificaciones > Servicios de notificación de > panel APNS. 

Hay una nueva propiedad: *Modo de autenticación*. Si selecciona el símbolo (token), podrá tooupdate el concentrador con todas las propiedades token pertinentes de Hola.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Especifique las propiedades de hello que recupera de la cuenta de desarrollador de Apple 
- Elija el modo de aplicación (producción o espacio aislado). 
- Haga clic en Guardar tooupdate sus credenciales APNS. 

### <a name="configure-via-management-api-rest"></a>Configurar mediante la API de administración (REST)

Puede usar nuestro [API de administración de](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate la autenticación basada en autorización token de notificación concentrador toouse.
Dependiendo de si la aplicación hello que está configurando es una aplicación de producción o de espacio aislado (especificada en la cuenta de desarrollador de Apple), utilice uno de los puntos de conexión correspondiente de hello:

- Punto de conexión de espacio aislado: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)
- Punto de conexión de producción: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> La autenticación basada en token requiere una versión de API de **04-2017 o posterior**.
> 
> 

Este es un ejemplo de un tooupdate de solicitud PUT un concentrador con autenticación basada en token:


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
        

### <a name="configure-via-hello-net-sdk"></a>Configurar a través de hello SDK para .NET
Puede configurar la autenticación basada en tokens de toouse concentrador mediante nuestro [SDK más reciente del cliente](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Este es un ejemplo de código que ilustra el uso correcto de hello:


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Autenticación basada en certificados toousing reversión
Puede recuperar en cualquier autenticación basada en certificados toousing mediante cualquier certificado de Hola de método y pasar anterior en lugar de propiedades de símbolo (token) de Hola. Que acción sobrescribe hello las credenciales almacenadas previamente.
