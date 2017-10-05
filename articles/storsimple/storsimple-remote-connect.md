---
title: Conectarse de forma remota al dispositivo StorSimple | Microsoft Docs
description: "Explica cómo configurar el dispositivo para la administración remota y, a continuación, cómo conectarse a Windows PowerShell para StorSimple a través de HTTP o HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b916173e127394d3ea06eded36285bdbbf884b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="41a91-103">Conexión de forma remota al dispositivo StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="41a91-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="41a91-104">Información general</span><span class="sxs-lookup"><span data-stu-id="41a91-104">Overview</span></span>
<span data-ttu-id="41a91-105">Puede usar la conexión remota de Windows PowerShell para conectarse al dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41a91-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="41a91-106">Cuando se conecta de este modo, no verá un menú.</span><span class="sxs-lookup"><span data-stu-id="41a91-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="41a91-107">(Verá un menú solo si utiliza la consola en serie del dispositivo para conectarse). Con la conexión remota de Windows PowerShell, se conecta a un espacio de ejecución específico.</span><span class="sxs-lookup"><span data-stu-id="41a91-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="41a91-108">También puede especificar el idioma de visualización.</span><span class="sxs-lookup"><span data-stu-id="41a91-108">You can also specify the display language.</span></span> 

<span data-ttu-id="41a91-109">Para obtener más información acerca del uso de la conexión remota de Windows PowerShell para administrar el dispositivo, vaya a [Uso de Windows PowerShell para StorSimple para administrar su dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="41a91-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="41a91-110">Este tutorial explica cómo configurar el dispositivo para la administración remota y, a continuación, cómo conectarse a Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41a91-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="41a91-111">Puede utilizar HTTP o HTTPS para conectarse a través de la conexión remota de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41a91-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="41a91-112">Sin embargo, cuando decide cómo conectarse a Windows PowerShell para StorSimple, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41a91-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span> 

* <span data-ttu-id="41a91-113">Es seguro conectarse directamente a la consola en serie del dispositivo, pero la conexión a la consola en serie a través conmutadores de red no lo es.</span><span class="sxs-lookup"><span data-stu-id="41a91-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="41a91-114">Tenga presente los riesgos de seguridad al conectarse a la consola en serie del dispositivo a través de los conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="41a91-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span> 
* <span data-ttu-id="41a91-115">Conectarse a través de una sesión HTTP puede ofrecer más seguridad que la conexión a través de la consola en serie a través de la red.</span><span class="sxs-lookup"><span data-stu-id="41a91-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="41a91-116">Aunque este no es el método más seguro, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="41a91-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="41a91-117">La conexión a través de una sesión HTTPS con un certificado autofirmado es la opción más segura y la recomendada.</span><span class="sxs-lookup"><span data-stu-id="41a91-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="41a91-118">Puede conectarse de forma remota a la interfaz de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41a91-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="41a91-119">No obstante, el acceso remoto a su dispositivo StorSimple mediante la interfaz de Windows PowerShell no está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="41a91-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="41a91-120">Deberá habilitar primero la administración remota en el dispositivo y, a continuación, habilitarlo en el cliente que se utilizará para acceder al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="41a91-121">Los pasos descritos en este artículo se realizaron en un sistema host con Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="41a91-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="41a91-122">Conectarse a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="41a91-122">Connect through HTTP</span></span>
<span data-ttu-id="41a91-123">Conectarse a Windows PowerShell para StorSimple a través de una sesión HTTP proporciona una mayor seguridad que la conexión a través de la consola en serie del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41a91-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="41a91-124">Aunque este no es el método más seguro, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="41a91-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="41a91-125">Puede usar el Portal de Azure clásico o la consola en serie para configurar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="41a91-125">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="41a91-126">Seleccione entre los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="41a91-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="41a91-127">Uso del Portal de Azure clásico para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="41a91-127">Use the Azure classic portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="41a91-128">Utilice la consola en serie para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="41a91-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="41a91-129">Después de habilitar la administración remota, utilice el procedimiento siguiente para preparar al cliente para una conexión remota.</span><span class="sxs-lookup"><span data-stu-id="41a91-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="41a91-130">Preparar al cliente para la conexión remota</span><span class="sxs-lookup"><span data-stu-id="41a91-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="41a91-131">Uso del Portal de Azure clásico para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="41a91-131">Use the Azure classic portal to enable remote management over HTTP</span></span>
<span data-ttu-id="41a91-132">Siga estos pasos en el Portal de Azure clásico para habilitar la administración remota a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="41a91-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a><span data-ttu-id="41a91-133">Para habilitar la administración remota a través del Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="41a91-133">To enable remote management through the Azure classic portal</span></span>
1. <span data-ttu-id="41a91-134">Acceda a **Dispositivos** > **Configurar** para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="41a91-135">Desplácese hacia abajo a la sección **Administración remota** .</span><span class="sxs-lookup"><span data-stu-id="41a91-135">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="41a91-136">Establezca **Habilitar administración remota** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="41a91-136">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="41a91-137">Ahora puede elegir conectarse con HTTP.</span><span class="sxs-lookup"><span data-stu-id="41a91-137">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="41a91-138">(La configuración predeterminada es conectarse a través de HTTPS). Asegúrese de que se selecciona HTTP.</span><span class="sxs-lookup"><span data-stu-id="41a91-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41a91-139">La conexión a través de HTTP solo es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="41a91-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="41a91-140">Haga clic en **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="41a91-140">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="41a91-141">Utilice la consola en serie para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="41a91-141">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="41a91-142">Realice los pasos siguientes en la consola en serie del dispositivo para habilitar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="41a91-142">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="41a91-143">Para habilitar la administración remota a través de la consola en serie del dispositivo</span><span class="sxs-lookup"><span data-stu-id="41a91-143">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="41a91-144">En el menú de la consola serie, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="41a91-144">On the serial console menu, select option 1.</span></span> <span data-ttu-id="41a91-145">Para obtener más información sobre el uso de la consola serie en el dispositivo, vaya a [Conéctese a Windows PowerShell para StorSimple mediante la consola serie del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="41a91-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="41a91-146">En el símbolo del sistema, escriba: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="41a91-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="41a91-147">Se le notificará acerca de las vulnerabilidades de seguridad del uso de HTTP para conectarse al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="41a91-148">Cuando se le solicite, confirme escribiendo **S**.</span><span class="sxs-lookup"><span data-stu-id="41a91-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="41a91-149">Compruebe que está habilitado HTTP escribiendo: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="41a91-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="41a91-150">Compruebe que el campo **RemoteManagementMode** muestre **HttpsAndHttpEnabled**. La ilustración siguiente muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="41a91-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS y HTTP habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="41a91-152">Preparar al cliente para la conexión remota</span><span class="sxs-lookup"><span data-stu-id="41a91-152">Prepare the client for remote connection</span></span>
<span data-ttu-id="41a91-153">Realice los pasos siguientes en el cliente para habilitar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="41a91-153">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="41a91-154">Para preparar al cliente para la conexión remota</span><span class="sxs-lookup"><span data-stu-id="41a91-154">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="41a91-155">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="41a91-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="41a91-156">Escriba el siguiente comando para agregar la dirección IP del dispositivo StorSimple a la lista de hosts de confianza del cliente:</span><span class="sxs-lookup"><span data-stu-id="41a91-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="41a91-157">Reemplace <*device_ip*> por la dirección IP del dispositivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="41a91-157">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="41a91-158">Escriba el siguiente comando para guardar las credenciales del dispositivo en una variable:</span><span class="sxs-lookup"><span data-stu-id="41a91-158">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="41a91-159">En el cuadro de diálogo que aparece:</span><span class="sxs-lookup"><span data-stu-id="41a91-159">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="41a91-160">Escriba el nombre de usuario en este formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="41a91-160">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="41a91-161">Escriba la contraseña del administrador de dispositivos que se estableció cuando configuró el dispositivo con el asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="41a91-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="41a91-162">La contraseña predeterminada es *Password1*.</span><span class="sxs-lookup"><span data-stu-id="41a91-162">The default password is *Password1*.</span></span>
5. <span data-ttu-id="41a91-163">Inicie una sesión de Windows PowerShell en el dispositivo mediante este comando:</span><span class="sxs-lookup"><span data-stu-id="41a91-163">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="41a91-164">Para crear una sesión de Windows PowerShell para su uso con el dispositivo virtual StorSimple, anexe el parámetro `–Port` y especifique el puerto público que configuró en Conexión remota para dispositivo virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41a91-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="41a91-165">En este momento, debe tener una sesión remota activa de Windows PowerShell en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-165">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
    ![Conexión remota de PowerShell mediante HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="41a91-167">Conectarse a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="41a91-167">Connect through HTTPS</span></span>
<span data-ttu-id="41a91-168">Conectarse a Windows PowerShell para StorSimple a través de una sesión HTTPS es el método más seguro y recomendado de conexión remota a su dispositivo StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="41a91-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="41a91-169">Los procedimientos siguientes explican cómo configurar los equipos cliente y consola en serie de modo que pueda usar HTTPS para conectarse a Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41a91-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="41a91-170">Puede usar el Portal de Azure clásico o la consola en serie para configurar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="41a91-170">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="41a91-171">Seleccione entre los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="41a91-171">Select from the following procedures:</span></span>

* [<span data-ttu-id="41a91-172">Uso del Portal de Azure clásico para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="41a91-172">Use the Azure classic portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="41a91-173">Utilice la consola en serie para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="41a91-173">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="41a91-174">Después de habilitar la administración remota, utilice los procedimientos siguientes para preparar el host para la administración remota y conectarse con el dispositivo desde el host remoto.</span><span class="sxs-lookup"><span data-stu-id="41a91-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="41a91-175">Preparar el host para la administración remota</span><span class="sxs-lookup"><span data-stu-id="41a91-175">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="41a91-176">Conectarse al dispositivo desde el host remoto</span><span class="sxs-lookup"><span data-stu-id="41a91-176">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="41a91-177">Uso del Portal de Azure clásico para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="41a91-177">Use the Azure classic portal to enable remote management over HTTPS</span></span>
<span data-ttu-id="41a91-178">Siga estos pasos en el Portal de Azure clásico para habilitar la administración remota a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="41a91-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a><span data-ttu-id="41a91-179">Para habilitar la administración remota a través de HTTPS desde el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="41a91-179">To enable remote management over HTTPS from the Azure classic portal</span></span>
1. <span data-ttu-id="41a91-180">Acceda a **Dispositivos** > **Configurar** para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="41a91-181">Desplácese hacia abajo a la sección **Administración remota** .</span><span class="sxs-lookup"><span data-stu-id="41a91-181">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="41a91-182">Establezca **Habilitar administración remota** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="41a91-182">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="41a91-183">Ahora puede elegir conectarse mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="41a91-183">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="41a91-184">(La configuración predeterminada es conectarse a través de HTTPS). Asegúrese de que se ha seleccionado HTTPS.</span><span class="sxs-lookup"><span data-stu-id="41a91-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="41a91-185">Haga clic en **Descargar certificado de administración remota**.</span><span class="sxs-lookup"><span data-stu-id="41a91-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="41a91-186">Especifique una ubicación para guardar este archivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-186">Specify a location to save this file.</span></span> <span data-ttu-id="41a91-187">Deberá instalar este certificado en el equipo cliente o host que usará para conectarse al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="41a91-188">Haga clic en **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="41a91-188">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="41a91-189">Utilice la consola en serie para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="41a91-189">Use the serial console to enable remote management over HTTPS</span></span>
<span data-ttu-id="41a91-190">Realice los pasos siguientes en la consola en serie del dispositivo para habilitar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="41a91-190">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="41a91-191">Para habilitar la administración remota a través de la consola en serie del dispositivo</span><span class="sxs-lookup"><span data-stu-id="41a91-191">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="41a91-192">En el menú de la consola serie, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="41a91-192">On the serial console menu, select option 1.</span></span> <span data-ttu-id="41a91-193">Para obtener más información sobre el uso de la consola serie en el dispositivo, vaya a [Conéctese a Windows PowerShell para StorSimple mediante la consola serie del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="41a91-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="41a91-194">En el símbolo del sistema, escriba: </span><span class="sxs-lookup"><span data-stu-id="41a91-194">At the prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="41a91-195">Esto debe habilitar HTTPS en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="41a91-196">Compruebe que se ha habilitado HTTPS escribiendo:</span><span class="sxs-lookup"><span data-stu-id="41a91-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="41a91-197">Asegúrese de que el campo **RemoteManagementMode** muestre **HttpsEnabled**. La ilustración siguiente muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="41a91-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="41a91-199">Desde la salida de `Get-HcsSystem`, copie el número de serie del dispositivo y guárdelo para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="41a91-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41a91-200">El número de serie se asigna al nombre CN en el certificado.</span><span class="sxs-lookup"><span data-stu-id="41a91-200">The serial number maps to the CN name in the certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="41a91-201">Obtenga un certificado de administración remota, escriba:</span><span class="sxs-lookup"><span data-stu-id="41a91-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="41a91-202">Aparecerá un certificado similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="41a91-202">A certificate similar to the following will appear.</span></span>
   
    ![Obtener certificado de administración remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="41a91-204">Copie la información en el certificado desde **---BEGIN CERTIFICATE---** hasta **---END CERTIFICATE---** en un editor de texto, como Bloc de notas, y guárdelo como un archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="41a91-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="41a91-205">(Copiará este archivo en el host remoto al preparar el host.)</span><span class="sxs-lookup"><span data-stu-id="41a91-205">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41a91-206">Para generar un nuevo certificado, utilice cmdlet `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="41a91-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="41a91-207">Preparar el host para la administración remota</span><span class="sxs-lookup"><span data-stu-id="41a91-207">Prepare the host for remote management</span></span>
<span data-ttu-id="41a91-208">Para preparar el equipo host para una conexión remota que utiliza una sesión HTTPS, realice los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="41a91-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="41a91-209">[Importación del archivo .cer en el almacén raíz del cliente o un host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="41a91-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="41a91-210">[Incorporación de los números de serie del dispositivo al archivo de hosts en el host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="41a91-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="41a91-211">A continuación se describe cada uno de estos procedimientos.</span><span class="sxs-lookup"><span data-stu-id="41a91-211">Each of these procedures is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="41a91-212">Para importar el certificado en el host remoto</span><span class="sxs-lookup"><span data-stu-id="41a91-212">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="41a91-213">Haga clic con el botón secundario en el archivo .cer y seleccione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="41a91-213">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="41a91-214">Esto iniciará al Asistente para importación de certificados.</span><span class="sxs-lookup"><span data-stu-id="41a91-214">This will start the Certificate Import Wizard.</span></span>
   
    ![Asistente para importación de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="41a91-216">Para **Ubicación de almacén**, seleccione **Equipo local** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="41a91-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="41a91-217">Seleccione **Colocar todos los certificados en el siguiente almacén** y, luego, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="41a91-217">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="41a91-218">Navegue al almacén raíz del host remoto y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="41a91-218">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Asistente para importación de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="41a91-220">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="41a91-220">Click **Finish**.</span></span> <span data-ttu-id="41a91-221">Aparece un mensaje que indica que la importación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="41a91-221">A message that tells you that the import was successful appears.</span></span>
   
    ![Asistente para importación de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="41a91-223">Para agregar números de serie del dispositivo con el host remoto</span><span class="sxs-lookup"><span data-stu-id="41a91-223">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="41a91-224">Inicie el Bloc de notas como administrador y, a continuación, abra el archivo de hosts que se encuentra en \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="41a91-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="41a91-225">Agregue las siguientes tres entradas al archivo de hosts: **Dirección IP de DATA 0**, **Dirección IP fija del Controlador 0** y **Dirección IP fija del Controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="41a91-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="41a91-226">Escriba el número de serie del dispositivo que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="41a91-226">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="41a91-227">Asigne esto a la dirección IP como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="41a91-227">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="41a91-228">Para Controlador 0 y 1, anexe **Controller0** y **Controller1** al final del número de serie (nombre CN).</span><span class="sxs-lookup"><span data-stu-id="41a91-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Adición de nombre CN a archivo de hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="41a91-230">Guarde el archivo de hosts.</span><span class="sxs-lookup"><span data-stu-id="41a91-230">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="41a91-231">Conectarse al dispositivo desde el host remoto</span><span class="sxs-lookup"><span data-stu-id="41a91-231">Connect to the device from the remote host</span></span>
<span data-ttu-id="41a91-232">Use Windows PowerShell y SSL para iniciar una sesión de SSAdmin en el dispositivo desde un host remoto o cliente.</span><span class="sxs-lookup"><span data-stu-id="41a91-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="41a91-233">La sesión de SSAdmin se asigna a la opción 1 en el menú de la [consola serie](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="41a91-234">Realice el procedimiento siguiente en el equipo desde el que desea realizar la conexión remota de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41a91-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="41a91-235">Para iniciar una sesión de SSAdmin en el dispositivo mediante el uso de Windows PowerShell y SSL</span><span class="sxs-lookup"><span data-stu-id="41a91-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="41a91-236">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="41a91-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="41a91-237">Agregue la dirección IP del dispositivo a los hosts de confianza del cliente, escriba:</span><span class="sxs-lookup"><span data-stu-id="41a91-237">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="41a91-238">Donde *<device_ip>* es la dirección IP del dispositivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="41a91-238">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="41a91-239">Cree una nueva credencial, escriba:</span><span class="sxs-lookup"><span data-stu-id="41a91-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="41a91-240">Donde <*dirección IP del dispositivo de destino*> es la dirección IP de DATA 0 para el dispositivo; por ejemplo, **10.126.173.90** tal como se muestra en la imagen anterior del archivo de hosts.</span><span class="sxs-lookup"><span data-stu-id="41a91-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="41a91-241">Además, proporcione la contraseña de administrador para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-241">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="41a91-242">Cree una sesión, escriba:</span><span class="sxs-lookup"><span data-stu-id="41a91-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="41a91-243">Para el parámetro -ComputerName del cmdlet, escriba el <*número de serie del dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="41a91-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="41a91-244">Este número de serie se asigna a la dirección IP de DATA 0 en el archivo de hosts del host remoto; Por ejemplo, **SHX0991003G44MT** tal como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="41a91-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="41a91-245">Escriba:</span><span class="sxs-lookup"><span data-stu-id="41a91-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="41a91-246">Deberá esperar unos minutos y, a continuación, se conectará al dispositivo a través de HTTPS con SSL.</span><span class="sxs-lookup"><span data-stu-id="41a91-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="41a91-247">Verá un mensaje que indica que está conectado al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41a91-247">You will see a message that indicates you are connected to your device.</span></span>
   
    ![Conexión remota de PowerShell mediante HTTP y SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="41a91-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41a91-249">Next steps</span></span>
* <span data-ttu-id="41a91-250">Obtenga más información acerca del [uso de Windows PowerShell para administrar el dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="41a91-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="41a91-251">Obtenga más información sobre el [uso del servicio StorSimple Manager para administrar su dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="41a91-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

