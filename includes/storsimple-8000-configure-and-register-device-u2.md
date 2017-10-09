<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="b9d14-101">dispositivo de hello tooconfigure y registro</span><span class="sxs-lookup"><span data-stu-id="b9d14-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="b9d14-102">Obtener acceso a la interfaz de Windows PowerShell de hello en la consola serie del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b9d14-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b9d14-103">Vea [consola serie del dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="b9d14-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="b9d14-104">**Ser exactamente procedimiento de hello toofollow seguro o no será capaz de tooaccess consola de Hola.**</span><span class="sxs-lookup"><span data-stu-id="b9d14-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="b9d14-105">En la sesión de Hola que se abre, presione **ENTRAR** una vez tooget un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b9d14-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="b9d14-106">Es posible que toochoose solicitadas Hola idioma que le gustaría tener tooset en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="b9d14-107">Especificar el idioma de hello y, a continuación, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="b9d14-108">En el menú de consola serie de Hola que aparece, elija la opción 1 demasiado**iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="b9d14-109">Complete los pasos 5-12 de valores de configuración de red mínimos requeridos de hello tooconfigure para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="b9d14-110">**Estos pasos de configuración deben toobe realizada en el controlador activo de hello de dispositivo de Hola.**</span><span class="sxs-lookup"><span data-stu-id="b9d14-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="b9d14-111">menú de la consola serie de Hello indica el estado de controlador de hello en el mensaje de pancarta Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="b9d14-112">Si no está conectado toohello controlador activo, desconéctese y, a continuación, conéctese toohello de controlador activo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="b9d14-113">En el símbolo de hello, escriba su contraseña.</span><span class="sxs-lookup"><span data-stu-id="b9d14-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="b9d14-114">es la contraseña predeterminada del dispositivo de Hello **Password1**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="b9d14-115">Hola de tipo siguiente comando: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="b9d14-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="b9d14-116">Un Asistente para la instalación aparecerán toohelp configurar configuración de red de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="b9d14-117">Fuente de alimentación Hola Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b9d14-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="b9d14-118">Dirección IP de interfaz de red 0 datos Hola</span><span class="sxs-lookup"><span data-stu-id="b9d14-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="b9d14-119">Máscara de subred</span><span class="sxs-lookup"><span data-stu-id="b9d14-119">Subnet mask</span></span>
   * <span data-ttu-id="b9d14-120">Puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="b9d14-120">Gateway</span></span>
   * <span data-ttu-id="b9d14-121">Dirección IP para el servidor DNS principal</span><span class="sxs-lookup"><span data-stu-id="b9d14-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="b9d14-122">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="b9d14-123">En hello anteriores resultados del ejemplo, puede ver que el sistema de hello está validando configuración de red después de cada paso en el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b9d14-124">Puede que tenga toowait durante unos minutos para la máscara de subred de Hola y Hola DNS configuración toobe aplicado.</span><span class="sxs-lookup"><span data-stu-id="b9d14-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="b9d14-125">Si recibe un mensaje de error de "Comprobación de hello red conectividad tooData 0", compruebe la conexión de red física de hello en hello datos interfaz de red 0 de su controlador activo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="b9d14-126">(Opcional) Configure el servidor proxy web.</span><span class="sxs-lookup"><span data-stu-id="b9d14-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="b9d14-127">Aunque la configuración del proxy web es opcional, **tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="b9d14-128">Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="b9d14-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="b9d14-129">Configure un servidor NTP principal para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="b9d14-130">Se requieren servidores NTP, dado que el dispositivo debe sincronizar la hora para que pueda autenticarse con los proveedores de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="b9d14-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="b9d14-131">Asegúrese de que su red permite toopass de tráfico NTP desde su toohello de centro de datos Internet.</span><span class="sxs-lookup"><span data-stu-id="b9d14-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="b9d14-132">Si esto no es posible, especifique un servidor NTP interno.</span><span class="sxs-lookup"><span data-stu-id="b9d14-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="b9d14-133">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="b9d14-134">Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira después de la primera sesión de Hola y deberá toochange TI ahora.</span><span class="sxs-lookup"><span data-stu-id="b9d14-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="b9d14-135">Cuando se le solicite, proporcione una contraseña de administrador del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="b9d14-136">Una contraseña de administrador del dispositivo válida debe tener entre 8 y 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b9d14-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="b9d14-137">Hello contraseña debe contener tres de hello siguientes: caracteres en minúsculas, mayúsculas, numéricos y especiales.</span><span class="sxs-lookup"><span data-stu-id="b9d14-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="b9d14-138">paso final de Hello en el Asistente para la instalación de hello registra el dispositivo con hello servicio Administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b9d14-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="b9d14-139">Para ello, necesitará la clave de registro del servicio Hola que obtuvo en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="b9d14-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="b9d14-140">Una vez proporcionada la clave de registro de hello, deberá toowait de 2 a 3 minutos antes de registrar el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b9d14-141">Puede presionar Ctrl + C en cualquier asistente para la instalación de tiempo tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="b9d14-142">Si ha especificado todas las configuraciones de red de hello (dirección IP de Data 0, máscara de subred y puerta de enlace), se conservarán las entradas.</span><span class="sxs-lookup"><span data-stu-id="b9d14-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="b9d14-143">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b9d14-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="b9d14-144">Una vez registrado el dispositivo de hello, aparecerá una clave de cifrado de datos de servicio.</span><span class="sxs-lookup"><span data-stu-id="b9d14-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="b9d14-145">Copie esta clave y guárdela en un lugar seguro,</span><span class="sxs-lookup"><span data-stu-id="b9d14-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="b9d14-146">**Esta clave será necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello servicio Administrador de dispositivos de StorSimple.**</span><span class="sxs-lookup"><span data-stu-id="b9d14-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="b9d14-147">Consulte demasiado[seguridad de StorSimple](../articles/storsimple/storsimple-security.md) para obtener más información acerca de esta clave.</span><span class="sxs-lookup"><span data-stu-id="b9d14-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Registrar el dispositivo 7 de StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="b9d14-149">texto de hello toocopy desde la ventana de consola serie de hello, simplemente seleccione texto hello.</span><span class="sxs-lookup"><span data-stu-id="b9d14-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="b9d14-150">A continuación, debe ser capaz de toopaste en el Portapapeles de Hola o cualquier editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b9d14-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="b9d14-151">No use Ctrl + clave de cifrado de datos de servicio de C toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="b9d14-152">Con Ctrl + C hará que a se tooexit Hola Asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="b9d14-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="b9d14-153">Como resultado, no se cambiarán la contraseña de administrador de dispositivos de Hola y dispositivo Hola restablecerá la contraseña predeterminada de toohello.</span><span class="sxs-lookup"><span data-stu-id="b9d14-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="b9d14-154">Consola serie de Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="b9d14-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="b9d14-155">Devolver toohello portal de Azure y completar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b9d14-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="b9d14-156">Servicio de administrador de dispositivos de StorSimple de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="b9d14-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="b9d14-157">Haga clic en **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="b9d14-158">Hola tabular listado de dispositivos, compruebe que ese dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9d14-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="b9d14-159">estado de dispositivo de Hello debe ser **listo tooset seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Página de dispositivos de StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="b9d14-161">Puede que necesite toowait para un par de minutos para toochange de estado de dispositivo de hello demasiado**listo tooset seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b9d14-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="b9d14-162">Si el dispositivo de hello no aparecen en esta lista, deberá toomake seguro de que la red de firewall se ha configurado como se describe en [requisitos de red para el dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b9d14-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="b9d14-163">Compruebe que el puerto 9354 esté abierto para comunicaciones de salida tal y como se utiliza por bus de servicio de hello para la comunicación de dispositivo del servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b9d14-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

