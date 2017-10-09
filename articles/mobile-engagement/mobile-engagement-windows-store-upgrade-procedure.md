---
title: "aaaWindows procedimientos de actualización del SDK de aplicaciones Universal"
description: "Procedimientos de actualización del SDK de Windows Universal Apps para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Procedimientos de actualización del SDK de aplicaciones Windows Universal
Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK. Por ejemplo, si migra desde 0.10.1 too0.11.0 tiene toofirst siga Hola "de 0.9.0 too0.10.1" procedimiento, a continuación, Hola "de 0.10.1 too0.11.0" procedimiento.

## <a name="from-330-too340"></a>Desde 3.3.0 too3.4.0
### <a name="test-logs"></a>Registros de prueba
Registros de la consola producidos por hello SDK ahora pueden habilitada, deshabilitada o filtrado. toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Recursos
se ha mejorado la superposición de cobertura de Hola. Forma parte de recursos del paquete de NuGet de SDK de Hola.

Al actualizar toohello nueva versión de hello SDK puede elegir que si desea que tookeep los archivos existentes de hello superposición de carpeta de los recursos:

* Si superposición anterior Hola funciona para usted o va a integrar hello `WebView` elementos manualmente, a continuación, puede decidir tookeep los archivos existentes, seguirá funcionando. 
* Si desea que tooupdate toohello nueva superposición, Hola simplemente reemplazar todo `overlay` carpeta de sus recursos con hello nueva del paquete SDK de hello (aplicaciones UWP: después de la actualización de hello, puede obtener nueva carpeta de superposición Hola desde % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Utilizando la superposición de hello nueva sobrescribirá todas las personalizaciones realizadas en la versión anterior de Hola.
> 
> 

## <a name="from-320-too330"></a>De 3.2.0 too3.3.0
### <a name="resources"></a>Recursos
Este paso se refiere solo a los recursos personalizados. Si ha personalizado los recursos de hello proporcionados por hello SDK (html, imágenes, superposición) tiene toobackup ellos antes de actualizar y volver a aplicar la personalización en actualiza recursos.

## <a name="from-310-too320"></a>Desde 3.1.0 too3.2.0
### <a name="resources"></a>Recursos
Este paso se refiere solo a los recursos personalizados. Si ha personalizado los recursos de hello proporcionados por hello SDK (html, imágenes, superposición) tiene toobackup ellos antes de actualizar y volver a aplicar la personalización en actualiza recursos.

### <a name="webview-integration"></a>integración de vista web.
Algunos factores de forma de otro dispositivo de toomatch mejoras introducidas en esta versión. Asegúrese de que la integración de hello webview coincidan siguientes de hello:

En la página XAML ():

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

Y en el archivo .cs asociado:

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>Desde 2.0.0 too3.0.0
### <a name="resources"></a>Recursos
Este paso se refiere solo a los recursos personalizados. Si ha personalizado los recursos de hello proporcionados por hello SDK (html, imágenes, superposición) tiene toobackup ellos antes de actualizar y volver a aplicar la personalización en actualiza recursos.

## <a name="from-111-too200"></a>Desde 1.1.1 too2.0.0
Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain e interacción móvil no se Hola los mismos servicios y procedimiento Hola indicado a continuación sólo resalta cómo toomigrate Hola aplicación cliente. Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores
> 
> 

Si va a migrar desde una versión anterior, por favor, consulte hello Capptain sitio web toomigrate too1.1.1 en primer lugar, aplique Hola procedimiento

### <a name="nuget-package"></a>Paquete de NuGet
Reemplace **Capptain.WindowsPhone** por el paquete Nuget **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Aplicar Mobile Engagement
Hola SDK utiliza el término de hello `Engagement`. Necesita tooupdate su toomatch proyecto este cambio.

Debe toouninstall el paquete de nuget Capptain actual. Tenga en cuenta que se van a quitar todos los cambios de la carpeta recursos de Capptain. Si desea que tookeep esos archivos, a continuación, haga una copia de ellos.

Después de eso, instale el nuevo paquete de nuget de Microsoft Azure Engagement hello en el proyecto. Puede encontrarlo directamente en [sitio web de nuget] o aquí en el índice. Este reemplaza acción todos los archivos de recursos utilizados por la interacción y agrega Hola nueva contratación DLL tooyour referencias del proyecto.

Eliminando las referencias de Capptain DLL tienen tooclean las referencias del proyecto. Si no hace esto, versión de Hola de Capptain entrarán en conflicto y se producirán errores.

Si ha personalizado los recursos de Capptain, copie el contenido de los archivos antiguos y péguelos en los nuevos archivos de contratación Hola. Tenga en cuenta que los archivos xaml y cs tienen toobe actualizado.

Una vez completados estos pasos solo tiene tooreplace Capptain las referencias anteriores a por nuevas referencias de contratación Hola.

1. Todos los espacios de nombres de Capptain tienen toobe actualizado.
   
    Antes de la migración:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Después de la migración:
   
        using Microsoft.Azure.Engagement;
2. Todas las clases de Capptain que contengan "Capptain" deberían contener "Engagement".
   
    Antes de la migración:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Después de la migración:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. En el caso de los archivos xaml, también cambian el espacio de nombres y los atributos de Capptain.
   
    Antes de la migración:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Después de la migración:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Cambios de la página de superposición
   
   > [!IMPORTANT]
   > También cambia la superposición Su espacio de nombres nuevo es `Microsoft.Azure.Engagement.Overlay`. Tiene toobe que se usa en los archivos xaml y cs. Además `CapptainGrid` se denomina toobe `EngagementGrid`, `capptain_notification_content` y `capptain_announcement_content` se denominan `engagement_notification_content` y `engagement_announcement_content`.
   > 
   > 
   
    Para la superposición:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Se convierte en:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Para hello otros recursos como Capptain imágenes y archivos HTML, tenga en cuenta que también han tenido toouse cuyo nombre ha cambiado "Interacción".

### <a name="project-declaration"></a>Declaración del proyecto
En Package.appxmanifest `File Type Associations` se ha actualizado de:

* capptain\_alcanzar\_tooengagement contenido\_alcanzar\_contenido
* capptain\_registro\_archivo tooengagement\_registro\_archivo

### <a name="application-id--sdk-key"></a>Identificador de aplicación o clave SDK
Engagement usa una cadena de conexión. Toospecify no tiene un identificador de la aplicación y una clave SDK con Mobile Engagement, solo tendrá toospecify una cadena de conexión. Esta se puede configurar en el archivo EngagementConfiguration.

configuración de la interacción de Hola se puede establecer el `Resources\EngagementConfiguration.xml` archivo del proyecto.

Editar este archivo toospecify:

* La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.

Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.

### <a name="items-name-change"></a>Cambio de nombre de elementos
Todos los elementos con el nombre *capptain* han cambiado a *engagement*. De forma similar para *Capptain* demasiado*interacción*.

Ejemplos de elementos Capptain que se usan habitualmente:

* CapptainConfiguration ahora se llama EngagementConfiguration
* CapptainAgent ahora se llama EngagementAgent
* CapptainReach ahora se llama EngagementReach
* CapptainHttpConfig ahora se llama EngagementHttpConfig
* GetCapptainPageName ahora se llama GetEngagementPageName

Tenga en cuenta que el cambio de nombre también afecta a los métodos invalidados.

