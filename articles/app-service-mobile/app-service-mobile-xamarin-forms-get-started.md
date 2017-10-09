---
title: "aaaGet a trabajar con aplicaciones móviles mediante el uso de Xamarin.Forms"
description: "Siga este tutorial toostart con aplicaciones móviles para el desarrollo de Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Creación de una aplicación Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo tooadd una aplicación móvil de servicio de back-end basado en la nube tooa Xamarin.Forms mediante el uso de Hola característica de aplicaciones móviles de servicio de aplicaciones de Azure como back-end de Hola. Va a crear tanto un back-end de Mobile Apps nuevo como una aplicación Xamarin.Forms simple de la lista de tareas pendientes que almacene los datos de la aplicación en Azure.

Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones Xamarin.Forms.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una cuenta, puede registrarse para obtener una evaluación de Azure y desarrollar aplicaciones móviles gratuitas too10 que puede seguir usando incluso después de la prueba finaliza. Para más información, consulte [Obtener una evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio con Xamarin. Para obtener información, vea hello [establecer una copia de seguridad e instale Visual Studio y Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) página.

* Un equipo Mac con Xcode v7.0 o versiones posteriores y Xamarin Studio Community instalados. Para más información, consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) de Visual Studio y Xamarin, y [Configuración, instalación y comprobaciones para usuarios de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Creación de un back-end de Mobile Apps

toocreate finalizar volver un nuevas aplicaciones móviles, Hola siguientes:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Ya ha configurado un back-end de Mobile Apps que puede usar con las aplicaciones cliente móviles. A continuación, descargar un proyecto de servidor para un tarea simple lista back-end y, a continuación, publicarlo tooAzure.

## <a name="configure-hello-server-project"></a>Configurar el proyecto de servidor hello

toouse del proyecto de servidor de tooconfigure Hola Hola Node.js o .NET back-end, Hola siguientes:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Descargue y ejecute la solución de Xamarin.Forms Hola

Puede descargar la solución de hello en cualquiera de estas dos maneras. Descargar tooa Mac y abrirlo en Xamarin Studio, o descargar tooa equipo con Windows y ábralo en Visual Studio mediante el uso de un Mac conectado en red para la creación de la aplicación de iOS de hello. Para más información, consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) de Visual Studio y Xamarin.

En un equipo Mac o Windows, Hola siguientes:

1. Vaya toohello [portal de Azure].

2. En hello **configuración** hoja para su aplicación móvil, en **Mobile**, seleccione **Introducción** > **Xamarin.Forms**. En el **paso 3**, seleccione **Crear aplicación** y, después, seleccione **Descargar**.

   Esta acción descarga un proyecto que contenga una aplicación cliente que está conectado tooyour aplicaciones móviles. Guardar el equipo local del tooyour de archivo comprimido proyectos hello y tome nota donde se guarda.

3. Extraer el proyecto de Hola que ha descargado y, a continuación, ábralo en Xamarin Studio (Mac) o Visual Studio (Windows).

   ![Proyecto extraído en Xamarin Studio][9]

   ![Proyecto extraído en Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Opcional) Ejecute el proyecto de iOS de Hola
En esta sección, se ejecuta el proyecto de iOS de Xamarin de Hola para dispositivos iOS. Puede omitir esta sección si no está trabajando con dispositivos iOS.

#### <a name="in-xamarin-studio"></a>En Xamarin Studio
1. Haga clic en proyecto de iOS de hello y, a continuación, seleccione **establecer como proyecto de inicio**.

2. En hello **ejecutar** menú, seleccione **Iniciar depuración** toobuild Hola proyecto e iniciar aplicación hello en el emulador de iPhone Hola.

#### <a name="in-visual-studio"></a>En Visual Studio
1. Haga clic en proyecto de iOS de hello y, a continuación, seleccione **establecer como proyecto de inicio**.

2. En hello **generar** menú, seleccione **Configuration Manager**.

3. Hola **Configuration Manager** cuadro de diálogo, seleccione hello **generar** y **implementar** proyecto de iOS de toohello siguiente de casillas de verificación.

4. toobuild Hola proyecto e iniciar aplicación hello en emulador de iPhone de hello, seleccione hello **F5** clave.

   > [!NOTE]
   > Si tiene problemas para crear el proyecto de hello, ejecute hello NuGet paquete manager y actualización toohello última versión de los paquetes de soporte técnico de hello Xamarin. Proyectos de inicio rápido podrían ser lenta tooupdate toohello últimas versiones.    
   >
   >

5. En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*, y, a continuación, seleccione Hola signo (**+**).

    ![][10]

    Esta acción envía un toohello de solicitud de post que nuevas aplicaciones de Mobile back-end que se hospeda en Azure. Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola. Elementos que se almacenan en la tabla de Hola se devuelven por hello aplicaciones móviles volver finalizar y Hola datos se muestran en la lista de Hola.

    > [!NOTE]
    > Puede encontrar código de hello que tiene acceso a su aplicaciones móviles de back-end en hello TodoItemManager.cs C# archivo de proyecto de biblioteca de clases portables hello de la solución.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Opcional) Ejecute el proyecto de Android Hola
En esta sección, se ejecuta el proyecto de droid de Xamarin de Hola para Android. Puede omitir esta sección si no está trabajando con dispositivos Android.

#### <a name="in-xamarin-studio"></a>En Xamarin Studio

1. Haga clic en proyecto de Android de hello y, a continuación, seleccione **establecer como proyecto de inicio**.

2. toobuild Hola proyecto e iniciar aplicación hello en un emulador de Android en hello **ejecutar** menú, seleccione **Iniciar depuración**.

#### <a name="in-visual-studio"></a>En Visual Studio

1. Haga clic en proyecto de Android (Droid) de hello y, a continuación, seleccione **establecer como proyecto de inicio**.

2. En hello **generar** menú, seleccione **Configuration Manager**.

3. Hola **Configuration Manager** cuadro de diálogo, seleccione hello **generar** y **implementar** casillas de verificación siguiente toohello proyecto Android.

4. toobuild Hola proyecto e iniciar aplicación hello en un emulador de Android, seleccione hello **F5** clave.

   > [!NOTE]
   > Si tiene problemas para crear el proyecto de hello, ejecute hello NuGet paquete manager y actualización toohello última versión de los paquetes de soporte técnico de hello Xamarin. Proyectos de inicio rápido podrían ser lenta tooupdate toohello últimas versiones.    
   >
   >

5. En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*, y, a continuación, seleccione Hola signo (**+**).

    ![][11]
    
    Esta acción envía un toohello de solicitud de post que nuevas aplicaciones de Mobile back-end que se hospeda en Azure. Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola. Elementos que se almacenan en la tabla de Hola se devuelven por hello aplicaciones móviles volver finalizar y Hola datos se muestran en la lista de Hola.
    
    > [!NOTE]
    > Puede encontrar código de hello que tiene acceso a su aplicaciones móviles de back-end en hello TodoItemManager.cs C# archivo de proyecto de biblioteca de clases portables hello de la solución.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Opcional) Ejecute el proyecto de Windows hello

En esta sección, ejecute hello proyecto Xamarin WinApp para dispositivos de Windows. Puede omitir esta sección si no está trabajando con dispositivos Windows.

#### <a name="in-visual-studio"></a>En Visual Studio

1. Haga clic en cualquiera de los proyectos de Windows hello y, a continuación, seleccione **establecer como proyecto de inicio**.

2. En hello **generar** menú, seleccione **Configuration Manager**.

3. Hola **Configuration Manager** cuadro de diálogo, seleccione hello **generar** y **implementar** casillas de verificación siguiente toohello proyecto de Windows que eligió.

4. toobuild Hola proyecto e iniciar aplicación hello en un emulador de Windows, seleccione hello **F5** clave.

   > [!NOTE]
   > Si tiene problemas para crear el proyecto de hello, ejecute hello NuGet paquete manager y actualización toohello última versión de los paquetes de soporte técnico de hello Xamarin. Proyectos de inicio rápido podrían ser lenta tooupdate toohello últimas versiones.    
   >
   >

5. En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*, y, a continuación, seleccione Hola signo (**+**).

    Esta acción envía un toohello de solicitud de post que nuevas aplicaciones de Mobile back-end que se hospeda en Azure. Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola. Elementos que se almacenan en la tabla de Hola se devuelven por hello aplicaciones móviles volver finalizar y Hola datos se muestran en la lista de Hola.
    
    ![][12]
    
    > [!NOTE]
    > Puede encontrar código de hello que tiene acceso a su aplicaciones móviles de back-end en hello TodoItemManager.cs C# archivo de proyecto de biblioteca de clases portables hello de la solución.
    >
    >

## <a name="next-steps"></a>Pasos siguientes

* [Agregar aplicación de autenticación tooyour](app-service-mobile-xamarin-forms-get-started-users.md)  
  Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.

* [Agregar aplicación de tooyour de notificaciones de inserción](app-service-mobile-xamarin-forms-get-started-push.md)  
  Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de aplicaciones móviles back-end toouse centros de notificaciones de Azure toosend Hola.

* [Activación de la sincronización sin conexión para la aplicación de Windows](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Obtenga información acerca de cómo tooadd compatibilidad sin conexión para la aplicación mediante el uso de aplicaciones móviles de un back-end. Con la sincronización sin conexión, podrá ver, agregar o modificar los datos en la aplicación móvil, incluso cuando no hay ninguna conexión de red.

* [Usar el cliente administrado de Hola para aplicaciones móviles](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Obtenga información acerca de cómo toowork con hello administra SDK del cliente de la aplicación de Xamarin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portal de Azure]: https://portal.azure.com/
