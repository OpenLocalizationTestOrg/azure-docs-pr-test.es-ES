---
title: "aaaRegistration administración"
description: "Este tema explica cómo los dispositivos tooregister con centros de notificaciones en orden tooreceive notificaciones de inserción."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="d7486-103">Administración de registros</span><span class="sxs-lookup"><span data-stu-id="d7486-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="d7486-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d7486-104">Overview</span></span>
<span data-ttu-id="d7486-105">Este tema explica cómo los dispositivos tooregister con centros de notificaciones en orden tooreceive notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="d7486-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="d7486-106">tema de Hello describe los registros en un nivel superior y luego presenta Hola dos patrones principales para registrar dispositivos: registro desde dispositivo Hola directamente toohello centro de notificaciones y registro mediante un aplicación de back-end.</span><span class="sxs-lookup"><span data-stu-id="d7486-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="d7486-107">Qué es el registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="d7486-107">What is device registration</span></span>
<span data-ttu-id="d7486-108">El registro de dispositivos en un Centro de notificaciones se logra mediante un **Registro** o una **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="d7486-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="d7486-109">Registros</span><span class="sxs-lookup"><span data-stu-id="d7486-109">Registrations</span></span>
<span data-ttu-id="d7486-110">Un registro asocia Hola controlar el servicio de notificación de plataforma (PNS) para un dispositivo con etiquetas y, posiblemente, una plantilla.</span><span class="sxs-lookup"><span data-stu-id="d7486-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="d7486-111">controlador de PNS Hola podría ser un URI del canal, el token del dispositivo o el Id. del registro GCM. Las etiquetas son las notificaciones de tooroute usado toohello conjunto correcto de controladores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7486-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="d7486-112">Para obtener más información, consulte [Expresiones de etiqueta y enrutamiento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="d7486-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="d7486-113">Las plantillas son tooimplement usado por registro transformación.</span><span class="sxs-lookup"><span data-stu-id="d7486-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="d7486-114">Para obtener más información, consulte [Plantillas](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d7486-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="d7486-115">Instalaciones</span><span class="sxs-lookup"><span data-stu-id="d7486-115">Installations</span></span>
<span data-ttu-id="d7486-116">Una Instalación es un registro mejorado que incluye un conjunto de propiedades relacionadas con la inserción.</span><span class="sxs-lookup"><span data-stu-id="d7486-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="d7486-117">Es Hola tooregistering enfoque mejor y más recientes de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7486-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="d7486-118">Sin embargo, aún no es compatible con el SDK para .NET del cliente ([SDK del centro de notificaciones para operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).</span><span class="sxs-lookup"><span data-stu-id="d7486-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="d7486-119">Esto significa que si va a registrar en el propio dispositivo de cliente hello, tendría hello toouse [API de REST de centros de notificaciones](https://msdn.microsoft.com/library/mt621153.aspx) enfocar toosupport instalaciones.</span><span class="sxs-lookup"><span data-stu-id="d7486-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="d7486-120">Si usas un servicio back-end, debe ser capaz de toouse [SDK de concentrador de notificación para las operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d7486-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="d7486-121">continuación de Hola se muestran algunas instalaciones de toousing de las principales ventajas:</span><span class="sxs-lookup"><span data-stu-id="d7486-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="d7486-122">Crear o actualizar una instalación es completamente idempotente.</span><span class="sxs-lookup"><span data-stu-id="d7486-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="d7486-123">Por lo tanto, puede volver a intentarla sin preocuparse de obtener registros duplicados.</span><span class="sxs-lookup"><span data-stu-id="d7486-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="d7486-124">el modelo de instalación de Hello, es fácil toodo individuales inserciones - dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="d7486-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="d7486-125">Una etiqueta de instalación **"$InstallationId:[IdentificadordeInstalación]"** se crea automáticamente con cada registro basado en instalación.</span><span class="sxs-lookup"><span data-stu-id="d7486-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="d7486-126">Por lo que puede llamar a un tootarget de etiqueta de envío toothis un dispositivo específico sin necesidad de toodo ninguna codificación adicional.</span><span class="sxs-lookup"><span data-stu-id="d7486-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="d7486-127">Usar las instalaciones, también permite actualizaciones parciales de registro toodo.</span><span class="sxs-lookup"><span data-stu-id="d7486-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="d7486-128">actualización parcial de una instalación Hello se solicita una con un método de revisión con hello [estándar de JSON-Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="d7486-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="d7486-129">Esto es especialmente útil cuando se desea tooupdate etiquetas en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="d7486-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="d7486-130">No tiene toopull hacia abajo el registro completo de Hola y vuelva a enviar todas las etiquetas anteriores Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="d7486-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="d7486-131">Una instalación puede contener Hola Hola propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="d7486-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="d7486-132">Para obtener una lista completa de hello, vea Propiedades instalación [crear o sobrescribir una instalación con la API de REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) o [propiedades de instalación](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para saludo.</span><span class="sxs-lookup"><span data-stu-id="d7486-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="d7486-133">Es importante toonote que ya no expiran los registros y las instalaciones de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d7486-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="d7486-134">Los registros y las instalaciones deben contener un controlador PNS válido para cada dispositivo o canal.</span><span class="sxs-lookup"><span data-stu-id="d7486-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="d7486-135">Dado que solo se pueden obtener controladores de PNS en una aplicación de cliente en el dispositivo de hello, un patrón de es tooregister directamente en ese dispositivo con la aplicación de cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="d7486-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="d7486-136">Hola otros mano, consideraciones de seguridad y lógica de negocios relacionan tootags podría requerir que el registro de dispositivos toomanage en hello aplicación back-end.</span><span class="sxs-lookup"><span data-stu-id="d7486-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="d7486-137">Plantillas</span><span class="sxs-lookup"><span data-stu-id="d7486-137">Templates</span></span>
<span data-ttu-id="d7486-138">Si desea que toouse [plantillas](notification-hubs-templates-cross-platform-push-messages.md), instalación de dispositivo de hello también contener todas las plantillas asociadas con ese dispositivo en JSON de formato (vea el ejemplo anterior).</span><span class="sxs-lookup"><span data-stu-id="d7486-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="d7486-139">Hello plantilla nombres ayudan a dirigirse a varias plantillas para hello mismo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7486-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="d7486-140">Tenga en cuenta que cada nombre de plantilla asigna tooa cuerpo de plantilla y un conjunto opcional de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d7486-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="d7486-141">Además, cada plataforma puede tener propiedades de plantilla adicionales.</span><span class="sxs-lookup"><span data-stu-id="d7486-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="d7486-142">Tienda de Windows (mediante WNS) y Windows Phone 8 (mediante MPNS), un conjunto adicional de encabezados puede formar parte de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="d7486-143">En caso de hello de APN, puede establecer una tooeither de expiración propiedad una expresión de plantilla constante o tooa.</span><span class="sxs-lookup"><span data-stu-id="d7486-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="d7486-144">Para obtener una lista completa de hello, vea Propiedades instalación [crear o sobrescribir una instalación con REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="d7486-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="d7486-145">Iconos secundarios de Aplicaciones de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="d7486-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="d7486-146">Para las aplicaciones de cliente de tienda Windows, enviar notificaciones es toosecondary iconos Hola mismo que enviarlos toohello principal.</span><span class="sxs-lookup"><span data-stu-id="d7486-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="d7486-147">Esto también se admite en las instalaciones.</span><span class="sxs-lookup"><span data-stu-id="d7486-147">This is also supported in installations.</span></span> <span data-ttu-id="d7486-148">Tenga en cuenta que los iconos secundarios tienen un URI de canal diferentes, qué Hola SDK en la aplicación cliente se controla de manera transparente.</span><span class="sxs-lookup"><span data-stu-id="d7486-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="d7486-149">Hola SecondaryTiles diccionario usa Hola mismo TileId que es objeto de SecondaryTiles de hello toocreate usado en la aplicación tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="d7486-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="d7486-150">Como con hello URI principal, ChannelUris de iconos secundarios puede cambiar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="d7486-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="d7486-151">En orden tookeep hello las instalaciones en el centro de notificaciones de hello actualizado, Hola dispositivo debe actualizarlos con hello ChannelUris actuales de iconos secundarios Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="d7486-152">Administración de registros desde dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="d7486-152">Registration management from hello device</span></span>
<span data-ttu-id="d7486-153">Cuando se administra el registro de dispositivos desde aplicaciones cliente, Hola back-end solamente es responsable de enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d7486-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="d7486-154">Las aplicaciones cliente de mantener los controladores de PNS una toodate y registran etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d7486-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="d7486-155">Hola siguiente muestra este modelo.</span><span class="sxs-lookup"><span data-stu-id="d7486-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="d7486-156">dispositivo Hola primero recupera Hola controlador de PNS de hello PNS, a continuación, registra directamente con el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="d7486-157">Después de que el registro de hello es correcto, Hola backend de la aplicación puede enviar una notificación dirigida a ese tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="d7486-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="d7486-158">Para obtener más información acerca de cómo toosend notificaciones, consulte [enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="d7486-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="d7486-159">Tenga en cuenta que en este caso, usará sólo escuche derechos tooaccess sus centros de notificaciones de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="d7486-160">Para obtener más información, consulte [Seguridad](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="d7486-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="d7486-161">Registro desde dispositivo hello es el método más sencillo de hello, pero tiene algunas desventajas.</span><span class="sxs-lookup"><span data-stu-id="d7486-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="d7486-162">Hola primera desventaja es que una aplicación cliente solo puede actualizar sus etiquetas cuando la aplicación hello está activo.</span><span class="sxs-lookup"><span data-stu-id="d7486-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="d7486-163">Por ejemplo, si un usuario tiene dos dispositivos que registran etiquetas relacionadas toosport equipos, al primer dispositivo de Hola se registra para una etiqueta adicional (por ejemplo, Seahawks), Hola segundo dispositivo no recibirá notificaciones de hello sobre hello Seahawks hasta que la aplicación hello en hello segundo dispositivo se ejecuta una segunda vez.</span><span class="sxs-lookup"><span data-stu-id="d7486-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="d7486-164">Por lo general, cuando las etiquetas se ven afectadas por los distintos dispositivos, administrar etiquetas de hello back-end es una opción conveniente.</span><span class="sxs-lookup"><span data-stu-id="d7486-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="d7486-165">segunda desventaja de Hello de la administración de registros desde la aplicación de cliente de hello es que, puesto que las aplicaciones podrían prestarse a intrusiones, protección de registro de hello toospecific etiquetas requiere especial atención, como se explica en la sección de Hola "seguridad de nivel de la etiqueta".</span><span class="sxs-lookup"><span data-stu-id="d7486-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="d7486-166">Tooregister de código de ejemplo con un centro de notificaciones desde un dispositivo mediante una instalación</span><span class="sxs-lookup"><span data-stu-id="d7486-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="d7486-167">En este momento, solo se admite con hello [API de REST de centros de notificación](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7486-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="d7486-168">También puede utilizar el método de revisión de hello mediante hello [estándar de JSON-Patch](https://tools.ietf.org/html/rfc6902) para actualizar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="d7486-169">Tooregister de código de ejemplo con un centro de notificaciones desde un dispositivo mediante un registro</span><span class="sxs-lookup"><span data-stu-id="d7486-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="d7486-170">Estos métodos crean o actualizan un registro para el dispositivo de hello en el que se llamó.</span><span class="sxs-lookup"><span data-stu-id="d7486-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="d7486-171">Esto significa que, en orden tooupdate Hola Hola o identificador de etiquetas, debe sobrescribir registro completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="d7486-172">Recuerde que los registros son transitorios, por lo que siempre debe tener un almacén confiable con etiquetas actuales de Hola que necesita un determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7486-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="d7486-173">Administración de registros desde un back-end</span><span class="sxs-lookup"><span data-stu-id="d7486-173">Registration management from a backend</span></span>
<span data-ttu-id="d7486-174">La administración de registros de back-end de hello, es necesario escribir código adicional.</span><span class="sxs-lookup"><span data-stu-id="d7486-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="d7486-175">la aplicación Hello de dispositivo de hello debe proporcionar Hola actualizada PNS identificador toohello back-end cada vez inicia la aplicación hello (junto con etiquetas y plantillas) y Hola back-end debe actualizar este controlador en el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="d7486-176">Hola después de la imagen muestra este diseño.</span><span class="sxs-lookup"><span data-stu-id="d7486-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="d7486-177">las ventajas de Hola de administrar los registros de back-end de hello incluyen hello capacidad toomodify etiquetas tooregistrations incluso cuando la aplicación correspondiente hello en dispositivo Hola está inactiva y aplicación de cliente hello tooauthenticate antes de agregar un registro de tooits de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d7486-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="d7486-178">Tooregister de código de ejemplo con un centro de notificaciones desde un back-end mediante la instalación</span><span class="sxs-lookup"><span data-stu-id="d7486-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="d7486-179">dispositivo de cliente de Hola todavía obtiene su controlador de PNS y propiedades de instalación pertinentes como antes y llamadas a una API personalizada en el back-end de Hola que puede realizar el registro de hello y autorizar etiquetas back-end de etc. Hola pueden aprovechar hello [SDK de concentrador de notificación para operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d7486-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="d7486-180">También puede utilizar el método de revisión de hello mediante hello [estándar de JSON-Patch](https://tools.ietf.org/html/rfc6902) para actualizar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7486-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="d7486-181">Tooregister de código de ejemplo con un centro de notificaciones desde un dispositivo mediante un identificador de registro</span><span class="sxs-lookup"><span data-stu-id="d7486-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="d7486-182">Desde el back-end de la aplicación, puede ejecutar operaciones de tipo CRUD en los registros.</span><span class="sxs-lookup"><span data-stu-id="d7486-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="d7486-183">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d7486-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="d7486-184">Hola back-end debe controlar la simultaneidad entre las actualizaciones de registro.</span><span class="sxs-lookup"><span data-stu-id="d7486-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="d7486-185">Bus de servicio ofrece un control de simultaneidad optimista para la administración de registros.</span><span class="sxs-lookup"><span data-stu-id="d7486-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="d7486-186">En el nivel de hello HTTP, esto se implementa con el uso de Hola de ETag en operaciones de administración de registros.</span><span class="sxs-lookup"><span data-stu-id="d7486-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="d7486-187">Los SDK de Microsoft utilizan esta característica de manera transparente y generan una excepción si se rechaza una actualización por motivos de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d7486-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="d7486-188">aplicación de Hello back-end es responsable de controlar estas excepciones y volver a intentar la actualización de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="d7486-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

