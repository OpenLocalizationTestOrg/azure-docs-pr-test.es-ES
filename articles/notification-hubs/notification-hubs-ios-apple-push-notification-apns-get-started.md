---
title: "aaaSending tooiOS de notificaciones de inserción con centros de notificaciones de Azure | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de tooan de notificaciones."
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
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="5702b-104">Enviar tooiOS de notificaciones de inserción con centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5702b-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5702b-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5702b-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="5702b-106">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="5702b-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5702b-107">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5702b-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5702b-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="5702b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="5702b-109">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de tooan de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5702b-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="5702b-110">Se creará una aplicación de iOS en blanco que recibe notificaciones de inserción mediante hello [servicio de notificaciones de inserción de Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="5702b-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="5702b-111">Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5702b-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5702b-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="5702b-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="5702b-113">código de Hello completado para este tutorial se puede encontrar [en GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="5702b-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5702b-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5702b-114">Prerequisites</span></span>
<span data-ttu-id="5702b-115">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="5702b-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="5702b-116">[servicios móviles iOS SDK versión 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="5702b-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="5702b-117">La versión más reciente de [Xcode]</span><span class="sxs-lookup"><span data-stu-id="5702b-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="5702b-118">Un dispositivo compatible con iOS 8 (o una versión posterior)</span><span class="sxs-lookup"><span data-stu-id="5702b-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="5702b-119">[programa para desarrolladores de Apple](https://developer.apple.com/programs/)</span><span class="sxs-lookup"><span data-stu-id="5702b-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5702b-120">Debido a los requisitos de configuración para las notificaciones de inserción, debe implementar y probar las notificaciones de inserción en un dispositivo físico iOS (iPhone o iPad) en lugar de simulador de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="5702b-121">La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones iOS.</span><span class="sxs-lookup"><span data-stu-id="5702b-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="5702b-122">Configuración del Centro de notificaciones para notificaciones push de iOS</span><span class="sxs-lookup"><span data-stu-id="5702b-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="5702b-123">En esta sección le guía a través de la creación de un nuevo centro de notificaciones y configurar la autenticación con APNS mediante hello **. p12** certificado de inserción que creó.</span><span class="sxs-lookup"><span data-stu-id="5702b-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="5702b-124">Si desea toouse un centro de notificaciones que ya haya creado, puede omitir toostep 5.</span><span class="sxs-lookup"><span data-stu-id="5702b-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="5702b-125">Haga clic en hello <b>Notification Services</b> botón en hello <b>configuración</b> blade, a continuación, seleccione <b>Apple (APN)</b>.</span><span class="sxs-lookup"><span data-stu-id="5702b-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="5702b-126">Haga clic en <b>cargar certificado</b> y seleccione hello <b>. p12</b> archivo que exportó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5702b-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="5702b-127">Asegúrese de que también especificar contraseña correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="5702b-128">Asegúrese de que tooselect <b>espacio aislado</b> modo ya que esto es para el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="5702b-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="5702b-129">Usar solo hello <b>producción</b> si desea toousers de notificaciones de inserción de toosend que han adquirido la aplicación desde el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="5702b-130">&emsp;&emsp;&emsp;&emsp;![Configurar APN en Portal de Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="5702b-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Configuración de certificados APNs en el Portal de Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="5702b-132">El centro de notificaciones está ahora configurado toowork con APNS, y tiene la aplicación de tooregister de cadenas de conexión de Hola y enviar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="5702b-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="5702b-133">Conectar su tooNotification de aplicación de iOS centros</span><span class="sxs-lookup"><span data-stu-id="5702b-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="5702b-134">En Xcode, cree un nuevo proyecto de iOS y seleccione hello **única aplicación de vista** plantilla.</span><span class="sxs-lookup"><span data-stu-id="5702b-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode: aplicación de vista única][8]
    
2. <span data-ttu-id="5702b-136">Al configurar las opciones de hello para el proyecto nuevo, asegúrese de que toouse Hola mismo **Product Name** y **identificador de la organización** que ha usado al establecidos previamente Id. del lote de hello en hello para desarrolladores de Apple Portal.</span><span class="sxs-lookup"><span data-stu-id="5702b-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode: opciones de proyecto][11]
    
3. <span data-ttu-id="5702b-138">En **destinos**, haga clic en el nombre del proyecto, haga clic en hello **configuración de generación** pestaña y expanda **identidad de firma de código**y, a continuación, en **depurar**, establecer la identidad de firma de código.</span><span class="sxs-lookup"><span data-stu-id="5702b-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="5702b-139">Alternar **niveles** de **básica** demasiado**todos los**y establezca **perfil de aprovisionamiento de** toohello perfil que creó previamente de aprovisionamiento .</span><span class="sxs-lookup"><span data-stu-id="5702b-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="5702b-140">Si no ve Hola nuevo perfil que creó en Xcode de aprovisionamiento, pruebe a actualizar los perfiles de hello para la identidad de firma.</span><span class="sxs-lookup"><span data-stu-id="5702b-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="5702b-141">Haga clic en **Xcode** en la barra de menús de hello, haga clic en **preferencias**, haga clic en hello **cuenta** , haga clic en hello **ver detalles** botón, haga clic en el identidad de firma y, a continuación, haga clic en el botón de actualización de hello en la esquina inferior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode: perfil de aprovisionamiento][9]
4. <span data-ttu-id="5702b-143">Descargar hello [servicios móviles iOS SDK versión 1.2.4] y descomprima el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="5702b-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="5702b-144">En Xcode, haga clic en el proyecto y haga clic en hello **agregar archivos a** Hola de opción tooadd **WindowsAzureMessaging.framework** proyecto de Xcode tooyour de carpeta.</span><span class="sxs-lookup"><span data-stu-id="5702b-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="5702b-145">Seleccione **Copy items if needed** (Copiar elementos si es necesario) y luego haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="5702b-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5702b-146">centros de notificaciones de Hello SDK no admite actualmente bitcode en Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="5702b-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="5702b-147">Debe establecer **habilitar Bitcode** demasiado**No** en hello **opciones de compilación** para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="5702b-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Descompresión del SDK de Azure][10]
5. <span data-ttu-id="5702b-149">Agregue un nuevo proyecto de tooyour de archivo de encabezado denominado `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="5702b-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="5702b-150">Este archivo contendrá constantes de hello para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5702b-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="5702b-151">Agregar Hola siguiendo las definiciones y reemplace los marcadores de literal de cadena de hello con su *nombre del concentrador* hello y *DefaultListenSharedAccessSignature* que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5702b-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="5702b-152">Abra su `AppDelegate.h` archivo agregar Hola siguiendo las directivas de importación:</span><span class="sxs-lookup"><span data-stu-id="5702b-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="5702b-153">En su `AppDelegate.m file`, agregar Hola después el código de hello `didFinishLaunchingWithOptions` método en función de su versión de iOS.</span><span class="sxs-lookup"><span data-stu-id="5702b-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="5702b-154">Este código registra el identificador de dispositivo en APNS:</span><span class="sxs-lookup"><span data-stu-id="5702b-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="5702b-155">Para iOS 8:</span><span class="sxs-lookup"><span data-stu-id="5702b-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="5702b-156">Para too8 anteriores versiones de iOS:</span><span class="sxs-lookup"><span data-stu-id="5702b-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="5702b-157">En Hola el mismo archivo, agregue Hola siguiendo métodos.</span><span class="sxs-lookup"><span data-stu-id="5702b-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="5702b-158">Este código conecta toohello centro de notificaciones utilizando información de conexión de Hola que especificó en HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="5702b-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="5702b-159">A continuación, ofrece centro de notificaciones de token toohello de dispositivo de Hola para que hello centro de notificaciones puede enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="5702b-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="5702b-160">En Hola el mismo archivo, agregue Hola siguiendo el método toodisplay una **UIAlert** si se recibe la notificación de hello mientras está activa la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="5702b-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="5702b-161">Compile y ejecute la aplicación hello en su tooverify de dispositivo que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="5702b-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="5702b-162">Prueba de envío de las notificaciones push</span><span class="sxs-lookup"><span data-stu-id="5702b-162">Send test push notifications</span></span>
<span data-ttu-id="5702b-163">Puede probar recibir notificaciones en la aplicación mediante el envío de notificaciones de inserción en hello [Portal de Azure] a través de hello **solución de problemas** sección en la hoja de la base de datos central de hello (usar hello *probar envío* opción).</span><span class="sxs-lookup"><span data-stu-id="5702b-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Portal de Azure: envío de prueba][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="5702b-165">(Opcional) Enviar notificaciones de inserción de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="5702b-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5702b-166">Este ejemplo de envío de notificaciones de la aplicación de cliente de hello se proporciona con fines de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="5702b-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="5702b-167">Puesto que esto requerirá hello `DefaultFullSharedAccessSignature` toobe presente en la aplicación de cliente de hello, expone el riesgo de toohello de concentrador de notificación que un usuario puede obtener acceso no autorizado de toosend notificaciones tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="5702b-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="5702b-168">Si desea que las notificaciones de inserción toosend desde dentro de una aplicación, esta sección proporciona un ejemplo de cómo toodo esta mediante Hola interfaz REST.</span><span class="sxs-lookup"><span data-stu-id="5702b-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="5702b-169">En Xcode, abra `Main.storyboard` y agregue Hola siguientes componentes de interfaz de usuario de hello objeto biblioteca tooallow Hola usuario toosend notificaciones de inserción en la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="5702b-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="5702b-170">Una etiqueta sin texto de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="5702b-170">A label with no label text.</span></span> <span data-ttu-id="5702b-171">Será usado tooreport errores en el envío de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5702b-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="5702b-172">Hola **líneas** propiedad debe establecerse demasiado**0** para que ajustará automáticamente el tamaño toohello restringida derecha y los márgenes izquierdos y parte superior de Hola de vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="5702b-173">Un campo de texto con **marcador de posición** texto se establece demasiado**escribir mensaje de notificación**.</span><span class="sxs-lookup"><span data-stu-id="5702b-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="5702b-174">Restringir campo Hola justo debajo de la etiqueta de hello tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="5702b-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="5702b-175">Establecer Hola View Controller como delegado de toma de corriente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="5702b-176">Un botón denominado **enviar notificación** limitada justo debajo de campo de texto de Hola y en el centro de hello horizontal.</span><span class="sxs-lookup"><span data-stu-id="5702b-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="5702b-177">vista de Hello debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="5702b-177">hello view should look as follows:</span></span>
     
     ![Diseñador de Xcode][32]
2. <span data-ttu-id="5702b-179">[Agregar salidas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) de campo de etiqueta y el texto hello conectado a la vista y actualizar su `interface` definición toosupport `UITextFieldDelegate` y `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="5702b-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="5702b-180">Agregue tres declaraciones de propiedad Hola que se muestra por debajo del soporte de toohelp llamando a Hola API de REST y analizar la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="5702b-181">El archivo ViewController.h debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="5702b-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="5702b-182">Abra `HubInfo.h` y agregue Hola después de constantes que se usará para el envío de concentrador de tooyour de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5702b-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="5702b-183">Reemplace el literal de cadena de marcador de posición de Hola por su real *DefaultFullSharedAccessSignature* cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="5702b-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="5702b-184">Agregue los siguiente hello `#import` instrucciones tooyour `ViewController.h` archivo.</span><span class="sxs-lookup"><span data-stu-id="5702b-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="5702b-185">En `ViewController.m` agregue Hola después de la implementación de interfaz de toohello de código.</span><span class="sxs-lookup"><span data-stu-id="5702b-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="5702b-186">Este código analizará la cadena de conexión *DefaultFullSharedAccessSignature* .</span><span class="sxs-lookup"><span data-stu-id="5702b-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="5702b-187">Como se mencionó en hello [referencia de la API de REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), esta información analizada será toogenerate usa un token de SaS para hello **autorización** encabezado de solicitud.</span><span class="sxs-lookup"><span data-stu-id="5702b-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="5702b-188">En `ViewController.m`, actualización hello `viewDidLoad` cadena de conexión de Hola de método tooparse cuando se carga la vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="5702b-189">Agregar métodos de utilidad de hello, se muestra a continuación, implementación de la interfaz de toohello.</span><span class="sxs-lookup"><span data-stu-id="5702b-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

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





1. <span data-ttu-id="5702b-190">En `ViewController.m`, agregar Hola después código toohello interfaz implementación toogenerate Hola autorización token de SaS que se proporcionará en hello **autorización** encabezado, tal y como se mencionó en hello [API de REST Referencia](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="5702b-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
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
2. <span data-ttu-id="5702b-191">CTRL + arrastrar de Hola **enviar notificación** botón demasiado`ViewController.m` tooadd una acción denominada **SendNotificationMessage** para hello **Touch hacia abajo** eventos.</span><span class="sxs-lookup"><span data-stu-id="5702b-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="5702b-192">Método de actualización con hello siguientes a la notificación de hello toosend de código mediante la API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
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
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
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
3. <span data-ttu-id="5702b-193">En `ViewController.m`, agregar Hola después toosupport de método de delegado Cerrar teclado hello para el campo de texto hello.</span><span class="sxs-lookup"><span data-stu-id="5702b-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="5702b-194">CTRL + arrastrar de icono View Controller toohello de campo de texto de Hola Hola Hola de diseñador tooset de interfaz ver controlador como delegado de toma de corriente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="5702b-195">En `ViewController.m`, agregar siguiente Hola delegar la respuesta de métodos toosupport análisis hello mediante `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="5702b-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
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
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="5702b-196">Compile el proyecto de Hola y compruebe que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="5702b-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="5702b-197">Si se produce un error de compilación en Xcode7 sobre la compatibilidad de bitcode, debe cambiar hello **configuración de generación** > **Bitcode habilitar (ENABLE_BITCODE)** demasiado**n** en Xcode.</span><span class="sxs-lookup"><span data-stu-id="5702b-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="5702b-198">Hola SDK de los centros de notificación no admite actualmente la bitcode.</span><span class="sxs-lookup"><span data-stu-id="5702b-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="5702b-199">Puede encontrar todas las cargas de notificación posibles Hola Hola Apple [locales y Guía de programación de notificaciones de inserción].</span><span class="sxs-lookup"><span data-stu-id="5702b-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="5702b-200">Comprobación de si la aplicación puede recibir notificaciones push</span><span class="sxs-lookup"><span data-stu-id="5702b-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="5702b-201">notificaciones de inserción de tootest en iOS, debe implementar el dispositivo de E/s físicas de hello aplicación tooa.</span><span class="sxs-lookup"><span data-stu-id="5702b-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="5702b-202">No se puede enviar notificaciones de inserción de Apple mediante el simulador de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="5702b-203">Ejecute la aplicación hello y compruebe que el registro se realiza correctamente y, a continuación, presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5702b-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Prueba de registro de notificación push de aplicación iOS][33]
2. <span data-ttu-id="5702b-205">Puede enviar una notificación de inserción de prueba de hello [Portal de Azure], tal y como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5702b-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="5702b-206">Si agrega código para enviar notificaciones de inserción en la aplicación hello, toque tooenter de campo de texto hello dentro de un mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="5702b-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="5702b-207">A continuación, presione hello **enviar** botón de teclado de Hola o hello **enviar notificación** botón en el mensaje de notificación de hello vista toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="5702b-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Prueba de envío de notificación push de aplicación iOS][34]
3. <span data-ttu-id="5702b-209">Hello notificación de inserción se envía tooall dispositivos registrado tooreceive notificaciones Hola Hola determinado centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5702b-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Prueba de recepción de notificación push de aplicación iOS][35]

## <a name="next-steps"></a><span data-ttu-id="5702b-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5702b-211">Next steps</span></span>
<span data-ttu-id="5702b-212">En este sencillo ejemplo, difunden tooall de notificaciones de inserción los dispositivos iOS registrados.</span><span class="sxs-lookup"><span data-stu-id="5702b-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="5702b-213">Se recomienda el siguiente paso en el aprendizaje que continúe toohello [Azure notificación centros de informar a los usuarios de iOS con back-end de .NET] tutorial, que le guiará por la creación de una inserción de toosend de back-end mediante etiquetas de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5702b-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="5702b-214">Si desea toosegment los usuarios por grupos de interés, además puede mover en toohello [toosend de centros de notificaciones utilice noticias de última hora] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5702b-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="5702b-215">Para más información sobre los Centros de notificaciones, consulte [Introducción a los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="5702b-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
[servicios móviles iOS SDK versión 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Introducción a los centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure notificación centros de informar a los usuarios de iOS con back-end de .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[locales y Guía de programación de notificaciones de inserción]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Portal de Azure]: https://portal.azure.com
