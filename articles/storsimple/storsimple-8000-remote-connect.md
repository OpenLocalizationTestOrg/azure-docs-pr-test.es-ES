---
title: Conectarse de forma remota al dispositivo StorSimple | Microsoft Docs
description: "Explica cómo configurar el dispositivo para la administración remota y, a continuación, cómo conectarse a Windows PowerShell para StorSimple a través de HTTP o HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="bfb3e-103">Conexión de forma remota al dispositivo StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="bfb3e-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="bfb3e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bfb3e-104">Overview</span></span>

<span data-ttu-id="bfb3e-105">Puede conectarse de forma remota al dispositivo a través de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="bfb3e-106">Cuando se conecta de este modo, no ve un menú.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="bfb3e-107">(Verá un menú solo si utiliza la consola en serie del dispositivo para conectarse). Con la conexión remota de Windows PowerShell, se conecta a un espacio de ejecución específico.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="bfb3e-108">También puede especificar el idioma de visualización.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-108">You can also specify the display language.</span></span>

<span data-ttu-id="bfb3e-109">Para obtener más información acerca del uso de la conexión remota de Windows PowerShell para administrar el dispositivo, vaya a [Uso de Windows PowerShell para StorSimple para administrar su dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="bfb3e-110">Este tutorial explica cómo configurar el dispositivo para la administración remota y, a continuación, cómo conectarse a Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="bfb3e-111">Puede utilizar HTTP o HTTPS para conectarse de forma remota mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="bfb3e-112">Sin embargo, cuando decide cómo conectarse a Windows PowerShell para StorSimple, tenga en cuenta la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="bfb3e-113">Es seguro conectarse directamente a la consola en serie del dispositivo, pero la conexión a la consola en serie a través conmutadores de red no lo es.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="bfb3e-114">Tenga presente los riesgos de seguridad al conectarse a la consola en serie del dispositivo a través de los conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="bfb3e-115">Conectarse a través de una sesión HTTP puede ofrecer más seguridad que la conexión a través de la consola en serie a través de la red.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="bfb3e-116">Aunque este no es el método más seguro, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="bfb3e-117">La conexión a través de una sesión HTTPS con un certificado autofirmado es la opción más segura y la recomendada.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="bfb3e-118">Puede conectarse de forma remota a la interfaz de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="bfb3e-119">No obstante, el acceso remoto a su dispositivo StorSimple mediante la interfaz de Windows PowerShell no está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="bfb3e-120">Deberá habilitar primero la administración remota en el dispositivo y, a continuación, habilitarlo en el cliente que se utilizará para acceder al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="bfb3e-121">Los pasos descritos en este artículo se realizaron en un sistema host con Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="bfb3e-122">Conectarse a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="bfb3e-122">Connect through HTTP</span></span>

<span data-ttu-id="bfb3e-123">Conectarse a Windows PowerShell para StorSimple a través de una sesión HTTP proporciona una mayor seguridad que la conexión a través de la consola en serie del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="bfb3e-124">Aunque este no es el método más seguro, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="bfb3e-125">Puede usar Azure Portal o la consola en serie para configurar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="bfb3e-126">Seleccione entre los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="bfb3e-127">Uso de Azure Portal para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="bfb3e-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="bfb3e-128">Utilice la consola en serie para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="bfb3e-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="bfb3e-129">Después de habilitar la administración remota, utilice el procedimiento siguiente para preparar al cliente para una conexión remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="bfb3e-130">Preparar al cliente para la conexión remota</span><span class="sxs-lookup"><span data-stu-id="bfb3e-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="bfb3e-131">Uso de Azure Portal para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="bfb3e-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="bfb3e-132">Siga estos pasos en Azure Portal para habilitar la administración remota a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="bfb3e-133">Para habilitar la administración remota a través de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bfb3e-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="bfb3e-134">Vaya al servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="bfb3e-135">Seleccione **Dispositivos** y, a continuación, seleccione y haga clic en el dispositivo que desea configurar para la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="bfb3e-136">Vaya a **Configuración del dispositivo > Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="bfb3e-137">En la hoja **Configuración de seguridad**, haga clic en **Administración remota**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="bfb3e-138">En la hoja **Administración remota**, establezca **Habilitar administración remota** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="bfb3e-139">Ahora puede elegir conectarse con HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="bfb3e-140">(La configuración predeterminada es conectarse a través de HTTPS). Asegúrese de que se selecciona HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bfb3e-141">La conexión a través de HTTP solo es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="bfb3e-142">Haga clic en **Guardar** y, cuando se le pida confirmación, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="bfb3e-143">Utilice la consola en serie para habilitar la administración remota a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="bfb3e-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="bfb3e-144">Realice los pasos siguientes en la consola en serie del dispositivo para habilitar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="bfb3e-145">Para habilitar la administración remota a través de la consola en serie del dispositivo</span><span class="sxs-lookup"><span data-stu-id="bfb3e-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="bfb3e-146">En el menú de la consola serie, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="bfb3e-147">Para obtener más información sobre el uso de la consola serie en el dispositivo, vaya a [Conéctese a Windows PowerShell para StorSimple mediante la consola serie del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="bfb3e-148">En el símbolo del sistema, escriba: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="bfb3e-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="bfb3e-149">Se le notificará acerca de las vulnerabilidades de seguridad del uso de HTTP para conectarse al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="bfb3e-150">Cuando se le solicite, confirme escribiendo **S**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="bfb3e-151">Compruebe que está habilitado HTTP escribiendo: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="bfb3e-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="bfb3e-152">Compruebe que el campo **RemoteManagementMode** muestre **HttpsAndHttpEnabled**. La ilustración siguiente muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS y HTTP habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="bfb3e-154">Preparar al cliente para la conexión remota</span><span class="sxs-lookup"><span data-stu-id="bfb3e-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="bfb3e-155">Realice los pasos siguientes en el cliente para habilitar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="bfb3e-156">Para preparar al cliente para la conexión remota</span><span class="sxs-lookup"><span data-stu-id="bfb3e-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="bfb3e-157">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="bfb3e-158">Escriba el siguiente comando para agregar la dirección IP del dispositivo StorSimple a la lista de hosts de confianza del cliente:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="bfb3e-159">Reemplace <*device_ip*> por la dirección IP del dispositivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="bfb3e-160">Escriba el siguiente comando para guardar las credenciales del dispositivo en una variable:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="bfb3e-161">En el cuadro de diálogo que aparece:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="bfb3e-162">Escriba el nombre de usuario en este formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="bfb3e-163">Escriba la contraseña del administrador de dispositivos que se estableció cuando configuró el dispositivo con el asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="bfb3e-164">La contraseña predeterminada es *Password1*.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="bfb3e-165">Inicie una sesión de Windows PowerShell en el dispositivo mediante este comando:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="bfb3e-166">Para crear una sesión de Windows PowerShell para su uso con el dispositivo virtual StorSimple, anexe el parámetro `–Port` y especifique el puerto público que configuró en Conexión remota para dispositivo virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="bfb3e-167">En este momento, debe tener una sesión remota activa de Windows PowerShell en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![Conexión remota de PowerShell mediante HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="bfb3e-169">Conectarse a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bfb3e-169">Connect through HTTPS</span></span>

<span data-ttu-id="bfb3e-170">Conectarse a Windows PowerShell para StorSimple a través de una sesión HTTPS es el método más seguro y recomendado de conexión remota a su dispositivo StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="bfb3e-171">Los procedimientos siguientes explican cómo configurar los equipos cliente y consola en serie de modo que pueda usar HTTPS para conectarse a Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="bfb3e-172">Puede usar Azure Portal o la consola en serie para configurar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="bfb3e-173">Seleccione entre los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="bfb3e-174">Uso de Azure Portal para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bfb3e-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="bfb3e-175">Utilice la consola en serie para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bfb3e-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="bfb3e-176">Después de habilitar la administración remota, utilice los procedimientos siguientes para preparar el host para la administración remota y conectarse con el dispositivo desde el host remoto.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="bfb3e-177">Preparar el host para la administración remota</span><span class="sxs-lookup"><span data-stu-id="bfb3e-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="bfb3e-178">Conectarse al dispositivo desde el host remoto</span><span class="sxs-lookup"><span data-stu-id="bfb3e-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="bfb3e-179">Uso de Azure Portal para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bfb3e-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="bfb3e-180">Siga estos pasos en Azure Portal para habilitar la administración remota a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="bfb3e-181">Para habilitar la administración remota a través de HTTPS desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bfb3e-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="bfb3e-182">Vaya al servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="bfb3e-183">Seleccione **Dispositivos** y, a continuación, seleccione y haga clic en el dispositivo que desea configurar para la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="bfb3e-184">Vaya a **Configuración del dispositivo > Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="bfb3e-185">En la hoja **Configuración de seguridad**, haga clic en **Administración remota**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="bfb3e-186">Establezca **Habilitar administración remota** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="bfb3e-187">Ahora puede elegir conectarse mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="bfb3e-188">(La configuración predeterminada es conectarse a través de HTTPS). Asegúrese de que se ha seleccionado HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="bfb3e-189">Haga clic en ... y, después, en **Descargar certificado de administración remota**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="bfb3e-190">Especifique una ubicación para guardar este archivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-190">Specify a location to save this file.</span></span> <span data-ttu-id="bfb3e-191">Deberá instalar este certificado en el equipo cliente o host que usará para conectarse al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="bfb3e-192">Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="bfb3e-193">Utilice la consola en serie para habilitar la administración remota a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bfb3e-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="bfb3e-194">Realice los pasos siguientes en la consola en serie del dispositivo para habilitar la administración remota.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="bfb3e-195">Para habilitar la administración remota a través de la consola en serie del dispositivo</span><span class="sxs-lookup"><span data-stu-id="bfb3e-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="bfb3e-196">En el menú de la consola serie, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="bfb3e-197">Para obtener más información sobre el uso de la consola serie en el dispositivo, vaya a [Conéctese a Windows PowerShell para StorSimple mediante la consola serie del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="bfb3e-198">En el símbolo del sistema, escriba: </span><span class="sxs-lookup"><span data-stu-id="bfb3e-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="bfb3e-199">Esto debe habilitar HTTPS en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="bfb3e-200">Compruebe que se ha habilitado HTTPS escribiendo:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="bfb3e-201">Asegúrese de que el campo **RemoteManagementMode** muestre **HttpsEnabled**. La ilustración siguiente muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="bfb3e-203">Desde la salida de `Get-HcsSystem`, copie el número de serie del dispositivo y guárdelo para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bfb3e-204">El número de serie se asigna al nombre CN en el certificado.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="bfb3e-205">Obtenga un certificado de administración remota, escriba:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="bfb3e-206">Aparecerá un certificado similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-206">A certificate similar to the following will appear.</span></span>
   
    ![Obtener certificado de administración remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="bfb3e-208">Copie la información en el certificado desde **---BEGIN CERTIFICATE---** hasta **---END CERTIFICATE---** en un editor de texto, como Bloc de notas, y guárdelo como un archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="bfb3e-209">(Copiará este archivo en el host remoto al preparar el host.)</span><span class="sxs-lookup"><span data-stu-id="bfb3e-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bfb3e-210">Para generar un nuevo certificado, utilice cmdlet `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="bfb3e-211">Preparar el host para la administración remota</span><span class="sxs-lookup"><span data-stu-id="bfb3e-211">Prepare the host for remote management</span></span>

<span data-ttu-id="bfb3e-212">Para preparar el equipo host para una conexión remota que utiliza una sesión HTTPS, realice los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="bfb3e-213">[Importación del archivo .cer en el almacén raíz del cliente o un host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="bfb3e-214">[Incorporación de los números de serie del dispositivo al archivo de hosts en el host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="bfb3e-215">A continuación se describe cada uno de los procedimientos anteriores.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="bfb3e-216">Para importar el certificado en el host remoto</span><span class="sxs-lookup"><span data-stu-id="bfb3e-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="bfb3e-217">Haga clic con el botón secundario en el archivo .cer y seleccione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="bfb3e-218">Esto iniciará el asistente para importar certificados.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-218">This starts the Certificate Import Wizard.</span></span>
   
    ![Asistente para importación de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="bfb3e-220">Para **Ubicación de almacén**, seleccione **Equipo local** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="bfb3e-221">Seleccione **Colocar todos los certificados en el siguiente almacén** y, luego, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="bfb3e-222">Navegue al almacén raíz del host remoto y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Asistente para importación de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="bfb3e-224">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="bfb3e-224">Click **Finish**.</span></span> <span data-ttu-id="bfb3e-225">Aparece un mensaje que indica que la importación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-225">A message that tells you that the import was successful appears.</span></span>
   
    ![Asistente para importación de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="bfb3e-227">Para agregar números de serie del dispositivo con el host remoto</span><span class="sxs-lookup"><span data-stu-id="bfb3e-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="bfb3e-228">Inicie el Bloc de notas como administrador y, a continuación, abra el archivo de hosts que se encuentra en \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="bfb3e-229">Agregue las siguientes tres entradas al archivo de hosts: **Dirección IP de DATA 0**, **Dirección IP fija del Controlador 0** y **Dirección IP fija del Controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="bfb3e-230">Escriba el número de serie del dispositivo que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="bfb3e-231">Asigne esto a la dirección IP como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="bfb3e-232">Para Controlador 0 y 1, anexe **Controller0** y **Controller1** al final del número de serie (nombre CN).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Adición de nombre CN a archivo de hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="bfb3e-234">Guarde el archivo de hosts.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="bfb3e-235">Conectarse al dispositivo desde el host remoto</span><span class="sxs-lookup"><span data-stu-id="bfb3e-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="bfb3e-236">Use Windows PowerShell y SSL para iniciar una sesión de SSAdmin en el dispositivo desde un host remoto o cliente.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="bfb3e-237">La sesión de SSAdmin se asigna a la opción 1 en el menú de la [consola serie](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="bfb3e-238">Realice el procedimiento siguiente en el equipo desde el que desea realizar la conexión remota de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="bfb3e-239">Para iniciar una sesión de SSAdmin en el dispositivo mediante el uso de Windows PowerShell y SSL</span><span class="sxs-lookup"><span data-stu-id="bfb3e-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="bfb3e-240">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="bfb3e-241">Agregue la dirección IP del dispositivo a los hosts de confianza del cliente, escriba:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="bfb3e-242">Donde *<device_ip>* es la dirección IP del dispositivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="bfb3e-243">Para crear una nueva credencial, escriba:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="bfb3e-244">Donde <*dirección IP del dispositivo de destino*> es la dirección IP de DATA 0 para el dispositivo; por ejemplo, **10.126.173.90** tal como se muestra en la imagen anterior del archivo de hosts.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="bfb3e-245">Además, proporcione la contraseña de administrador para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="bfb3e-246">Cree una sesión, escriba:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="bfb3e-247">Para el parámetro -ComputerName del cmdlet, escriba el <*número de serie del dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="bfb3e-248">Este número de serie se asigna a la dirección IP de DATA 0 en el archivo de hosts del host remoto; Por ejemplo, **SHX0991003G44MT** tal como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="bfb3e-249">Escriba:</span><span class="sxs-lookup"><span data-stu-id="bfb3e-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="bfb3e-250">Deberá esperar unos minutos y, a continuación, se conectará al dispositivo a través de HTTPS con SSL.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="bfb3e-251">Verá un mensaje que indica que está conectado al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfb3e-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![Conexión remota de PowerShell mediante HTTP y SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="bfb3e-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfb3e-253">Next steps</span></span>

* <span data-ttu-id="bfb3e-254">Obtenga más información acerca del [uso de Windows PowerShell para administrar el dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="bfb3e-255">Más información sobre el [uso del servicio StorSimple Device Manager para administrar su dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bfb3e-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

