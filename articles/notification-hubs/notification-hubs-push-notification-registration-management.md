---
title: "Administración de registros"
description: "En este tema se explica cómo registrar dispositivos en los centros de notificaciones para recibir notificaciones push."
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
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="19746-103">Administración de registros</span><span class="sxs-lookup"><span data-stu-id="19746-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="19746-104">Información general</span><span class="sxs-lookup"><span data-stu-id="19746-104">Overview</span></span>
<span data-ttu-id="19746-105">En este tema se explica cómo registrar dispositivos en los centros de notificaciones para recibir notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="19746-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="19746-106">El tema describe los registros en un alto nivel y, luego, presenta los dos patrones principales para registrar dispositivos: el registro desde el dispositivo directamente al centro de notificaciones y el registro a través de un back-end de aplicación.</span><span class="sxs-lookup"><span data-stu-id="19746-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="19746-107">Qué es el registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="19746-107">What is device registration</span></span>
<span data-ttu-id="19746-108">El registro de dispositivos en un Centro de notificaciones se logra mediante un **Registro** o una **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="19746-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="19746-109">Registros</span><span class="sxs-lookup"><span data-stu-id="19746-109">Registrations</span></span>
<span data-ttu-id="19746-110">Un registro asocia el identificador del Servicio de notificación de plataforma (PNS) de un dispositivo con etiquetas y, posiblemente, una plantilla.</span><span class="sxs-lookup"><span data-stu-id="19746-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="19746-111">El identificador del PNS puede ser un ChannelURI, un token de dispositivo o un identificador de registro de GCM.</span><span class="sxs-lookup"><span data-stu-id="19746-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="19746-112">Las etiquetas se usan para enrutar las notificaciones al conjunto correcto de identificadores de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="19746-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="19746-113">Para obtener más información, consulte [Expresiones de etiqueta y enrutamiento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="19746-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="19746-114">Se utilizan plantillas para implementar la transformación por registro.</span><span class="sxs-lookup"><span data-stu-id="19746-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="19746-115">Para obtener más información, consulte [Plantillas](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="19746-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="19746-116">Instalaciones</span><span class="sxs-lookup"><span data-stu-id="19746-116">Installations</span></span>
<span data-ttu-id="19746-117">Una Instalación es un registro mejorado que incluye un conjunto de propiedades relacionadas con la inserción.</span><span class="sxs-lookup"><span data-stu-id="19746-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="19746-118">Sin embargo, es el mejor y más reciente enfoque al registro de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="19746-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="19746-119">Sin embargo, aún no es compatible con el SDK para .NET del cliente ([SDK del centro de notificaciones para operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).</span><span class="sxs-lookup"><span data-stu-id="19746-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="19746-120">Esto significa que si registra desde el propio dispositivo cliente, tendría que usar el enfoque [API de REST de Centros de notificaciones](https://msdn.microsoft.com/library/mt621153.aspx) para admitir las instalaciones.</span><span class="sxs-lookup"><span data-stu-id="19746-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="19746-121">Si usa un servicio back-end, debe ser capaz de usar el [SDK del Centro de notificaciones para las operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="19746-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="19746-122">Las siguientes son algunas ventajas clave de usar las instalaciones:</span><span class="sxs-lookup"><span data-stu-id="19746-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="19746-123">Crear o actualizar una instalación es completamente idempotente.</span><span class="sxs-lookup"><span data-stu-id="19746-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="19746-124">Por lo tanto, puede volver a intentarla sin preocuparse de obtener registros duplicados.</span><span class="sxs-lookup"><span data-stu-id="19746-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="19746-125">El modelo de instalación facilita la realización de inserciones individuales, orientándose a un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="19746-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="19746-126">Una etiqueta de instalación **"$InstallationId:[IdentificadordeInstalación]"** se crea automáticamente con cada registro basado en instalación.</span><span class="sxs-lookup"><span data-stu-id="19746-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="19746-127">Por lo tanto, puede llamar un envío a esta etiqueta para orientarse a un dispositivo específico sin tener que realizar ninguna codificación adicional.</span><span class="sxs-lookup"><span data-stu-id="19746-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="19746-128">El uso de las instalaciones también le permite realizar actualizaciones parciales de registros.</span><span class="sxs-lookup"><span data-stu-id="19746-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="19746-129">La actualización parcial de una instalación se solicita con un método PATCH a través del [estándar JSON-Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="19746-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="19746-130">Esto resulta especialmente útil cuando desea actualizar las etiquetas del registro.</span><span class="sxs-lookup"><span data-stu-id="19746-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="19746-131">No es necesario desplegar todo el registro y reenviar todas las etiquetas anteriores.</span><span class="sxs-lookup"><span data-stu-id="19746-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="19746-132">Una instalación puede contener las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="19746-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="19746-133">Para ver una lista completa de las propiedades de instalación, vea [Creación o sobrescritura de una instalación con API de REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) o [Installation (propiedades)](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="19746-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
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



<span data-ttu-id="19746-134">Es importante tener en cuenta que los registros y las instalaciones, de forma predeterminada, ya no expiran.</span><span class="sxs-lookup"><span data-stu-id="19746-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="19746-135">Los registros y las instalaciones deben contener un controlador PNS válido para cada dispositivo o canal.</span><span class="sxs-lookup"><span data-stu-id="19746-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="19746-136">Debido a que los identificadores de PNS solo se pueden obtener en una aplicación cliente del dispositivo, un patrón es registrarse directamente en ese dispositivo con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="19746-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="19746-137">Por otro lado, las consideraciones de seguridad y la lógica de negocios relacionadas con las etiquetas pueden requerir que administre el registro de dispositivos en el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19746-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="19746-138">Plantillas</span><span class="sxs-lookup"><span data-stu-id="19746-138">Templates</span></span>
<span data-ttu-id="19746-139">Si desea usar [Plantillas](notification-hubs-templates-cross-platform-push-messages.md), la instalación de dispositivo también contiene todas las plantillas asociadas con ese dispositivo en un formato JSON (consulte el ejemplo anterior).</span><span class="sxs-lookup"><span data-stu-id="19746-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="19746-140">Los nombres de las plantillas ayudan a dirigirse a distintas plantillas para el mismo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="19746-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="19746-141">Observe que cada nombre de plantilla está asignado al cuerpo de una plantilla y a un conjunto opcional de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="19746-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="19746-142">Además, cada plataforma puede tener propiedades de plantilla adicionales.</span><span class="sxs-lookup"><span data-stu-id="19746-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="19746-143">En el caso de Tienda Windows (con WNS) y Windows Phone 8 (con MPNS), un conjunto de encabezados adicional puede formar parte de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="19746-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="19746-144">En el caso de APNs, puede establecer una propiedad de expiración en una constante o en una expresión de plantilla.</span><span class="sxs-lookup"><span data-stu-id="19746-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="19746-145">Para obtener una lista completa de las propiedades de la instalación, consulte el tema [Creación o sobrescritura de una instalación con REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) .</span><span class="sxs-lookup"><span data-stu-id="19746-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="19746-146">Iconos secundarios de Aplicaciones de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="19746-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="19746-147">En el caso de las aplicaciones cliente de la Tienda Windows, enviar notificaciones a los iconos secundarios es igual que enviarlos al icono principal.</span><span class="sxs-lookup"><span data-stu-id="19746-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="19746-148">Esto también se admite en las instalaciones.</span><span class="sxs-lookup"><span data-stu-id="19746-148">This is also supported in installations.</span></span> <span data-ttu-id="19746-149">Tenga en cuenta que los iconos secundarios tienen un ChannelUri distinto, que el SDK de la aplicación cliente administra sin problemas.</span><span class="sxs-lookup"><span data-stu-id="19746-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="19746-150">El diccionario SecondaryTiles utiliza el mismo TileId que se usa para crear el objeto SecondaryTiles en la aplicación de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="19746-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="19746-151">Al igual que lo que ocurre con el ChannelUri principal, los ChannelUri de los iconos secundarios pueden cambiar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="19746-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="19746-152">Para mantener actualizadas las instalaciones en el centro de notificaciones, el dispositivo debe actualizarlas con los ChannelUri actuales de los iconos secundarios.</span><span class="sxs-lookup"><span data-stu-id="19746-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="19746-153">Administración de registros desde el dispositivo</span><span class="sxs-lookup"><span data-stu-id="19746-153">Registration management from the device</span></span>
<span data-ttu-id="19746-154">Cuando administra el registro del dispositivo desde las aplicaciones cliente, el back-end es el único responsable de enviar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="19746-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="19746-155">Las aplicaciones cliente mantienen actualizados los identificadores de PNS y registran las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="19746-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="19746-156">La siguiente ilustración muestra este patrón.</span><span class="sxs-lookup"><span data-stu-id="19746-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="19746-157">El dispositivo primero recupera el identificador de PNS desde el PSN y, luego, se registra directamente con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="19746-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="19746-158">Una vez que el registro se realiza correctamente, el back-end de la aplicación puede enviar una notificación orientada a ese registro.</span><span class="sxs-lookup"><span data-stu-id="19746-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="19746-159">Para obtener más información sobre cómo enviar notificaciones, consulte [Expresiones de etiqueta y enrutamiento](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="19746-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="19746-160">Tenga en cuenta que, en este caso, solo usará derechos de escucha para tener acceso a los centros de notificaciones desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="19746-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="19746-161">Para obtener más información, consulte [Seguridad](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="19746-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="19746-162">El registro desde el dispositivo es el método más sencillo, pero presenta algunos inconvenientes.</span><span class="sxs-lookup"><span data-stu-id="19746-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="19746-163">La primera desventaja es que una aplicación cliente solo puede actualizar sus etiquetas cuando la aplicación está activa.</span><span class="sxs-lookup"><span data-stu-id="19746-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="19746-164">Por ejemplo, si un usuario tiene dos dispositivos que registran las etiquetas relacionadas con equipos deportivos, cuando el primer dispositivo registra una etiqueta adicional (por ejemplo, Seahawks), el segundo dispositivo no recibirá las notificaciones sobre los Seahawks hasta que la aplicación del segundo dispositivo se ejecute por segunda vez.</span><span class="sxs-lookup"><span data-stu-id="19746-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="19746-165">De manera más general, cuando son varios los dispositivos que afectan las etiquetas, la administración de estas desde el back-end es una opción conveniente.</span><span class="sxs-lookup"><span data-stu-id="19746-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="19746-166">La segunda desventaja de la administración de registros desde la aplicación cliente es que, debido a que es posible piratear las aplicaciones, proteger el registro de etiquetas específicas requiere un cuidado adicional, tal como se explica en la sección "Seguridad a nivel de etiqueta".</span><span class="sxs-lookup"><span data-stu-id="19746-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="19746-167">Ejemplo de código para el registro en un centro de notificaciones desde un dispositivo con una instalación</span><span class="sxs-lookup"><span data-stu-id="19746-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="19746-168">En este momento, esta opción solo es compatible si se usa la [API de REST de Centros de notificaciones](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="19746-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="19746-169">También puede utilizar el método PATCH con el [estándar JSON-Patch](https://tools.ietf.org/html/rfc6902) para actualizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="19746-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

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

        // Determine the targetUri that we will sign
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



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="19746-170">Ejemplo de código para el registro en un centro de notificaciones desde un dispositivo con un registro</span><span class="sxs-lookup"><span data-stu-id="19746-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="19746-171">Estos métodos crean o actualizan un registro para el dispositivo en el que se los llamaron.</span><span class="sxs-lookup"><span data-stu-id="19746-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="19746-172">Esto significa que, para actualizar el identificador o las etiquetas, debe sobrescribir todo el registro.</span><span class="sxs-lookup"><span data-stu-id="19746-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="19746-173">Recuerde que los registros son transitorios, por lo que siempre debe tener un almacenamiento confiable con las etiquetas actuales que necesita un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="19746-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="19746-174">Administración de registros desde un back-end</span><span class="sxs-lookup"><span data-stu-id="19746-174">Registration management from a backend</span></span>
<span data-ttu-id="19746-175">Administrar los registros desde el back-end requiere escribir código adicional.</span><span class="sxs-lookup"><span data-stu-id="19746-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="19746-176">La aplicación del dispositivo debe proporcionar el identificador de PNS actualizado al back-end cada vez que se inicie la aplicación (junto con las etiquetas y las plantillas) y, además, el back-end debe actualizar este identificador en el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="19746-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="19746-177">La siguiente ilustración muestra este diseño.</span><span class="sxs-lookup"><span data-stu-id="19746-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="19746-178">Las ventajas que presenta la administración de registros desde el back-end incluyen la capacidad de modificar etiquetas de los registros, incluso cuando la aplicación correspondiente en el dispositivo se encuentra inactiva, y de autenticar la aplicación cliente antes de agregar una etiqueta a su registro.</span><span class="sxs-lookup"><span data-stu-id="19746-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="19746-179">Ejemplo de código para el registro en un centro de notificaciones desde un back-end con una instalación</span><span class="sxs-lookup"><span data-stu-id="19746-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="19746-180">El dispositivo cliente todavía obtiene su identificador de PNS y las propiedades de instalación importantes, tal como antes, y llama a una API personalizada en el back-end que puede realizar el registro, autorizar etiquetas, etc. El back-end puede usar el [SDK del Centro de notificaciones para operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="19746-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="19746-181">También puede utilizar el método PATCH con el [estándar JSON-Patch](https://tools.ietf.org/html/rfc6902) para actualizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="19746-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
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


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="19746-182">Ejemplo de código para el registro en un centro de notificaciones desde un dispositivo con un identificador de registro</span><span class="sxs-lookup"><span data-stu-id="19746-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="19746-183">Desde el back-end de la aplicación, puede ejecutar operaciones de tipo CRUD en los registros.</span><span class="sxs-lookup"><span data-stu-id="19746-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="19746-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19746-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
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


<span data-ttu-id="19746-185">El back-end debe controlar la simultaneidad entre las actualizaciones de los registros.</span><span class="sxs-lookup"><span data-stu-id="19746-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="19746-186">Bus de servicio ofrece un control de simultaneidad optimista para la administración de registros.</span><span class="sxs-lookup"><span data-stu-id="19746-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="19746-187">A nivel de HTTP, se implementa con el uso de ETag en las operaciones de administración de registros.</span><span class="sxs-lookup"><span data-stu-id="19746-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="19746-188">Los SDK de Microsoft utilizan esta característica de manera transparente y generan una excepción si se rechaza una actualización por motivos de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="19746-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="19746-189">El back-end de aplicación es responsable de controlar estas excepciones y de volver a intentar la actualización, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="19746-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

