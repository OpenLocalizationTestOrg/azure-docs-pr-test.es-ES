---
title: Acceso a sus aplicaciones desde cualquier dispositivo | Microsoft Docs
description: "Obtenga información sobre qué clientes son compatibles con Azure RemoteApp y cómo tener acceso a sus aplicaciones."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="0a2d8-103">Acceso a las aplicaciones de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0a2d8-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0a2d8-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0a2d8-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="0a2d8-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0a2d8-106">Una de las ventajas de Azure RemoteApp es que puede tener acceso a las aplicaciones desde cualquiera de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="0a2d8-107">Aún mejor, puede comenzar a trabajar en un dispositivo y, a continuación, realizar una transición a un segundo dispositivo y continuar el trabajo desde donde lo dejó.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="0a2d8-108">Para empezar, deberá descargar el cliente apropiado para el dispositivo e iniciar sesión en el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="0a2d8-109">En este tema, revisaremos los clientes admitidos actualmente y cómo descargarlos antes de mostrar cómo iniciar sesión en RemoteApp desde cada uno de los clientes.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="0a2d8-110">Clientes compatibles</span><span class="sxs-lookup"><span data-stu-id="0a2d8-110">Supported clients</span></span>
<span data-ttu-id="0a2d8-111">Puede acceder a RemoteApp mediante los siguientes pasos si el dispositivo está ejecutando uno de estos sistemas operativos:</span><span class="sxs-lookup"><span data-stu-id="0a2d8-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="0a2d8-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="0a2d8-112">Windows 10</span></span> 
* <span data-ttu-id="0a2d8-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="0a2d8-113">Windows 8.1</span></span>
* <span data-ttu-id="0a2d8-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="0a2d8-114">Windows 8</span></span>
* <span data-ttu-id="0a2d8-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="0a2d8-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="0a2d8-116">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="0a2d8-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="0a2d8-117">iOS</span><span class="sxs-lookup"><span data-stu-id="0a2d8-117">iOS</span></span>
* <span data-ttu-id="0a2d8-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="0a2d8-118">Mac OS X</span></span>
* <span data-ttu-id="0a2d8-119">Android</span><span class="sxs-lookup"><span data-stu-id="0a2d8-119">Android</span></span>

 <span data-ttu-id="0a2d8-120">Información acerca de los clientes ligeros.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-120">What about thin clients?</span></span> <span data-ttu-id="0a2d8-121">Se admiten los siguientes clientes ligeros de Windows Embedded:</span><span class="sxs-lookup"><span data-stu-id="0a2d8-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="0a2d8-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="0a2d8-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="0a2d8-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="0a2d8-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="0a2d8-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="0a2d8-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="0a2d8-125">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="0a2d8-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="0a2d8-126">Descarga del cliente</span><span class="sxs-lookup"><span data-stu-id="0a2d8-126">Downloading the client</span></span>
<span data-ttu-id="0a2d8-127">Independientemente de la plataforma que esté utilizando, el cliente que necesita que acceda a RemoteApp puede encontrarse en la página [Descarga del cliente de Escritorio remoto](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0a2d8-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="0a2d8-128">Al hacer clic en los diferentes vínculos se comenzará a descargar el cliente directamente o será dirigido a la página de descarga del cliente descarga de la tienda de aplicaciones de esa plataforma.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="0a2d8-129">Siga las instrucciones en pantalla para instalar el cliente.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="0a2d8-130">Una vez haya instalado el cliente en el dispositivo y lo haya iniciado, salte a la sección correspondiente a continuación para obtener información sobre cómo iniciar sesión en RemoteApp desde ese cliente.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="0a2d8-131">Android</span><span class="sxs-lookup"><span data-stu-id="0a2d8-131">Android</span></span>
<span data-ttu-id="0a2d8-132">Una vez haya instalado la aplicación de Escritorio remoto de Microsoft desde la tienda Google Play, podrá encontrarla en la lista de aplicaciones en **Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="0a2d8-133">Al iniciar la aplicación se accede a un Centro de conexiones vacío, a menos que ya ha utilizado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="0a2d8-134">Para empezar a trabajar con Azure RemoteApp, toque el botón Agregar **"" +""** y **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Centro de conexiones vacío](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="0a2d8-136">Debe iniciar sesión con su dirección de correo electrónico para tener acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="0a2d8-137">Pulse **Primeros pasos**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-137">Tap **Get started**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="0a2d8-139">En la siguiente página, escriba en su **dirección de correo electrónico** y toque **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="0a2d8-140">Esto comenzará el proceso de inicio de sesión mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![Primera página de Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="0a2d8-142">Siga las instrucciones en pantalla para iniciar sesión con su cuenta de Microsoft (denominada anteriormente "LiveID") o su id. de organización.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="0a2d8-143">En cuanto haya iniciado sesión, es posible que se le presente una página con todas las invitaciones que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="0a2d8-144">Si es así, seleccione las invitaciones de confianza y toque en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![Página de invitaciones](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="0a2d8-146">Después de aceptar las invitaciones, se descargará en el dispositivo la lista de aplicaciones a las que tiene acceso y estarán disponibles en el Centro de la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="0a2d8-147">Toque una de las aplicaciones para empezar a usarla.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-147">Tap one of the apps to start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="0a2d8-149">Si todavía no tiene una invitación, todavía puede probar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="0a2d8-150">Para ello, toque **Ir a la versión de prueba gratuita** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="0a2d8-152">Esto le dará acceso a un conjunto básico de aplicaciones para comenzar a usar RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="0a2d8-154">iOS</span><span class="sxs-lookup"><span data-stu-id="0a2d8-154">iOS</span></span>
<span data-ttu-id="0a2d8-155">Una vez haya instalado la aplicación de Escritorio remoto de Microsoft desde App Store, podrá encontrarla en la lista de aplicaciones en **Cliente de RD**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="0a2d8-156">Al iniciar la aplicación se accede a un Centro de conexiones vacío, a menos que ya ha utilizado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="0a2d8-157">Para empezar a trabajar con Azure RemoteApp, toque el botón de agregar **""+""** y **Agregar Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Centro de conexiones vacío](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="0a2d8-159">Debe iniciar sesión con su dirección de correo electrónico para tener acceso al servicio. Para iniciar ese proceso, escriba su **dirección de correo electrónico** y toque **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="0a2d8-161">Siga las instrucciones en pantalla para iniciar sesión con su cuenta de Microsoft (LiveID) o su id. de organización.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0a2d8-162">En cuanto haya iniciado sesión, es posible que se le presente una página con todas las invitaciones que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="0a2d8-163">Si es así, seleccione las invitaciones de confianza y toque en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![Página de invitaciones](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="0a2d8-165">Después de aceptar las invitaciones, se descargará en el dispositivo la lista de aplicaciones a las que tiene acceso y estarán disponibles en el Centro de la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="0a2d8-166">Toque una de las aplicaciones para iniciarla y empezar a usarla.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="0a2d8-168">Si todavía no tiene una invitación, todavía puede probar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="0a2d8-169">Para ello, toque **Ir a la versión de prueba gratuita** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="0a2d8-171">Esto le dará acceso a un conjunto básico de aplicaciones para comenzar a usar RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="0a2d8-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="0a2d8-173">Mac OS X</span></span>
<span data-ttu-id="0a2d8-174">Una vez haya instalado la aplicación de Escritorio remoto de Microsoft desde la App Store, podrá encontrarla en la lista de aplicaciones en **Escritorio remoto de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="0a2d8-175">Al iniciar la aplicación se accede a un Centro de conexiones vacío, a menos que ya ha utilizado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="0a2d8-176">Para empezar a trabajar con Azure RemoteApp, haga clic en el botón **Azure RemoteApp** .</span><span class="sxs-lookup"><span data-stu-id="0a2d8-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![Centro de conexiones vacío](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="0a2d8-178">Debe iniciar sesión con su dirección de correo electrónico para tener acceso al servicio. Para iniciar ese proceso, toque **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="0a2d8-180">En la siguiente página, escriba en su **dirección de correo electrónico** y toque **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="0a2d8-181">Esto comenzará el proceso de inicio de sesión mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Primera página de Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="0a2d8-183">Siga las instrucciones en pantalla para iniciar sesión con su cuenta de Microsoft (LiveID) o su id. de organización.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0a2d8-184">En cuanto haya iniciado sesión, es posible que se le presente una página con todas las invitaciones que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="0a2d8-185">Si es así, seleccione las invitaciones de confianza y cierre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![Página de invitaciones](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="0a2d8-187">Después de aceptar las invitaciones, se descargará en el dispositivo la lista de aplicaciones a las que tiene acceso y estarán disponibles en el Centro de la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="0a2d8-188">Haga doble clic en una de las aplicaciones para iniciarla y empezar a usarla.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="0a2d8-190">Si todavía no tiene una invitación, todavía puede probar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="0a2d8-191">Para ello, haga clic en **Ir a la versión de prueba gratuita** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="0a2d8-193">Esto le dará acceso a un conjunto básico de aplicaciones para comenzar a usar RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="0a2d8-195">Windows (todas las versiones compatibles excepto Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="0a2d8-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="0a2d8-196">El cliente se inicia automáticamente una vez finalizada la instalación, sin embargo, cuando necesite tener acceso a este más adelante, lo encontrará en la lista de aplicaciones con el nombre **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="0a2d8-197">Después de iniciar el cliente, la primera página que verá le dará la bienvenida a Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="0a2d8-198">Para continuar, haga clic en **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-198">To proceed, click on **Get Started**.</span></span>
   
    ![Página de bienvenida del cliente RemoteApp de Azure](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="0a2d8-200">La página siguiente inicia el proceso de inicio de sesión de Azure RemoteApp mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="0a2d8-201">Este proceso debe resultarle familiar si ha usado servicios Microsoft en el pasado.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="0a2d8-202">Comience escribiendo su **dirección de correo electrónico** y haga clic en **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Primer aviso del sistema de Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="0a2d8-204">Siga las instrucciones en pantalla para iniciar sesión con su cuenta de Microsoft (LiveID) o su id. de organización.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0a2d8-205">En cuanto haya iniciado sesión, es posible que se le presente una página con todas las invitaciones que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="0a2d8-206">Si es así, seleccione las invitaciones de confianza y haga clic en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Página de invitaciones del cliente RemoteApp de Azure](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="0a2d8-208">Después de aceptar las invitaciones, se descargará en el dispositivo la lista de aplicaciones a las que tiene acceso y estarán disponibles en el Centro de la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="0a2d8-209">Haga doble clic en una de las aplicaciones para iniciarla y empezar a usarla.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Centro de conexiones del cliente RemoteApp de Azure](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="0a2d8-211">No se preocupe si nadie le ha enviado una invitación aún, nosotros nos ocupamos.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="0a2d8-212">Continuará teniendo acceso a una colección de demostración para que pueda probar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="0a2d8-214">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="0a2d8-214">Windows Phone 8.1</span></span>
<span data-ttu-id="0a2d8-215">Una vez haya instalado la aplicación de Escritorio remoto de Microsoft desde la tienda Windows Phone 8.1, podrá encontrarla en la lista de aplicaciones en **Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="0a2d8-216">Al iniciar la aplicación se accede directamente a un Centro de conexiones vacío, a menos que ya ha utilizado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="0a2d8-217">Para empezar a trabajar con Azure RemoteApp, toque el botón de agregar **""+""** en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![Centro de conexiones vacío](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="0a2d8-219">A continuación, toque **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Agregar página de elemento](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="0a2d8-221">Debe iniciar sesión con su dirección de correo electrónico para tener acceso al servicio. Para iniciar este proceso, toque **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="0a2d8-223">En la siguiente página, escriba en su **dirección de correo electrónico** y toque **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="0a2d8-224">Esto comenzará el proceso de inicio de sesión mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Primera página de Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="0a2d8-226">Siga las instrucciones en pantalla para iniciar sesión con su cuenta de Microsoft (LiveID) o su id. de organización.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0a2d8-227">En cuanto haya iniciado sesión, es posible que se le presente una página con todas las invitaciones que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="0a2d8-228">Si es así, seleccione las invitaciones de confianza y toque **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![Página de invitaciones](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="0a2d8-230">Después de aceptar las invitaciones, se descargará en el dispositivo la lista de aplicaciones a las que tiene acceso y estarán disponibles en el Centro de la conexión.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="0a2d8-231">Toque una de las aplicaciones para iniciarla y empezar a usarla.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="0a2d8-233">Si todavía no tiene una invitación, todavía puede probar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="0a2d8-234">Para ello, toque **Sí** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-234">To do so, tap **yes** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="0a2d8-236">Esto le dará acceso a un conjunto básico de aplicaciones para comenzar a usar RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0a2d8-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/WinPhone8.png)

