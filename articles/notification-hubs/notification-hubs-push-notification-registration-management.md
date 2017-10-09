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
# <a name="registration-management"></a>Administración de registros
## <a name="overview"></a>Información general
Este tema explica cómo los dispositivos tooregister con centros de notificaciones en orden tooreceive notificaciones de inserción. tema de Hello describe los registros en un nivel superior y luego presenta Hola dos patrones principales para registrar dispositivos: registro desde dispositivo Hola directamente toohello centro de notificaciones y registro mediante un aplicación de back-end. 

## <a name="what-is-device-registration"></a>Qué es el registro de dispositivos
El registro de dispositivos en un Centro de notificaciones se logra mediante un **Registro** o una **Instalación**.

#### <a name="registrations"></a>Registros
Un registro asocia Hola controlar el servicio de notificación de plataforma (PNS) para un dispositivo con etiquetas y, posiblemente, una plantilla. controlador de PNS Hola podría ser un URI del canal, el token del dispositivo o el Id. del registro GCM. Las etiquetas son las notificaciones de tooroute usado toohello conjunto correcto de controladores de dispositivo. Para obtener más información, consulte [Expresiones de etiqueta y enrutamiento](notification-hubs-tags-segment-push-message.md). Las plantillas son tooimplement usado por registro transformación. Para obtener más información, consulte [Plantillas](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Instalaciones
Una Instalación es un registro mejorado que incluye un conjunto de propiedades relacionadas con la inserción. Es Hola tooregistering enfoque mejor y más recientes de los dispositivos. Sin embargo, aún no es compatible con el SDK para .NET del cliente ([SDK del centro de notificaciones para operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).  Esto significa que si va a registrar en el propio dispositivo de cliente hello, tendría hello toouse [API de REST de centros de notificaciones](https://msdn.microsoft.com/library/mt621153.aspx) enfocar toosupport instalaciones. Si usas un servicio back-end, debe ser capaz de toouse [SDK de concentrador de notificación para las operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

continuación de Hola se muestran algunas instalaciones de toousing de las principales ventajas:

* Crear o actualizar una instalación es completamente idempotente. Por lo tanto, puede volver a intentarla sin preocuparse de obtener registros duplicados.
* el modelo de instalación de Hello, es fácil toodo individuales inserciones - dispositivo de destino. Una etiqueta de instalación **"$InstallationId:[IdentificadordeInstalación]"** se crea automáticamente con cada registro basado en instalación. Por lo que puede llamar a un tootarget de etiqueta de envío toothis un dispositivo específico sin necesidad de toodo ninguna codificación adicional.
* Usar las instalaciones, también permite actualizaciones parciales de registro toodo. actualización parcial de una instalación Hello se solicita una con un método de revisión con hello [estándar de JSON-Patch](https://tools.ietf.org/html/rfc6902). Esto es especialmente útil cuando se desea tooupdate etiquetas en el registro de hello. No tiene toopull hacia abajo el registro completo de Hola y vuelva a enviar todas las etiquetas anteriores Hola de nuevo.

Una instalación puede contener Hola Hola propiedades siguientes. Para obtener una lista completa de hello, vea Propiedades instalación [crear o sobrescribir una instalación con la API de REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) o [propiedades de instalación](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) para saludo.

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



Es importante toonote que ya no expiran los registros y las instalaciones de forma predeterminada.

Los registros y las instalaciones deben contener un controlador PNS válido para cada dispositivo o canal. Dado que solo se pueden obtener controladores de PNS en una aplicación de cliente en el dispositivo de hello, un patrón de es tooregister directamente en ese dispositivo con la aplicación de cliente de hello. Hola otros mano, consideraciones de seguridad y lógica de negocios relacionan tootags podría requerir que el registro de dispositivos toomanage en hello aplicación back-end. 

#### <a name="templates"></a>Plantillas
Si desea que toouse [plantillas](notification-hubs-templates-cross-platform-push-messages.md), instalación de dispositivo de hello también contener todas las plantillas asociadas con ese dispositivo en JSON de formato (vea el ejemplo anterior). Hello plantilla nombres ayudan a dirigirse a varias plantillas para hello mismo dispositivo.

Tenga en cuenta que cada nombre de plantilla asigna tooa cuerpo de plantilla y un conjunto opcional de etiquetas. Además, cada plataforma puede tener propiedades de plantilla adicionales. Tienda de Windows (mediante WNS) y Windows Phone 8 (mediante MPNS), un conjunto adicional de encabezados puede formar parte de la plantilla de Hola. En caso de hello de APN, puede establecer una tooeither de expiración propiedad una expresión de plantilla constante o tooa. Para obtener una lista completa de hello, vea Propiedades instalación [crear o sobrescribir una instalación con REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tema.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Iconos secundarios de Aplicaciones de la Tienda Windows
Para las aplicaciones de cliente de tienda Windows, enviar notificaciones es toosecondary iconos Hola mismo que enviarlos toohello principal. Esto también se admite en las instalaciones. Tenga en cuenta que los iconos secundarios tienen un URI de canal diferentes, qué Hola SDK en la aplicación cliente se controla de manera transparente.

Hola SecondaryTiles diccionario usa Hola mismo TileId que es objeto de SecondaryTiles de hello toocreate usado en la aplicación tienda Windows.
Como con hello URI principal, ChannelUris de iconos secundarios puede cambiar en cualquier momento. En orden tookeep hello las instalaciones en el centro de notificaciones de hello actualizado, Hola dispositivo debe actualizarlos con hello ChannelUris actuales de iconos secundarios Hola.

## <a name="registration-management-from-hello-device"></a>Administración de registros desde dispositivo Hola
Cuando se administra el registro de dispositivos desde aplicaciones cliente, Hola back-end solamente es responsable de enviar notificaciones. Las aplicaciones cliente de mantener los controladores de PNS una toodate y registran etiquetas. Hola siguiente muestra este modelo.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

dispositivo Hola primero recupera Hola controlador de PNS de hello PNS, a continuación, registra directamente con el centro de notificaciones de Hola. Después de que el registro de hello es correcto, Hola backend de la aplicación puede enviar una notificación dirigida a ese tipo de registro. Para obtener más información acerca de cómo toosend notificaciones, consulte [enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).
Tenga en cuenta que en este caso, usará sólo escuche derechos tooaccess sus centros de notificaciones de dispositivo de Hola. Para obtener más información, consulte [Seguridad](notification-hubs-push-notification-security.md).

Registro desde dispositivo hello es el método más sencillo de hello, pero tiene algunas desventajas.
Hola primera desventaja es que una aplicación cliente solo puede actualizar sus etiquetas cuando la aplicación hello está activo. Por ejemplo, si un usuario tiene dos dispositivos que registran etiquetas relacionadas toosport equipos, al primer dispositivo de Hola se registra para una etiqueta adicional (por ejemplo, Seahawks), Hola segundo dispositivo no recibirá notificaciones de hello sobre hello Seahawks hasta que la aplicación hello en hello segundo dispositivo se ejecuta una segunda vez. Por lo general, cuando las etiquetas se ven afectadas por los distintos dispositivos, administrar etiquetas de hello back-end es una opción conveniente.
segunda desventaja de Hello de la administración de registros desde la aplicación de cliente de hello es que, puesto que las aplicaciones podrían prestarse a intrusiones, protección de registro de hello toospecific etiquetas requiere especial atención, como se explica en la sección de Hola "seguridad de nivel de la etiqueta".

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Tooregister de código de ejemplo con un centro de notificaciones desde un dispositivo mediante una instalación
En este momento, solo se admite con hello [API de REST de centros de notificación](https://msdn.microsoft.com/library/mt621153.aspx).

También puede utilizar el método de revisión de hello mediante hello [estándar de JSON-Patch](https://tools.ietf.org/html/rfc6902) para actualizar la instalación de Hola.

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Tooregister de código de ejemplo con un centro de notificaciones desde un dispositivo mediante un registro
Estos métodos crean o actualizan un registro para el dispositivo de hello en el que se llamó. Esto significa que, en orden tooupdate Hola Hola o identificador de etiquetas, debe sobrescribir registro completo de Hola. Recuerde que los registros son transitorios, por lo que siempre debe tener un almacén confiable con etiquetas actuales de Hola que necesita un determinado dispositivo.

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


## <a name="registration-management-from-a-backend"></a>Administración de registros desde un back-end
La administración de registros de back-end de hello, es necesario escribir código adicional. la aplicación Hello de dispositivo de hello debe proporcionar Hola actualizada PNS identificador toohello back-end cada vez inicia la aplicación hello (junto con etiquetas y plantillas) y Hola back-end debe actualizar este controlador en el centro de notificaciones de Hola. Hola después de la imagen muestra este diseño.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

las ventajas de Hola de administrar los registros de back-end de hello incluyen hello capacidad toomodify etiquetas tooregistrations incluso cuando la aplicación correspondiente hello en dispositivo Hola está inactiva y aplicación de cliente hello tooauthenticate antes de agregar un registro de tooits de etiqueta.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Tooregister de código de ejemplo con un centro de notificaciones desde un back-end mediante la instalación
dispositivo de cliente de Hola todavía obtiene su controlador de PNS y propiedades de instalación pertinentes como antes y llamadas a una API personalizada en el back-end de Hola que puede realizar el registro de hello y autorizar etiquetas back-end de etc. Hola pueden aprovechar hello [SDK de concentrador de notificación para operaciones de back-end](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

También puede utilizar el método de revisión de hello mediante hello [estándar de JSON-Patch](https://tools.ietf.org/html/rfc6902) para actualizar la instalación de Hola.

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Tooregister de código de ejemplo con un centro de notificaciones desde un dispositivo mediante un identificador de registro
Desde el back-end de la aplicación, puede ejecutar operaciones de tipo CRUD en los registros. Por ejemplo:

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


Hola back-end debe controlar la simultaneidad entre las actualizaciones de registro. Bus de servicio ofrece un control de simultaneidad optimista para la administración de registros. En el nivel de hello HTTP, esto se implementa con el uso de Hola de ETag en operaciones de administración de registros. Los SDK de Microsoft utilizan esta característica de manera transparente y generan una excepción si se rechaza una actualización por motivos de simultaneidad. aplicación de Hello back-end es responsable de controlar estas excepciones y volver a intentar la actualización de hello si es necesario.

