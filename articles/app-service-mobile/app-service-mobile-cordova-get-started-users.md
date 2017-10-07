---
title: "autenticación de aaaAdd en Apache Cordova con aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse aplicaciones móviles en el servicio de aplicación de Azure tooauthenticate a los usuarios de aplicaciones de Apache Cordova a través de una serie de proveedores de identidades, como Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Agregar aplicación de Apache Cordova de autenticación tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Resumen
En este tutorial, agregará un proyecto de inicio rápido de autenticación toohello todolist en Apache Cordova mediante un proveedor de identidades admitidos. Este tutorial se basa en hello [empezar a trabajar con aplicaciones móviles] tutorial, que debe completar primero.

## <a name="register"></a>Registrar la aplicación para la autenticación y configurar Hola servicio de aplicaciones
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Visualización de un vídeo donde se muestren pasos similares](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Ahora, puede comprobar que tooyour el acceso anónimo, back-end se ha deshabilitado. En Visual Studio:

* Proyecto abierto Hola que creó al completar el tutorial de hello [empezar a trabajar con aplicaciones móviles].
* Ejecutar la aplicación en hello **emulador de Google Android**.
* Compruebe que se muestra un error inesperado de la conexión una vez iniciada la aplicación hello.

A continuación, actualizar los usuarios tooauthenticate de aplicación Hola antes de solicitar recursos de aplicación móvil de hello back-end.

## <a name="add-authentication"></a>Agregar aplicación de autenticación toohello
1. Abra el proyecto en **Visual Studio**, a continuación, abra hello `www/index.html` archivo para su edición.
2. Busque hello `Content-Security-Policy` meta etiqueta en la sección principal de Hola.  Agregue hello OAuth host toohello lista de orígenes permitidos.

   | Proveedor | Nombre del proveedor del SDK | Host de OAuth |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    A continuación se muestra un ejemplo de Content-Security-Policy (implementado para Azure Active Directory):

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Reemplace `https://login.microsoftonline.com` a host OAuth Hola Hola tabla anterior.  Para obtener más información acerca de la etiqueta meta de directiva de seguridad de contenido de hello, vea hello [documentación de directiva de seguridad de contenido].

    Algunos proveedores de autenticación no requieren cambios en Content-Security-Policy cuando se usa en dispositivos móviles adecuados.  Por ejemplo, no se requiere ningún cambio en Content-Security-Policy cuando se usa la autenticación de Google en un dispositivo Android.

3. Abra hello `www/js/index.js` para su edición de archivos, busque hello `onDeviceReady()` método, y en la creación de cliente de hello código agregar Hola siguiente código:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Este código reemplaza el código de existente de Hola que crea la referencia de tabla de Hola y actualiza la interfaz de usuario de Hola.

    método login() de Hello inicia la autenticación con el proveedor de Hola. método de Hello login() es una función de async que devuelve una promesa de JavaScript.  resto de Hola de inicialización de Hola se coloca dentro de respuesta de compromiso de Hola para que no se ejecuta hasta que se complete el método de hello login().

4. En el código de hello que acaba de agregar, reemplazar `SDK_Provider_Name` con el nombre de Hola de su proveedor de inicio de sesión. Por ejemplo, para Azure Active Directory, use `client.login('aad')`.
5. Ejecute el proyecto.  Al proyecto de hello ha terminado de inicializar, la aplicación muestra la página de inicio de sesión de OAuth de Hola para hello elegido el proveedor de autenticación.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información [sobre la autenticación] con el Servicio de aplicaciones de Azure.
* Continuar con tutorial Hola agregando [notificaciones Push] tooyour aplicaciones de Apache Cordova.

Obtenga información acerca de cómo toouse Hola SDK.

* [SDK de Apache Cordova]
* [SDK de servidor ASP.NET]
* [SDK de servidor Node.js]

<!-- URLs. -->
[Introducción a Aplicaciones móviles]: app-service-mobile-cordova-get-started.md
[documentación de Content-Security-Policy]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[notificaciones push]: app-service-mobile-cordova-get-started-push.md
[sobre la autenticación]: app-service-mobile-auth.md
[SDK de Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK de servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK de servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
