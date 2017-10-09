---
title: "notificaciones de inserción de aaaSending con centros de notificaciones de Azure y Node.js"
description: "Obtenga información acerca de cómo toosend de centros de notificaciones de toouse notificaciones de inserción desde una aplicación Node.js."
keywords: "notificación push,notificaciones push,inserción de node.js,inserción de ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="2e830-104">Envío de notificaciones push seguras con los Centros de notificaciones de Azure y Node.js</span><span class="sxs-lookup"><span data-stu-id="2e830-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="2e830-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2e830-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2e830-106">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e830-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2e830-107">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2e830-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2e830-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="2e830-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="2e830-109">Esta guía le mostrará cómo toosend notificaciones de inserción con ayuda de Hola de centros de notificaciones de Azure directamente desde una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="2e830-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="2e830-110">escenarios de Hello descritos incluyen enviar tooapplications de notificaciones de inserción en hello siguientes plataformas:</span><span class="sxs-lookup"><span data-stu-id="2e830-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="2e830-111">Android</span><span class="sxs-lookup"><span data-stu-id="2e830-111">Android</span></span>
* <span data-ttu-id="2e830-112">iOS</span><span class="sxs-lookup"><span data-stu-id="2e830-112">iOS</span></span>
* <span data-ttu-id="2e830-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="2e830-113">Windows Phone</span></span>
* <span data-ttu-id="2e830-114">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="2e830-114">Universal Windows Platform</span></span> 

<span data-ttu-id="2e830-115">Para obtener más información sobre los centros de notificaciones, consulte hello [pasos](#next) sección.</span><span class="sxs-lookup"><span data-stu-id="2e830-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="2e830-116">¿Qué son los Centros de notificaciones?</span><span class="sxs-lookup"><span data-stu-id="2e830-116">What are Notification Hubs?</span></span>
<span data-ttu-id="2e830-117">Centros de notificaciones de Azure proporcionan una infraestructura fácil de usar, multiplataforma y escalable para el envío de dispositivos de toomobile de notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="2e830-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="2e830-118">Para obtener detalles sobre la infraestructura de servicio de hello, vea hello [centros de notificaciones de Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="2e830-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="2e830-119">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="2e830-119">Create a Node.js Application</span></span>
<span data-ttu-id="2e830-120">Hola primer paso en este tutorial es crear una nueva aplicación Node.js en blanco.</span><span class="sxs-lookup"><span data-stu-id="2e830-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="2e830-121">Para obtener instrucciones sobre cómo crear una aplicación Node.js, vea [crear e implementar un tooAzure de aplicación sitio Web de Node.js][nodejswebsite], [servicio de nube de Node.js] [ Node.js Cloud Service] con Windows PowerShell, o [sitio Web con WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="2e830-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="2e830-122">Configurar los centros de notificaciones de la aplicación tooUse</span><span class="sxs-lookup"><span data-stu-id="2e830-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="2e830-123">toouse centros de notificaciones de Azure, necesitará toodownload y use hello Node.js [paquete azure](https://www.npmjs.com/package/azure), que incluye un conjunto integrado de bibliotecas de aplicación auxiliar que se comunican con servicios REST de notificación de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e830-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="2e830-124">Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete</span><span class="sxs-lookup"><span data-stu-id="2e830-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="2e830-125">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Linux) y desplazarse por las carpetas de toohello en la que creó la aplicación en blanco .</span><span class="sxs-lookup"><span data-stu-id="2e830-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="2e830-126">Tipo de **npm instalar azure sb** en la ventana de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e830-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="2e830-127">También puede ejecutar manualmente hello **ls** o **dir** tooverify de comando que un **nodo\_módulos** se creó la carpeta.</span><span class="sxs-lookup"><span data-stu-id="2e830-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="2e830-128">Dentro de esa carpeta, busque hello **azure** paquete, que contiene las bibliotecas de Hola que necesita tooaccess Hola centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2e830-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2e830-129">Puede aprender más acerca de cómo instalar NPM en oficial de hello [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="2e830-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="2e830-130">Módulo de Hola de importación</span><span class="sxs-lookup"><span data-stu-id="2e830-130">Import hello module</span></span>
<span data-ttu-id="2e830-131">Con un editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="2e830-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="2e830-132">Configuración de una conexión de Centro de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="2e830-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="2e830-133">Hola **NotificationHubService** objeto le permite trabajar con los centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2e830-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="2e830-134">Hello código siguiente se crea un **NotificationHubService** objeto para el concentrador de notificación de hello denominado **hubname**.</span><span class="sxs-lookup"><span data-stu-id="2e830-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="2e830-135">Agregar cerca de parte superior de Hola de hello **server.js** archivo, después de módulo de hello instrucción tooimport hello azure:</span><span class="sxs-lookup"><span data-stu-id="2e830-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="2e830-136">Hola conexión **connectionstring** se puede obtener el valor de hello [Portal de Azure] realizando Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2e830-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="2e830-137">En el panel de navegación izquierdo de hello, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="2e830-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="2e830-138">Seleccione **centros de notificaciones**y, a continuación, buscar Hola concentrador desea toouse de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e830-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="2e830-139">Puede hacer referencia a toohello [tutorial de introducción a Windows almacén](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) si necesita ayuda para crear un nuevo centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2e830-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="2e830-140">Seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="2e830-140">Select **Settings**.</span></span>
4. <span data-ttu-id="2e830-141">Haga clic en **Directivas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="2e830-141">Click on **Access Policies**.</span></span> <span data-ttu-id="2e830-142">Verá las cadenas de conexión de acceso, tanto las compartidas como las de acceso completo.</span><span class="sxs-lookup"><span data-stu-id="2e830-142">You will see both shared and full access connection strings.</span></span>

![Portal de Azure: Centros de notificaciones](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="2e830-144">También puede recuperar la cadena de conexión de hello con hello **Get-AzureSbNamespace** cmdlet proporcionado por [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello **show de espacio de nombres de azure sb** con Hola [interfaz de línea de comandos de Azure (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2e830-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="2e830-145">Arquitectura general</span><span class="sxs-lookup"><span data-stu-id="2e830-145">General architecture</span></span>
<span data-ttu-id="2e830-146">Hola **NotificationHubService** objeto expone Hola siguientes instancias de objeto para el envío de aplicaciones y dispositivos de toospecific de notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="2e830-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="2e830-147">**Android** -usar hello **GcmService** objeto, que está disponible en **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="2e830-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="2e830-148">**iOS** -usar hello **ApnsService** objeto, que puede tener acceso al **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="2e830-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="2e830-149">**Windows Phone** -usar hello **MpnsService** objeto, que está disponible en **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="2e830-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="2e830-150">**Plataforma universal de Windows** -usar hello **WnsService** objeto, que está disponible en **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="2e830-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="2e830-151">Cómo: enviar aplicaciones tooAndroid de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="2e830-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="2e830-152">Hola **GcmService** objeto proporciona un **enviar** método que puede ser aplicaciones de tooAndroid de notificaciones de inserción de toosend usado.</span><span class="sxs-lookup"><span data-stu-id="2e830-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="2e830-153">Hola **enviar** método acepta Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="2e830-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="2e830-154">**Etiquetas** -Hola identificador de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="2e830-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="2e830-155">Si no se proporciona ninguna etiqueta, se enviará a notificación de hello tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="2e830-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="2e830-156">**Carga** -Hola JSON o la carga de cadena sin formato del mensaje.</span><span class="sxs-lookup"><span data-stu-id="2e830-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="2e830-157">**Devolución de llamada** -Hola función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="2e830-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="2e830-158">Para obtener más información sobre el formato de carga de hello, vea hello **carga** sección de hello [implementar servidores de GCM](http://developer.android.com/google/gcm/server.html#payload) documento.</span><span class="sxs-lookup"><span data-stu-id="2e830-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="2e830-159">Hello código siguiente usa hello **GcmService** instancia expuesto por hello **NotificationHubService** toosend un tooall de notificación de inserción registrado los clientes.</span><span class="sxs-lookup"><span data-stu-id="2e830-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="2e830-160">Cómo: enviar aplicaciones tooiOS de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="2e830-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="2e830-161">Igual al igual que con las aplicaciones de Android se ha descrito anteriormente, Hola **ApnsService** objeto proporciona un **enviar** método que puede ser aplicaciones de tooiOS de notificaciones de inserción de toosend usado.</span><span class="sxs-lookup"><span data-stu-id="2e830-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="2e830-162">Hola **enviar** método acepta Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="2e830-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="2e830-163">**Etiquetas** -Hola identificador de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="2e830-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="2e830-164">Si no se proporciona ninguna etiqueta, se enviará a notificación de hello tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="2e830-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="2e830-165">**Carga** : Hola JSON del mensaje o carga de cadena.</span><span class="sxs-lookup"><span data-stu-id="2e830-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="2e830-166">**Devolución de llamada** -Hola función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="2e830-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="2e830-167">Para el formato de carga de Hola de más información, vea hello **carga de notificaciones** sección de hello [locales y Guía de programación de notificaciones de inserción](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.</span><span class="sxs-lookup"><span data-stu-id="2e830-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="2e830-168">Hello código siguiente usa hello **ApnsService** instancia expuesto por hello **NotificationHubService** toosend una alerta de mensaje tooall clientes:</span><span class="sxs-lookup"><span data-stu-id="2e830-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="2e830-169">Cómo: enviar aplicaciones de teléfono de tooWindows de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="2e830-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="2e830-170">Hola **MpnsService** objeto proporciona un **enviar** método que puede ser tooWindows de notificaciones de inserción toosend usado aplicaciones de teléfono.</span><span class="sxs-lookup"><span data-stu-id="2e830-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="2e830-171">Hola **enviar** método acepta Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="2e830-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="2e830-172">**Etiquetas** -Hola identificador de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="2e830-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="2e830-173">Si no se proporciona ninguna etiqueta, se enviará a notificación de hello tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="2e830-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="2e830-174">**Carga** -Hola carga XML del mensaje.</span><span class="sxs-lookup"><span data-stu-id="2e830-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="2e830-175">**TargetName** - `toast` para notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="2e830-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="2e830-176">`token` para notificaciones de icono.</span><span class="sxs-lookup"><span data-stu-id="2e830-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="2e830-177">**Clase de notificación** -Hola prioridad de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e830-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="2e830-178">Vea hello **elementos de encabezado HTTP** sección de hello [notificaciones de inserción desde un servidor](http://msdn.microsoft.com/library/hh221551.aspx) documento para los valores válidos.</span><span class="sxs-lookup"><span data-stu-id="2e830-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="2e830-179">**Options** : encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="2e830-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="2e830-180">**Devolución de llamada** -Hola función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="2e830-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="2e830-181">Para obtener una lista de válido **TargetName**, **clases de notificación** y opciones de encabezado, desproteger hello [notificaciones de inserción desde un servidor](http://msdn.microsoft.com/library/hh221551.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="2e830-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="2e830-182">Hola siguiente código de ejemplo utiliza hello **MpnsService** instancia expuesto por hello **NotificationHubService** toosend una notificación de inserción del sistema:</span><span class="sxs-lookup"><span data-stu-id="2e830-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="2e830-183">Cómo: enviar aplicaciones de plataforma de Windows (UWP) tooUniversal de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="2e830-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="2e830-184">Hola **WnsService** objeto proporciona un **enviar** método que puede ser utilizados toosend inserción notificaciones tooUniversal plataforma Windows aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2e830-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="2e830-185">Hola **enviar** método acepta Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="2e830-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="2e830-186">**Etiquetas** -Hola identificador de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="2e830-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="2e830-187">Si no se proporciona ninguna etiqueta, se enviará a notificación de hello clientes tooall registrado.</span><span class="sxs-lookup"><span data-stu-id="2e830-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="2e830-188">**Carga** -carga de mensaje de Hola XML.</span><span class="sxs-lookup"><span data-stu-id="2e830-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="2e830-189">**Tipo** -Hola tipo de notificación.</span><span class="sxs-lookup"><span data-stu-id="2e830-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="2e830-190">**Options** : encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="2e830-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="2e830-191">**Devolución de llamada** -Hola función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="2e830-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="2e830-192">Para obtener una lista de tipos y encabezados de solicitud válidos, consulte [Encabezados de respuesta y solicitud del servicio de notificaciones de inserción (aplicaciones de Windows en tiempo de ejecución)](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e830-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="2e830-193">Hello código siguiente usa hello **WnsService** instancia expuesto por hello **NotificationHubService** toosend una aplicación de UWP notificaciones del sistema tooa de notificación de inserción:</span><span class="sxs-lookup"><span data-stu-id="2e830-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="2e830-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2e830-194">Next Steps</span></span>
<span data-ttu-id="2e830-195">fragmentos de código del ejemplo de Hola anteriores permiten tooeasily compilación servicio infraestructura toodeliver inserción notificaciones tooa amplia variedad de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2e830-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="2e830-196">Ahora que conoce los fundamentos de hello del uso de los centros de notificaciones con node.js, siga estos toolearn de vínculos más información acerca de cómo puede ampliar estas capacidades aún más.</span><span class="sxs-lookup"><span data-stu-id="2e830-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="2e830-197">Vea Hola referencia MSDN para [centros de notificaciones de Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e830-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="2e830-198">Visite hello [Azure SDK para el nodo] repositorio en GitHub para obtener más ejemplos y detalles de implementación.</span><span class="sxs-lookup"><span data-stu-id="2e830-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK para el nodo]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[sitio Web con WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Portal de Azure]: https://portal.azure.com
