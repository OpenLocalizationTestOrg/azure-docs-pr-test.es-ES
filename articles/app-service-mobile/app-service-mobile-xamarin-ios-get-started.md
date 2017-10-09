---
title: "aaaGet a trabajar con aplicaciones móviles de Azure aplicación de servicio para las aplicaciones de Xamarin.iOS | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de aplicaciones móviles para el desarrollo de Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Creación de una aplicación Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo tooadd un back-end basado en la nube service aplicación móvil de tooa Xamarin.iOS mediante el uso de un aplicación móvil Azure de back-end.  Creará tanto un back-end de aplicación móvil nuevo como una aplicación Xamarin.iOS simple de la *lista de tareas pendientes* que almacene los datos de la aplicación en Azure.

Completar este tutorial es un requisito previo para todos los otros tutoriales de Xamarin.iOS sobre cómo usar la característica de aplicaciones móviles de hello en el servicio de aplicación de Azure.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:

* Una cuenta de Azure activa. Si no tiene una cuenta, registrarse para obtener una evaluación de Azure y desarrollar aplicaciones móviles gratuitas too10 que puede seguir usando incluso después de la prueba finaliza. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio con Xamarin. Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) para obtener instrucciones.
* Un equipo Mac con Xcode v7.0 o versiones posteriores y Xamarin Studio Community instalados. Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) y [Configuración, instalación y comprobaciones para usuarios de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Creación de un nuevo back-end de Azure Mobile App
Siga estos toocreate pasos un aplicación móvil de back-end.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Configurar el proyecto de servidor hello
Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil. A continuación, descargar un proyecto de servidor para un simple "lista de tareas" back-end y publicarlo tooAzure.

Siga Hola siguiendo los pasos tooconfigure Hola servidor proyecto toouse cualquier hello Node.js o .NET back-end.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Descargue y ejecute la aplicación de hello Xamarin.iOS
1. Abra hello [portal de Azure] en una ventana del explorador.
2. En la hoja de configuración de Hola para su aplicación móvil, haga clic en **Introducción** > **Xamarin.iOS**. En el paso 3, haga clic en **Crear una nueva aplicación** , en caso de que no esté seleccionado.  A continuación haga clic en hello **descargar** botón.

      Se descarga una aplicación cliente que se conecta back-end de tooyour móvil. Guarde el archivo de proyecto comprimida de hello en el equipo local y tome nota donde se guarda.
3. Extraer el proyecto de Hola que ha descargado y, a continuación, ábralo en Xamarin Studio (o Visual Studio).

    ![][9]

    ![][8]
4. Presione proyecto Hola de hello F5 toobuild clave e iniciar aplicación hello en el emulador de iPhone Hola.
5. En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*y, a continuación, haga clic en hello  **+**  botón.

    ![][10]

    Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola. Se devuelven los elementos almacenados en la tabla de hello back-end de aplicación móvil de Hola y los datos se muestran en la lista de Hola.

> [!NOTE]
> Puede revisar el código de hello que tiene acceso a su tooquery de back-end de la aplicación móvil e insertar datos en hello archivo QSTodoService.cs C#.
>
>

## <a name="next-steps"></a>Pasos siguientes
* [Agregar aplicación de sincronización sin conexión tooyour](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Agregar aplicación de autenticación tooyour](app-service-mobile-xamarin-ios-get-started-users.md)
* [Agregar aplicación de Xamarin.Android de tooyour de notificaciones de inserción](app-service-mobile-xamarin-ios-get-started-push.md)
* [Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portal de Azure]: https://portal.azure.com/
