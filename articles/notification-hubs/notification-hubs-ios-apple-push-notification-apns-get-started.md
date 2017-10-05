---
title: "Envío de notificaciones push a iOS con los Azure Notification Hubs | Microsoft Docs"
description: "En este tutorial aprenderá a usar Centros de notificaciones de Azure para enviar notificaciones push a una aplicación iOS."
services: notification-hubs
documentationcenter: ios
keywords: "notificación push,notificaciones push,notificaciones push de ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="9d9b9-104">Envío de notificaciones push a iOS con los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="9d9b9-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9d9b9-105">Información general</span><span class="sxs-lookup"><span data-stu-id="9d9b9-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="9d9b9-106">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9d9b9-107">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9d9b9-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="9d9b9-109">Este tutorial muestra cómo puede utilizar los Centros de notificaciones de Azure para enviar notificaciones de inserción a una aplicación iOS.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="9d9b9-110">Creará una aplicación iOS vacía que recibe notificaciones push mediante el [Servicio de notificaciones push de Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="9d9b9-111">Cuando haya finalizado, podrá usar el centro de notificaciones para difundir notificaciones push a todos los dispositivos que ejecutan su aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9d9b9-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9d9b9-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="9d9b9-113">El código completo de este tutorial se puede encontrar [en GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9d9b9-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d9b9-114">Prerequisites</span></span>
<span data-ttu-id="9d9b9-115">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="9d9b9-116">[SDK de iOS versión 1.2.4 para Servicios móviles]</span><span class="sxs-lookup"><span data-stu-id="9d9b9-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="9d9b9-117">La versión más reciente de [Xcode]</span><span class="sxs-lookup"><span data-stu-id="9d9b9-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="9d9b9-118">Un dispositivo compatible con iOS 8 (o una versión posterior)</span><span class="sxs-lookup"><span data-stu-id="9d9b9-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="9d9b9-119">[programa para desarrolladores de Apple](https://developer.apple.com/programs/) </span><span class="sxs-lookup"><span data-stu-id="9d9b9-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9d9b9-120">Debido a los requisitos de configuración de las notificaciones push, debe implementar y probar estas en un dispositivo iOs físico (iPhone o iPad) en lugar de en el simulador de iOS.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="9d9b9-121">La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones iOS.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="9d9b9-122">Configuración del Centro de notificaciones para notificaciones push de iOS</span><span class="sxs-lookup"><span data-stu-id="9d9b9-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="9d9b9-123">Esta sección le guía en la creación de un nuevo centro de notificaciones y la configuración de la autenticación con APNS mediante el certificado de inserción **.p12** que creó.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="9d9b9-124">Si desea usar un centro de notificaciones ya creado, puede omitir los pasos hasta el paso 5.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="9d9b9-125">Haga clic en el botón <b>Servicios de notificaciones</b> en la hoja <b>Configuración</b> y, después, seleccione <b>Apple (APNs)</b>.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="9d9b9-126">Haga clic en <b>Cargar certificado</b> y seleccione el archivo <b>.p12</b> que exportó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="9d9b9-127">Asegúrese de que también especifica la contraseña correcta.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="9d9b9-128">Asegúrese de seleccionar el modo <b>Espacio aislado</b> ya que esto es para desarrollo.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="9d9b9-129">Use el modo <b>Producción</b> únicamente si desea enviar notificaciones de inserción a los usuarios que compraron la aplicación en la tienda.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="9d9b9-130">&emsp;&emsp;&emsp;&emsp;![Configurar APN en Portal de Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="9d9b9-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configuración de certificados APNs en el Portal de Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="9d9b9-132">Su centro de notificaciones está ahora configurado para funcionar con APNS, y tiene las cadenas de conexión para registrar su aplicación y enviar notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="9d9b9-133">Conexión de la aplicación iOS a los Centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9d9b9-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="9d9b9-134">En XCode, cree un nuevo proyecto iOS y seleccione la plantilla **Single View Application** (Aplicación de vista sencilla).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode: aplicación de vista única][8]
    
2. <span data-ttu-id="9d9b9-136">Al configurar las opciones para su nuevo proyecto, asegúrese de usar el mismo **nombre de producto** e **identificador de organización** que usó cuando estableció anteriormente el identificador de paquete en el portal de desarrollo de Apple.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode: opciones de proyecto][11]
    
3. <span data-ttu-id="9d9b9-138">En **Targets** (Destinos), haga clic en el nombre de proyecto, luego haga clic en la pestaña **Build Settings** (Compilar configuración) y expanda **Code Signing Identity** (Identidad de firma de código); a continuación, en **Debug** (Depurar), establezca la identidad de firma de código.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="9d9b9-139">Alterne los **niveles** entre **Basic** (Básico) hasta **All** (Todos) y establezca el **perfil de aprovisionamiento** en el perfil de aprovisionamiento que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="9d9b9-140">Si no ve el nuevo perfil de aprovisionamiento que creó en Xcode, intente actualizar los perfiles de la identidad de firma.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="9d9b9-141">Haga clic en **Xcode** en la barra de menús, en **Preferences** (Preferencias), en la pestaña **Account** (Cuenta), en el botón **View Details** (Ver detalles), en la identidad de firma y, por último, en el botón Refresh (Actualizar) en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode: perfil de aprovisionamiento][9]
4. <span data-ttu-id="9d9b9-143">Descargue el [SDK de iOS versión 1.2.4 para Servicios móviles] y descomprima el archivo.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="9d9b9-144">En XCode, haga clic con el botón derecho en el proyecto y haga clic en la opción **Add Files to** (Agregar archivos a) para agregar la carpeta **WindowsAzureMessaging.framework** al proyecto de XCode.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="9d9b9-145">Seleccione **Copy items if needed** (Copiar elementos si es necesario) y luego haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d9b9-146">El SDK de los Centros de notificaciones no es compatible con bitcode en Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="9d9b9-147">Debe establecer **Enable Bitcode** (Habilitar Bitcode) en **No** en **Build Options** (Opciones de compilación) en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Descompresión del SDK de Azure][10]
5. <span data-ttu-id="9d9b9-149">Agregue un nuevo archivo de encabezado al proyecto denominado `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="9d9b9-150">Este archivo contendrá las constantes para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="9d9b9-151">Agregue las siguientes definiciones y reemplace los marcadores de posición de literal de cadena por su *nombre del centro* y el valor de *DefaultListenSharedAccessSignature* que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="9d9b9-152">Abra el archivo `AppDelegate.h` y agregue las siguientes directivas de importación:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="9d9b9-153">En el archivo `AppDelegate.m file`, agregue el siguiente código al método `didFinishLaunchingWithOptions` en función de la versión de iOS.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="9d9b9-154">Este código registra el identificador de dispositivo en APNS:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="9d9b9-155">Para iOS 8:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="9d9b9-156">Para la versión de iOS antes de la 8:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="9d9b9-157">En el mismo archivo, agregue los siguientes métodos.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-157">In the same file, add the following methods.</span></span> <span data-ttu-id="9d9b9-158">Este código se conecta al centro de notificaciones usando la información de conexión especificada en HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="9d9b9-159">Luego proporciona el token del dispositivo al centro de notificaciones para que el centro de notificaciones pueda enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="9d9b9-160">En el mismo archivo, agregue el siguiente método para mostrar una **UIAlert** si la notificación se recibe mientras la aplicación está activa:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="9d9b9-161">Compile y ejecute la aplicación en el dispositivo para comprobar si hay errores.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="9d9b9-162">Prueba de envío de las notificaciones push</span><span class="sxs-lookup"><span data-stu-id="9d9b9-162">Send test push notifications</span></span>
<span data-ttu-id="9d9b9-163">Para probar la recepción de notificaciones en la aplicación, envíe notificaciones push en el [Portal de Azure] a través de la sección **Solución del problemas** en la hoja del centro de notificaciones (utilice la opción *Envío de prueba* ).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Portal de Azure: envío de prueba][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="9d9b9-165">(Opcional) Envío de notificaciones push desde la aplicación</span><span class="sxs-lookup"><span data-stu-id="9d9b9-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9d9b9-166">Este ejemplo sobre el envío de notificaciones desde la aplicación cliente se ha diseñado exclusivamente con fines informativos.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="9d9b9-167">`DefaultFullSharedAccessSignature` deberá estar presente en la aplicación cliente, lo que supone un riesgo para el Centro de notificaciones, ya que un usuario podría obtener acceso para enviar notificaciones no autorizadas a los clientes.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="9d9b9-168">Si desea enviar notificaciones push desde dentro de una aplicación, esta sección le proporciona un ejemplo de cómo hacerlo mediante la interfaz REST.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="9d9b9-169">En XCode, abra `Main.storyboard` y agregue los siguientes componentes de interfaz de usuario de la biblioteca de objetos para permitir que el usuario envíe notificaciones push en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="9d9b9-170">Una etiqueta sin texto de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-170">A label with no label text.</span></span> <span data-ttu-id="9d9b9-171">Se usará para notificar errores al enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="9d9b9-172">La propiedad **Lines** se debe establecer en **0** para que el tamaño se ajuste automáticamente a los márgenes derecho e izquierdo y a la parte superior de la vista.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="9d9b9-173">Un campo de texto con el texto de **Placeholder** (Marcador de posición) establecido en **Enter Notification Message** (Escribir mensaje de notificación).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="9d9b9-174">Restrinja el campo justo debajo de la etiqueta, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="9d9b9-175">Establezca el Controlador de vista como delegado de salida.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="9d9b9-176">Un botón llamado **Send Notification** (Enviar notificación) se restringió justo debajo del campo de texto y horizontalmente en el centro.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="9d9b9-177">La vista debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-177">The view should look as follows:</span></span>
     
     ![Diseñador de Xcode][32]
2. <span data-ttu-id="9d9b9-179">[Agregue salidas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) para la etiqueta y el campo de texto conectados a la vista y actualice la definición `interface` para que admita `UITextFieldDelegate` y `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="9d9b9-180">Agregue las tres declaraciones de propiedades que se muestran a continuación para ayudar a admitir la llamada a la API de REST y el análisis de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="9d9b9-181">El archivo ViewController.h debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d9b9-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="9d9b9-182">Abra `HubInfo.h` y agregue las siguientes constantes que se usarán para enviar notificaciones a su centro.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="9d9b9-183">Reemplace el literal de cadena del marcador de posición por la cadena de conexión *DefaultFullSharedAccessSignature* real.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="9d9b9-184">Agregue las siguientes instrucciones `#import` al archivo `ViewController.h`.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="9d9b9-185">En `ViewController.m` , agregue el siguiente código a la implementación de la interfaz.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="9d9b9-186">Este código analizará la cadena de conexión *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="9d9b9-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="9d9b9-187">Como se mencionó en la [Referencia de la API de REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), esta información analizada se usará para generar un token SaS para el encabezado de la solicitud **Autorización** .</span><span class="sxs-lookup"><span data-stu-id="9d9b9-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="9d9b9-188">En `ViewController.m`, actualice el método `viewDidLoad` para analizar la cadena de conexión cuando se cargue la vista.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="9d9b9-189">Agregue los métodos de utilidad que se muestran a continuación a la implementación de la interfaz.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="9d9b9-190">En `ViewController.m`, agregue el código siguiente a la implementación de interfaz para generar el token de autorización SaS que se proporcionará en el encabezado **Authorization** (Autorización) tal como se mencionó en la [Referencia de la API de REST](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="9d9b9-191">Presione Ctrl y arrastre desde el botón **Enviar notificación** hasta `ViewController.m` a fin de agregar una acción denominada **SendNotificationMessage** para el evento **Touch Down**.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="9d9b9-192">Método de actualización con el código siguiente para enviar la notificación mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-192">Update method with the following code to send the notification using the REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="9d9b9-193">En `ViewController.m`, agregue el siguiente método delegado para admitir el cierre del teclado para el campo de texto.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="9d9b9-194">Presione Ctrl y arrastre desde el campo de texto al icono de Controlador de vista en el diseñador de la interfaz para establecer el controlador de vista como el delegado de salida.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="9d9b9-195">En `ViewController.m`, agregue los siguientes métodos delegados para admitir el análisis de la respuesta mediante `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="9d9b9-196">Compile el proyecto y compruebe si hay errores.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="9d9b9-197">Si encuentra un error de compilación en Xcode7 relacionado con la compatibilidad de bitcode, debe cambiar el valor de **Build Settings (Configuración de compilación)** > **Enable Bitcode (ENABLE_BITCODE)** (Habilitar Bitcode [ENABLE_BITCODE]) a **NO** en Xcode.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="9d9b9-198">El SDK de los Centros de notificaciones no es compatible con bitcode.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="9d9b9-199">Puede buscar todas las cargas de notificaciones posibles en la guía [Local and Push Notification Programming Guide]de Apple.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="9d9b9-200">Comprobación de si la aplicación puede recibir notificaciones push</span><span class="sxs-lookup"><span data-stu-id="9d9b9-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="9d9b9-201">Para probar las notificaciones push en iOS, debe implementar la aplicación en un dispositivo iOS físico.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="9d9b9-202">No puede enviar notificaciones push de Apple con el simulador de iOS.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="9d9b9-203">Ejecute la aplicación y compruebe que el registro se realiza correctamente, luego presione **OK**(Aceptar).</span><span class="sxs-lookup"><span data-stu-id="9d9b9-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Prueba de registro de notificación push de aplicación iOS][33]
2. <span data-ttu-id="9d9b9-205">Puede enviar una notificación push de prueba desde el [Portal de Azure], como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="9d9b9-206">Si agregó código para enviar las notificaciones push en la aplicación, pulse dentro del campo de texto para escribir un mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="9d9b9-207">A continuación, pulse el botón **Send** (Enviar) en el teclado, o el botón **Send Notification** (Enviar notificación) en la vista, para enviar el mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![Prueba de envío de notificación push de aplicación iOS][34]
3. <span data-ttu-id="9d9b9-209">La notificación push se envía a todos los dispositivos registrados para recibir las notificaciones desde el Centro de notificaciones concreto.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![Prueba de recepción de notificación push de aplicación iOS][35]

## <a name="next-steps"></a><span data-ttu-id="9d9b9-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d9b9-211">Next steps</span></span>
<span data-ttu-id="9d9b9-212">En este sencillo ejemplo, se difunden notificaciones push a todos los dispositivos iOS registrados.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="9d9b9-213">Como paso siguiente en su aprendizaje le sugerimos que continúe con el tutorial [Los Centros de notificaciones de Azure notifican a los usuarios para iOS con back-end de .NET] , que le guiará a través de la creación de un back-end para enviar notificaciones push mediante etiquetas.</span><span class="sxs-lookup"><span data-stu-id="9d9b9-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="9d9b9-214">Si desea segmentar sus usuarios por grupos de interés, puede leer también el tutorial [Uso de los Centros de notificaciones para enviar noticias de última hora] .</span><span class="sxs-lookup"><span data-stu-id="9d9b9-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="9d9b9-215">Para más información sobre los Centros de notificaciones, consulte [Introducción a los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="9d9b9-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
<span data-ttu-id="9d9b9-216">[SDK de iOS versión 1.2.4 para Servicios móviles]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="9d9b9-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="9d9b9-217">[Introducción a los centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="9d9b9-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="9d9b9-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="9d9b9-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="9d9b9-219">[Los Centros de notificaciones de Azure notifican a los usuarios para iOS con back-end de .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span><span class="sxs-lookup"><span data-stu-id="9d9b9-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="9d9b9-220">[Uso de los Centros de notificaciones para enviar noticias de última hora]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="9d9b9-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="9d9b9-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="9d9b9-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="9d9b9-222">[Portal de Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9d9b9-222">[Azure Portal]: https://portal.azure.com</span></span>
