---
title: "Procedimientos de actualización del SDK de aplicaciones Windows Universal"
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
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="28b28-103">Procedimientos de actualización del SDK de aplicaciones Windows Universal</span><span class="sxs-lookup"><span data-stu-id="28b28-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="28b28-104">Si ya integró una versión anterior de Engagement en la aplicación, debería tener en cuenta los siguientes puntos a la hora de actualizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="28b28-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="28b28-105">Es posible que tenga que seguir varios procedimientos si se perdió varias versiones del SDK.</span><span class="sxs-lookup"><span data-stu-id="28b28-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="28b28-106">Por ejemplo, si migra desde 0.10.1 a 0.11.0, primero debe seguir el procedimiento "de 0.9.0 a 0.10.1" y luego el procedimiento "de 0.10.1 a 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="28b28-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="28b28-107">De 3.3.0 a 3.4.0</span><span class="sxs-lookup"><span data-stu-id="28b28-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="28b28-108">Registros de prueba</span><span class="sxs-lookup"><span data-stu-id="28b28-108">Test logs</span></span>
<span data-ttu-id="28b28-109">Los registros de consola generados por el SDK ahora se pueden habilitar, deshabilitar o filtrar.</span><span class="sxs-lookup"><span data-stu-id="28b28-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="28b28-110">Para personalizar esto, actualice la propiedad `EngagementAgent.Instance.TestLogEnabled` a uno de los valores disponibles en la enumeración `EngagementTestLogLevel`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="28b28-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="28b28-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="28b28-111">Resources</span></span>
<span data-ttu-id="28b28-112">Se ha mejorado la superposición de Reach.</span><span class="sxs-lookup"><span data-stu-id="28b28-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="28b28-113">Forma parte de los recursos del paquete NuGet del SDK.</span><span class="sxs-lookup"><span data-stu-id="28b28-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="28b28-114">Al actualizar a la nueva versión del SDK puede elegir si desea conservar o no los archivos existentes de la carpeta de superposición de los recursos:</span><span class="sxs-lookup"><span data-stu-id="28b28-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="28b28-115">Si la superposición anterior funciona o va a integrar los elementos `WebView` manualmente, entonces puede decidir mantener los archivos de salida, lo cual seguirá funcionando.</span><span class="sxs-lookup"><span data-stu-id="28b28-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="28b28-116">Si desea actualizar a la nueva superposición, simplemente reemplace toda la carpeta `overlay` de sus recursos por la nueva desde el paquete del SDK (aplicaciones UWP: tras la actualización, puede obtener la nueva carpeta de superposición desde %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="28b28-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="28b28-117">El uso de la nueva superposición sobrescribirá todas las personalizaciones realizadas en la versión anterior.</span><span class="sxs-lookup"><span data-stu-id="28b28-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="28b28-118">De 3.2.0 a 3.3.0</span><span class="sxs-lookup"><span data-stu-id="28b28-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="28b28-119">Recursos</span><span class="sxs-lookup"><span data-stu-id="28b28-119">Resources</span></span>
<span data-ttu-id="28b28-120">Este paso se refiere solo a los recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="28b28-120">This step concerns customized resources only.</span></span> <span data-ttu-id="28b28-121">Si ha personalizado los recursos proporcionados por el SDK (html, imágenes, superposición), tendrá que hacer una copia de seguridad de estos antes de actualizar y volver a aplicar la personalización en los recursos actualizados.</span><span class="sxs-lookup"><span data-stu-id="28b28-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="28b28-122">De 3.1.0 a 3.2.0</span><span class="sxs-lookup"><span data-stu-id="28b28-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="28b28-123">Recursos</span><span class="sxs-lookup"><span data-stu-id="28b28-123">Resources</span></span>
<span data-ttu-id="28b28-124">Este paso se refiere solo a los recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="28b28-124">This step concerns customized resources only.</span></span> <span data-ttu-id="28b28-125">Si ha personalizado los recursos proporcionados por el SDK (html, imágenes, superposición), tendrá que hacer una copia de seguridad de estos antes de actualizar y volver a aplicar la personalización en los recursos actualizados.</span><span class="sxs-lookup"><span data-stu-id="28b28-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="28b28-126">integración de vista web.</span><span class="sxs-lookup"><span data-stu-id="28b28-126">Webview integration</span></span>
<span data-ttu-id="28b28-127">En esta versión se introdujeron algunas mejoras para disponer de compatibilidad con distintos factores de formulario de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="28b28-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="28b28-128">Asegúrese de que la integración de las vistas web coincida con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="28b28-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="28b28-129">En la página XAML ():</span><span class="sxs-lookup"><span data-stu-id="28b28-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="28b28-130">Y en el archivo .cs asociado:</span><span class="sxs-lookup"><span data-stu-id="28b28-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
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
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="28b28-131">De 2.0.0 a 3.0.0</span><span class="sxs-lookup"><span data-stu-id="28b28-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="28b28-132">Recursos</span><span class="sxs-lookup"><span data-stu-id="28b28-132">Resources</span></span>
<span data-ttu-id="28b28-133">Este paso se refiere solo a los recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="28b28-133">This step concerns customized resources only.</span></span> <span data-ttu-id="28b28-134">Si ha personalizado los recursos proporcionados por el SDK (html, imágenes, superposición), tendrá que hacer una copia de seguridad de estos antes de actualizar y volver a aplicar la personalización en los recursos actualizados.</span><span class="sxs-lookup"><span data-stu-id="28b28-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="28b28-135">De 1.1.1 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="28b28-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="28b28-136">A continuación se describe cómo migrar una integración del SDK desde el servicio Capptain que ofrece Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="28b28-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="28b28-137">Capptain y Mobile Engagement no son los mismos servicios, y el procedimiento que se indica a continuación destaca únicamente cómo migrar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="28b28-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="28b28-138">La migración del SDK en la aplicación NO migrará los datos desde los servidores Capptain a los servidores Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="28b28-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="28b28-139">Si va a migrar desde una versión anterior, consulte el sitio web de Capptain para migrar a 1.1.1 en primer lugar luego aplique el siguiente procedimiento.</span><span class="sxs-lookup"><span data-stu-id="28b28-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="28b28-140">Paquete de NuGet</span><span class="sxs-lookup"><span data-stu-id="28b28-140">Nuget package</span></span>
<span data-ttu-id="28b28-141">Reemplace **Capptain.WindowsPhone** por el paquete Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="28b28-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="28b28-142">Aplicar Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="28b28-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="28b28-143">El SDK usa el término `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="28b28-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="28b28-144">Debe actualizar el proyecto para que coincida con este cambio.</span><span class="sxs-lookup"><span data-stu-id="28b28-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="28b28-145">Debe desinstalar el paquete NuGet de Capptain actual.</span><span class="sxs-lookup"><span data-stu-id="28b28-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="28b28-146">Tenga en cuenta que se van a quitar todos los cambios de la carpeta recursos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="28b28-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="28b28-147">Si desea conservar los archivos, haga una copia de ellos.</span><span class="sxs-lookup"><span data-stu-id="28b28-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="28b28-148">Después, instale el nuevo paquete NuGet de Microsoft Azure Mobile Engagement en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="28b28-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="28b28-149">Puede encontrarlo directamente en [sitio web de nuget]</span><span class="sxs-lookup"><span data-stu-id="28b28-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="28b28-150">o aquí en el índice.</span><span class="sxs-lookup"><span data-stu-id="28b28-150">or here index.</span></span> <span data-ttu-id="28b28-151">Esta acción reemplaza todos los archivos de recursos que Engagement usa y agrega el nuevo archivo DLL de Engagement a las referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="28b28-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="28b28-152">Tendrá que limpiar las referencias del proyecto al eliminar de referencias del archivo DLL de Capptain.</span><span class="sxs-lookup"><span data-stu-id="28b28-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="28b28-153">Si no lo hace, la versión de Capptain entrará en conflicto y se producirán errores.</span><span class="sxs-lookup"><span data-stu-id="28b28-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="28b28-154">Si tiene recursos Capptain personalizados, copie el contenido de los archivos antiguos y péguelos en los nuevos archivos de Engagement.</span><span class="sxs-lookup"><span data-stu-id="28b28-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="28b28-155">Tenga en cuenta que se deben actualizar tanto los archivos xaml como los archivos cs.</span><span class="sxs-lookup"><span data-stu-id="28b28-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="28b28-156">Una vez completados estos pasos, solo tendrá que reemplazar las referencias de Capptain antiguas por las nuevas referencias de Engagement.</span><span class="sxs-lookup"><span data-stu-id="28b28-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="28b28-157">Se deben actualizar todos los espacios de nombres de Capptain.</span><span class="sxs-lookup"><span data-stu-id="28b28-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="28b28-158">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="28b28-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="28b28-159">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="28b28-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="28b28-160">Todas las clases de Capptain que contengan "Capptain" deberían contener "Engagement".</span><span class="sxs-lookup"><span data-stu-id="28b28-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="28b28-161">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="28b28-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="28b28-162">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="28b28-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="28b28-163">En el caso de los archivos xaml, también cambian el espacio de nombres y los atributos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="28b28-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="28b28-164">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="28b28-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="28b28-165">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="28b28-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="28b28-166">Cambios de la página de superposición</span><span class="sxs-lookup"><span data-stu-id="28b28-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="28b28-167">También cambia la superposición</span><span class="sxs-lookup"><span data-stu-id="28b28-167">Overlay also changes.</span></span> <span data-ttu-id="28b28-168">Su espacio de nombres nuevo es `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="28b28-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="28b28-169">Se debe usar tanto en los archivos xaml como los archivos cs.</span><span class="sxs-lookup"><span data-stu-id="28b28-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="28b28-170">Además `CapptainGrid` se debe denominar `EngagementGrid`, `capptain_notification_content` y `capptain_announcement_content` se denominan `engagement_notification_content` y `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="28b28-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="28b28-171">Para la superposición:</span><span class="sxs-lookup"><span data-stu-id="28b28-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="28b28-172">Se convierte en:</span><span class="sxs-lookup"><span data-stu-id="28b28-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="28b28-173">En el caso de otros recursos, como imágenes Capptain y archivos HTML, tenga en cuenta que su nombre también habrá cambiado para usar "Engagement".</span><span class="sxs-lookup"><span data-stu-id="28b28-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="28b28-174">Declaración del proyecto</span><span class="sxs-lookup"><span data-stu-id="28b28-174">Project declaration</span></span>
<span data-ttu-id="28b28-175">En Package.appxmanifest `File Type Associations` se ha actualizado de:</span><span class="sxs-lookup"><span data-stu-id="28b28-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="28b28-176">capptain\_reach\_content to engagement\_reach\_content</span><span class="sxs-lookup"><span data-stu-id="28b28-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="28b28-177">capptain\_log\_file to engagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="28b28-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="28b28-178">Identificador de aplicación o clave SDK</span><span class="sxs-lookup"><span data-stu-id="28b28-178">Application ID / SDK Key</span></span>
<span data-ttu-id="28b28-179">Engagement usa una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="28b28-179">Engagement uses a connection string.</span></span> <span data-ttu-id="28b28-180">No es necesario especificar un identificador de aplicación y una clave SDK con Mobile Engagement, solo tiene que especificar una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="28b28-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="28b28-181">Esta se puede configurar en el archivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="28b28-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="28b28-182">La configuración de Engagement se puede establecer en el archivo `Resources\EngagementConfiguration.xml` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="28b28-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="28b28-183">Edite este archivo para especificar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="28b28-183">Edit this file to specify:</span></span>

* <span data-ttu-id="28b28-184">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="28b28-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="28b28-185">Si desea especificarla en tiempo de ejecución, puede llamar al método siguiente antes de la inicialización del agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="28b28-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="28b28-186">La cadena de conexión de la aplicación se muestra en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="28b28-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="28b28-187">Cambio de nombre de elementos</span><span class="sxs-lookup"><span data-stu-id="28b28-187">Items name change</span></span>
<span data-ttu-id="28b28-188">Todos los elementos con el nombre *capptain* han cambiado a *engagement*.</span><span class="sxs-lookup"><span data-stu-id="28b28-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="28b28-189">De forma similar, *Capptain* cambió a *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="28b28-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="28b28-190">Ejemplos de elementos Capptain que se usan habitualmente:</span><span class="sxs-lookup"><span data-stu-id="28b28-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="28b28-191">CapptainConfiguration ahora se llama EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="28b28-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="28b28-192">CapptainAgent ahora se llama EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="28b28-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="28b28-193">CapptainReach ahora se llama EngagementReach</span><span class="sxs-lookup"><span data-stu-id="28b28-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="28b28-194">CapptainHttpConfig ahora se llama EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="28b28-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="28b28-195">GetCapptainPageName ahora se llama GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="28b28-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="28b28-196">Tenga en cuenta que el cambio de nombre también afecta a los métodos invalidados.</span><span class="sxs-lookup"><span data-stu-id="28b28-196">Note that rename also affects overridden methods.</span></span>

