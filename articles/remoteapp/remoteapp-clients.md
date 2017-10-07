---
title: aaaAccessing las aplicaciones desde cualquier dispositivo | Documentos de Microsoft
description: "Obtenga información acerca de qué clientes son compatibles con Azure RemoteApp y cómo tooaccess las aplicaciones."
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
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="02623-103">Acceso a las aplicaciones de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="02623-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="02623-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="02623-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="02623-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="02623-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="02623-106">Uno de los atractivos de Hola de RemoteApp de Azure es que puede tener acceso a aplicaciones desde cualquiera de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="02623-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="02623-107">Incluso mejor, puede empezar a trabajar en un dispositivo y, a continuación, simplificarán la transición tooa segundo dispositivo y retomar desde donde lo dejó.</span><span class="sxs-lookup"><span data-stu-id="02623-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="02623-108">tooget inició necesita el cliente apropiado de toodownload hello para el dispositivo e inicie sesión en el servicio toohello.</span><span class="sxs-lookup"><span data-stu-id="02623-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="02623-109">En este tema, revisaremos los clientes de hello admitidos actualmente y cómo toodownload ellos antes de mostrar cómo toosign en tooRemoteApp de cada uno de los clientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="02623-110">Clientes compatibles</span><span class="sxs-lookup"><span data-stu-id="02623-110">Supported clients</span></span>
<span data-ttu-id="02623-111">Puede tener acceso a RemoteApp mediante estos pasos Hola si el dispositivo está ejecutando uno de estos sistemas operativos:</span><span class="sxs-lookup"><span data-stu-id="02623-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="02623-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="02623-112">Windows 10</span></span> 
* <span data-ttu-id="02623-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="02623-113">Windows 8.1</span></span>
* <span data-ttu-id="02623-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="02623-114">Windows 8</span></span>
* <span data-ttu-id="02623-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="02623-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="02623-116">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="02623-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="02623-117">iOS</span><span class="sxs-lookup"><span data-stu-id="02623-117">iOS</span></span>
* <span data-ttu-id="02623-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="02623-118">Mac OS X</span></span>
* <span data-ttu-id="02623-119">Android</span><span class="sxs-lookup"><span data-stu-id="02623-119">Android</span></span>

 <span data-ttu-id="02623-120">¿Qué clientes ligeros? Hola siguientes se admiten clientes ligeros Windows Embedded:</span><span class="sxs-lookup"><span data-stu-id="02623-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="02623-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="02623-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="02623-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="02623-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="02623-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="02623-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="02623-124">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="02623-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="02623-125">Descargar el cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="02623-125">Downloading hello client</span></span>
<span data-ttu-id="02623-126">Independientemente de la plataforma que está usando, cliente hello necesita tooaccess RemoteApp puede encontrarse en hello [descarga de cliente de escritorio remoto](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="02623-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="02623-127">Al hacer clic en vínculos diferentes Hola ya sea directamente comenzarán a descargar el cliente de Hola o enviarán toohello página de descarga de cliente en la tienda de aplicaciones de Hola para esa plataforma.</span><span class="sxs-lookup"><span data-stu-id="02623-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="02623-128">Instalar a cliente de hello siguiendo las instrucciones de hello en pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="02623-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="02623-129">Una vez que haya instalado el cliente de hello en el dispositivo y lo inició, saltar toohello sección correspondiente a continuación toolearn cómo toosign en tooRemoteApp de ese cliente.</span><span class="sxs-lookup"><span data-stu-id="02623-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="02623-130">Android</span><span class="sxs-lookup"><span data-stu-id="02623-130">Android</span></span>
<span data-ttu-id="02623-131">Una vez haya instalado la aplicación de escritorio remoto de Microsoft de hello de hello Google Play store, lo encontrará en la lista de aplicaciones en **escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="02623-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="02623-132">Iniciar aplicación hello pone a disposición tooan vacía el centro de conexiones, a menos que ya ha estado utilizando aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="02623-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="02623-133">tooget a trabajar con Azure RemoteApp, puntee Hola Agregar botón **"" +""** y pulse **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="02623-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Centro de conexiones vacío](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="02623-135">Deberá toosign con su servicio de Hola de tooaccess de dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="02623-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="02623-136">Pulse **Primeros pasos**.</span><span class="sxs-lookup"><span data-stu-id="02623-136">Tap **Get started**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="02623-138">En la página siguiente de hello, escriba en su **dirección de correo electrónico** y pulse **continuar**.</span><span class="sxs-lookup"><span data-stu-id="02623-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="02623-139">Esto inicia Hola inicio de sesión en proceso con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02623-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![Primera página de Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="02623-141">Siga las instrucciones de Hola Hola pantalla toosign con su cuenta de Microsoft (anteriormente denominada "LiveID") o el identificador de organización.</span><span class="sxs-lookup"><span data-stu-id="02623-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="02623-142">Una vez iniciado sesión, puede aparecer una página de lista de todas las invitaciones de Hola que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="02623-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="02623-143">Si está, seleccione las invitaciones de hello confiar y pulse **realiza**.</span><span class="sxs-lookup"><span data-stu-id="02623-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![Página de invitaciones](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="02623-145">Después de aceptar su invitaciones, lista de Hola de las aplicaciones tienen acceso toowill ser dispositivo tooyour descargado y estará disponible en el centro de conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="02623-146">Puntee en uno de hello aplicaciones toostart con él.</span><span class="sxs-lookup"><span data-stu-id="02623-146">Tap one of hello apps toostart using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="02623-148">Si no tiene todavía una invitación, todavía puede probar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="02623-149">por lo tanto, pulse toodo **vaya toofree prueba** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="02623-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="02623-151">Esto le proporcionará acceso tooa conjunto básico de tooget aplicaciones para trabajar con conexión de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="02623-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="02623-153">iOS</span><span class="sxs-lookup"><span data-stu-id="02623-153">iOS</span></span>
<span data-ttu-id="02623-154">Una vez haya instalado la aplicación de escritorio remoto de Microsoft de hello de tienda de aplicaciones de hello, encontrará en la lista de aplicaciones en **cliente de escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="02623-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="02623-155">Iniciar aplicación hello pone a disposición tooan vacía el centro de conexiones, a menos que ya ha estado utilizando aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="02623-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="02623-156">tooget a trabajar con Azure RemoteApp, puntee Hola Agregar botón **"" +""** y pulse **agregar Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="02623-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Centro de conexiones vacío](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="02623-158">Deberá toosign con su servicio de saludo de correo electrónico dirección tooaccess, toostart dicho proceso, escriba su **dirección de correo electrónico** y pulse **continuar**.</span><span class="sxs-lookup"><span data-stu-id="02623-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="02623-160">Siga las instrucciones de Hola Hola pantalla toosign con su cuenta de Microsoft (Live ID) o el identificador de la organización.</span><span class="sxs-lookup"><span data-stu-id="02623-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="02623-161">Una vez iniciado sesión, puede aparecer una página de lista de todas las invitaciones de Hola que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="02623-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="02623-162">Si está, seleccione las invitaciones de hello confiar y pulse **realiza**.</span><span class="sxs-lookup"><span data-stu-id="02623-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![Página de invitaciones](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="02623-164">Después de aceptar su invitaciones, lista de Hola de las aplicaciones tienen acceso toowill ser dispositivo tooyour descargado y estará disponible en el centro de conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="02623-165">Puntee en uno de hello aplicaciones toolaunch y empieza a usarlo.</span><span class="sxs-lookup"><span data-stu-id="02623-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="02623-167">Si no tiene todavía una invitación, todavía puede probar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="02623-168">por lo tanto, pulse toodo **vaya toofree prueba** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="02623-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="02623-170">Esto le proporcionará acceso tooa conjunto básico de tooget aplicaciones para trabajar con conexión de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="02623-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="02623-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="02623-172">Mac OS X</span></span>
<span data-ttu-id="02623-173">Una vez haya instalado la aplicación de escritorio remoto de Microsoft de hello de tienda de aplicaciones de hello, encontrará en la lista de aplicaciones en **Microsoft Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="02623-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="02623-174">Iniciar aplicación hello pone a disposición tooan vacía el centro de conexiones, a menos que ya ha estado utilizando aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="02623-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="02623-175">tooget a trabajar con Azure RemoteApp, haga clic en hello **Azure RemoteApp** botón.</span><span class="sxs-lookup"><span data-stu-id="02623-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![Centro de conexiones vacío](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="02623-177">Necesita toosign con su servicio de saludo de correo electrónico dirección tooaccess, toostart que procesar, pulse **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="02623-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="02623-179">En la página siguiente de hello, escriba en su **dirección de correo electrónico** y pulse **continuar**.</span><span class="sxs-lookup"><span data-stu-id="02623-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="02623-180">Esto inicia Hola inicio de sesión en proceso con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02623-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Primera página de Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="02623-182">Siga las instrucciones de Hola Hola pantalla toosign con su cuenta de Microsoft (Live ID) o el identificador de la organización.</span><span class="sxs-lookup"><span data-stu-id="02623-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="02623-183">Una vez iniciado sesión, puede aparecer una página de lista de todas las invitaciones de Hola que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="02623-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="02623-184">Si está, seleccione las invitaciones de hello confía y cerrar el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![Página de invitaciones](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="02623-186">Después de aceptar su invitaciones, lista de Hola de las aplicaciones tienen acceso toowill ser dispositivo tooyour descargado y estará disponible en el centro de conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="02623-187">Haga doble clic en uno de hello aplicaciones toolaunch y empieza a usarlo.</span><span class="sxs-lookup"><span data-stu-id="02623-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="02623-189">Si no tiene todavía una invitación, todavía puede probar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="02623-190">por lo tanto, haga clic en la toodo **vaya toofree prueba** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="02623-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="02623-192">Esto le proporcionará acceso tooa conjunto básico de tooget aplicaciones para trabajar con conexión de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="02623-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="02623-194">Windows (todas las versiones compatibles excepto Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="02623-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="02623-195">Hola client se inicia automáticamente cuando finaliza la instalación, sin embargo cuando necesite tooaccess más tarde puede encontrarse en la lista de aplicaciones en nombre de hello **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="02623-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="02623-196">Más arde iniciar a cliente hello, primera página de hello verá agradece tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="02623-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="02623-197">tooproceed, haga clic en **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="02623-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Página de bienvenida del cliente de Azure RemoteApp Hola](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="02623-199">página siguiente de Hello inicia Hola inicio de sesión en proceso de Azure RemoteApp con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02623-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="02623-200">Este proceso debe resultarle familiar si ha usado los servicios de Microsoft en hello anterior.</span><span class="sxs-lookup"><span data-stu-id="02623-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="02623-201">Comience escribiendo su **dirección de correo electrónico** y haga clic en **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="02623-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Primer aviso del sistema de Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="02623-203">Siga las instrucciones de Hola Hola pantalla toosign con su cuenta de Microsoft (Live ID) o el identificador de la organización.</span><span class="sxs-lookup"><span data-stu-id="02623-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="02623-204">Una vez iniciado sesión, puede aparecer una página de lista de todas las invitaciones de Hola que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="02623-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="02623-205">Si está, seleccione las invitaciones de Hola de confianza y haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="02623-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Página de invitaciones de cliente de Azure RemoteApp Hola](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="02623-207">Después de aceptar su invitaciones, lista de Hola de las aplicaciones tienen acceso toowill ser dispositivo tooyour descargado y estará disponible en el centro de conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="02623-208">Haga doble clic en uno de hello aplicaciones toolaunch y empieza a usarlo.</span><span class="sxs-lookup"><span data-stu-id="02623-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro de conexiones de cliente de Azure RemoteApp Hola](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="02623-210">No se preocupe si nadie le ha enviado una invitación aún, nosotros nos ocupamos.</span><span class="sxs-lookup"><span data-stu-id="02623-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="02623-211">Todavía tendrá acceso tooa demostración colección para que pueda probar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="02623-213">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="02623-213">Windows Phone 8.1</span></span>
<span data-ttu-id="02623-214">Una vez haya instalado la aplicación de escritorio remoto de Microsoft de hello de almacén de hello Windows Phone 8.1, puede encontrarla en la lista de aplicaciones en **escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="02623-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="02623-215">Iniciar aplicación hello pone a disposición directamente tooan vacía el centro de conexiones, a menos que ya ha estado utilizando aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="02623-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="02623-216">tooget a trabajar con Azure RemoteApp, puntee Hola Agregar botón **"" +""** final Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="02623-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![Centro de conexiones vacío](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="02623-218">A continuación, toque **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="02623-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Agregar página de elemento](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="02623-220">Necesita toosign con su servicio de saludo de correo electrónico dirección tooaccess, toostart que procesar, pulse **conectar**.</span><span class="sxs-lookup"><span data-stu-id="02623-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![Solicitud de inicio de sesión](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="02623-222">En la página siguiente de hello, escriba en su **dirección de correo electrónico** y pulse **continuar**.</span><span class="sxs-lookup"><span data-stu-id="02623-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="02623-223">Esto inicia Hola inicio de sesión en proceso con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02623-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Primera página de Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="02623-225">Siga las instrucciones de Hola Hola pantalla toosign con su cuenta de Microsoft (Live ID) o el identificador de la organización.</span><span class="sxs-lookup"><span data-stu-id="02623-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="02623-226">Una vez iniciado sesión, puede aparecer una página de lista de todas las invitaciones de Hola que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="02623-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="02623-227">Si está, seleccione las invitaciones de hello confiar y pulse **guardar**.</span><span class="sxs-lookup"><span data-stu-id="02623-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![Página de invitaciones](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="02623-229">Después de aceptar su invitaciones, lista de Hola de las aplicaciones tienen acceso toowill ser dispositivo tooyour descargado y estará disponible en el centro de conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="02623-230">Puntee en uno de hello aplicaciones toolaunch y empieza a usarlo.</span><span class="sxs-lookup"><span data-stu-id="02623-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro de conexiones con una fuente](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="02623-232">Si no tiene todavía una invitación, todavía puede probar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="02623-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="02623-233">por lo tanto, pulse toodo **Sí** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="02623-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![Solicitud de fuente de demostración](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="02623-235">Esto le proporcionará acceso tooa conjunto básico de tooget aplicaciones para trabajar con conexión de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="02623-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Fuente de demostración de RemoteApp de Azure](./media/remoteapp-clients/WinPhone8.png)

