<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="3eb67-101">dispositivo de hello tooconfigure y registro</span><span class="sxs-lookup"><span data-stu-id="3eb67-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="3eb67-102">Obtener acceso a la interfaz de Windows PowerShell de hello en la consola serie del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3eb67-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="3eb67-103">Vea [consola serie del dispositivo Use PuTTY tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3eb67-103">See [Use PuTTY tooconnect toohello device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="3eb67-104">**Ser exactamente procedimiento de hello toofollow seguro o no será capaz de tooaccess consola de Hola.**</span><span class="sxs-lookup"><span data-stu-id="3eb67-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="3eb67-105">En la sesión de Hola que se abre, presione Intro una vez tooget un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="3eb67-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span>
3. <span data-ttu-id="3eb67-106">Es posible que toochoose solicitadas Hola idioma que le gustaría tener tooset en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3eb67-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="3eb67-107">Especifique el idioma de hello y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="3eb67-107">Specify hello language, and then press Enter.</span></span>
   
    ![Configurar y registrar el dispositivo 1 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="3eb67-109">En el menú de consola serie de Hola que aparece, elija toolog opción 1 en con acceso completo.</span><span class="sxs-lookup"><span data-stu-id="3eb67-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span>
   
    ![Registrar el dispositivo 2 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="3eb67-111">Realizar Hola después de la configuración de red mínimos requeridos de pasos tooconfigure hello para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3eb67-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3eb67-112">Estos pasos de configuración deben toobe realizada en el controlador activo de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="3eb67-113">menú de la consola serie de Hello indica el estado de controlador de hello en el mensaje de pancarta Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="3eb67-114">Si no se conectó toohello de controlador activo, desconéctese y, a continuación, conéctese controlador activo toohello.</span><span class="sxs-lookup"><span data-stu-id="3eb67-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="3eb67-115">En el símbolo de hello, escriba su contraseña.</span><span class="sxs-lookup"><span data-stu-id="3eb67-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="3eb67-116">es la contraseña predeterminada del dispositivo de Hello **Password1**.</span><span class="sxs-lookup"><span data-stu-id="3eb67-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="3eb67-117">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="3eb67-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="3eb67-118">Un Asistente para la instalación aparecerán toohelp configurar configuración de red de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="3eb67-119">Fuente de alimentación Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="3eb67-119">Supply hello following information:</span></span>
      
      * <span data-ttu-id="3eb67-120">Dirección IP para la interfaz de red DATA 0</span><span class="sxs-lookup"><span data-stu-id="3eb67-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="3eb67-121">Máscara de subred</span><span class="sxs-lookup"><span data-stu-id="3eb67-121">Subnet mask</span></span>
      * <span data-ttu-id="3eb67-122">Puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="3eb67-122">Gateway</span></span>
      * <span data-ttu-id="3eb67-123">Dirección IP para el servidor DNS principal</span><span class="sxs-lookup"><span data-stu-id="3eb67-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="3eb67-124">Dirección IP para el servidor NTP principal</span><span class="sxs-lookup"><span data-stu-id="3eb67-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="3eb67-125">Puede que tenga toowait durante unos minutos para la máscara de subred de Hola y toobe de configuración de DNS aplicado.</span><span class="sxs-lookup"><span data-stu-id="3eb67-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="3eb67-126">De manera opcional, configure el servidor proxy web.</span><span class="sxs-lookup"><span data-stu-id="3eb67-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="3eb67-127">Aunque la configuración del proxy web es opcional, tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="3eb67-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="3eb67-128">Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="3eb67-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="3eb67-129">Presione Ctrl + C Asistente para la instalación de tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="3eb67-130">Instalar actualizaciones de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="3eb67-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="3eb67-131">Usar hello siguiente cmdlet tooset direcciones IP de ambos controladores hello:</span><span class="sxs-lookup"><span data-stu-id="3eb67-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="3eb67-132">En el símbolo de hello, ejecute `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="3eb67-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="3eb67-133">Debe recibir una notificación para avisarle de que hay actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="3eb67-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="3eb67-134">Ejecute `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="3eb67-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="3eb67-135">Puede ejecutar este comando en cualquier nodo.</span><span class="sxs-lookup"><span data-stu-id="3eb67-135">You can run this command on any node.</span></span> <span data-ttu-id="3eb67-136">Las actualizaciones se aplicarán en el primer controlador de hello, controlador Hola conmutarán por error y, a continuación, hello las actualizaciones se aplicarán en Hola otro controlador.</span><span class="sxs-lookup"><span data-stu-id="3eb67-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="3eb67-137">Puede supervisar el progreso de Hola de actualización de hello ejecutando `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="3eb67-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="3eb67-138">Hello siguiente salida de ejemplo muestra hello actualización en curso.</span><span class="sxs-lookup"><span data-stu-id="3eb67-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="3eb67-139">Después de la salida de ejemplo de Hola indica que la actualización Hola ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="3eb67-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="3eb67-140">Esta operación puede tardar horas too11 Hola a tooapply todos hello las actualizaciones, incluidas las actualizaciones de Windows.</span><span class="sxs-lookup"><span data-stu-id="3eb67-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>
8. <span data-ttu-id="3eb67-141">Ejecute hello siguiendo el portal de Microsoft Azure Government cmdlet toopoint Hola dispositivos toohello (porque señala toohello pública portal de Azure clásico de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="3eb67-141">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="3eb67-142">Ambos controladores se reiniciarán.</span><span class="sxs-lookup"><span data-stu-id="3eb67-142">This will restart both controllers.</span></span> <span data-ttu-id="3eb67-143">Recomendamos que utilice dos sesiones PuTTY toosimultaneously conectar tooboth controladores para que puedan ver cuando se reinicia cada controlador.</span><span class="sxs-lookup"><span data-stu-id="3eb67-143">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="3eb67-144">Aparecerá un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="3eb67-144">You will see a confirmation message.</span></span> <span data-ttu-id="3eb67-145">Acepte el predeterminado de hello (**Y**).</span><span class="sxs-lookup"><span data-stu-id="3eb67-145">Accept hello default (**Y**).</span></span>
9. <span data-ttu-id="3eb67-146">Ejecute hello después de la instalación de tooresume de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3eb67-146">Run hello following cmdlet tooresume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Asistente para reanudar la instalación](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="3eb67-148">Cuando se reanude el programa de instalación, el Asistente de hello serán la versión de Hola Update 2.</span><span class="sxs-lookup"><span data-stu-id="3eb67-148">When you resume setup, hello wizard will be hello Update 2 version.</span></span>
10. <span data-ttu-id="3eb67-149">Acepte la configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-149">Accept hello network settings.</span></span> <span data-ttu-id="3eb67-150">Verá un mensaje de validación después de aceptar cada configuración.</span><span class="sxs-lookup"><span data-stu-id="3eb67-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="3eb67-151">Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira después de la primera sesión de Hola y deberá toochange TI ahora.</span><span class="sxs-lookup"><span data-stu-id="3eb67-151">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="3eb67-152">Cuando se le solicite, proporcione una contraseña de administrador del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3eb67-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="3eb67-153">Una contraseña de administrador del dispositivo válida debe tener entre 8 y 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="3eb67-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="3eb67-154">Hello contraseña debe contener tres de hello siguientes: caracteres en minúsculas, mayúsculas, numéricos y especiales.</span><span class="sxs-lookup"><span data-stu-id="3eb67-154">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Registrar el dispositivo 5 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="3eb67-156">paso final de Hello en el Asistente para la instalación de hello registra el dispositivo con hello el servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="3eb67-156">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="3eb67-157">Para ello, necesita Hola clave de registro del servicio que obtuvo en [paso 2: clave de registro del servicio de Get hello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="3eb67-157">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="3eb67-158">Una vez proporcionada la clave de registro de hello, deberá toowait de 2 a 3 minutos antes de registrar el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-158">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3eb67-159">Puede presionar Ctrl + C en cualquier asistente para la instalación de tiempo tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-159">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="3eb67-160">Si ha especificado todas las configuraciones de red de hello (dirección IP de Data 0, máscara de subred y puerta de enlace), se conservarán las entradas.</span><span class="sxs-lookup"><span data-stu-id="3eb67-160">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progreso de registro de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="3eb67-162">Una vez registrado el dispositivo de hello, aparecerá una clave de cifrado de datos de servicio.</span><span class="sxs-lookup"><span data-stu-id="3eb67-162">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="3eb67-163">Copie esta clave y guárdela en un lugar seguro,</span><span class="sxs-lookup"><span data-stu-id="3eb67-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="3eb67-164">**Esta clave será necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello el servicio StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="3eb67-164">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="3eb67-165">Consulte demasiado[seguridad de StorSimple](../articles/storsimple/storsimple-security.md) para obtener más información acerca de esta clave.</span><span class="sxs-lookup"><span data-stu-id="3eb67-165">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Registrar el dispositivo 7 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="3eb67-167">texto de hello toocopy desde la ventana de consola serie de hello, simplemente seleccione texto hello.</span><span class="sxs-lookup"><span data-stu-id="3eb67-167">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="3eb67-168">A continuación, debe ser capaz de toopaste en el Portapapeles de Hola o cualquier editor de texto.</span><span class="sxs-lookup"><span data-stu-id="3eb67-168">You should then be able toopaste it in hello clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="3eb67-169">No use Ctrl + clave de cifrado de datos de servicio de C toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="3eb67-169">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="3eb67-170">Con Ctrl + C hará que a se tooexit Hola Asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="3eb67-170">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="3eb67-171">Como resultado, no se cambiarán la contraseña de administrador de dispositivos de Hola y dispositivo Hola restablecerá la contraseña predeterminada de toohello.</span><span class="sxs-lookup"><span data-stu-id="3eb67-171">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
14. <span data-ttu-id="3eb67-172">Consola serie de Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="3eb67-172">Exit hello serial console.</span></span>
15. <span data-ttu-id="3eb67-173">Devolver toohello Portal de administración pública de Azure y completar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3eb67-173">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="3eb67-174">Haga doble clic en su hello tooaccess de servicio de administrador de StorSimple **inicio rápido** página.</span><span class="sxs-lookup"><span data-stu-id="3eb67-174">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="3eb67-175">Haga clic en **Ver los dispositivos conectados**.</span><span class="sxs-lookup"><span data-stu-id="3eb67-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="3eb67-176">En hello **dispositivos** página, compruebe que dicho dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de saludo.</span><span class="sxs-lookup"><span data-stu-id="3eb67-176">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="3eb67-177">estado de dispositivo de Hello debe ser **Online**.</span><span class="sxs-lookup"><span data-stu-id="3eb67-177">hello device status should be **Online**.</span></span>
       
        ![Página de dispositivos de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="3eb67-179">Si el estado del dispositivo de hello es **sin conexión**, espere unos minutos para hello toocome de dispositivo en línea.</span><span class="sxs-lookup"><span data-stu-id="3eb67-179">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span>
       
        <span data-ttu-id="3eb67-180">Si el dispositivo de hello sigue estando sin conexión después de unos minutos, deberá toomake seguro de que la red de firewall se ha configurado como se describe en [requisitos de red para el dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3eb67-180">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="3eb67-181">Compruebe que el puerto 9354 esté abierto para comunicaciones de salida tal y como se utiliza por bus de servicio de hello para la comunicación de servicio al dispositivo de StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="3eb67-181">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager Service-to-device communication.</span></span>

