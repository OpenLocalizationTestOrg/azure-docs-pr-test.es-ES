---
title: aaaConnect remotamente el dispositivo de StorSimple tooyour | Documentos de Microsoft
description: "Explica cómo tooconfigure el dispositivo para la administración remota y cómo tooconnect tooWindows PowerShell para StorSimple a través de HTTP o HTTPS."
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
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="3ab35-103">Conectar dispositivo de la serie 8000 de StorSimple tooyour de forma remota</span><span class="sxs-lookup"><span data-stu-id="3ab35-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="3ab35-104">Información general</span><span class="sxs-lookup"><span data-stu-id="3ab35-104">Overview</span></span>

<span data-ttu-id="3ab35-105">Puede conectarse de forma remota dispositivos tooyour mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ab35-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="3ab35-106">Cuando se conecta de este modo, no ve un menú.</span><span class="sxs-lookup"><span data-stu-id="3ab35-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="3ab35-107">(Verá un menú solo si usa la consola serie de hello en hello dispositivo tooconnect). Con la comunicación remota de Windows PowerShell, conecte tooa espacio de ejecución específica.</span><span class="sxs-lookup"><span data-stu-id="3ab35-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="3ab35-108">También puede especificar el idioma para mostrar hello.</span><span class="sxs-lookup"><span data-stu-id="3ab35-108">You can also specify hello display language.</span></span>

<span data-ttu-id="3ab35-109">Para obtener más información acerca del uso de Windows PowerShell remoting toomanage el dispositivo, vaya demasiado[usar Windows PowerShell para StorSimple tooadminister dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3ab35-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="3ab35-110">Este tutorial le explica cómo tooconfigure el dispositivo para la administración remota y, a continuación, cómo tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3ab35-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="3ab35-111">Puede utilizar HTTP o HTTPS tooremotely conectarse mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ab35-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="3ab35-112">Sin embargo, cuando decida cómo tooconnect tooWindows PowerShell para StorSimple, considere la posibilidad de hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="3ab35-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="3ab35-113">Conexión directa toohello consola serie del dispositivo es segura, pero conexión toohello de consola serie a través de conmutadores de red no lo es.</span><span class="sxs-lookup"><span data-stu-id="3ab35-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="3ab35-114">Tenga cuidado de riesgos de seguridad de hello cuando se conecte la consola serie del dispositivo toohello a través de conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="3ab35-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="3ab35-115">Conexión a través de una sesión HTTP puede ofrecer más seguridad que la conexión a través de la consola serie de Hola a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="3ab35-116">Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="3ab35-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="3ab35-117">Conexión a través de una sesión HTTPS con un certificado autofirmado es más segura de Hola y Hola opción recomendada.</span><span class="sxs-lookup"><span data-stu-id="3ab35-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="3ab35-118">Puede conectarse remotamente toohello interfaz de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ab35-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="3ab35-119">Sin embargo, el dispositivo de StorSimple de tooyour de acceso remoto a través de la interfaz de Windows PowerShell de hello no está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3ab35-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="3ab35-120">Debe habilitar la administración remota en el dispositivo de hello en primer lugar y, a continuación, en Hola a cliente que sea tooaccess usa el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="3ab35-121">pasos de Hello descritos en este artículo se han ejecutado en un sistema host que ejecute Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="3ab35-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="3ab35-122">Conectarse a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="3ab35-122">Connect through HTTP</span></span>

<span data-ttu-id="3ab35-123">Conexión tooWindows PowerShell para StorSimple a través de una sesión HTTP ofrece más seguridad que la conexión a través de la consola de serie de hello de dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3ab35-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="3ab35-124">Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="3ab35-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="3ab35-125">Puede usar cualquier hello Azure portal o hello consola serie tooconfigure administración remota.</span><span class="sxs-lookup"><span data-stu-id="3ab35-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="3ab35-126">Seleccione una de hello procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ab35-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="3ab35-127">Utilizar la administración remota de tooenable portal Azure de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="3ab35-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="3ab35-128">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="3ab35-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="3ab35-129">Después de habilitar la administración remota, use Hola siguiendo el procedimiento tooprepare Hola del cliente para una conexión remota.</span><span class="sxs-lookup"><span data-stu-id="3ab35-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="3ab35-130">Preparar el cliente de Hola para conexión remota</span><span class="sxs-lookup"><span data-stu-id="3ab35-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="3ab35-131">Utilizar la administración remota de tooenable portal Azure de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="3ab35-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="3ab35-132">Realizar Hola siguiendo los pasos en la administración remota de hello Azure tooenable portal a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="3ab35-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="3ab35-133">administración remota de tooenable a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3ab35-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="3ab35-134">Servicio de administrador de dispositivos de StorSimple de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="3ab35-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="3ab35-135">Seleccione **dispositivos** y, a continuación, seleccione y haga clic en el dispositivo de hello desea tooconfigure para la administración remota.</span><span class="sxs-lookup"><span data-stu-id="3ab35-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="3ab35-136">Vaya demasiado**configuración del dispositivo > seguridad**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="3ab35-137">Hola **configuración de seguridad** hoja, haga clic en **administración remota**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="3ab35-138">Hola **administración remota** hoja, establezca **habilitar la administración remota** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="3ab35-139">Ahora puede elegir tooconnect mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="3ab35-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="3ab35-140">(el valor predeterminado de hello es tooconnect a través de HTTPS). Asegúrese de que se selecciona HTTP.</span><span class="sxs-lookup"><span data-stu-id="3ab35-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3ab35-141">La conexión a través de HTTP solo es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="3ab35-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="3ab35-142">Haga clic en **Guardar** y, cuando se le pida confirmación, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="3ab35-143">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="3ab35-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="3ab35-144">Realizar Hola pasos Hola administración de dispositivos consola serie tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="3ab35-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="3ab35-145">administración remota de tooenable a través de la consola serie del dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="3ab35-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="3ab35-146">En el menú de la consola serie de hello, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="3ab35-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="3ab35-147">Para obtener más información acerca del uso de consola serie de hello en dispositivo hello, vaya demasiado[conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="3ab35-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="3ab35-148">En el símbolo del sistema de hello, escriba:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="3ab35-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="3ab35-149">Se le notificará acerca de las vulnerabilidades de seguridad de Hola de usar HTTP tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="3ab35-150">Cuando se le solicite, confirme escribiendo **S**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="3ab35-151">Compruebe que está habilitado HTTP escribiendo: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="3ab35-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="3ab35-152">Compruebe que hello **RemoteManagementMode** campo muestra **HttpsAndHttpEnabled**.hello después de la ilustración se muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3ab35-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS y HTTP habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="3ab35-154">Preparar el cliente de Hola para conexión remota</span><span class="sxs-lookup"><span data-stu-id="3ab35-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="3ab35-155">Realizar Hola siguiendo los pasos en la administración remota de hello cliente tooenable.</span><span class="sxs-lookup"><span data-stu-id="3ab35-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="3ab35-156">cliente de hello tooprepare para conexión remota</span><span class="sxs-lookup"><span data-stu-id="3ab35-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="3ab35-157">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="3ab35-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="3ab35-158">Escriba Hola siguiente dirección IP de comando tooadd Hola de lista de hosts de confianza del cliente de toohello de hello StorSimple dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3ab35-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="3ab35-159">Reemplace <*device_ip*> con la dirección IP de Hola de su dispositivo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3ab35-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="3ab35-160">Escriba Hola después comando toosave hello las credenciales del dispositivo en una variable:</span><span class="sxs-lookup"><span data-stu-id="3ab35-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="3ab35-161">En el cuadro de diálogo de Hola que aparece:</span><span class="sxs-lookup"><span data-stu-id="3ab35-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="3ab35-162">Escriba el nombre de usuario de hello en este formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="3ab35-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="3ab35-163">Escriba la contraseña del Administrador de dispositivos de Hola que se estableció al dispositivo de Hola se configuró con el Asistente para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="3ab35-164">es la contraseña predeterminada de Hello *Password1*.</span><span class="sxs-lookup"><span data-stu-id="3ab35-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="3ab35-165">Iniciar una sesión de Windows PowerShell en el dispositivo de hello, escriba este comando:</span><span class="sxs-lookup"><span data-stu-id="3ab35-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="3ab35-166">toocreate una sesión de Windows PowerShell para su uso con el dispositivo virtual StorSimple de hello, anexar hello `–Port` parámetro y especifique el puerto público de Hola que configuró en la comunicación remota de dispositivo Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3ab35-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="3ab35-167">En este punto, debe tener un dispositivo de toohello de sesión de Windows PowerShell remoto activo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![Conexión remota de PowerShell mediante HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="3ab35-169">Conectarse a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="3ab35-169">Connect through HTTPS</span></span>

<span data-ttu-id="3ab35-170">Conexión tooWindows PowerShell para StorSimple a través de una sesión HTTPS es más segura de hello y método de conexión de forma remota dispositivos de Microsoft Azure StorSimple tooyour recomendado.</span><span class="sxs-lookup"><span data-stu-id="3ab35-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="3ab35-171">Hola procedimientos siguientes explica cómo tooset seguridad Hola serie consola y los equipos cliente para que puedan utilizar HTTPS tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3ab35-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="3ab35-172">Puede usar cualquier hello Azure portal o hello consola serie tooconfigure administración remota.</span><span class="sxs-lookup"><span data-stu-id="3ab35-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="3ab35-173">Seleccione una de hello procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ab35-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="3ab35-174">Utilizar la administración remota de tooenable portal Azure de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="3ab35-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="3ab35-175">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="3ab35-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="3ab35-176">Después de habilitar la administración remota, use Hola después de host de hello tooprepare de procedimientos para una administración remota y conecte toohello dispositivo desde el host remoto Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="3ab35-177">Preparar el host de hello para la administración remota</span><span class="sxs-lookup"><span data-stu-id="3ab35-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="3ab35-178">Conecte el dispositivo de toohello desde el host remoto hello</span><span class="sxs-lookup"><span data-stu-id="3ab35-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="3ab35-179">Utilizar la administración remota de tooenable portal Azure de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="3ab35-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="3ab35-180">Realizar Hola siguiendo los pasos en la administración remota de hello Azure tooenable portal a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3ab35-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="3ab35-181">tooenable la administración remota a través de HTTPS de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3ab35-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="3ab35-182">Servicio de administrador de dispositivos de StorSimple de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="3ab35-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="3ab35-183">Seleccione **dispositivos** y, a continuación, seleccione y haga clic en el dispositivo de hello desea tooconfigure para la administración remota.</span><span class="sxs-lookup"><span data-stu-id="3ab35-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="3ab35-184">Vaya demasiado**configuración del dispositivo > seguridad**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="3ab35-185">Hola **configuración de seguridad** hoja, haga clic en **administración remota**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="3ab35-186">Establecer **habilitar la administración remota** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="3ab35-187">Ahora puede elegir tooconnect mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3ab35-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="3ab35-188">(el valor predeterminado de hello es tooconnect a través de HTTPS). Asegúrese de que se ha seleccionado HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3ab35-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="3ab35-189">Haga clic en ... y, después, en **Descargar certificado de administración remota**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="3ab35-190">Especifique una ubicación toosave este archivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-190">Specify a location toosave this file.</span></span> <span data-ttu-id="3ab35-191">Necesita tooinstall este certificado en el equipo cliente o host Hola que va a usar tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="3ab35-192">Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="3ab35-193">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="3ab35-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="3ab35-194">Realizar Hola pasos Hola administración de dispositivos consola serie tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="3ab35-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="3ab35-195">administración remota de tooenable a través de la consola serie del dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="3ab35-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="3ab35-196">En el menú de la consola serie de hello, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="3ab35-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="3ab35-197">Para obtener más información acerca del uso de consola serie de hello en dispositivo hello, vaya demasiado[conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="3ab35-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="3ab35-198">En el símbolo del sistema de hello, escriba:</span><span class="sxs-lookup"><span data-stu-id="3ab35-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="3ab35-199">Esto debe habilitar HTTPS en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="3ab35-200">Compruebe que se ha habilitado HTTPS escribiendo:</span><span class="sxs-lookup"><span data-stu-id="3ab35-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="3ab35-201">Asegúrese de que ese hello **RemoteManagementMode** campo muestra **HttpsEnabled**.hello después de la ilustración se muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3ab35-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="3ab35-203">De salida de hello de `Get-HcsSystem`, copie Hola de número de serie del dispositivo de Hola y guardarlo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="3ab35-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3ab35-204">número de serie de Hello asigna toohello nombre CN de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="3ab35-205">Obtenga un certificado de administración remota, escriba:</span><span class="sxs-lookup"><span data-stu-id="3ab35-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="3ab35-206">Aparecerá un siguiente toohello similar de certificado.</span><span class="sxs-lookup"><span data-stu-id="3ab35-206">A certificate similar toohello following will appear.</span></span>
   
    ![Obtener certificado de administración remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="3ab35-208">Copiar información de hello en el certificado de Hola de **---BEGIN CERTIFICATE---** demasiado**---END CERTIFICATE---** en un editor de texto como Bloc de notas y guárdelo como un archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="3ab35-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="3ab35-209">(Copiará este host remoto de archivo tooyour al preparar los host de Hola.)</span><span class="sxs-lookup"><span data-stu-id="3ab35-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3ab35-210">toogenerate un nuevo certificado, utilice hello `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ab35-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="3ab35-211">Preparar el host de hello para la administración remota</span><span class="sxs-lookup"><span data-stu-id="3ab35-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="3ab35-212">equipo de host de hello tooprepare para una conexión remota que utiliza una sesión HTTPS, lleve a cabo Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ab35-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="3ab35-213">[Archivo de importación hello .cer en almacén raíz de Hola de hello cliente o host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="3ab35-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="3ab35-214">[Agregar archivo hosts toohello de números de serie de dispositivo de hello en el host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="3ab35-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="3ab35-215">Cada uno de hello anteriores procedimientos, se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="3ab35-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="3ab35-216">certificado de hello tooimport en host remoto hello</span><span class="sxs-lookup"><span data-stu-id="3ab35-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="3ab35-217">Haga clic en el archivo .cer de hello y seleccione **instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="3ab35-218">Esto inicia Hola Asistente para importación de certificados.</span><span class="sxs-lookup"><span data-stu-id="3ab35-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![Asistente para importación de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="3ab35-220">Para **Ubicación de almacén**, seleccione **Equipo local** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="3ab35-221">Seleccione **colocar todos los certificados en hello después almacén**y, a continuación, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="3ab35-222">Navegar por el almacén raíz de toohello del host remoto y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Asistente para importación de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="3ab35-224">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="3ab35-224">Click **Finish**.</span></span> <span data-ttu-id="3ab35-225">Aparece un mensaje que indica que la importación de hello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="3ab35-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![Asistente para importación de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="3ab35-227">host remoto del toohello tooadd dispositivo números de serie</span><span class="sxs-lookup"><span data-stu-id="3ab35-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="3ab35-228">Inicie el Bloc de notas como administrador y, a continuación, abra el archivo de hosts de hello ubicado en \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="3ab35-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="3ab35-229">Agregar Hola siguiente archivo de hosts de tres entradas tooyour: **dirección IP de DATA 0**, **dirección IP fija del controlador 0**, y **dirección IP fija del controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="3ab35-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="3ab35-230">Escriba el número de serie del dispositivo Hola que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3ab35-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="3ab35-231">Asigne esta dirección IP de toohello como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="3ab35-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="3ab35-232">Para el controlador 0 y 1, anexe **Controller0** y **Controller1** final Hola Hola del número de serie (nombre CN).</span><span class="sxs-lookup"><span data-stu-id="3ab35-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Agregar nombre CN toohosts archivo](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="3ab35-234">Guardar el archivo de hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="3ab35-235">Conecte el dispositivo de toohello desde el host remoto hello</span><span class="sxs-lookup"><span data-stu-id="3ab35-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="3ab35-236">Usar Windows PowerShell y SSL tooenter una sesión de SSAdmin en el dispositivo desde un cliente o host remoto.</span><span class="sxs-lookup"><span data-stu-id="3ab35-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="3ab35-237">sesión de SSAdmin Hola asigna toooption 1 Hola [consola serie](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menú del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="3ab35-238">Realizar Hola siguiendo el procedimiento en el equipo Hola del que desea que la conexión remota de Windows PowerShell de toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="3ab35-239">tooenter una sesión de SSAdmin en dispositivo hello mediante Windows PowerShell y SSL</span><span class="sxs-lookup"><span data-stu-id="3ab35-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="3ab35-240">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="3ab35-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="3ab35-241">Agregar hosts de confianza del cliente de hello dispositivo IP dirección toohello, escriba:</span><span class="sxs-lookup"><span data-stu-id="3ab35-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="3ab35-242">Donde <*device_ip*> Hola dirección de IP del dispositivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3ab35-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="3ab35-243">toocreate una nueva credencial, escriba:</span><span class="sxs-lookup"><span data-stu-id="3ab35-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="3ab35-244">Donde <*dirección IP del dispositivo de destino*> Hola dirección de IP de DATA 0 de su dispositivo; por ejemplo, **10.126.173.90** como se muestra en hello delante de la imagen del archivo de hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab35-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="3ab35-245">Además, proporcione la contraseña de administrador de hello para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="3ab35-246">Cree una sesión, escriba:</span><span class="sxs-lookup"><span data-stu-id="3ab35-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="3ab35-247">Para el parámetro - ComputerName de hello en cmdlet hello, proporcionar Hola <*número de serie del dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="3ab35-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="3ab35-248">Se ha asignado este número de serie toohello dirección IP de DATA 0 en el archivo de hosts de hello en el host remoto; Por ejemplo, **SHX0991003G44MT** como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="3ab35-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="3ab35-249">Escriba:</span><span class="sxs-lookup"><span data-stu-id="3ab35-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="3ab35-250">Necesitará toowait unos minutos y, a continuación, podrá dispositivo tooyour conectado a través de HTTPS a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="3ab35-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="3ab35-251">Verá un mensaje que indica que está conectado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ab35-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![Conexión remota de PowerShell mediante HTTP y SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="3ab35-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ab35-253">Next steps</span></span>

* <span data-ttu-id="3ab35-254">Obtenga más información sobre [mediante Windows PowerShell tooadminister dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3ab35-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="3ab35-255">Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3ab35-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

