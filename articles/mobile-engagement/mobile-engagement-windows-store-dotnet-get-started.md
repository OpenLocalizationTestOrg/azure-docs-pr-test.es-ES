---
title: aaaGet a trabajar con Windows Universal aplicaciones de Azure Mobile Engagement
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción y de análisis para aplicaciones universales de Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Introducción a Azure Mobile Engagement para aplicaciones universales de Windows
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción a los usuarios toosegmented de notificaciones de una aplicación Universal de Windows.
Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement. Creará una aplicación Windows Universal vacía que recopila datos básicos de uso de aplicaciones y recibe notificaciones push mediante el Servicio de notificaciones de Windows (WNS).

> [!NOTE]
> servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible. Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Configuración de Mobile Engagement para su aplicación universal de Windows
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción. Encontrará documentación de integración completa de Hola Hola [integración con el SDK de Mobile Engagement Windows Universal](mobile-engagement-windows-store-sdk-overview.md).

Crear una aplicación básica con la integración de Visual Studio toodemonstrate Hola.

### <a name="create-a-windows-universal-app-project"></a>Creación de un proyecto de aplicación universal de Windows
Hello siguientes pasos supone Hola uso de Visual Studio 2015 aunque Hola pasos son similares en versiones anteriores de Visual Studio.

1. Inicie Visual Studio y en hello **inicio** pantalla, seleccione **nuevo proyecto**.
2. En el menú emergente de hello, seleccione **Windows** -> **Universal** -> **aplicación vacía (Windows Universal)**. Rellene la aplicación hello **nombre** y **nombre de la solución**y, a continuación, haga clic en **Aceptar**.

    ![][1]

Ahora ha creado un proyecto de aplicación Universal de Windows en la que a continuación se integran hello Azure Mobile Engagement SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar el backend de interacción de tooMobile de aplicación
1. Instalar hello [MicrosoftAzure.MobileEngagement] paquete de Nuget en el proyecto. Si tiene como destino plataformas Windows y Windows Phone, deberá toodo esto para ambos proyectos. Para Windows 8.x y Windows Phone 8.1, Hola mismos Nuget paquete lugares Hola correcto específico de la plataforma binarios en cada proyecto.
2. Abra **Package.appxmanifest** y asegúrese de que ese Hola después capacidad agregada no existe:

        Internet (Client)

    ![][2]
3. Ahora, copie la cadena de conexión de Hola que copió anteriormente para la aplicación de interacción móvil y péguelo en hello `Resources\EngagementConfiguration.xml` archivo entre hello `<connectionString>` y `</connectionString>` etiquetas:

    ![][3]

    > [!TIP]
    > Si su aplicación va a tener como destino las plataformas Windows y Windows Phone, aun así se deben crear dos aplicaciones Mobile Engagement, una para cada plataforma compatible. Existencia de dos aplicaciones garantiza que se puede crear segmentación correcta de audiencia de Hola y puede enviar notificaciones de destino de forma adecuada para cada plataforma.

    > [!IMPORTANT]
    > NuGet no copia automáticamente los recursos SDK de hello en la aplicación de UWP de Windows 10. Tenerla toodo manualmente siguiendo los pasos de Hola que mostrarán (readme.txt) cuando se instala el paquete de Nuget Hola.  

1. Hola `App.xaml.cs` archivo:

    a. Agregar hello `using` instrucción:

            using Microsoft.Azure.Engagement;

    b. Agregue un método que inicialice Hola interacción:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Inicializar Hola SDK en hello **OnLaunched** método:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Inserte el siguiente de Hola Hola **OnActivated** método y agregue el método hello si todavía no está presente:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Habilitación de la supervisión en tiempo real
toostart enviando los datos y garantizar que los usuarios de hello están activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).

1. Hola **MainPage.xaml.cs**, agregue los siguientes hello `using` instrucción:

    using Microsoft.Azure.Engagement.Overlay;
2. Cambiar la clase base hello de **MainPage** de **página** demasiado**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. Hola `MainPage.xaml` archivo:

    a. Agregue las declaraciones de espacios de nombres tooyour:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Reemplace hello **página** en nombre de etiqueta XML de hello con **interacción: EngagementPageOverlay**

> [!IMPORTANT]
> Si la página invalida hello `OnNavigatedTo` método, ser seguro toocall `base.OnNavigatedTo(e)`. En caso contrario, no se notifica la actividad hello `EngagementPage` llamadas `StartActivity` dentro de su `OnNavigatedTo` método). Esto es especialmente importante en un proyecto de Windows Phone que no tiene plantilla predeterminada de hello un `OnNavigatedTo` método.
>
> Para **aplicaciones universales de Windows 10**, utilice método hello recomendada Hola "método recomendado: sobrecargar las clases de página" sección de [avanzada Reporting con SDK de interacción de aplicaciones Universal de Windows hello](mobile-engagement-windows-store-advanced-reporting.md) , en lugar de hello uno mencionadas anteriormente.

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación
Mobile Engagement le permite toointeract y llegar a los usuarios con las notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hello las secciones siguientes configure su aplicación tooreceive ellos.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Habilitar la tooreceive de la aplicación notificaciones de inserción de WNS
1. Hola `Package.appxmanifest` archivo Hola **aplicación** ficha **notificaciones**, establezca **capacidad de aviso:** demasiado**sí**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inicializar Hola REACH SDK
En `App.xaml.cs`, llame a **EngagementReach.Instance.Init(e);** en hello **InitEngagement** función justo después de la inicialización del agente de hello:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Ya está listo toosend una notificación del sistema. Ahora comprobaremos que ha llevado a cabo correctamente esta integración básica.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Conceder acceso tooMobile interacción toosend notificaciones
1. Abra el [Centro de desarrollo de Tienda Windows] en el explorador web, inicie sesión y cree una cuenta, si es necesario.
2. Haga clic en **panel** en hello parte superior derecha de las esquinas y, a continuación, haga clic en **crear una nueva aplicación** en el menú del panel izquierdo de Hola.

    ![][9]
3. Cree la aplicación mediante la reserva de su nombre.

    ![][10]
4. Una vez creada la aplicación hello, navegue demasiado**servicios -> notificaciones de inserción** desde el menú de la izquierda Hola.

    ![][11]
5. Hola sección notificaciones de inserción, haga clic en hello **sitio de los servicios de Live** vínculo.

    ![][12]
6. Navegue toohello sección de credenciales de inserción. Asegúrese de que se encuentre en hello **configuración de la aplicación** sección y, a continuación, copie su **SID del paquete** y **secreto de cliente**

    ![][13]
7. Navegue toohello **configuración** de portal de interacción móvil y haga clic en hello **inserción nativa** sección Hola izquierda. A continuación, haga clic en hello **editar** tooenter botón su **identificador de seguridad (SID) de paquete** y su **clave secreta** tal como se muestra:

    ![][6]
8. Por último, asegúrese de que la aplicación de Visual Studio se ha asociado con esta aplicación creada en la tienda de aplicaciones de Hola. Haga clic en **Asociar aplicación con la Tienda** en Visual Studio.

    ![][7]

## <a id="send"></a>Enviar una aplicación de tooyour de notificación
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Si está ejecutando la aplicación hello, verá una notificación en la aplicación. en caso contrario, si se cierra la aplicación hello, verá una notificación del sistema.
Si aparece una notificación en la aplicación pero no una notificación del sistema y está ejecutando la aplicación hello en modo de depuración en Visual Studio, vuelva a intentar **eventos de ciclo de vida -> Suspender** en tooensure de barra de herramientas de Hola se suspende esa aplicación Hola. Si hace clic en botón de inicio de hello mientras se depura la aplicación hello en Visual Studio, a continuación, no siempre suspendido y mientras ve notificación hello como en la aplicación, no se muestre como una notificación del sistema.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centro de desarrollo de Tienda Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
