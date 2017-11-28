---
title: "aaaWindows integración de SDK de alcanzar de aplicaciones Universal"
description: "¿Cómo tooIntegrate Azure Mobile Engagement alcanzar con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="a314d-103">Integración del SDK de Cobertura de Windows Universal Apps</span><span class="sxs-lookup"><span data-stu-id="a314d-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="a314d-104">Debe seguir el procedimiento de integración de hello descrito en hello [integración del SDK de interacción Universal de Windows](mobile-engagement-windows-store-integrate-engagement.md) antes de seguir esta guía.</span><span class="sxs-lookup"><span data-stu-id="a314d-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="a314d-105">Incrustar Hola interacción Reach SDK en el proyecto Universal de Windows</span><span class="sxs-lookup"><span data-stu-id="a314d-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="a314d-106">No tiene nada tooadd.</span><span class="sxs-lookup"><span data-stu-id="a314d-106">You do not have anything tooadd.</span></span> <span data-ttu-id="a314d-107">`EngagementReach` y los recursos de ya están en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a314d-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="a314d-108">Puede personalizar imágenes ubicado en hello `Resources` carpeta del proyecto, especialmente icono de marca de hello (ese icono de interacción de toohello predeterminado).</span><span class="sxs-lookup"><span data-stu-id="a314d-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="a314d-109">En las aplicaciones universales también puede mover hello `Resources` carpeta en su tooshare de proyecto compartido su contenido entre aplicaciones, sino tendrá hello tookeep `Resources\EngagementConfiguration.xml` de archivos en su ubicación predeterminada tal cual depende de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="a314d-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="a314d-110">Habilitar el servicio de notificación de Windows hello</span><span class="sxs-lookup"><span data-stu-id="a314d-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="a314d-111">Solo Windows 8.x y Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="a314d-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="a314d-112">Hola de orden toouse **servicio de notificación de Windows** (denominadas WNS) en su `Package.appxmanifest` de archivos en `Application UI` haga clic en `All Image Assets` en cuadro de hello bot izquierdo.</span><span class="sxs-lookup"><span data-stu-id="a314d-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="a314d-113">En hello derecha del cuadro de hello en `Notifications`, cambiar `toast capable` de `(not set)` demasiado`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="a314d-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="a314d-114">Todas las plataformas</span><span class="sxs-lookup"><span data-stu-id="a314d-114">All platforms</span></span>
<span data-ttu-id="a314d-115">Debe toosynchronize su aplicación tooyour cuenta y toohello interacción plataforma de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a314d-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="a314d-116">Para ello necesita toocreate una cuenta o inicio de sesión [centro de desarrollo de windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="a314d-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="a314d-117">Una vez que cree una nueva aplicación y busque Hola SID y una clave secreta.</span><span class="sxs-lookup"><span data-stu-id="a314d-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="a314d-118">En el servidor front-end de la interacción de hello, ir en la configuración de aplicación en `native push` y pegue las credenciales.</span><span class="sxs-lookup"><span data-stu-id="a314d-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="a314d-119">Luego, haga clic con el botón secundario del mouse en el proyecto, seleccione `store` y `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="a314d-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="a314d-120">Aplicación de hello tooselect debe lo crear antes de toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="a314d-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="a314d-121">Inicializar Hola interacción Reach SDK</span><span class="sxs-lookup"><span data-stu-id="a314d-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="a314d-122">Modificar Hola `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="a314d-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="a314d-123">Inserte `EngagementReach.Instance.Init` justo después de `EngagementAgent.Instance.Init` en su método `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="a314d-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="a314d-124">Hola `EngagementReach.Instance.Init` se ejecuta en un subproceso dedicado.</span><span class="sxs-lookup"><span data-stu-id="a314d-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="a314d-125">No tiene toodo usted mismo.</span><span class="sxs-lookup"><span data-stu-id="a314d-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="a314d-126">Si está utilizando las notificaciones de inserción en otra parte de la aplicación, entonces tiene demasiado[compartir su canal de inserción](#push-channel-sharing) con interacción alcanzar.</span><span class="sxs-lookup"><span data-stu-id="a314d-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="a314d-127">Integración</span><span class="sxs-lookup"><span data-stu-id="a314d-127">Integration</span></span>
<span data-ttu-id="a314d-128">Interacción proporciona banners de la aplicación de dos maneras tooadd Hola alcance y vistas intersticiales para sondeos en la aplicación y anuncios: Hola superposición de integración y la integración de hello web vistas manuales.</span><span class="sxs-lookup"><span data-stu-id="a314d-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="a314d-129">No debería combinar ambos enfoque en hello sintonía.</span><span class="sxs-lookup"><span data-stu-id="a314d-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="a314d-130">elección de Hello entre integración dos Hola podía resumirse así:</span><span class="sxs-lookup"><span data-stu-id="a314d-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="a314d-131">Puede elegir la integración de superposición de hello si las páginas ya hereda de hello agente `EngagementPage`, es simplemente una cuestión de sustitución de `EngagementPage` por `EngagementPageOverlay` y `xmlns:engagement="using:Microsoft.Azure.Engagement"` por `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` en las páginas.</span><span class="sxs-lookup"><span data-stu-id="a314d-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="a314d-132">Puede elegir integración manual de hello web vistas si desea tooprecisely lugar Hola llegar a la interfaz de usuario dentro de las páginas o si no desea tooadd otro páginas de nivel tooyour de herencia.</span><span class="sxs-lookup"><span data-stu-id="a314d-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="a314d-133">Integración de superposición</span><span class="sxs-lookup"><span data-stu-id="a314d-133">Overlay integration</span></span>
<span data-ttu-id="a314d-134">superposición de interacción de Hello agrega dinámicamente elementos de interfaz de usuario de hello usan campañas toodisplay en la página.</span><span class="sxs-lookup"><span data-stu-id="a314d-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="a314d-135">Si la superposición de hello no se ajusta a su diseño debe considerar vistas de hello web integración manual en su lugar.</span><span class="sxs-lookup"><span data-stu-id="a314d-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="a314d-136">En el cambio de los archivos .xaml `EngagementPage` referencia demasiado`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="a314d-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="a314d-137">Agregue las declaraciones de espacios de nombres tooyour:</span><span class="sxs-lookup"><span data-stu-id="a314d-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="a314d-138">Reemplace `engagement:EngagementPage` por `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="a314d-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="a314d-139">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="a314d-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="a314d-140">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="a314d-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="a314d-141">Después, en el archivo. cs, etiquete la página en `EngagementPageOverlay` en lugar de `EngagementPage` e importe `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="a314d-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="a314d-142">Reemplace `EngagementPage` por `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="a314d-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="a314d-143">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="a314d-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="a314d-144">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="a314d-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="a314d-145">Agrega Hello superposición de interacción una `Grid` elemento encima de la página está formada por su diseño y Hola dos `WebView` elementos uno para hello banner y Hola otro uno para la vista intersticiales Hola.</span><span class="sxs-lookup"><span data-stu-id="a314d-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="a314d-146">Se pueden personalizar elementos de la superposición de hello directamente en hello `EngagementPageOverlay.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="a314d-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="a314d-147">Integración manual de vistas web</span><span class="sxs-lookup"><span data-stu-id="a314d-147">Web views manual integration</span></span>
<span data-ttu-id="a314d-148">Alcance buscan las páginas para hello dos `WebView` elementos responsables de mostrar pancarta hello y vista intersticiales Hola.</span><span class="sxs-lookup"><span data-stu-id="a314d-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="a314d-149">Hola solo lo tienes toodo es tooadd esos dos `WebView` elementos en alguna parte de las páginas, este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a314d-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="a314d-150">En este Hola ejemplo `WebView` elementos es toofit ajustado su contenedor que automáticamente volver a tamaños de ellos en el caso de cambio de tamaño de ventana o la rotación de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a314d-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="a314d-151">Es importante tookeep Hola misma nomenclatura `engagement_notification_content` y `engagement_announcement_content` para hello `WebView` elementos.</span><span class="sxs-lookup"><span data-stu-id="a314d-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="a314d-152">Reach los identifica por su nombre.</span><span class="sxs-lookup"><span data-stu-id="a314d-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="a314d-153">Controlar la inserción de datos (opcional)</span><span class="sxs-lookup"><span data-stu-id="a314d-153">Handle datapush (optional)</span></span>
<span data-ttu-id="a314d-154">Si desea que su inserciones de datos de aplicación toobe tooreceive capaz de alcance, deberá tooimplement dos eventos de hello EngagementReach clase:</span><span class="sxs-lookup"><span data-stu-id="a314d-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="a314d-155">En App.xaml.cs en el constructor de hello App() agregar:</span><span class="sxs-lookup"><span data-stu-id="a314d-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="a314d-156">Puede ver esa devolución de llamada de Hola de cada método devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="a314d-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="a314d-157">Interacción envía un back-end de tooits de comentarios después de enviar la inserción de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a314d-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="a314d-158">Si la devolución de llamada de hello devuelve false, Hola `exit` comentarios se estarán.</span><span class="sxs-lookup"><span data-stu-id="a314d-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="a314d-159">De lo contrario, será `action`.</span><span class="sxs-lookup"><span data-stu-id="a314d-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="a314d-160">Si no se establece ninguna devolución de llamada para los eventos de hello, Hola `drop` comentarios se devolverá tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="a314d-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="a314d-161">Interacción no es capaz de tooreceive opiniones de múltiplos para una inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="a314d-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="a314d-162">Si tiene previsto tooset varios controladores en un evento, tenga en cuenta que los comentarios de Hola corresponderá toohello penúltima enviado.</span><span class="sxs-lookup"><span data-stu-id="a314d-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="a314d-163">En este caso, se recomienda tooalways devuelve Hola mismo tooavoid valor tener comentarios confuso en hello front-end.</span><span class="sxs-lookup"><span data-stu-id="a314d-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="a314d-164">Personalizar la interfaz de usuario (opcional)</span><span class="sxs-lookup"><span data-stu-id="a314d-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="a314d-165">Primer paso</span><span class="sxs-lookup"><span data-stu-id="a314d-165">First step</span></span>
<span data-ttu-id="a314d-166">Le permitimos alcance de hello toocustomize interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a314d-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="a314d-167">toodo por lo tanto, tiene una subclase de hello toocreate `EngagementReachHandler` clase.</span><span class="sxs-lookup"><span data-stu-id="a314d-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="a314d-168">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="a314d-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="a314d-169">A continuación, establezca el contenido de Hola de hello `EngagementReach.Instance.Handler` campo con su objeto personalizado en su `App.xaml.cs` clase dentro de hello `App()` método.</span><span class="sxs-lookup"><span data-stu-id="a314d-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="a314d-170">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="a314d-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="a314d-171">De forma predeterminada, Engagement usa su propia implementación de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="a314d-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="a314d-172">No tienes toocreate el suyo propio, y si lo hace, no tiene toooverride cada método.</span><span class="sxs-lookup"><span data-stu-id="a314d-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="a314d-173">comportamiento predeterminado de Hello es objeto de base de tooselect Hola interacción.</span><span class="sxs-lookup"><span data-stu-id="a314d-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="a314d-174">Vista web</span><span class="sxs-lookup"><span data-stu-id="a314d-174">Web View</span></span>
<span data-ttu-id="a314d-175">De forma predeterminada, alcance usará recursos Hola incrustada de las notificaciones de hello DLL toodisplay hello y páginas.</span><span class="sxs-lookup"><span data-stu-id="a314d-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="a314d-176">tooprovide una completa de posibilidades de personalización solo se utiliza vista web.</span><span class="sxs-lookup"><span data-stu-id="a314d-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="a314d-177">Si desea toocustomize diseños, invalidar directamente los archivos de recursos de hello `EngagementAnnouncement.html` y `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="a314d-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="a314d-178">Todo el código, se precisa `<body></body>` toorun correctamente.</span><span class="sxs-lookup"><span data-stu-id="a314d-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="a314d-179">No obstante, puede agregar una etiqueta exterior `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="a314d-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="a314d-180">Sin embargo, puede decidir toouse sus propios recursos.</span><span class="sxs-lookup"><span data-stu-id="a314d-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="a314d-181">Puede invalidar `EngagementReachHandler` métodos en su toouse de interacción de subclase tootell los diseños, pero toman mecanismo de interacción de atención tooembedded hello:</span><span class="sxs-lookup"><span data-stu-id="a314d-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="a314d-182">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="a314d-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="a314d-183">De forma predeterminada, AnnouncementHTML es `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="a314d-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="a314d-184">Que representa el archivo html hello que diseñar Hola contenido de un mensaje de inserción (anuncio de texto, anoucement Web y anuncio de sondeo).</span><span class="sxs-lookup"><span data-stu-id="a314d-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="a314d-185">AnnouncementName es `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="a314d-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="a314d-186">Es nombre Hola Hola webview del diseño de en la página xaml.</span><span class="sxs-lookup"><span data-stu-id="a314d-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="a314d-187">NotfificationHTML es `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="a314d-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="a314d-188">Que representa el archivo html hello que diseñar Hola notificación de un mensaje de inserción.</span><span class="sxs-lookup"><span data-stu-id="a314d-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="a314d-189">NotfificationName es `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="a314d-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="a314d-190">Es nombre Hola Hola webview del diseño de en la página xaml.</span><span class="sxs-lookup"><span data-stu-id="a314d-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="a314d-191">Personalización</span><span class="sxs-lookup"><span data-stu-id="a314d-191">Customization</span></span>
<span data-ttu-id="a314d-192">Puede personalizar la vista web de notificación y anuncio como desee si quiere conservar el objeto de Engagement.</span><span class="sxs-lookup"><span data-stu-id="a314d-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="a314d-193">Tenga cuidado de que se describe webview objeto tres veces: hello primera vez en el archivo xaml, en segundo lugar de tiempo en el archivo .cs en método de "setwebview()" hello y en tercer lugar hora en el archivo html de hello.</span><span class="sxs-lookup"><span data-stu-id="a314d-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="a314d-194">En el xaml se describe el componente de webview de diseño gráfico actual Hola.</span><span class="sxs-lookup"><span data-stu-id="a314d-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="a314d-195">En el archivo .cs puede definir "setwebview()" en el que establecer dimensión Hola de hello dos webview (notificación, anuncio).</span><span class="sxs-lookup"><span data-stu-id="a314d-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="a314d-196">Es muy eficaz cuando está cambiando el tamaño de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a314d-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="a314d-197">En el archivo html de interacción de Hola se describir Hola webview contenido, diseño y Hola posiciones de elementos entre sí.</span><span class="sxs-lookup"><span data-stu-id="a314d-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="a314d-198">Iniciar el mensaje</span><span class="sxs-lookup"><span data-stu-id="a314d-198">Launch message</span></span>
<span data-ttu-id="a314d-199">Cuando un usuario hace clic en una notificación del sistema (una notificación del sistema), interacción inicia la aplicación hello, carga Hola contenido de hello envíen mensajes y mostrar página Hola campaña correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="a314d-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="a314d-200">Hay un retraso entre el inicio de Hola de pantalla de hello y aplicación Hola de página hello (según la velocidad de saludo de la red).</span><span class="sxs-lookup"><span data-stu-id="a314d-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="a314d-201">usuario de toohello tooindicate que algo se está cargando, debe proporcionar una información visual, como una barra de progreso o un indicador de progreso.</span><span class="sxs-lookup"><span data-stu-id="a314d-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="a314d-202">Engagement no puede controlar esto por sí solo, pero le ofrece algunos controladores para ello.</span><span class="sxs-lookup"><span data-stu-id="a314d-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="a314d-203">Agregar tooimplement Hola devolución de llamada, en App.xaml.cs "App() pública {}":</span><span class="sxs-lookup"><span data-stu-id="a314d-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="a314d-204">Puede establecer la devolución de llamada de hello en el método "App() pública {}" de la `App.xaml.cs` archivo, preferentemente antes de hello `EngagementReach.Instance.Init()` llamar.</span><span class="sxs-lookup"><span data-stu-id="a314d-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="a314d-205">Hola subprocesos de interfaz de usuario llama a cada controlador.</span><span class="sxs-lookup"><span data-stu-id="a314d-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="a314d-206">No es necesario tooworry cuando se utiliza un cuadro de mensajes o algo relacionado con la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a314d-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="a314d-207"><a id="push-channel-sharing"></a> Uso compartido de canal de inserción</span><span class="sxs-lookup"><span data-stu-id="a314d-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="a314d-208">Si está utilizando las notificaciones de inserción para otro fin en la aplicación tendrá canal de inserción de hello toouse característica de hello SDK de interacción de uso compartido.</span><span class="sxs-lookup"><span data-stu-id="a314d-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="a314d-209">Se trata de inserción tooavoid perdido.</span><span class="sxs-lookup"><span data-stu-id="a314d-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="a314d-210">Puede proporcionar su propia inicialización de llegar a la interacción de inserción de canales toohello.</span><span class="sxs-lookup"><span data-stu-id="a314d-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="a314d-211">Hola SDK lo utilizará en lugar de solicitar una nueva.</span><span class="sxs-lookup"><span data-stu-id="a314d-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="a314d-212">Actualizar inicialización de llegar a la interacción de hello con el canal de inserción en hello `InitEngagement` método de hello `App.xaml.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="a314d-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="a314d-213">O bien, si su intención es tooconsume Hola push canal después de la inicialización de alcance de hello, a continuación, puede establecer una devolución de llamada en el canal de contratación alcanzar tooget Hola inserción una vez que se crea mediante Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="a314d-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="a314d-214">Establezca la devolución de llamada en cualquier lugar **después** Hola inicialización alcance:</span><span class="sxs-lookup"><span data-stu-id="a314d-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="a314d-215">Sugerencia de esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="a314d-215">Custom scheme tip</span></span>
<span data-ttu-id="a314d-216">Se incluye el uso de esquemas personalizados.</span><span class="sxs-lookup"><span data-stu-id="a314d-216">We provide custom scheme use.</span></span> <span data-ttu-id="a314d-217">Puede enviar un tipo diferente de URI de contratación front-end toobe utilizado en la aplicación de interacción.</span><span class="sxs-lookup"><span data-stu-id="a314d-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="a314d-218">Los esquemas predeterminados, como `http, ftp, ...`, los administra Windows. Una ventana pedirá información si no hay ninguna aplicación predeterminada instalada en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a314d-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="a314d-219">También puede crear su propio esquema personalizado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a314d-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="a314d-220">tooset de manera sencilla de Hello una combinación personalizada en su aplicación es tooopen su `Package.appxmanifest` vaya en `Declarations` panel.</span><span class="sxs-lookup"><span data-stu-id="a314d-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="a314d-221">Seleccione `Protocol` Hola declaraciones disponibles desplácese cuadro y agréguelo.</span><span class="sxs-lookup"><span data-stu-id="a314d-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="a314d-222">Editar hello `Name` nombre de campo con el nuevo protocolo deseado.</span><span class="sxs-lookup"><span data-stu-id="a314d-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="a314d-223">Ahora toouse este protocolo, edite su `App.xaml.cs` con hello `OnActivated` método y no olvide tooinitialize interacción aquí también:</span><span class="sxs-lookup"><span data-stu-id="a314d-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

