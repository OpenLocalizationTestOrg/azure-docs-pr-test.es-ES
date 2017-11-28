---
title: "aaaGet a trabajar con Azure notificación concentradores para aplicaciones universales de Windows plataforma | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toopush notificaciones tooa aplicación de plataforma Universal de Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="65248-103">Introducción a Notification Hubs para aplicaciones de la plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="65248-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="65248-104">Información general</span><span class="sxs-lookup"><span data-stu-id="65248-104">Overview</span></span>
<span data-ttu-id="65248-105">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa plataforma Universal de Windows (UWP) aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="65248-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="65248-106">En este tutorial, creará una aplicación de tienda Windows en blanco que recibe notificaciones de inserción mediante Hola servicios de notificación de inserción de Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="65248-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="65248-107">Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="65248-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="65248-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="65248-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="65248-109">código de Hello completado para este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="65248-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65248-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="65248-110">Prerequisites</span></span>
<span data-ttu-id="65248-111">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="65248-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="65248-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) o posterior</span><span class="sxs-lookup"><span data-stu-id="65248-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="65248-113">Herramientas de desarrollo de aplicaciones universales de Windows instaladas</span><span class="sxs-lookup"><span data-stu-id="65248-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="65248-114">Una cuenta activa de Azure</span><span class="sxs-lookup"><span data-stu-id="65248-114">An active Azure account</span></span> <br/><span data-ttu-id="65248-115">En caso de no tener cuenta, puede crear una de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="65248-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="65248-116">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="65248-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="65248-117">Una cuenta de la Tienda Windows activa</span><span class="sxs-lookup"><span data-stu-id="65248-117">An active Windows Store account</span></span>

<span data-ttu-id="65248-118">Completar este tutorial es un requisito previo para todos los tutoriales de Notification Hubs para aplicaciones de la plataforma universal de Windows.</span><span class="sxs-lookup"><span data-stu-id="65248-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="65248-119">Registrar la aplicación para hello tienda Windows</span><span class="sxs-lookup"><span data-stu-id="65248-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="65248-120">aplicaciones de tooUWP de notificaciones de inserción toosend, debe asociar la tienda Windows toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="65248-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="65248-121">A continuación, debe configurar su toointegrate de concentrador de notificación con WNS.</span><span class="sxs-lookup"><span data-stu-id="65248-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="65248-122">Si todavía no ha registrado su aplicación, vaya a toohello [centro de desarrollo de Windows](https://dev.windows.com/overview), inicie sesión con su cuenta de Microsoft y, a continuación, haga clic en **crear una nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="65248-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="65248-123">Escriba un nombre para la aplicación y haga clic en **Reservar nombre de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="65248-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="65248-124">Se crea un nuevo registro de la Tienda Windows para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="65248-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="65248-125">En Visual Studio, cree un nuevo proyecto de Visual C# aplicaciones de la tienda mediante el uso de hello universales de Windows **aplicación vacía** plantilla y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="65248-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="65248-126">Acepte valores predeterminados de hello para el destino de Hola y versiones de plataforma mínima.</span><span class="sxs-lookup"><span data-stu-id="65248-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="65248-127">En el Explorador de soluciones, proyecto de aplicación de tienda de Windows de Hola de menú contextual, haga clic en **almacén**y, a continuación, haga clic en **asociar aplicación con hello almacén...** . Hola **asociar la aplicación con hello tienda Windows** aparece el Asistente para.</span><span class="sxs-lookup"><span data-stu-id="65248-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="65248-128">En el Asistente de hello, inicie sesión con su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="65248-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="65248-129">Haga clic en la aplicación hello que registró en el paso 2, haga clic en **siguiente**y, a continuación, haga clic en **asociar**.</span><span class="sxs-lookup"><span data-stu-id="65248-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="65248-130">Esto agrega manifiesto de aplicación Hola necesario tienda Windows registro información toohello.</span><span class="sxs-lookup"><span data-stu-id="65248-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="65248-131">En hello [centro de desarrollo de Windows](http://dev.windows.com/overview) página de la aplicación nueva, haga clic en **servicios**, haga clic en **notificaciones de inserción**y, a continuación, haga clic en **estado de MPNS**.</span><span class="sxs-lookup"><span data-stu-id="65248-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="65248-132">Haga clic en **New Notification** (Nueva notificación).</span><span class="sxs-lookup"><span data-stu-id="65248-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="65248-133">Haga clic en la plantilla **Blank (Toast)** (En blanco [sistema]) y luego haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="65248-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="65248-134">Escriba el **nombre** de la notificación y el mensaje de **contexto** visual.</span><span class="sxs-lookup"><span data-stu-id="65248-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="65248-135">A continuación, haga clic en **Save as draft** (Guardar como borrador).</span><span class="sxs-lookup"><span data-stu-id="65248-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="65248-136">Navegue toohello [Portal de registro de aplicación](http://apps.dev.microsoft.com) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="65248-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="65248-137">Haga clic en el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="65248-137">Click on your application name.</span></span> <span data-ttu-id="65248-138">Tome nota de hello **secreto de aplicación** hello y contraseña **identificador de seguridad (SID) de paquete** ubicado en hello **tienda Windows** configuración de plataforma.</span><span class="sxs-lookup"><span data-stu-id="65248-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="65248-139">secreto de aplicación Hola y el SID del paquete son credenciales de seguridad importantes.</span><span class="sxs-lookup"><span data-stu-id="65248-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="65248-140">No los comparta con nadie ni los distribuya con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="65248-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="65248-141">Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="65248-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="65248-142">Seleccione hello <b>Notification Services</b> hello y opción <b>de Windows (WNS)</b> opción.</span><span class="sxs-lookup"><span data-stu-id="65248-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="65248-143">A continuación, escriba Hola <b>secreto de aplicación</b> contraseña Hola <b>clave de seguridad</b> campo.</span><span class="sxs-lookup"><span data-stu-id="65248-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="65248-144">Escriba su <b>SID del paquete</b> valor que ha obtenido de WNS en la sección anterior de hello y, a continuación, haga clic en <b>guardar</b>.</span><span class="sxs-lookup"><span data-stu-id="65248-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="65248-145">El centro de notificaciones está ahora configurado toowork con WNS, y tiene la aplicación de tooregister de cadenas de conexión de Hola y enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="65248-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="65248-146">Conectar el centro de notificaciones de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="65248-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="65248-147">En Visual Studio, haga clic en soluciones de hello y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="65248-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="65248-148">Esto muestra hello **administrar paquetes de NuGet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65248-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="65248-149">Busque `WindowsAzure.Messaging.Managed` y haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="65248-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="65248-150">Esto descarga, se instala y se agrega una biblioteca de referencia para la mensajería de Azure de toohello para Windows mediante el uso de Hola <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">paquete WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="65248-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="65248-151">Abrir archivo de proyecto de hello App.xaml.cs y agregue Hola siguiente `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="65248-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="65248-152">En App.xaml.cs, agregue Hola siguiente **InitNotificationsAsync** toohello de definición de método **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="65248-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="65248-153">Este código recupera el URI del canal de hello para la aplicación hello de WNS y, a continuación, registra ese URI del canal con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="65248-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="65248-154">Asegúrese de tooreplace seguro Hola marcador de posición "el nombre de base de datos central" con el nombre de Hola de centro de notificaciones de Hola que aparece en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="65248-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="65248-155">También reemplace el marcador de posición de cadena de conexión de hello con hello **DefaultListenSharedAccessSignature** cadena de conexión que obtiene de hello **directivas de acceso** página del centro de notificaciones en un sección anterior.</span><span class="sxs-lookup"><span data-stu-id="65248-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="65248-156">En parte superior de Hola de hello **OnLaunched** controlador de eventos en App.xaml.cs, agregue Hola después llamada toohello nueva **InitNotificationsAsync** método:</span><span class="sxs-lookup"><span data-stu-id="65248-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="65248-157">Esto garantiza que ese canal Hola que URI está registrado en el centro de notificaciones que se inicia cada aplicación Hola de tiempo.</span><span class="sxs-lookup"><span data-stu-id="65248-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="65248-158">Hola presione **F5** toorun clave Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="65248-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="65248-159">Se muestra un cuadro de diálogo emergente que contiene la clave de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="65248-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="65248-160">La aplicación ya está listo tooreceive recibir notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="65248-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="65248-161">Envío de notificaciones</span><span class="sxs-lookup"><span data-stu-id="65248-161">Send notifications</span></span>
<span data-ttu-id="65248-162">Puede probar rápidamente recibir notificaciones en la aplicación mediante el envío de notificaciones en hello [Portal de Azure](https://portal.azure.com/) con hello **probar envío** situado en el centro de notificaciones de hello, como se muestra en la siguiente pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="65248-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="65248-163">Las notificaciones push se envían normalmente en un servicio back-end como Mobile Services o ASP.NET mediante una biblioteca compatible.</span><span class="sxs-lookup"><span data-stu-id="65248-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="65248-164">También puede utilizar Hola API de REST directamente si una biblioteca no está disponible para el back-end de los mensajes de notificación toosend.</span><span class="sxs-lookup"><span data-stu-id="65248-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="65248-165">En este tutorial, agregaremos simplificar y solo muestran probar la aplicación cliente mediante el envío de notificaciones mediante Hola .NET SDK centrales de notificaciones en una aplicación de consola en lugar de un servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="65248-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="65248-166">Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial como paso siguiente de Hola para enviar notificaciones desde un back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="65248-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="65248-167">Sin embargo, Hola siguiendo métodos puede utilizarse para enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="65248-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="65248-168">**Interfaz REST**: admitir la notificación en cualquier plataforma de back-end mediante hello [interfaz REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="65248-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="65248-169">**SDK de .NET de Microsoft Azure notificación concentradores**: Hola Administrador de paquetes de Nuget para Visual Studio, ejecutar [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="65248-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="65248-170">**Node.js** : [cómo toouse centros de notificaciones de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="65248-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="65248-171">**Aplicaciones móviles de Azure**: para obtener un ejemplo de cómo toosend notificaciones desde una aplicación móvil de Azure que se integra con centros de notificaciones, consulte [agregar notificaciones de inserción para aplicaciones móviles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="65248-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="65248-172">**Java / PHP**: para obtener un ejemplo de cómo toosend notificaciones mediante el uso de hello las API de REST, vea "cómo toouse centros de notificaciones de Java y PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="65248-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="65248-173">(Opcional) Enviar notificaciones desde una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="65248-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="65248-174">notificaciones de toosend mediante el uso de una aplicación de consola .NET siguen estos pasos.</span><span class="sxs-lookup"><span data-stu-id="65248-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="65248-175">Solución de Hola de menú contextual, seleccione **agregar** y **nuevo proyecto...** y, a continuación, en **Visual C#**, haga clic en **Windows** y **aplicación de consola**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="65248-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="65248-176">Esto agrega una nueva solución de toohello para aplicaciones de Visual C# consola.</span><span class="sxs-lookup"><span data-stu-id="65248-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="65248-177">También puede hacer esto en una solución separada.</span><span class="sxs-lookup"><span data-stu-id="65248-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="65248-178">En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="65248-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="65248-179">Esto muestra hello consola de administrador de paquetes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65248-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="65248-180">En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="65248-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="65248-181">Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="65248-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="65248-182">Abra el archivo Program.cs de hello y agregue Hola siguiente `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="65248-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="65248-183">Hola **programa** clase, agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="65248-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="65248-184">Asegúrese de que usar cadena de conexión de hello tiene **completa** acceso, no **escuchar** acceso.</span><span class="sxs-lookup"><span data-stu-id="65248-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="65248-185">cadena de acceso de la escucha de Hello no tiene las notificaciones de toosend de permisos.</span><span class="sxs-lookup"><span data-stu-id="65248-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="65248-186">Agregar Hola después de las líneas de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="65248-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="65248-187">Haga clic en proyecto de aplicación de consola de hello en Visual Studio y haga clic en **establecer como proyecto de inicio** tooset como proyecto de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="65248-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="65248-188">A continuación, presione hello **F5** aplicación de hello toorun de clave.</span><span class="sxs-lookup"><span data-stu-id="65248-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="65248-189">Debería recibir una notificación del sistema en todos los dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="65248-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="65248-190">Banner de notificación del sistema de hello clic o pulsando en carga la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="65248-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="65248-191">Puede encontrar todas las cargas de hello admitida Hola [catálogo del sistema], [catálogo iconos], y [información general de identificación] temas en MSDN.</span><span class="sxs-lookup"><span data-stu-id="65248-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65248-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65248-192">Next steps</span></span>
<span data-ttu-id="65248-193">En este sencillo ejemplo, envía notificaciones difusión tooall los dispositivos de Windows mediante el portal de Hola o una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="65248-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="65248-194">Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial como paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="65248-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="65248-195">Le mostraremos cómo toosend notificaciones desde un back-end ASP.NET con etiquetas tootarget determinados usuarios.</span><span class="sxs-lookup"><span data-stu-id="65248-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="65248-196">Si desea toosegment los usuarios por grupos de interés, vea [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="65248-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="65248-197">toolearn obtener más información sobre los centros de notificaciones, consulte [instrucciones de los centros de notificación](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65248-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers de notificaciones de los centros de notificaciones de uso toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catálogo del sistema]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[catálogo iconos]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[información general de identificación]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
