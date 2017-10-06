---
title: aaaGet iniciado con aplicaciones de Azure Mobile para aplicaciones de Xamarin.Android
description: "Siga este tutorial tooget iniciado con aplicaciones móviles de Azure para desarrollo de Xamarin para Android"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Creación de una aplicación Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo tooadd un back-end basado en la nube service tooa Xamarin.Android aplicación. Para obtener más información, consulte [¿Qué son las aplicaciones móviles?](app-service-mobile-value-prop.md)

Una captura de pantalla de la aplicación hello completado es menor que:

![][0]

Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones Xamarin.Android.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:

* Una cuenta de Azure activa. Si no tiene una cuenta, suscríbase a una versión de evaluación de Azure y desarrollar aplicaciones móviles gratuitas de too10. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio con Xamarin. Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) para obtener instrucciones.

## <a name="create-an-azure-mobile-app-backend"></a>Creación de un nuevo back-end de Azure Mobile App
Siga estos toocreate pasos un aplicación móvil de back-end.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil. A continuación, descargar un proyecto de servidor para un simple "lista de tareas" back-end y publicarlo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar el proyecto de servidor hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Descargue y ejecute la aplicación de hello Xamarin.Android
1. En **descargar y ejecutar el proyecto Xamarin.Android**, haga clic en hello **descargar** botón.

      Guardar el equipo local del tooyour de archivo comprimido proyectos hello y tome nota donde se guarda.
2. Hola presione **F5** clave proyecto de hello toobuild e iniciar la aplicación hello.
3. En la aplicación hello, escriba texto significativo, como *tutorial Hola completa* y, a continuación, haga clic en hello **agregar** botón.

    ![][10]

    Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola. Se devuelven los elementos almacenados en la tabla de hello back-end de aplicación móvil de Hola y los datos aparecen en la lista de Hola.

   > [!NOTE]
   > Puede revisar el código de hello que tiene acceso a su tooquery de back-end de la aplicación móvil e insertar datos, que se encuentra en hello archivo ToDoActivity.cs C#.
   >
   >

## <a name="next-steps"></a>Pasos siguientes
* [Agregar aplicación de sincronización sin conexión tooyour](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Agregar aplicación de autenticación tooyour](app-service-mobile-xamarin-android-get-started-users.md)
* [Agregar aplicación de Xamarin.Android de tooyour de notificaciones de inserción](app-service-mobile-xamarin-android-get-started-push.md)
* [Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
