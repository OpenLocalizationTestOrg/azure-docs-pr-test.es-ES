---
title: "Integración del SDK de cobertura de Windows Phone Silverlight"
description: "Cómo integrar Cobertura de Azure Mobile Engagement con aplicaciones Windows Phone Silverlight"
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
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="16a1b-103">Integración del SDK de cobertura de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="16a1b-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="16a1b-104">Debe seguir el procedimiento de integración descrito en el documento [Integración del SDK de Windows Phone Silverlight Engagement](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir con esta guía.</span><span class="sxs-lookup"><span data-stu-id="16a1b-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="16a1b-105">Integrar el SDK de Engagement Reach en el proyecto de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="16a1b-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="16a1b-106">No hace falta agregar nada.</span><span class="sxs-lookup"><span data-stu-id="16a1b-106">You do not have anything to add.</span></span> <span data-ttu-id="16a1b-107">`EngagementReach` ya están en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="16a1b-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="16a1b-108">Puede personalizar las imágenes que se encuentran en la carpeta `Resources` del proyecto, especialmente el icono de marca (el valor predeterminado para el icono Engagement).</span><span class="sxs-lookup"><span data-stu-id="16a1b-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="16a1b-109">Agregar las capacidades</span><span class="sxs-lookup"><span data-stu-id="16a1b-109">Add the capabilities</span></span>
<span data-ttu-id="16a1b-110">El SDK de Engagement Reach necesita algunas capacidades adicionales.</span><span class="sxs-lookup"><span data-stu-id="16a1b-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="16a1b-111">Abra el archivo `WMAppManifest.xml` y asegúrese de que en el panel se han declarado las siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="16a1b-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="16a1b-112">El primero es usado por el servicio de MPNS para permitir la visualización de la notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="16a1b-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="16a1b-113">La segunda se usa para insertar una tarea de explorador en el SDK.</span><span class="sxs-lookup"><span data-stu-id="16a1b-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="16a1b-114">Edite el archivo `WMAppManifest.xml` y agréguelo dentro de la etiqueta `<Capabilities />`:</span><span class="sxs-lookup"><span data-stu-id="16a1b-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="16a1b-115">Habilitar el Servicio de notificaciones push de Microsoft</span><span class="sxs-lookup"><span data-stu-id="16a1b-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="16a1b-116">Para poder usar el **Servicio de notificaciones de inserción de Microsoft** (conocido como MPNS), el archivo `WMAppManifest.xml` debe tener una etiqueta `<App />` con un atributo `Publisher` establecido en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="16a1b-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="16a1b-117">Inicializar el SDK de Engagement Reach</span><span class="sxs-lookup"><span data-stu-id="16a1b-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="16a1b-118">Configuración de Engagement</span><span class="sxs-lookup"><span data-stu-id="16a1b-118">Engagement configuration</span></span>
<span data-ttu-id="16a1b-119">La configuración de Engagement se centraliza en el archivo `Resources\EngagementConfiguration.xml` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="16a1b-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="16a1b-120">Edite este archivo para especificar la configuración de Reach:</span><span class="sxs-lookup"><span data-stu-id="16a1b-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="16a1b-121">*Opcional*: indique si se debe activar la inserción nativa (MPNS) o no entre las etiquetas `<enableNativePush>` y `</enableNativePush>`, (`true` de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="16a1b-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="16a1b-122">*Opcional*: indique el nombre del canal de inserción entre las etiquetas `<channelName>` y `</channelName>` y proporcione el mismo nombre que usa la aplicación o deje el valor en blanco.</span><span class="sxs-lookup"><span data-stu-id="16a1b-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="16a1b-123">Si, en cambio, quiere especificarlo en tiempo de ejecución, puede llamar al método siguiente antes de la inicialización del agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="16a1b-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="16a1b-124">Puede especificar el nombre del canal de inserción de MPNS de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16a1b-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="16a1b-125">De forma predeterminada, Engagement crea un nombre basado en el appId.</span><span class="sxs-lookup"><span data-stu-id="16a1b-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="16a1b-126">No hace falta que especifique el nombre usted mismo, excepto si tiene previsto usar el canal de inserción fuera de Engagement.</span><span class="sxs-lookup"><span data-stu-id="16a1b-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="16a1b-127">Inicialización de Engagement</span><span class="sxs-lookup"><span data-stu-id="16a1b-127">Engagement initialization</span></span>
<span data-ttu-id="16a1b-128">Modifique `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="16a1b-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="16a1b-129">Agregue las instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="16a1b-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="16a1b-130">Inserte `EngagementReach.Instance.Init` justo después de `EngagementAgent.Instance.Init` en `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="16a1b-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="16a1b-131">Inserte `EngagementReach.Instance.OnActivated` en el método `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="16a1b-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="16a1b-132">`EngagementReach.Instance.Init` se ejecuta en un subproceso dedicado.</span><span class="sxs-lookup"><span data-stu-id="16a1b-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="16a1b-133">No es necesario que lo haga usted.</span><span class="sxs-lookup"><span data-stu-id="16a1b-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="16a1b-134">Consideraciones de envío de la tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="16a1b-134">App store submission considerations</span></span>
<span data-ttu-id="16a1b-135">Microsoft impone algunas reglas al usar las notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="16a1b-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="16a1b-136">De la documentación sobre las [directivas de aplicación] de Microsoft, sección 2.9:</span><span class="sxs-lookup"><span data-stu-id="16a1b-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="16a1b-137">Debe pedir al usuario que acepte recibir notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="16a1b-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="16a1b-138">A continuación, en la configuración, agregue una manera de deshabilitar las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="16a1b-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="16a1b-139">En el objeto EngagementReach se proporcionan dos métodos para administrar la participación o no participación, `EnableNativePush()` y `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="16a1b-140">Por ejemplo, podría crear una opción en la configuración con un control que permite deshabilitar o habilitar MPNS.</span><span class="sxs-lookup"><span data-stu-id="16a1b-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="16a1b-141">También puede decidir desactivar MPNS a través de la configuración de Engagement \<windows-phone-sdk-reach-configuration\>.</span><span class="sxs-lookup"><span data-stu-id="16a1b-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="16a1b-142">2.9.1) La aplicación primero debe describir las notificaciones que se proporcionarán y **obtener el permiso explícito del usuario (participar)**. Además, **debe proporcionar un mecanismo a través del cual el usuario puede optar por dejar de recibir las notificaciones de inserción**.</span><span class="sxs-lookup"><span data-stu-id="16a1b-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="16a1b-143">Todas las notificaciones que se proporcionan mediante el Servicio de notificaciones de inserción de Microsoft deben ser coherentes con la descripción que se proporciona al usuario y deben cumplir con todas las [directivas de aplicación][Content Policies] y [requisitos adicionales para tipos específicos de aplicación vigentes].</span><span class="sxs-lookup"><span data-stu-id="16a1b-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="16a1b-144">No debería usar demasiadas notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="16a1b-144">You should not use too many push notifications.</span></span> <span data-ttu-id="16a1b-145">Engagement controlará las notificaciones por usted.</span><span class="sxs-lookup"><span data-stu-id="16a1b-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="16a1b-146">2.9.2) La aplicación y el uso que hace del Servicio de notificaciones de inserción de Microsoft no deben usar excesivamente la capacidad de la red o el ancho de banda del Servicio de notificaciones de inserción de Microsoft. Tampoco deben sobrecargar innecesariamente un dispositivo Windows Phone u otro dispositivo o servicio de Microsoft con notificaciones de inserción excesivas, según determine Microsoft bajo su razonable criterio, ni dañar las redes o los servidores de Microsoft, los servidores de terceros o las redes conectadas al Servicio de notificaciones de inserción de Microsoft, ni interferir con ellos.</span><span class="sxs-lookup"><span data-stu-id="16a1b-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="16a1b-147">No confíe en MPNS para enviar información crítica.</span><span class="sxs-lookup"><span data-stu-id="16a1b-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="16a1b-148">Engagement usa MPNS, por lo que esta regla también se aplica a las campañas que se crean en el front-end de Engagement.</span><span class="sxs-lookup"><span data-stu-id="16a1b-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="16a1b-149">2.9.3) El Servicio de notificaciones de inserción de Microsoft no se puede usar para enviar notificaciones de misión crítica o que de otro modo podrían afectar a asuntos de vida o muerte, incluidas, sin limitación, las notificaciones críticas relacionadas con un dispositivo o condición médicos.</span><span class="sxs-lookup"><span data-stu-id="16a1b-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="16a1b-150">MICROSOFT RENUNCIA A TODA GARANTÍA QUE EL USO DEL SERVICIO DE NOTIFICACIONES PUSH DE MICROSOFT O LA ENTREGA DE NOTIFICACIONES DEL SERVICIO DE NOTIFICACIONES PUSH DE MICROSOFT SE HARÁN SIN INTERRUPCIONES, SEAN LIBRE DE ERRORES O DE OTRO MODO SE GARANTICE QUE SE PRODUCIRÁN EN TIEMPO REAL.</span><span class="sxs-lookup"><span data-stu-id="16a1b-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="16a1b-151">**No podemos garantizar que la aplicación aprobará el proceso de validación si no se respetan estas recomendaciones.**</span><span class="sxs-lookup"><span data-stu-id="16a1b-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="16a1b-152">Control de la inserción de datos (opcional)</span><span class="sxs-lookup"><span data-stu-id="16a1b-152">Handle data push (optional)</span></span>
<span data-ttu-id="16a1b-153">Si desea que la aplicación pueda recibir inserciones de datos Reach, debe implementar dos eventos de la clase EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="16a1b-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

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

<span data-ttu-id="16a1b-154">Puede ver que la devolución de llamada de cada método devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="16a1b-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="16a1b-155">Engagement envía un comentario a su back-end después de enviar la inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="16a1b-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="16a1b-156">Si la devolución de llamada devuelve un valor falso, se enviará el comentario `exit` .</span><span class="sxs-lookup"><span data-stu-id="16a1b-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="16a1b-157">De lo contrario, será `action`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="16a1b-158">Si no se establece ninguna devolución de llamada para los eventos, el comentario `drop` se devolverá a Engagement.</span><span class="sxs-lookup"><span data-stu-id="16a1b-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="16a1b-159">Engagement no puede recibir varios comentarios para la inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="16a1b-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="16a1b-160">Si tiene previsto establecer varios controladores en un evento, tenga en cuenta que los comentarios corresponderán al último controlador enviado.</span><span class="sxs-lookup"><span data-stu-id="16a1b-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="16a1b-161">En este caso, es recomendable devolver siempre el mismo valor para evitar tener comentarios confusos en el front-end.</span><span class="sxs-lookup"><span data-stu-id="16a1b-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="16a1b-162">Personalizar la interfaz de usuario (opcional)</span><span class="sxs-lookup"><span data-stu-id="16a1b-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="16a1b-163">Primer paso</span><span class="sxs-lookup"><span data-stu-id="16a1b-163">First step</span></span>
<span data-ttu-id="16a1b-164">Puede personalizar la interfaz de usuario de Reach.</span><span class="sxs-lookup"><span data-stu-id="16a1b-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="16a1b-165">Para ello, debe crear una subclase de la clase `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="16a1b-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="16a1b-166">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="16a1b-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="16a1b-167">A continuación, establezca el contenido del campo `EngagementReach.Instance.Handler` con el objeto personalizado en la clase `App.xaml.cs` del método `Application_Launching`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="16a1b-168">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="16a1b-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="16a1b-169">De forma predeterminada, Engagement usa su propia implementación de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="16a1b-170">No hace falta crear elementos propios. Si lo hace, tiene que invalidar todos los métodos.</span><span class="sxs-lookup"><span data-stu-id="16a1b-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="16a1b-171">El comportamiento predeterminado consiste en seleccionar el objeto base de Engagement.</span><span class="sxs-lookup"><span data-stu-id="16a1b-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="16a1b-172">Diseños</span><span class="sxs-lookup"><span data-stu-id="16a1b-172">Layouts</span></span>
<span data-ttu-id="16a1b-173">De forma predeterminada, Reach usará los recursos integrados del archivo DLL para mostrar las notificaciones y páginas.</span><span class="sxs-lookup"><span data-stu-id="16a1b-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="16a1b-174">Sin embargo, puede decidir usar sus propios recursos para reflejar su marca en estos componentes.</span><span class="sxs-lookup"><span data-stu-id="16a1b-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="16a1b-175">Puede invalidar los métodos `EngagementReachHandler` en la subclase para indicar a Engagement que debe usar sus diseños:</span><span class="sxs-lookup"><span data-stu-id="16a1b-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="16a1b-176">**Código de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="16a1b-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="16a1b-177">El método `CreateNotification` puede devolver un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="16a1b-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="16a1b-178">La notificación no se mostrará y se quitará la campaña de Reach.</span><span class="sxs-lookup"><span data-stu-id="16a1b-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="16a1b-179">Para simplificar la implementación del diseño, también proporcionamos nuestro propio xaml que puede servir como base para el código.</span><span class="sxs-lookup"><span data-stu-id="16a1b-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="16a1b-180">Estos códigos se encuentran en el archivo de SDK de Engagement (/src/reach/).</span><span class="sxs-lookup"><span data-stu-id="16a1b-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="16a1b-181">Los orígenes que proporcionamos son los mismos que usamos.</span><span class="sxs-lookup"><span data-stu-id="16a1b-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="16a1b-182">Por lo tanto, si desea modificarlos directamente, no olvide cambiar el espacio de nombres y el nombre.</span><span class="sxs-lookup"><span data-stu-id="16a1b-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="16a1b-183">Posición de notificación</span><span class="sxs-lookup"><span data-stu-id="16a1b-183">Notification position</span></span>
<span data-ttu-id="16a1b-184">De forma predeterminada, una notificación de la aplicación se muestra en la parte inferior izquierda de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16a1b-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="16a1b-185">Puede cambiar este comportamiento al invalidar el método `GetNotificationPosition` del objeto `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="16a1b-186">Actualmente, puede elegir entre las posiciones `BOTTOM` (valor predeterminado) y `TOP`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="16a1b-187">Iniciar el mensaje</span><span class="sxs-lookup"><span data-stu-id="16a1b-187">Launch message</span></span>
<span data-ttu-id="16a1b-188">Cuando un usuario hace clic en una notificación del sistema, Engagement inicia la aplicación, carga el contenido de los mensajes de inserción y muestra la página de la campaña correspondiente.</span><span class="sxs-lookup"><span data-stu-id="16a1b-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="16a1b-189">Hay un retraso entre el inicio de la aplicación y la presentación de la página (según la velocidad de la red).</span><span class="sxs-lookup"><span data-stu-id="16a1b-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="16a1b-190">Para indicar al usuario que algo se está cargando, debería proporcionar algún tipo de información visual, tal como una barra de progreso o un indicador de progreso.</span><span class="sxs-lookup"><span data-stu-id="16a1b-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="16a1b-191">Engagement no puede controlar esto por sí solo, pero le ofrece algunos controladores para ello.</span><span class="sxs-lookup"><span data-stu-id="16a1b-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="16a1b-192">Para implementar la devolución de llamada, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="16a1b-192">To implement the callback, do:</span></span>

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

<span data-ttu-id="16a1b-193">Puede establecer la devolución de llamada en el método `Application_Launching` del archivo `App.xaml.cs`, preferentemente antes de la llamada `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="16a1b-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="16a1b-194">A cada controlador lo llama el subproceso de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="16a1b-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="16a1b-195">No tiene que preocuparse cuando se usa un objeto MessageBox u otro elemento relacionado con la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="16a1b-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

<span data-ttu-id="16a1b-196">[directivas de aplicación]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="16a1b-196">[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span></span>
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
<span data-ttu-id="16a1b-197">[requisitos adicionales para tipos específicos de aplicación vigentes]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="16a1b-197">[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span></span>

