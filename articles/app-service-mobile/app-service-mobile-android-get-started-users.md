---
title: "autenticación de aaaAdd en Android con aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola característica de aplicaciones móviles de usuarios de tooauthenticate de servicio de aplicaciones de Azure de su aplicación Android a través de una serie de proveedores de identidades, como Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Agregar aplicación Android de autenticación tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Resumen
En este tutorial, Agregar proyecto de inicio rápido de autenticación toohello todolist en Android mediante un proveedor de identidades admitidos. Este tutorial se basa en hello [empezar a trabajar con aplicaciones móviles] tutorial, que debe completar primero.

## <a name="register"></a>Registro de la aplicación para la autenticación y configuración de Azure App Service
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello

La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación. Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola. En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo. Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija. Debe ser único tooyour aplicaciones móviles. redirección de hello tooenable en servidor hello:

1. Hola [portal de Azure], seleccione su servicio en la aplicación.

2. Haga clic en hello **autenticación / autorización** opción de menú.

3. Hola **permite redirigir direcciones URL externas de**, escriba `appname://easyauth.callback`.  Hola _appname_ de esta cadena es hello esquema de dirección URL para la aplicación móvil.  Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).  Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.

4. Haga clic en **Aceptar**.

5. Haga clic en **Guardar**.

## <a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* En Android Studio, abra el proyecto de Hola que completado con el tutorial de hello [empezar a trabajar con aplicaciones móviles]. De hello **ejecutar** menú, haga clic en **ejecutar aplicación**y compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.

     Esta excepción ocurre porque los intentos de aplicación Hola tooaccess Hola volver end que un usuario no autenticado, pero Hola *TodoItem* tabla ahora requiere autenticación.

A continuación, actualizar los usuarios tooauthenticate de aplicación Hola antes de solicitar recursos de hello que terminar de aplicaciones móviles de nuevo. 

## <a name="add-authentication-toohello-app"></a>Agregar aplicación de autenticación toohello
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Almacenar en caché los tokens de autenticación de cliente hello
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Pasos siguientes
Completado este tutorial de la autenticación básica, considere la posibilidad de continuar en tooone de hello tutoriales:

* [Agregar aplicación de Android de tooyour de notificaciones de inserción](app-service-mobile-android-get-started-push.md).
  Obtenga información acerca de cómo tooconfigure realizar copias de las aplicaciones móviles finalizar notificaciones de inserción de toosend de bases de datos centrales de notificación de Azure de toouse.
* [Habilitación de la sincronización sin conexión para la aplicación móvil de Android](app-service-mobile-android-get-started-offline-data.md)
  Obtenga información acerca de cómo tooadd sin conexión son compatibles con tooyour aplicación mediante el uso de un back-end de aplicaciones móviles. La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[empezar a trabajar con aplicaciones móviles]: app-service-mobile-android-get-started.md
