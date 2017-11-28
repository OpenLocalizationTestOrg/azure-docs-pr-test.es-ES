---
title: "aaaWindows Phone Silverlight alcanzar integración con el SDK"
description: "¿Cómo tooIntegrate Azure Mobile Engagement alcanzar con aplicaciones de Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="fd1e5-103">Integración del SDK de cobertura de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fd1e5-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="fd1e5-104">Debe seguir el procedimiento de integración de hello descrito en hello [integración del SDK de interacción de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir esta guía.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="fd1e5-105">Incrustar Hola interacción Reach SDK en el proyecto de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fd1e5-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="fd1e5-106">No tiene nada tooadd.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-106">You do not have anything tooadd.</span></span> <span data-ttu-id="fd1e5-107">`EngagementReach` y los recursos de ya están en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="fd1e5-108">Puede personalizar imágenes ubicado en hello `Resources` carpeta del proyecto, especialmente icono de marca de hello (ese icono de interacción de toohello predeterminado).</span><span class="sxs-lookup"><span data-stu-id="fd1e5-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="fd1e5-109">Agregar capacidades de Hola</span><span class="sxs-lookup"><span data-stu-id="fd1e5-109">Add hello capabilities</span></span>
<span data-ttu-id="fd1e5-110">Hola interacción Reach SDK tiene algunas capacidades adicionales.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="fd1e5-111">Abra su `WMAppManifest.xml` de archivos y asegúrese de que se declaran ese Hola siguiendo las capacidades:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="fd1e5-112">Hello uno se utiliza por primera vez mostrar hello MPNS servicio tooallow Hola de notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="fd1e5-113">Hello segunda es tooembed usa una tarea de explorador en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="fd1e5-114">Editar hello `WMAppManifest.xml` de archivos y agregar dentro de hello `<Capabilities />` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="fd1e5-115">Habilitar Hola servicio de notificaciones Push de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd1e5-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="fd1e5-116">Hola de orden toouse **servicio de notificaciones Push de Microsoft** (denominadas MPNS) su `WMAppManifest.xml` archivo debe tener un `<App />` etiquetar con un `Publisher` atributo establece toohello nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="fd1e5-117">Inicializar Hola interacción Reach SDK</span><span class="sxs-lookup"><span data-stu-id="fd1e5-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="fd1e5-118">Configuración de Engagement</span><span class="sxs-lookup"><span data-stu-id="fd1e5-118">Engagement configuration</span></span>
<span data-ttu-id="fd1e5-119">configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="fd1e5-120">Editar este archivo de configuración de alcance toospecify:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="fd1e5-121">*Opcional*, indicar si se activa la inserción nativa de hello (MPNS) o no entre `<enableNativePush>` y `</enableNativePush>` etiquetas, (`true` de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="fd1e5-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="fd1e5-122">*Opcional*, indicar Hola nombre de canal de inserción de hello entre `<channelName>` y `</channelName>` etiquetas, proporcionar Hola misma que la aplicación puede usar o déjela en blanco actualmente.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="fd1e5-123">Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="fd1e5-124">Puede especificar nombre de Hola de canal de inserción de hello MPNS de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="fd1e5-125">De forma predeterminada, interacción crea un nombre basado en hello appId.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="fd1e5-126">No tenga necesidad de toospecify Hola nombre usted mismo, excepto si tiene intención de canal de inserción de hello toouse fuera de contratación.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="fd1e5-127">Inicialización de Engagement</span><span class="sxs-lookup"><span data-stu-id="fd1e5-127">Engagement initialization</span></span>
<span data-ttu-id="fd1e5-128">Modificar Hola `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="fd1e5-129">Agregar tooyour `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="fd1e5-130">Inserte `EngagementReach.Instance.Init` justo después de `EngagementAgent.Instance.Init` en `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="fd1e5-131">Insertar `EngagementReach.Instance.OnActivated` en hello `Application_Activated` método:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="fd1e5-132">Hola `EngagementReach.Instance.Init` se ejecuta en un subproceso dedicado.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="fd1e5-133">No tiene toodo usted mismo.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="fd1e5-134">Consideraciones de envío de la tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fd1e5-134">App store submission considerations</span></span>
<span data-ttu-id="fd1e5-135">Microsoft impone algunas reglas al usar notificaciones de inserción de hello:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="fd1e5-136">De hello Microsoft [las directivas de aplicación] documentación, sección 2.9:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="fd1e5-137">Debe solicitar notificaciones de inserción de hello usuario tooaccept tooreceive.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="fd1e5-138">A continuación, en la configuración, agregue un notificaciones de inserción de manera toodisable Hola.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="fd1e5-139">objeto de Hello EngagementReach proporciona dos métodos toomanage Hola/opt: desactivación, `EnableNativePush()` y `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="fd1e5-140">Por ejemplo, podría crear una opción en la configuración de hello con un toodisable de alternancia o habilitar MPNS.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="fd1e5-141">También puede decidir toodeactivate MPNS a través de la configuración de la interacción de hello\<windows phone sdk alcance configuración\>.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="fd1e5-142">2.9.1) aplicación hello en primer lugar debe describir Hola notificaciones toobe proporcionado y **obtener permiso de express del usuario de hello (OPC-in)**, y **debe proporcionar un mecanismo a través de qué Hola usuario puede optar por recibir notificaciones de inserción**.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="fd1e5-143">Todas las notificaciones que se proporciona mediante Hola servicio de notificaciones Push de Microsoft deben ser coherentes con hello descripción proporcionada toohello usuario y debe cumplir con todas las aplicables [las directivas de aplicación] [ Content Policies]y [requisitos adicionales para los tipos de aplicación específica].</span><span class="sxs-lookup"><span data-stu-id="fd1e5-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="fd1e5-144">No debería usar demasiadas notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-144">You should not use too many push notifications.</span></span> <span data-ttu-id="fd1e5-145">Engagement controlará las notificaciones por usted.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="fd1e5-146">2.9.2) aplicación hello y su uso del programa Hola a servicio de notificaciones Push de Microsoft deben no excesivamente usar ancho de banda de hello servicio de notificaciones Push de Microsoft o la capacidad de red, o en caso contrario, sobrecargar innecesariamente un Windows Phone u otros dispositivos de Microsoft o el servicio con excesivo push notificaciones, según lo determinado por Microsoft en el criterio razonable y no debe dañar ni interferir con las redes de Microsoft o servidores o los servidores de terceros o redes conectadas toohello servicio de notificaciones de inserción de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="fd1e5-147">No confíe en la información de MPNS toosend criticals.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="fd1e5-148">Interacción usa MPNS, por lo que esta regla también se aplica de las campañas de hello creadas dentro de hello interacción front-end.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="fd1e5-149">2.9.3) Hola servicio de notificaciones Push de Microsoft no puede ser toosend usado notificaciones que son de misión crítica o de otra manera podría afectar a cuestiones de vida o muerte, incluyendo pero sin las notificaciones críticas relacionadas tooa médicas limitador o condición.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="fd1e5-150">MICROSOFT expresamente rechaza cualquier garantía que Hola uso de hello MICROSOFT PUSH notificación servicio o entrega de MICROSOFT PUSH notificación servicio las notificaciones le puede sin interrupción, libre de errores, o en caso contrario garantiza tooOCCUR base en tiempo real de ON A.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="fd1e5-151">**No podemos garantizar que la aplicación pasará el proceso de validación de hello si no respeta estas recomendaciones.**</span><span class="sxs-lookup"><span data-stu-id="fd1e5-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="fd1e5-152">Control de la inserción de datos (opcional)</span><span class="sxs-lookup"><span data-stu-id="fd1e5-152">Handle data push (optional)</span></span>
<span data-ttu-id="fd1e5-153">Si desea que su inserciones de datos de aplicación toobe tooreceive capaz de alcance, deberá tooimplement dos eventos de hello EngagementReach clase:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="fd1e5-154">Puede ver esa devolución de llamada de Hola de cada método devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="fd1e5-155">Interacción envía un back-end de tooits de comentarios después de enviar la inserción de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="fd1e5-156">Si la devolución de llamada de hello devuelve false, Hola `exit` comentarios se estarán.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="fd1e5-157">De lo contrario, será `action`.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="fd1e5-158">Si no se establece ninguna devolución de llamada para los eventos de hello, Hola `drop` comentarios se devolverá tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="fd1e5-159">Interacción no es capaz de tooreceive opiniones de múltiplos para una inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="fd1e5-160">Si tiene previsto tooset varios controladores en un evento, tenga en cuenta que los comentarios de Hola corresponderá toohello penúltima enviado.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="fd1e5-161">En este caso, se recomienda tooalways devuelve Hola mismo tooavoid valor tener comentarios confuso en hello front-end.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="fd1e5-162">Personalizar la interfaz de usuario (opcional)</span><span class="sxs-lookup"><span data-stu-id="fd1e5-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="fd1e5-163">Primer paso</span><span class="sxs-lookup"><span data-stu-id="fd1e5-163">First step</span></span>
<span data-ttu-id="fd1e5-164">Le permitimos alcance de hello toocustomize interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="fd1e5-165">toodo por lo tanto, tiene una subclase de hello toocreate `EngagementReachHandler` clase.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="fd1e5-166">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="fd1e5-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="fd1e5-167">A continuación, establezca el contenido de Hola de hello `EngagementReach.Instance.Handler` campo con su objeto personalizado en su `App.xaml.cs` clase dentro de hello `Application_Launching` método.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="fd1e5-168">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="fd1e5-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="fd1e5-169">De forma predeterminada, Engagement usa su propia implementación de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="fd1e5-170">No tienes toocreate el suyo propio, y si lo hace, no tiene toooverride cada método.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="fd1e5-171">comportamiento predeterminado de Hello es objeto de base de tooselect Hola interacción.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="fd1e5-172">Diseños</span><span class="sxs-lookup"><span data-stu-id="fd1e5-172">Layouts</span></span>
<span data-ttu-id="fd1e5-173">De forma predeterminada, alcance usará recursos Hola incrustada de las notificaciones de hello DLL toodisplay hello y páginas.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="fd1e5-174">Sin embargo, puede decidir los toouse su propios recursos tooreflect su marca en estos componentes.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="fd1e5-175">Puede invalidar `EngagementReachHandler` métodos en su toouse de interacción de subclase tootell los diseños:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="fd1e5-176">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="fd1e5-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="fd1e5-177">Hola `CreateNotification` método puede devolver null.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="fd1e5-178">no se mostrarán notificaciones de Hola y campaña de cobertura de Hola se van a quitar.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="fd1e5-179">toosimplify su implementación de diseño, también proporcionamos nuestro propio xaml que puede servir como base para el código.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="fd1e5-180">Se encuentran en el archivo del SDK de interacción de hello (/ src/alcance /).</span><span class="sxs-lookup"><span data-stu-id="fd1e5-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="fd1e5-181">orígenes de Hola que ofrecemos son Hola exacto que mismo que utilizamos.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="fd1e5-182">Por lo que si desea toomodify ellos directamente, no olvide el espacio de nombres de toochange Hola y Hola nombre.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="fd1e5-183">Posición de notificación</span><span class="sxs-lookup"><span data-stu-id="fd1e5-183">Notification position</span></span>
<span data-ttu-id="fd1e5-184">De forma predeterminada, se muestra una notificación en la aplicación en hello parte inferior izquierda de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="fd1e5-185">Puede cambiar este comportamiento mediante la invalidación hello `GetNotificationPosition` método de hello `EngagementReachHandler` objeto.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="fd1e5-186">Actualmente, puede elegir entre hello `BOTTOM` (valor predeterminado) y `TOP` posiciones.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="fd1e5-187">Iniciar el mensaje</span><span class="sxs-lookup"><span data-stu-id="fd1e5-187">Launch message</span></span>
<span data-ttu-id="fd1e5-188">Cuando un usuario hace clic en una notificación del sistema (una notificación del sistema), inicia interacción Hola aplicación, carga Hola contenido de hello envíen mensajes y mostrar página Hola Hola correspondiente de la campaña.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="fd1e5-189">Hay un retraso entre el inicio de Hola de pantalla de hello y aplicación Hola de página hello (según la velocidad de saludo de la red).</span><span class="sxs-lookup"><span data-stu-id="fd1e5-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="fd1e5-190">usuario de toohello tooindicate que algo se está cargando, debe proporcionar una información visual, como una barra de progreso o un indicador de progreso.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="fd1e5-191">Engagement no puede controlar esto por sí solo, pero le ofrece algunos controladores para ello.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="fd1e5-192">tooimplement Hola de devolución de llamada, realice:</span><span class="sxs-lookup"><span data-stu-id="fd1e5-192">tooimplement hello callback, do:</span></span>

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

<span data-ttu-id="fd1e5-193">Puede establecer la devolución de llamada de hello en su `Application_Launching` método de su `App.xaml.cs` archivo, preferentemente antes de hello `EngagementReach.Instance.Init()` llamar.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="fd1e5-194">Hola subprocesos de interfaz de usuario llama a cada controlador.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="fd1e5-195">No es necesario tooworry cuando se utiliza un cuadro de mensajes o algo relacionado con la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="fd1e5-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[las directivas de aplicación]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisitos adicionales para los tipos de aplicación específica]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

