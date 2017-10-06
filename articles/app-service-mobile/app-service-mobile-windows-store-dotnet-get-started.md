---
title: "aaaCreate una plataforma Universal de Windows (UWP) que se usa en aplicaciones móviles | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de back-ends de aplicaciones móviles Azure para desarrollo de aplicaciones de plataforma Universal de Windows (UWP) en C#, Visual Basic o JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Creación de una aplicación para Windows
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo tooadd un back-end basado en la nube service tooa aplicación de plataforma Universal de Windows (UWP). Para obtener más información, consulte [¿Qué son las aplicaciones móviles?](app-service-mobile-value-prop.md) son las siguientes Hola capturas de pantalla de la aplicación hello completado:

![Aplicación de escritorio completada](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
Ejecutándose en un equipo de escritorio

![Aplicación de teléfono completada](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
Ejecutándose en un teléfono

Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones para UWP.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una cuenta, puede registrarse para obtener una evaluación de Azure y desarrollar aplicaciones móviles gratuitas too10 que puede seguir usando incluso después de la prueba finaliza. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio Community 2015] o versión posterior.

## <a name="create-a-new-azure-mobile-app-backend"></a>Creación de un nuevo back-end de Aplicaciones móviles de Azure
Siga estos toocreate pasos aplicación móvil back-end.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil. A continuación, se descargará un proyecto de servidor para un simple "lista de tareas" back-end y publicarlo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar el proyecto de servidor hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Descargue y ejecute el proyecto de cliente de Hola
Una vez haya configurado el aplicación móvil de back-end, puede crear una nueva aplicación de cliente o modificar una existente tooAzure tooconnect de aplicación. En esta sección, descargar un proyecto de plantilla de aplicación UWP que está personalizado tooconnect tooyour aplicación móvil back-end.

1. En hello **inicio rápido** hoja para su aplicación móvil de back-end, haga clic en **crear una nueva aplicación** > **descargar**, a continuación, extraer los archivos de proyecto de hello comprimido tooyour equipo local.

    ![Descargar el proyecto de inicio rápido de Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Opcional) Agregar toohello de proyecto de aplicación UWP Hola misma solución como proyecto de servidor de Hola. Esto facilita toodebug y prueba ambos Hola back-end de aplicación y hello en Hola la misma solución de Visual Studio, si elige toodo lo. tooadd una solución de toohello del proyecto de aplicación UWP, debe utilizar Visual Studio 2015 o una versión posterior.
3. Con la aplicación UWP hello como proyecto de inicio de hello, presione Hola F5 clave toodeploy y aplicación hello de ejecución.
4. En la aplicación hello, escriba texto significativo, como *tutorial Hola completa*, Hola **insertar un TodoItem** cuadro de texto y, a continuación, haga clic en **guardar**.

    ![Inicio rápido de Windows completo - Escritorio](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Esto envía un POST solicitud toohello nueva aplicación móvil back-end que se hospeda en Azure.
5. (Opcional) Detener aplicación hello y reiniciarlo en un dispositivo diferente o un emulador de dispositivos móvil.

    ![Inicio rápido de Windows completo - Teléfono](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Tenga en cuenta que guardó en el paso anterior de hello carga los datos de Azure después de hello aplicación UWP se inicia.

## <a name="next-steps"></a>Pasos siguientes
* [Agregar aplicación de autenticación tooyour](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.
* [Agregar aplicación de tooyour de notificaciones de inserción](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de toosend de aplicación móvil back-end toouse centros de notificaciones de Azure.
* [Habilitación de la sincronización sin conexión para su aplicación](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end. Sincronización sin conexión permite a los usuarios finales toointeract con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
