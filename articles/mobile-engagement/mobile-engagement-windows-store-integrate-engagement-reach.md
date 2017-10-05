---
title: "Integración del SDK de Cobertura de Windows Universal Apps"
description: "Cómo integrar Cobertura de Azure Mobile Engagement con aplicaciones Windows Universal"
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
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="78b83-103">Integración del SDK de Cobertura de Windows Universal Apps</span><span class="sxs-lookup"><span data-stu-id="78b83-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="78b83-104">Debe seguir el procedimiento de integración descrito en el documento [Integración del SDK de Windows Universal Engagement](mobile-engagement-windows-store-integrate-engagement.md) antes de seguir con esta guía.</span><span class="sxs-lookup"><span data-stu-id="78b83-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="78b83-105">Integre el SDK de Cobertura de Engagement en el proyecto de Windows Universal</span><span class="sxs-lookup"><span data-stu-id="78b83-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="78b83-106">No hace falta agregar nada.</span><span class="sxs-lookup"><span data-stu-id="78b83-106">You do not have anything to add.</span></span> <span data-ttu-id="78b83-107">`EngagementReach` ya están en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="78b83-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="78b83-108">Puede personalizar las imágenes que se encuentran en la carpeta `Resources` del proyecto, especialmente el icono de marca (el valor predeterminado para el icono Engagement).</span><span class="sxs-lookup"><span data-stu-id="78b83-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="78b83-109">En las aplicaciones universales también puede mover la carpeta `Resources` del proyecto compartido para compartir su contenido entre aplicaciones, pero tendrá que mantener el archivo `Resources\EngagementConfiguration.xml` en su ubicación predeterminada debido a que depende de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="78b83-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="78b83-110">Habilitar el Servicio de notificaciones de Windows</span><span class="sxs-lookup"><span data-stu-id="78b83-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="78b83-111">Solo Windows 8.x y Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="78b83-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="78b83-112">Para poder usar el **Servicio de notificaciones de Windows** (conocido como WNS) en el archivo `Package.appxmanifest` en `Application UI`, haga clic en `All Image Assets` en el cuadro inferior izquierdo.</span><span class="sxs-lookup"><span data-stu-id="78b83-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="78b83-113">A la derecha del cuadro de `Notifications`, cambie `toast capable` de `(not set)` a `(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="78b83-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="78b83-114">Todas las plataformas</span><span class="sxs-lookup"><span data-stu-id="78b83-114">All platforms</span></span>
<span data-ttu-id="78b83-115">Deberá sincronizar la aplicación con su cuenta de Microsoft y la plataforma de Engagement.</span><span class="sxs-lookup"><span data-stu-id="78b83-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="78b83-116">Para esto deberá crear una cuenta o iniciar sesión en el [Centro de desarrollo de Windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="78b83-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="78b83-117">Después, cree una nueva aplicación y busque el SID y la clave secreta.</span><span class="sxs-lookup"><span data-stu-id="78b83-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="78b83-118">En el servidor front-end de Engagement, vaya a la opción de configuración de la aplicación en `native push` y pegue sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="78b83-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="78b83-119">Luego, haga clic con el botón secundario del mouse en el proyecto, seleccione `store` y `Associate App with the Store...`.</span><span class="sxs-lookup"><span data-stu-id="78b83-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="78b83-120">Solo tiene que seleccionar la aplicación que creó antes para sincronizarla.</span><span class="sxs-lookup"><span data-stu-id="78b83-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="78b83-121">Inicializar el SDK de Engagement Reach</span><span class="sxs-lookup"><span data-stu-id="78b83-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="78b83-122">Modifique `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="78b83-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="78b83-123">Inserte `EngagementReach.Instance.Init` justo después de `EngagementAgent.Instance.Init` en su método `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="78b83-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="78b83-124">`EngagementReach.Instance.Init` se ejecuta en un subproceso dedicado.</span><span class="sxs-lookup"><span data-stu-id="78b83-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="78b83-125">No es necesario que lo haga usted.</span><span class="sxs-lookup"><span data-stu-id="78b83-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="78b83-126">Si está usando las notificaciones de inserción en otra parte de la aplicación, tendrá que [compartir su canal de inserción](#push-channel-sharing) con Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="78b83-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="78b83-127">Integración</span><span class="sxs-lookup"><span data-stu-id="78b83-127">Integration</span></span>
<span data-ttu-id="78b83-128">Engagement proporciona dos maneras de agregar las vistas intersticiales y los banners en aplicación de Reach para anuncios y sondeos en la aplicación: la integración de superposición y la integración manual de vistas web.</span><span class="sxs-lookup"><span data-stu-id="78b83-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="78b83-129">No debe combinar ambos enfoques en la misma página.</span><span class="sxs-lookup"><span data-stu-id="78b83-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="78b83-130">La elección entre las dos integraciones podía resumirse así:</span><span class="sxs-lookup"><span data-stu-id="78b83-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="78b83-131">Puede elegir la integración de superposición si las páginas ya heredan desde el agente `EngagementPage`; solo es cuestión de reemplazar `EngagementPage` por `EngagementPageOverlay` y `xmlns:engagement="using:Microsoft.Azure.Engagement"` por `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` en las páginas.</span><span class="sxs-lookup"><span data-stu-id="78b83-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="78b83-132">Puede elegir la integración manual de vistas web si desea colocar de forma precisa la IU de Reach dentro de las páginas o si no desea agregar otro nivel de herencia a las páginas.</span><span class="sxs-lookup"><span data-stu-id="78b83-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="78b83-133">Integración de superposición</span><span class="sxs-lookup"><span data-stu-id="78b83-133">Overlay integration</span></span>
<span data-ttu-id="78b83-134">La superposición de Engagement agrega dinámicamente los elementos de IU utilizados para mostrar las campañas de Reach en la página.</span><span class="sxs-lookup"><span data-stu-id="78b83-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="78b83-135">Si la superposición no se adapta a su diseño, plantéese la integración manual de vistas web en su lugar.</span><span class="sxs-lookup"><span data-stu-id="78b83-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="78b83-136">En el cambio de archivo .xaml, cambie la referencia `EngagementPage` a `EngagementPageOverlay`.</span><span class="sxs-lookup"><span data-stu-id="78b83-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="78b83-137">Agregue a las declaraciones de espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="78b83-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="78b83-138">Reemplace `engagement:EngagementPage` por `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="78b83-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="78b83-139">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="78b83-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="78b83-140">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="78b83-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="78b83-141">Después, en el archivo. cs, etiquete la página en `EngagementPageOverlay` en lugar de `EngagementPage` e importe `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="78b83-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="78b83-142">Reemplace `EngagementPage` por `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="78b83-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="78b83-143">**Con EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="78b83-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="78b83-144">**Con EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="78b83-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="78b83-145">La superposición de Engagement agrega un elemento `Grid` encima de la página compuesta del diseño y los dos elementos `WebView`, uno para el banner y el otro para la vista intersticial.</span><span class="sxs-lookup"><span data-stu-id="78b83-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="78b83-146">Puede personalizar los elementos de superposición directamente en el archivo `EngagementPageOverlay.cs`.</span><span class="sxs-lookup"><span data-stu-id="78b83-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="78b83-147">Integración manual de vistas web</span><span class="sxs-lookup"><span data-stu-id="78b83-147">Web views manual integration</span></span>
<span data-ttu-id="78b83-148">Reach buscará las páginas para los dos elementos `WebView` responsables de mostrar el banner y la vista intersticial.</span><span class="sxs-lookup"><span data-stu-id="78b83-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="78b83-149">Lo único que debe hacer es agregar esos dos elementos `WebView` en algún lugar de las páginas. A continuación se muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="78b83-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="78b83-150">En este ejemplo los elementos `WebView` se estiran para ajustarse a su contenedor que automáticamente los cambia el tamaño en caso de rotación de la pantalla o de cambio de tamaño de la ventana.</span><span class="sxs-lookup"><span data-stu-id="78b83-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="78b83-151">Es importante mantener la misma convención de nomenclatura `engagement_notification_content` y `engagement_announcement_content` para los elementos `WebView`.</span><span class="sxs-lookup"><span data-stu-id="78b83-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="78b83-152">Reach los identifica por su nombre.</span><span class="sxs-lookup"><span data-stu-id="78b83-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="78b83-153">Controlar la inserción de datos (opcional)</span><span class="sxs-lookup"><span data-stu-id="78b83-153">Handle datapush (optional)</span></span>
<span data-ttu-id="78b83-154">Si desea que la aplicación pueda recibir inserciones de datos Reach, debe implementar dos eventos de la clase EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="78b83-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="78b83-155">En App.xaml.cs, en el constructor App(), agregue:</span><span class="sxs-lookup"><span data-stu-id="78b83-155">In App.xaml.cs in the App() constructor add:</span></span>

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

<span data-ttu-id="78b83-156">Puede ver que la devolución de llamada de cada método devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="78b83-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="78b83-157">Engagement envía un comentario a su back-end después de enviar la inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="78b83-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="78b83-158">Si la devolución de llamada devuelve un valor falso, se enviará el comentario `exit` .</span><span class="sxs-lookup"><span data-stu-id="78b83-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="78b83-159">De lo contrario, será `action`.</span><span class="sxs-lookup"><span data-stu-id="78b83-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="78b83-160">Si no se establece ninguna devolución de llamada para los eventos, el comentario `drop` se devolverá a Engagement.</span><span class="sxs-lookup"><span data-stu-id="78b83-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="78b83-161">Engagement no puede recibir varios comentarios para la inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="78b83-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="78b83-162">Si tiene previsto establecer varios controladores en un evento, tenga en cuenta que los comentarios corresponderán al último controlador enviado.</span><span class="sxs-lookup"><span data-stu-id="78b83-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="78b83-163">En este caso, es recomendable devolver siempre el mismo valor para evitar tener comentarios confusos en el front-end.</span><span class="sxs-lookup"><span data-stu-id="78b83-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="78b83-164">Personalizar la interfaz de usuario (opcional)</span><span class="sxs-lookup"><span data-stu-id="78b83-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="78b83-165">Primer paso</span><span class="sxs-lookup"><span data-stu-id="78b83-165">First step</span></span>
<span data-ttu-id="78b83-166">Puede personalizar la interfaz de usuario de Reach.</span><span class="sxs-lookup"><span data-stu-id="78b83-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="78b83-167">Para ello, debe crear una subclase de la clase `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="78b83-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="78b83-168">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="78b83-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="78b83-169">A continuación, establezca el contenido del campo `EngagementReach.Instance.Handler` con el objeto personalizado en la clase `App.xaml.cs` del método `App()`.</span><span class="sxs-lookup"><span data-stu-id="78b83-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="78b83-170">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="78b83-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="78b83-171">De forma predeterminada, Engagement usa su propia implementación de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="78b83-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="78b83-172">No hace falta crear elementos propios. Si lo hace, tiene que invalidar todos los métodos.</span><span class="sxs-lookup"><span data-stu-id="78b83-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="78b83-173">El comportamiento predeterminado consiste en seleccionar el objeto base de Engagement.</span><span class="sxs-lookup"><span data-stu-id="78b83-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="78b83-174">Vista web</span><span class="sxs-lookup"><span data-stu-id="78b83-174">Web View</span></span>
<span data-ttu-id="78b83-175">De forma predeterminada, Reach usará los recursos integrados del archivo DLL para mostrar las notificaciones y páginas.</span><span class="sxs-lookup"><span data-stu-id="78b83-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="78b83-176">Para proporcionar posibilidades de personalización completa, solo se usa la vista web.</span><span class="sxs-lookup"><span data-stu-id="78b83-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="78b83-177">Si desea personalizar diseños, invalide directamente los archivos de recursos `EngagementAnnouncement.html` y `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="78b83-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="78b83-178">Engagement necesita todo el código de `<body></body>` para que se ejecute correctamente.</span><span class="sxs-lookup"><span data-stu-id="78b83-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="78b83-179">No obstante, puede agregar una etiqueta exterior `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="78b83-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="78b83-180">Sin embargo, puede decidir usar sus propios recursos.</span><span class="sxs-lookup"><span data-stu-id="78b83-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="78b83-181">Puede invalidar los métodos `EngagementReachHandler` en la subclase para indicar a Engagement que debe usar sus diseños (asegúrese de integrar el mecanismo de Engagement):</span><span class="sxs-lookup"><span data-stu-id="78b83-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="78b83-182">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="78b83-182">**Sample Code :**</span></span>

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


<span data-ttu-id="78b83-183">De forma predeterminada, AnnouncementHTML es `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="78b83-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="78b83-184">Representa el archivo html que diseña el contenido de un mensaje de inserción (anuncio de texto, anuncio web y anuncio de sondeo).</span><span class="sxs-lookup"><span data-stu-id="78b83-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="78b83-185">AnnouncementName es `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="78b83-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="78b83-186">Es el nombre del diseño de vista web de la página xaml.</span><span class="sxs-lookup"><span data-stu-id="78b83-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="78b83-187">NotfificationHTML es `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="78b83-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="78b83-188">Representa el archivo html que diseña la notificación de un mensaje de inserción.</span><span class="sxs-lookup"><span data-stu-id="78b83-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="78b83-189">NotfificationName es `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="78b83-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="78b83-190">Es el nombre del diseño de vista web de la página xaml.</span><span class="sxs-lookup"><span data-stu-id="78b83-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="78b83-191">Personalización</span><span class="sxs-lookup"><span data-stu-id="78b83-191">Customization</span></span>
<span data-ttu-id="78b83-192">Puede personalizar la vista web de notificación y anuncio como desee si quiere conservar el objeto de Engagement.</span><span class="sxs-lookup"><span data-stu-id="78b83-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="78b83-193">Asegúrese de que el objeto de vista web se describa tres veces: la primera, en el archivo xaml, la segunda en el archivo .cs del método "setwebview()" y la tercera en el archivo html.</span><span class="sxs-lookup"><span data-stu-id="78b83-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="78b83-194">En el código xaml, describa el componente webview de diseño gráfico actual.</span><span class="sxs-lookup"><span data-stu-id="78b83-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="78b83-195">En el archivo .cs, puede definir "setwebview()" en el que establecer la dimensión de las dos vistas web de dos (notificación, anuncio).</span><span class="sxs-lookup"><span data-stu-id="78b83-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="78b83-196">Es muy eficaz al cambiar el tamaño de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78b83-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="78b83-197">En el archivo html de Engagement, se describen el contenido de la vista web, el diseño y las posiciones de los elementos entre sí.</span><span class="sxs-lookup"><span data-stu-id="78b83-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="78b83-198">Iniciar el mensaje</span><span class="sxs-lookup"><span data-stu-id="78b83-198">Launch message</span></span>
<span data-ttu-id="78b83-199">Cuando un usuario hace clic en una notificación del sistema, Engagement inicia la aplicación, carga el contenido de los mensajes de inserción y muestra la página de la campaña correspondiente.</span><span class="sxs-lookup"><span data-stu-id="78b83-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="78b83-200">Hay un retraso entre el inicio de la aplicación y la presentación de la página (según la velocidad de la red).</span><span class="sxs-lookup"><span data-stu-id="78b83-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="78b83-201">Para indicar al usuario que algo se está cargando, debería proporcionar algún tipo de información visual, tal como una barra de progreso o un indicador de progreso.</span><span class="sxs-lookup"><span data-stu-id="78b83-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="78b83-202">Engagement no puede controlar esto por sí solo, pero le ofrece algunos controladores para ello.</span><span class="sxs-lookup"><span data-stu-id="78b83-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="78b83-203">Para implementar la devolución de llamada, en App.xaml.cs, en "Public App(){}", agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78b83-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="78b83-204">Puede establecer la devolución de llamada en el método "Public App(){}" del archivo `App.xaml.cs`, preferentemente antes de la llamada `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="78b83-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="78b83-205">A cada controlador lo llama el subproceso de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="78b83-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="78b83-206">No tiene que preocuparse cuando se usa un objeto MessageBox u otro elemento relacionado con la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="78b83-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="78b83-207"><a id="push-channel-sharing"></a> Uso compartido de canal de inserción</span><span class="sxs-lookup"><span data-stu-id="78b83-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="78b83-208">Si está usando las notificaciones de inserción para otra finalidad en la aplicación, tendrá que usar la característica de uso compartido del canal de inserción del SDK de Engagement.</span><span class="sxs-lookup"><span data-stu-id="78b83-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="78b83-209">Esto es para evitar la inserción perdida.</span><span class="sxs-lookup"><span data-stu-id="78b83-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="78b83-210">Puede proporcionar su propio canal de inserción a la inicialización de Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="78b83-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="78b83-211">El SDK lo usará en lugar de solicitar uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="78b83-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="78b83-212">Actualice la inicialización de Engagement Reach con el canal de inserción en el método de `InitEngagement` desde el archivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="78b83-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="78b83-213">También, si desea usar el canal de inserción después de la inicialización de Reach, puede establecer una devolución de llamada en Engagement Reach para obtener el canal de inserción una vez creado por el SDK.</span><span class="sxs-lookup"><span data-stu-id="78b83-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="78b83-214">Establezca la devolución de llamada en cualquier lugar **después** de la inicialización de Reach:</span><span class="sxs-lookup"><span data-stu-id="78b83-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="78b83-215">Sugerencia de esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="78b83-215">Custom scheme tip</span></span>
<span data-ttu-id="78b83-216">Se incluye el uso de esquemas personalizados.</span><span class="sxs-lookup"><span data-stu-id="78b83-216">We provide custom scheme use.</span></span> <span data-ttu-id="78b83-217">Puede enviar otro tipo de URI desde el front-end de Engagement para usarse en la aplicación de Engagement.</span><span class="sxs-lookup"><span data-stu-id="78b83-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="78b83-218">Los esquemas predeterminados, como `http, ftp, ...`, los administra Windows. Una ventana pedirá información si no hay ninguna aplicación predeterminada instalada en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="78b83-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="78b83-219">También puede crear su propio esquema personalizado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="78b83-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="78b83-220">Es una manera sencilla de establecer un esquema personalizado en la aplicación es abrir `Package.appxmanifest` en el panel `Declarations`.</span><span class="sxs-lookup"><span data-stu-id="78b83-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="78b83-221">Seleccione `Protocol` del cuadro desplegable Declaraciones disponibles y agréguelo.</span><span class="sxs-lookup"><span data-stu-id="78b83-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="78b83-222">Edite el campo `Name` con el nombre deseado del nuevo protocolo.</span><span class="sxs-lookup"><span data-stu-id="78b83-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="78b83-223">Ahora, para usar este protocolo, edite `App.xaml.cs` mediante el método `OnActivated` y no se olvide de inicializar Engagement aquí también:</span><span class="sxs-lookup"><span data-stu-id="78b83-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

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

