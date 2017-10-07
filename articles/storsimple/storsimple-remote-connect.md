---
title: aaaConnect remotamente el dispositivo de StorSimple tooyour | Documentos de Microsoft
description: "Explica cómo tooconfigure el dispositivo para la administración remota y cómo tooconnect tooWindows PowerShell para StorSimple a través de HTTP o HTTPS."
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
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="f29f0-103">Conectar dispositivo de la serie 8000 de StorSimple tooyour de forma remota</span><span class="sxs-lookup"><span data-stu-id="f29f0-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="f29f0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f29f0-104">Overview</span></span>
<span data-ttu-id="f29f0-105">Puede usar el dispositivo de StorSimple de tooyour de tooconnect de comunicación remota de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f29f0-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="f29f0-106">Cuando se conecta de este modo, no verá un menú.</span><span class="sxs-lookup"><span data-stu-id="f29f0-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="f29f0-107">(Verá un menú solo si usa la consola serie de hello en hello dispositivo tooconnect). Con la comunicación remota de Windows PowerShell, conecte tooa espacio de ejecución específica.</span><span class="sxs-lookup"><span data-stu-id="f29f0-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="f29f0-108">También puede especificar el idioma para mostrar hello.</span><span class="sxs-lookup"><span data-stu-id="f29f0-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="f29f0-109">Para obtener más información acerca del uso de Windows PowerShell remoting toomanage el dispositivo, vaya demasiado[usar Windows PowerShell para StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f29f0-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="f29f0-110">Este tutorial le explica cómo tooconfigure el dispositivo para la administración remota y, a continuación, cómo tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f29f0-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="f29f0-111">Puede usar tooconnect HTTP o HTTPS a través de comunicación remota de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f29f0-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="f29f0-112">Sin embargo, cuando decida cómo tooconnect tooWindows PowerShell para StorSimple, tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f29f0-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="f29f0-113">Conexión directa toohello consola serie del dispositivo es segura, pero conexión toohello de consola serie a través de conmutadores de red no lo es.</span><span class="sxs-lookup"><span data-stu-id="f29f0-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="f29f0-114">Tenga cuidado de riesgos de seguridad de hello cuando se conecte la consola serie del dispositivo toohello a través de conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="f29f0-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="f29f0-115">Conexión a través de una sesión HTTP puede ofrecer más seguridad que la conexión a través de la consola serie de Hola a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="f29f0-116">Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="f29f0-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="f29f0-117">Conexión a través de una sesión HTTPS con un certificado autofirmado es más segura de Hola y Hola opción recomendada.</span><span class="sxs-lookup"><span data-stu-id="f29f0-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="f29f0-118">Puede conectarse remotamente toohello interfaz de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f29f0-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="f29f0-119">Sin embargo, el dispositivo de StorSimple de tooyour de acceso remoto a través de la interfaz de Windows PowerShell de hello no está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f29f0-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="f29f0-120">Se necesita tooenable administración remota en el dispositivo de hello en primer lugar y, a continuación, en Hola a cliente que sea tooaccess usa el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="f29f0-121">pasos de Hello descritos en este artículo se han ejecutado en un sistema host que ejecute Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f29f0-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="f29f0-122">Conectarse a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="f29f0-122">Connect through HTTP</span></span>
<span data-ttu-id="f29f0-123">Conexión tooWindows PowerShell para StorSimple a través de una sesión HTTP ofrece más seguridad que la conexión a través de la consola de serie de hello de dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f29f0-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="f29f0-124">Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="f29f0-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="f29f0-125">Puede usar Hola portal de Azure clásico o administración remota de hello consola serie tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f29f0-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="f29f0-126">Seleccione una de hello procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f29f0-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="f29f0-127">Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="f29f0-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="f29f0-128">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="f29f0-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="f29f0-129">Después de habilitar la administración remota, use Hola siguiendo el procedimiento tooprepare Hola del cliente para una conexión remota.</span><span class="sxs-lookup"><span data-stu-id="f29f0-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="f29f0-130">Preparar el cliente de Hola para conexión remota</span><span class="sxs-lookup"><span data-stu-id="f29f0-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="f29f0-131">Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="f29f0-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="f29f0-132">Realizar Hola siguiendo los pasos en la administración remota de hello Azure tooenable portal clásico a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="f29f0-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="f29f0-133">administración remota de tooenable a través de hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="f29f0-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="f29f0-134">Acceda a **Dispositivos** > **Configurar** para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="f29f0-135">Desplácese hacia abajo toohello **administración remota** sección.</span><span class="sxs-lookup"><span data-stu-id="f29f0-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="f29f0-136">Establecer **habilitar la administración remota** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="f29f0-137">Ahora puede elegir tooconnect mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="f29f0-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="f29f0-138">(el valor predeterminado de hello es tooconnect a través de HTTPS). Asegúrese de que se selecciona HTTP.</span><span class="sxs-lookup"><span data-stu-id="f29f0-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f29f0-139">La conexión a través de HTTP solo es aceptable en redes de confianza.</span><span class="sxs-lookup"><span data-stu-id="f29f0-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="f29f0-140">Haga clic en **guardar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="f29f0-141">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTP</span><span class="sxs-lookup"><span data-stu-id="f29f0-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="f29f0-142">Realizar Hola pasos Hola administración de dispositivos consola serie tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="f29f0-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="f29f0-143">administración remota de tooenable a través de la consola serie del dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="f29f0-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="f29f0-144">En el menú de la consola serie de hello, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="f29f0-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="f29f0-145">Para obtener más información acerca del uso de consola serie de hello en dispositivo hello, vaya demasiado[conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f29f0-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="f29f0-146">En el símbolo del sistema de hello, escriba:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="f29f0-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="f29f0-147">Se le notificará acerca de las vulnerabilidades de seguridad de Hola de usar HTTP tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="f29f0-148">Cuando se le solicite, confirme escribiendo **S**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="f29f0-149">Compruebe que está habilitado HTTP escribiendo: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="f29f0-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="f29f0-150">Compruebe que hello **RemoteManagementMode** campo muestra **HttpsAndHttpEnabled**.hello después de la ilustración se muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f29f0-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS y HTTP habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="f29f0-152">Preparar el cliente de Hola para conexión remota</span><span class="sxs-lookup"><span data-stu-id="f29f0-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="f29f0-153">Realizar Hola siguiendo los pasos en la administración remota de hello cliente tooenable.</span><span class="sxs-lookup"><span data-stu-id="f29f0-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="f29f0-154">cliente de hello tooprepare para conexión remota</span><span class="sxs-lookup"><span data-stu-id="f29f0-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="f29f0-155">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="f29f0-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="f29f0-156">Escriba Hola siguiente dirección IP de comando tooadd Hola de lista de hosts de confianza del cliente de toohello de hello StorSimple dispositivo:</span><span class="sxs-lookup"><span data-stu-id="f29f0-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="f29f0-157">Reemplace <*device_ip*> con la dirección IP de Hola de su dispositivo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f29f0-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="f29f0-158">Escriba Hola después comando toosave hello las credenciales del dispositivo en una variable:</span><span class="sxs-lookup"><span data-stu-id="f29f0-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="f29f0-159">En el cuadro de diálogo de Hola que aparece:</span><span class="sxs-lookup"><span data-stu-id="f29f0-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="f29f0-160">Escriba el nombre de usuario de hello en este formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="f29f0-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="f29f0-161">Escriba la contraseña del Administrador de dispositivos de Hola que se estableció al dispositivo de Hola se configuró con el Asistente para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="f29f0-162">es la contraseña predeterminada de Hello *Password1*.</span><span class="sxs-lookup"><span data-stu-id="f29f0-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="f29f0-163">Iniciar una sesión de Windows PowerShell en el dispositivo de hello, escriba este comando:</span><span class="sxs-lookup"><span data-stu-id="f29f0-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="f29f0-164">toocreate una sesión de Windows PowerShell para su uso con el dispositivo virtual StorSimple de hello, anexar hello `–Port` parámetro y especifique el puerto público de Hola que configuró en la comunicación remota de dispositivo Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f29f0-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="f29f0-165">En este punto, debe tener un dispositivo de toohello de sesión de Windows PowerShell remoto activo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Conexión remota de PowerShell mediante HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="f29f0-167">Conectarse a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="f29f0-167">Connect through HTTPS</span></span>
<span data-ttu-id="f29f0-168">Conexión tooWindows PowerShell para StorSimple a través de una sesión HTTPS es más segura de hello y método de conexión de forma remota dispositivos de Microsoft Azure StorSimple tooyour recomendado.</span><span class="sxs-lookup"><span data-stu-id="f29f0-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="f29f0-169">Hola procedimientos siguientes explica cómo tooset seguridad Hola serie consola y los equipos cliente para que puedan utilizar HTTPS tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f29f0-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="f29f0-170">Puede usar Hola portal de Azure clásico o administración remota de hello consola serie tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f29f0-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="f29f0-171">Seleccione una de hello procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f29f0-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="f29f0-172">Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="f29f0-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="f29f0-173">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="f29f0-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="f29f0-174">Después de habilitar la administración remota, use Hola después de host de hello tooprepare de procedimientos para una administración remota y conecte toohello dispositivo desde el host remoto Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="f29f0-175">Preparar el host de hello para la administración remota</span><span class="sxs-lookup"><span data-stu-id="f29f0-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="f29f0-176">Conecte el dispositivo de toohello desde el host remoto hello</span><span class="sxs-lookup"><span data-stu-id="f29f0-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="f29f0-177">Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="f29f0-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="f29f0-178">Realizar Hola siguiendo los pasos en la administración remota de hello Azure tooenable portal clásico a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f29f0-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="f29f0-179">tooenable la administración remota a través de HTTPS de hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="f29f0-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="f29f0-180">Acceda a **Dispositivos** > **Configurar** para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="f29f0-181">Desplácese hacia abajo toohello **administración remota** sección.</span><span class="sxs-lookup"><span data-stu-id="f29f0-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="f29f0-182">Establecer **habilitar la administración remota** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="f29f0-183">Ahora puede elegir tooconnect mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f29f0-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="f29f0-184">(el valor predeterminado de hello es tooconnect a través de HTTPS). Asegúrese de que se ha seleccionado HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f29f0-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="f29f0-185">Haga clic en **Descargar certificado de administración remota**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="f29f0-186">Especifique una ubicación toosave este archivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-186">Specify a location toosave this file.</span></span> <span data-ttu-id="f29f0-187">Necesitará tooinstall este certificado en el equipo cliente o host Hola que va a usar tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="f29f0-188">Haga clic en **guardar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="f29f0-189">Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="f29f0-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="f29f0-190">Realizar Hola pasos Hola administración de dispositivos consola serie tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="f29f0-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="f29f0-191">administración remota de tooenable a través de la consola serie del dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="f29f0-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="f29f0-192">En el menú de la consola serie de hello, seleccione la opción 1.</span><span class="sxs-lookup"><span data-stu-id="f29f0-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="f29f0-193">Para obtener más información acerca del uso de consola serie de hello en dispositivo hello, vaya demasiado[conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f29f0-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="f29f0-194">En el símbolo del sistema de hello, escriba:</span><span class="sxs-lookup"><span data-stu-id="f29f0-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="f29f0-195">Esto debe habilitar HTTPS en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="f29f0-196">Compruebe que se ha habilitado HTTPS escribiendo:</span><span class="sxs-lookup"><span data-stu-id="f29f0-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="f29f0-197">Asegúrese de que ese hello **RemoteManagementMode** campo muestra **HttpsEnabled**.hello después de la ilustración se muestra esta configuración en PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f29f0-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serie HTTPS habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="f29f0-199">De salida de hello de `Get-HcsSystem`, copie Hola de número de serie del dispositivo de Hola y guardarlo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="f29f0-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f29f0-200">número de serie de Hello asigna toohello nombre CN de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="f29f0-201">Obtenga un certificado de administración remota, escriba:</span><span class="sxs-lookup"><span data-stu-id="f29f0-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="f29f0-202">Aparecerá un siguiente toohello similar de certificado.</span><span class="sxs-lookup"><span data-stu-id="f29f0-202">A certificate similar toohello following will appear.</span></span>
   
    ![Obtener certificado de administración remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="f29f0-204">Copiar información de hello en el certificado de Hola de **---BEGIN CERTIFICATE---** demasiado**---END CERTIFICATE---** en un editor de texto como Bloc de notas y guárdelo como un archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="f29f0-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="f29f0-205">(Copiará este host remoto de archivo tooyour al preparar los host de Hola.)</span><span class="sxs-lookup"><span data-stu-id="f29f0-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f29f0-206">toogenerate un nuevo certificado, utilice hello `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f29f0-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="f29f0-207">Preparar el host de hello para la administración remota</span><span class="sxs-lookup"><span data-stu-id="f29f0-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="f29f0-208">equipo de host de hello tooprepare para una conexión remota que utiliza una sesión HTTPS, lleve a cabo Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f29f0-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="f29f0-209">[Archivo de importación hello .cer en almacén raíz de Hola de hello cliente o host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="f29f0-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="f29f0-210">[Agregar archivo hosts toohello de números de serie de dispositivo de hello en el host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="f29f0-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="f29f0-211">A continuación se describe cada uno de estos procedimientos.</span><span class="sxs-lookup"><span data-stu-id="f29f0-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="f29f0-212">certificado de hello tooimport en host remoto hello</span><span class="sxs-lookup"><span data-stu-id="f29f0-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="f29f0-213">Haga clic en el archivo .cer de hello y seleccione **instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="f29f0-214">Esto iniciará Hola Asistente para importación de certificados.</span><span class="sxs-lookup"><span data-stu-id="f29f0-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Asistente para importación de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="f29f0-216">Para **Ubicación de almacén**, seleccione **Equipo local** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="f29f0-217">Seleccione **colocar todos los certificados en hello después almacén**y, a continuación, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="f29f0-218">Navegar por el almacén raíz de toohello del host remoto y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Asistente para importación de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="f29f0-220">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="f29f0-220">Click **Finish**.</span></span> <span data-ttu-id="f29f0-221">Aparece un mensaje que indica que la importación de hello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="f29f0-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Asistente para importación de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="f29f0-223">host remoto del toohello tooadd dispositivo números de serie</span><span class="sxs-lookup"><span data-stu-id="f29f0-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="f29f0-224">Inicie el Bloc de notas como administrador y, a continuación, abra el archivo de hosts de hello ubicado en \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="f29f0-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="f29f0-225">Agregar Hola siguiente archivo de hosts de tres entradas tooyour: **dirección IP de DATA 0**, **dirección IP fija del controlador 0**, y **dirección IP fija del controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="f29f0-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="f29f0-226">Escriba el número de serie del dispositivo Hola que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f29f0-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="f29f0-227">Asigne esta dirección IP de toohello como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="f29f0-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="f29f0-228">Para el controlador 0 y 1, anexe **Controller0** y **Controller1** final Hola Hola del número de serie (nombre CN).</span><span class="sxs-lookup"><span data-stu-id="f29f0-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Agregar nombre CN toohosts archivo](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="f29f0-230">Guardar el archivo de hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="f29f0-231">Conecte el dispositivo de toohello desde el host remoto hello</span><span class="sxs-lookup"><span data-stu-id="f29f0-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="f29f0-232">Usar Windows PowerShell y SSL tooenter una sesión de SSAdmin en el dispositivo desde un cliente o host remoto.</span><span class="sxs-lookup"><span data-stu-id="f29f0-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="f29f0-233">sesión de SSAdmin Hola asigna toooption 1 Hola [consola serie](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menú del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="f29f0-234">Realizar Hola siguiendo el procedimiento en el equipo Hola del que desea que la conexión remota de Windows PowerShell de toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="f29f0-235">tooenter una sesión de SSAdmin en dispositivo hello mediante Windows PowerShell y SSL</span><span class="sxs-lookup"><span data-stu-id="f29f0-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="f29f0-236">Iniciar una sesión de Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="f29f0-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="f29f0-237">Agregar hosts de confianza del cliente de hello dispositivo IP dirección toohello, escriba:</span><span class="sxs-lookup"><span data-stu-id="f29f0-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="f29f0-238">Donde <*device_ip*> Hola dirección de IP del dispositivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f29f0-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="f29f0-239">Cree una nueva credencial, escriba:</span><span class="sxs-lookup"><span data-stu-id="f29f0-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="f29f0-240">Donde <*dirección IP del dispositivo de destino*> Hola dirección de IP de DATA 0 de su dispositivo; por ejemplo, **10.126.173.90** como se muestra en hello delante de la imagen del archivo de hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29f0-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="f29f0-241">Además, proporcione la contraseña de administrador de hello para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="f29f0-242">Cree una sesión, escriba:</span><span class="sxs-lookup"><span data-stu-id="f29f0-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="f29f0-243">Para el parámetro - ComputerName de hello en cmdlet hello, proporcionar Hola <*número de serie del dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="f29f0-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="f29f0-244">Se ha asignado este número de serie toohello dirección IP de DATA 0 en el archivo de hosts de hello en el host remoto; Por ejemplo, **SHX0991003G44MT** como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="f29f0-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="f29f0-245">Escriba:</span><span class="sxs-lookup"><span data-stu-id="f29f0-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="f29f0-246">Necesitará toowait unos minutos y, a continuación, podrá dispositivo tooyour conectado a través de HTTPS a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="f29f0-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="f29f0-247">Verá un mensaje que indica que está conectado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f29f0-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![Conexión remota de PowerShell mediante HTTP y SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="f29f0-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f29f0-249">Next steps</span></span>
* <span data-ttu-id="f29f0-250">Obtenga más información sobre [mediante Windows PowerShell tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f29f0-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="f29f0-251">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f29f0-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

