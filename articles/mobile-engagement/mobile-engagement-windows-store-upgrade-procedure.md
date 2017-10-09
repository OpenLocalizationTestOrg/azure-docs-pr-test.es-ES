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
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="8e057-103">Procedimientos de actualización del SDK de aplicaciones Windows Universal</span><span class="sxs-lookup"><span data-stu-id="8e057-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="8e057-104">Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="8e057-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="8e057-105">Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="8e057-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="8e057-106">Por ejemplo, si migra desde 0.10.1 too0.11.0 tiene toofirst siga Hola "de 0.9.0 too0.10.1" procedimiento, a continuación, Hola "de 0.10.1 too0.11.0" procedimiento.</span><span class="sxs-lookup"><span data-stu-id="8e057-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="8e057-107">Desde 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="8e057-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="8e057-108">Registros de prueba</span><span class="sxs-lookup"><span data-stu-id="8e057-108">Test logs</span></span>
<span data-ttu-id="8e057-109">Registros de la consola producidos por hello SDK ahora pueden habilitada, deshabilitada o filtrado.</span><span class="sxs-lookup"><span data-stu-id="8e057-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="8e057-110">toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8e057-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="8e057-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="8e057-111">Resources</span></span>
<span data-ttu-id="8e057-112">se ha mejorado la superposición de cobertura de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e057-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="8e057-113">Forma parte de recursos del paquete de NuGet de SDK de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e057-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="8e057-114">Al actualizar toohello nueva versión de hello SDK puede elegir que si desea que tookeep los archivos existentes de hello superposición de carpeta de los recursos:</span><span class="sxs-lookup"><span data-stu-id="8e057-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="8e057-115">Si superposición anterior Hola funciona para usted o va a integrar hello `WebView` elementos manualmente, a continuación, puede decidir tookeep los archivos existentes, seguirá funcionando.</span><span class="sxs-lookup"><span data-stu-id="8e057-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="8e057-116">Si desea que tooupdate toohello nueva superposición, Hola simplemente reemplazar todo `overlay` carpeta de sus recursos con hello nueva del paquete SDK de hello (aplicaciones UWP: después de la actualización de hello, puede obtener nueva carpeta de superposición Hola desde % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="8e057-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="8e057-117">Utilizando la superposición de hello nueva sobrescribirá todas las personalizaciones realizadas en la versión anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e057-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="8e057-118">De 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="8e057-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="8e057-119">Recursos</span><span class="sxs-lookup"><span data-stu-id="8e057-119">Resources</span></span>
<span data-ttu-id="8e057-120">Este paso se refiere solo a los recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="8e057-120">This step concerns customized resources only.</span></span> <span data-ttu-id="8e057-121">Si ha personalizado los recursos de hello proporcionados por hello SDK (html, imágenes, superposición) tiene toobackup ellos antes de actualizar y volver a aplicar la personalización en actualiza recursos.</span><span class="sxs-lookup"><span data-stu-id="8e057-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="8e057-122">Desde 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="8e057-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="8e057-123">Recursos</span><span class="sxs-lookup"><span data-stu-id="8e057-123">Resources</span></span>
<span data-ttu-id="8e057-124">Este paso se refiere solo a los recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="8e057-124">This step concerns customized resources only.</span></span> <span data-ttu-id="8e057-125">Si ha personalizado los recursos de hello proporcionados por hello SDK (html, imágenes, superposición) tiene toobackup ellos antes de actualizar y volver a aplicar la personalización en actualiza recursos.</span><span class="sxs-lookup"><span data-stu-id="8e057-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="8e057-126">integración de vista web.</span><span class="sxs-lookup"><span data-stu-id="8e057-126">Webview integration</span></span>
<span data-ttu-id="8e057-127">Algunos factores de forma de otro dispositivo de toomatch mejoras introducidas en esta versión.</span><span class="sxs-lookup"><span data-stu-id="8e057-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="8e057-128">Asegúrese de que la integración de hello webview coincidan siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="8e057-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="8e057-129">En la página XAML ():</span><span class="sxs-lookup"><span data-stu-id="8e057-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="8e057-130">Y en el archivo .cs asociado:</span><span class="sxs-lookup"><span data-stu-id="8e057-130">And in your associated .cs file:</span></span>

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

## <a name="from-200-too300"></a><span data-ttu-id="8e057-131">Desde 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="8e057-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="8e057-132">Recursos</span><span class="sxs-lookup"><span data-stu-id="8e057-132">Resources</span></span>
<span data-ttu-id="8e057-133">Este paso se refiere solo a los recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="8e057-133">This step concerns customized resources only.</span></span> <span data-ttu-id="8e057-134">Si ha personalizado los recursos de hello proporcionados por hello SDK (html, imágenes, superposición) tiene toobackup ellos antes de actualizar y volver a aplicar la personalización en actualiza recursos.</span><span class="sxs-lookup"><span data-stu-id="8e057-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="8e057-135">Desde 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="8e057-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="8e057-136">Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e057-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8e057-137">Capptain e interacción móvil no se Hola los mismos servicios y procedimiento Hola indicado a continuación sólo resalta cómo toomigrate Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="8e057-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="8e057-138">Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores</span><span class="sxs-lookup"><span data-stu-id="8e057-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="8e057-139">Si va a migrar desde una versión anterior, por favor, consulte hello Capptain sitio web toomigrate too1.1.1 en primer lugar, aplique Hola procedimiento</span><span class="sxs-lookup"><span data-stu-id="8e057-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="8e057-140">Paquete de NuGet</span><span class="sxs-lookup"><span data-stu-id="8e057-140">Nuget package</span></span>
<span data-ttu-id="8e057-141">Reemplace **Capptain.WindowsPhone** por el paquete Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="8e057-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="8e057-142">Aplicar Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8e057-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="8e057-143">Hola SDK utiliza el término de hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="8e057-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="8e057-144">Necesita tooupdate su toomatch proyecto este cambio.</span><span class="sxs-lookup"><span data-stu-id="8e057-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="8e057-145">Debe toouninstall el paquete de nuget Capptain actual.</span><span class="sxs-lookup"><span data-stu-id="8e057-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="8e057-146">Tenga en cuenta que se van a quitar todos los cambios de la carpeta recursos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="8e057-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="8e057-147">Si desea que tookeep esos archivos, a continuación, haga una copia de ellos.</span><span class="sxs-lookup"><span data-stu-id="8e057-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="8e057-148">Después de eso, instale el nuevo paquete de nuget de Microsoft Azure Engagement hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e057-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="8e057-149">Puede encontrarlo directamente en [sitio web de nuget]</span><span class="sxs-lookup"><span data-stu-id="8e057-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="8e057-150">o aquí en el índice.</span><span class="sxs-lookup"><span data-stu-id="8e057-150">or here index.</span></span> <span data-ttu-id="8e057-151">Este reemplaza acción todos los archivos de recursos utilizados por la interacción y agrega Hola nueva contratación DLL tooyour referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e057-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="8e057-152">Eliminando las referencias de Capptain DLL tienen tooclean las referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e057-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="8e057-153">Si no hace esto, versión de Hola de Capptain entrarán en conflicto y se producirán errores.</span><span class="sxs-lookup"><span data-stu-id="8e057-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="8e057-154">Si ha personalizado los recursos de Capptain, copie el contenido de los archivos antiguos y péguelos en los nuevos archivos de contratación Hola.</span><span class="sxs-lookup"><span data-stu-id="8e057-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="8e057-155">Tenga en cuenta que los archivos xaml y cs tienen toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="8e057-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="8e057-156">Una vez completados estos pasos solo tiene tooreplace Capptain las referencias anteriores a por nuevas referencias de contratación Hola.</span><span class="sxs-lookup"><span data-stu-id="8e057-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="8e057-157">Todos los espacios de nombres de Capptain tienen toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="8e057-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="8e057-158">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="8e057-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="8e057-159">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="8e057-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="8e057-160">Todas las clases de Capptain que contengan "Capptain" deberían contener "Engagement".</span><span class="sxs-lookup"><span data-stu-id="8e057-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="8e057-161">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="8e057-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="8e057-162">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="8e057-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="8e057-163">En el caso de los archivos xaml, también cambian el espacio de nombres y los atributos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="8e057-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="8e057-164">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="8e057-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="8e057-165">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="8e057-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="8e057-166">Cambios de la página de superposición</span><span class="sxs-lookup"><span data-stu-id="8e057-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8e057-167">También cambia la superposición</span><span class="sxs-lookup"><span data-stu-id="8e057-167">Overlay also changes.</span></span> <span data-ttu-id="8e057-168">Su espacio de nombres nuevo es `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="8e057-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="8e057-169">Tiene toobe que se usa en los archivos xaml y cs.</span><span class="sxs-lookup"><span data-stu-id="8e057-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="8e057-170">Además `CapptainGrid` se denomina toobe `EngagementGrid`, `capptain_notification_content` y `capptain_announcement_content` se denominan `engagement_notification_content` y `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="8e057-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="8e057-171">Para la superposición:</span><span class="sxs-lookup"><span data-stu-id="8e057-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="8e057-172">Se convierte en:</span><span class="sxs-lookup"><span data-stu-id="8e057-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="8e057-173">Para hello otros recursos como Capptain imágenes y archivos HTML, tenga en cuenta que también han tenido toouse cuyo nombre ha cambiado "Interacción".</span><span class="sxs-lookup"><span data-stu-id="8e057-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="8e057-174">Declaración del proyecto</span><span class="sxs-lookup"><span data-stu-id="8e057-174">Project declaration</span></span>
<span data-ttu-id="8e057-175">En Package.appxmanifest `File Type Associations` se ha actualizado de:</span><span class="sxs-lookup"><span data-stu-id="8e057-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="8e057-176">capptain\_alcanzar\_tooengagement contenido\_alcanzar\_contenido</span><span class="sxs-lookup"><span data-stu-id="8e057-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="8e057-177">capptain\_registro\_archivo tooengagement\_registro\_archivo</span><span class="sxs-lookup"><span data-stu-id="8e057-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="8e057-178">Identificador de aplicación o clave SDK</span><span class="sxs-lookup"><span data-stu-id="8e057-178">Application ID / SDK Key</span></span>
<span data-ttu-id="8e057-179">Engagement usa una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="8e057-179">Engagement uses a connection string.</span></span> <span data-ttu-id="8e057-180">Toospecify no tiene un identificador de la aplicación y una clave SDK con Mobile Engagement, solo tendrá toospecify una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="8e057-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="8e057-181">Esta se puede configurar en el archivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="8e057-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="8e057-182">configuración de la interacción de Hola se puede establecer el `Resources\EngagementConfiguration.xml` archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e057-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="8e057-183">Editar este archivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="8e057-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="8e057-184">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="8e057-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="8e057-185">Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="8e057-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="8e057-186">cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e057-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="8e057-187">Cambio de nombre de elementos</span><span class="sxs-lookup"><span data-stu-id="8e057-187">Items name change</span></span>
<span data-ttu-id="8e057-188">Todos los elementos con el nombre *capptain* han cambiado a *engagement*.</span><span class="sxs-lookup"><span data-stu-id="8e057-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="8e057-189">De forma similar para *Capptain* demasiado*interacción*.</span><span class="sxs-lookup"><span data-stu-id="8e057-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="8e057-190">Ejemplos de elementos Capptain que se usan habitualmente:</span><span class="sxs-lookup"><span data-stu-id="8e057-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="8e057-191">CapptainConfiguration ahora se llama EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="8e057-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="8e057-192">CapptainAgent ahora se llama EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="8e057-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="8e057-193">CapptainReach ahora se llama EngagementReach</span><span class="sxs-lookup"><span data-stu-id="8e057-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="8e057-194">CapptainHttpConfig ahora se llama EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="8e057-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="8e057-195">GetCapptainPageName ahora se llama GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="8e057-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="8e057-196">Tenga en cuenta que el cambio de nombre también afecta a los métodos invalidados.</span><span class="sxs-lookup"><span data-stu-id="8e057-196">Note that rename also affects overridden methods.</span></span>

