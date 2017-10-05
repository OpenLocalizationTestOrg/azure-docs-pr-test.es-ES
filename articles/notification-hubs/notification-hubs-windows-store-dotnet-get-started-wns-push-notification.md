---
title: "Introducción a Azure Notification Hubs para aplicaciones de la plataforma universal de Windows | Microsoft Docs"
description: "En este tutorial aprenderá a usar Azure Notification Hubs para enviar notificaciones push a una aplicación de la plataforma universal de Windows."
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
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="29bae-103">Introducción a Notification Hubs para aplicaciones de la plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="29bae-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="29bae-104">Información general</span><span class="sxs-lookup"><span data-stu-id="29bae-104">Overview</span></span>
<span data-ttu-id="29bae-105">Este tutorial muestra cómo usar Azure Notification Hubs para enviar notificaciones push a una aplicación de la plataforma universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="29bae-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="29bae-106">En este tutorial puede crear una aplicación de la Tienda Windows vacía que recibe notificaciones push mediante el Servicios de notificaciones de inserción de Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="29bae-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="29bae-107">Cuando haya finalizado, podrá usar el centro de notificaciones para difundir notificaciones push a todos los dispositivos que ejecutan su aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="29bae-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="29bae-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="29bae-109">El código completo de este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="29bae-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29bae-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29bae-110">Prerequisites</span></span>
<span data-ttu-id="29bae-111">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="29bae-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="29bae-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) o posterior</span><span class="sxs-lookup"><span data-stu-id="29bae-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="29bae-113">Herramientas de desarrollo de aplicaciones universales de Windows instaladas</span><span class="sxs-lookup"><span data-stu-id="29bae-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="29bae-114">Una cuenta activa de Azure</span><span class="sxs-lookup"><span data-stu-id="29bae-114">An active Azure account</span></span> <br/><span data-ttu-id="29bae-115">En caso de no tener cuenta, puede crear una de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="29bae-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="29bae-116">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="29bae-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="29bae-117">Una cuenta de la Tienda Windows activa</span><span class="sxs-lookup"><span data-stu-id="29bae-117">An active Windows Store account</span></span>

<span data-ttu-id="29bae-118">Completar este tutorial es un requisito previo para todos los tutoriales de Notification Hubs para aplicaciones de la plataforma universal de Windows.</span><span class="sxs-lookup"><span data-stu-id="29bae-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="29bae-119">Registro de la aplicación para la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="29bae-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="29bae-120">Para enviar notificaciones push a las aplicaciones de la UWP, debe asociar su aplicación a la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="29bae-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="29bae-121">A continuación, debe configurar su Centro de notificaciones para que se integre con WNS.</span><span class="sxs-lookup"><span data-stu-id="29bae-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="29bae-122">Si aún no ha registrado la aplicación, navegue al [Centro de desarrollo de Windows](https://dev.windows.com/overview), conéctese con su cuenta Microsoft y, a continuación, haga clic en **Crear una nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="29bae-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="29bae-123">Escriba un nombre para la aplicación y haga clic en **Reservar nombre de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="29bae-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="29bae-124">Se crea un nuevo registro de la Tienda Windows para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="29bae-125">En Visual Studio, cree un nuevo proyecto de aplicaciones de la Tienda en Visual C# con la plantilla **Aplicación vacía** de Windows Universal y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="29bae-125">In Visual Studio, create a new Visual C# Store Apps project by using the Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="29bae-126">Acepte los valores predeterminados para las versiones de plataforma mínima y de destino.</span><span class="sxs-lookup"><span data-stu-id="29bae-126">Accept the defaults for the target and minimum platform versions.</span></span>

5. <span data-ttu-id="29bae-127">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto de la aplicación para la Tienda Windows, haga clic en **Tienda** y, a continuación, en **Asociar aplicación con la Tienda...**.</span><span class="sxs-lookup"><span data-stu-id="29bae-127">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span> <span data-ttu-id="29bae-128">Aparece el asistente **Asocie la aplicación con la Tienda Windows** .</span><span class="sxs-lookup"><span data-stu-id="29bae-128">The **Associate Your App with the Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="29bae-129">En el asistente, inicie sesión con su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29bae-129">In the wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="29bae-130">Haga clic en la aplicación que registró en el paso 2, haga clic en **Siguiente** y, después, en **Asociar**.</span><span class="sxs-lookup"><span data-stu-id="29bae-130">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="29bae-131">Se agrega la información de registro necesaria de la Tienda Windows al manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-131">This adds the required Windows Store registration information to the application manifest.</span></span>

8. <span data-ttu-id="29bae-132">De vuelta en la página [Centro de desarrollo de Windows](http://dev.windows.com/overview) de su nueva aplicación, haga clic en **Services** (Servicios), **Push notifications** (Insertar notificaciones) y, luego, en **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="29bae-132">Back on the [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="29bae-133">Haga clic en **New Notification** (Nueva notificación).</span><span class="sxs-lookup"><span data-stu-id="29bae-133">Click **New Notification**.</span></span>

10. <span data-ttu-id="29bae-134">Haga clic en la plantilla **Blank (Toast)** (En blanco [sistema]) y luego haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="29bae-134">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="29bae-135">Escriba el **nombre** de la notificación y el mensaje de **contexto** visual.</span><span class="sxs-lookup"><span data-stu-id="29bae-135">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="29bae-136">A continuación, haga clic en **Save as draft** (Guardar como borrador).</span><span class="sxs-lookup"><span data-stu-id="29bae-136">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="29bae-137">Vaya al [Portal de registro de aplicaciones](http://apps.dev.microsoft.com) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="29bae-137">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="29bae-138">Haga clic en el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-138">Click on your application name.</span></span> <span data-ttu-id="29bae-139">Anote la contraseña del **Secreto de aplicación** y del **identificador de seguridad de paquete (SID)** ubicado en la configuración de plataforma de la **Tienda Windows**.</span><span class="sxs-lookup"><span data-stu-id="29bae-139">Make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="29bae-140">El secreto de aplicación y el SID del paquete son credenciales de seguridad importantes.</span><span class="sxs-lookup"><span data-stu-id="29bae-140">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="29bae-141">No los comparta con nadie ni los distribuya con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-141">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="29bae-142">Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="29bae-142">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="29bae-143">Seleccione la opción <b>Notification Services</b> y la opción <b>Windows (WNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="29bae-143">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="29bae-144">A continuación, escriba la contraseña del <b>secreto de aplicación</b> en el campo <b>Clave de seguridad</b>.</span><span class="sxs-lookup"><span data-stu-id="29bae-144">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="29bae-145">Escriba el valor del <b>SID del paquete</b> obtenido de WNS en la sección anterior y, a continuación, haga clic en <b>Guardar</b>.</span><span class="sxs-lookup"><span data-stu-id="29bae-145">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="29bae-146">Su Centro de notificaciones está ahora configurado para funcionar con WNS y tiene las cadenas de conexión para registrar su aplicación y enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="29bae-146">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="29bae-147">Conexión de la aplicación al Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="29bae-147">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="29bae-148">En Visual Studio, haga clic con el botón derecho en la solución y, a continuación, haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="29bae-148">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="29bae-149">Se muestra el cuadro de diálogo **Administrar paquetes de NuGet** .</span><span class="sxs-lookup"><span data-stu-id="29bae-149">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="29bae-150">Busque `WindowsAzure.Messaging.Managed` y haga clic en **Instalar**, seleccione todos los proyectos en la solución y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="29bae-150">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="29bae-151">A continuación, se descarga, instala y agrega una referencia a la biblioteca de Mensajería de Azure para Windows mediante el <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">paquete de NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="29bae-151">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="29bae-152">Abra el archivo de proyecto App.xaml.cs y agregue las siguientes instrucciones `using` .</span><span class="sxs-lookup"><span data-stu-id="29bae-152">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="29bae-153">También en App.xaml.cs, agregue la siguiente definición de método **InitNotificationsAsync** a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="29bae-153">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="29bae-154">Este código recupera el URI del canal de la aplicación desde WNS y, luego, lo registra en el Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="29bae-154">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="29bae-155">Asegúrese de reemplazar el marcador de posición con el "nombre del centro" por el nombre del centro de notificaciones que aparece en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="29bae-155">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="29bae-156">Sustituya también el marcador de posición de la cadena de conexión por la cadena de conexión **DefaultListenSharedAccessSignature** que obtuvo en la página **Directivas de acceso** del Centro de notificaciones en una sección anterior.</span><span class="sxs-lookup"><span data-stu-id="29bae-156">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="29bae-157">En la parte superior del controlador de eventos **OnLaunched** en App.xaml.cs, agregue la siguiente llamada al nuevo método **InitNotificationsAsync**:</span><span class="sxs-lookup"><span data-stu-id="29bae-157">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="29bae-158">Esto garantiza que el URI del canal se registre en su Centro de notificaciones cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-158">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="29bae-159">Presione la tecla **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-159">Press the **F5** key to run the app.</span></span> <span data-ttu-id="29bae-160">Se muestra un cuadro de diálogo emergente que contiene la clave de registro.</span><span class="sxs-lookup"><span data-stu-id="29bae-160">A pop-up dialog that contains the registration key is displayed.</span></span>

<span data-ttu-id="29bae-161">La carpeta ahora ya está lista para recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="29bae-161">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="29bae-162">Envío de notificaciones</span><span class="sxs-lookup"><span data-stu-id="29bae-162">Send notifications</span></span>
<span data-ttu-id="29bae-163">Para probar de forma rápida la recepción de notificaciones en su aplicación, envíe notificaciones en [Azure Portal](https://portal.azure.com/) mediante el botón **Envío de prueba** en el centro de notificaciones, tal como se muestra en la pantalla que aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="29bae-163">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="29bae-164">Las notificaciones push se envían normalmente en un servicio back-end como Mobile Services o ASP.NET mediante una biblioteca compatible.</span><span class="sxs-lookup"><span data-stu-id="29bae-164">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="29bae-165">También puede usar la API de REST directamente para enviar mensajes de notificación si no hay disponible una biblioteca para su back-end.</span><span class="sxs-lookup"><span data-stu-id="29bae-165">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="29bae-166">En este tutorial, vamos a simplificar las cosas y mostrar solo la prueba de su aplicación cliente mediante el envío de notificaciones con el SDK de .NET para los centros de notificaciones en una aplicación de consola en lugar de un servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="29bae-166">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="29bae-167">Se recomienda seguir el tutorial [Notificación a los usuarios con Azure Notification Hubs] como paso siguiente para enviar notificaciones desde un back-end de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="29bae-167">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="29bae-168">Sin embargo, se pueden usar los siguientes enfoques para enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="29bae-168">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="29bae-169">**Interfaz de REST**: puede admitir notificaciones en cualquier plataforma de back-end mediante la [interfaz de REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="29bae-169">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="29bae-170">**SDK para .NET de Microsoft Azure Notification Hubs**: en el Administrador de paquetes NuGet para Visual Studio, ejecute [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="29bae-170">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="29bae-171">**Node.js** : [Uso de Notification Hubs desde Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="29bae-171">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="29bae-172">**Azure Mobile Apps**: para ver un ejemplo de cómo enviar notificaciones desde una aplicación móvil de Azure integrada en Notification Hubs, consulte [Incorporación de notificaciones push a la aplicación universal Windows en tiempo de ejecución 8.1](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="29bae-172">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="29bae-173">**Java / PHP**: para ver un ejemplo de cómo enviar notificaciones con las API de REST, consulte "Uso de Notification Hubs desde Java o PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="29bae-173">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="29bae-174">(Opcional) Enviar notificaciones desde una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="29bae-174">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="29bae-175">Para enviar notificaciones con una aplicación de consola .NET, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="29bae-175">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="29bae-176">Haga clic con el botón derecho en la solución, seleccione **Agregar** y **Nuevo proyecto...** y, a continuación, en **Visual C#**, haga clic en **Windows**, **Aplicación de consola** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="29bae-176">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="29bae-177">Esta acción agrega una aplicación de consola nueva de Visual C# a la solución.</span><span class="sxs-lookup"><span data-stu-id="29bae-177">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="29bae-178">También puede hacer esto en una solución separada.</span><span class="sxs-lookup"><span data-stu-id="29bae-178">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="29bae-179">En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="29bae-179">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="29bae-180">Esto muestra la Consola del administrador de paquetes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29bae-180">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="29bae-181">En la ventana de la Consola del Administrador de paquetes, seleccione en **Proyecto predeterminado** el nuevo proyecto de aplicación de consola y, a continuación, ejecute el siguiente comando en la ventana de la consola:</span><span class="sxs-lookup"><span data-stu-id="29bae-181">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="29bae-182">Así se agrega una referencia al SDK de Azure Notification Hubs mediante el <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="29bae-182">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="29bae-183">Abra el archivo Program.cs y agregue la siguiente instrucción `using` :</span><span class="sxs-lookup"><span data-stu-id="29bae-183">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="29bae-184">En la clase **Program** , agregue el siguiente método.</span><span class="sxs-lookup"><span data-stu-id="29bae-184">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="29bae-185">Asegúrese de usar una cadena de conexión con acceso **Total**, no con acceso de **Escucha**.</span><span class="sxs-lookup"><span data-stu-id="29bae-185">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="29bae-186">La cadena de acceso de escucha no tiene permisos para enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="29bae-186">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="29bae-187">Agregue las siguientes líneas al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="29bae-187">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="29bae-188">Haga clic con el botón derecho en el proyecto de la aplicación de consola en Visual Studio y haga clic en **Establecer como proyecto de inicio** para establecerlo como proyecto de inicio.</span><span class="sxs-lookup"><span data-stu-id="29bae-188">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="29bae-189">A continuación, presione la tecla **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-189">Then press the **F5** key to run the application.</span></span>
   
    <span data-ttu-id="29bae-190">Debería recibir una notificación del sistema en todos los dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="29bae-190">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="29bae-191">Si hace clic o toca el banner de notificaciones se carga la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29bae-191">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="29bae-192">Puede encontrar todas las cargas compatibles en los temas de [catálogo de notificaciones del sistema], el [catálogo de iconos] y la [información general de distintivos] en MSDN (en inglés).</span><span class="sxs-lookup"><span data-stu-id="29bae-192">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29bae-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29bae-193">Next steps</span></span>
<span data-ttu-id="29bae-194">En este sencillo ejemplo, ha difundido notificaciones a todos los dispositivos con Windows mediante el portal o aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="29bae-194">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="29bae-195">Se recomienda seguir el tutorial [Notificación a los usuarios con Azure Notification Hubs] como paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="29bae-195">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="29bae-196">Le mostrará cómo enviar notificaciones desde un back-end de ASP.NET mediante etiquetas para dirigirse a usuarios específicos.</span><span class="sxs-lookup"><span data-stu-id="29bae-196">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="29bae-197">Si desea segmentar los usuarios por grupos de interés, consulte [Uso de Notification Hubs para enviar noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="29bae-197">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="29bae-198">Para más información general sobre Notification Hubs, consulte [Guía de Notification Hubs](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29bae-198">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

<span data-ttu-id="29bae-199">[Notificación a los usuarios con Azure Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="29bae-199">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="29bae-200">[Uso de Notification Hubs para enviar noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="29bae-200">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

<span data-ttu-id="29bae-201">[catálogo de notificaciones del sistema]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span><span class="sxs-lookup"><span data-stu-id="29bae-201">[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span></span>
<span data-ttu-id="29bae-202">[catálogo de iconos]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span><span class="sxs-lookup"><span data-stu-id="29bae-202">[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span></span>
<span data-ttu-id="29bae-203">[información general de distintivos]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span><span class="sxs-lookup"><span data-stu-id="29bae-203">[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span></span>
