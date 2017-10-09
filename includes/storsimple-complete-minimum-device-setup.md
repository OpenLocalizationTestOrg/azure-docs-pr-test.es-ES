<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>instalación de dispositivo de StorSimple mínima de toocomplete Hola
1. Hola **dispositivos** página, dispositivo Hola seleccione, haga clic en la flecha de hello en página de hello dispositivo nombre toogo toohello dispositivo específico. 
   
    ![Página de dispositivos con el dispositivo en línea](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Haga clic en el icono de inicio rápido ![el icono de inicio rápido](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess Hola página de inicio rápido de dispositivo. Haga clic en **completar el programa de instalación de dispositivo** toostart hello **Configurar dispositivo** asistente.
   
    ![Página de inicio rápido del dispositivo](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. En hello **configuración básica** página, Hola siguientes:
   
   1. Proporcione un **nombre descriptivo** para el dispositivo. nombre de dispositivo predeterminado de Hello refleja información como el modelo de dispositivo de Hola y número de serie. Puede asignar un nombre descriptivo de la too64 caracteres toomanage el dispositivo.
   2. Conjunto hello **zona horaria** basadas en ubicación geográfica de hello en qué Hola se va a implementar el dispositivo. El dispositivo usará esta zona horaria para todas las operaciones programadas.
   3. En **Configuración DNS**, proporcione una dirección para el **Servidor DNS secundario**. Si usas IPv6, campo Hola se rellenará según Hola prefijo de IPv6 proporcionado en la interfaz de Windows PowerShell de Hola. 
      Si no está configurado el servidor DNS secundario de hello, es posible no que permiten toosave la configuración del dispositivo.
   4. En Interfaces habilitadas para iSCSI, habilite al menos una red para iSCSI. Al menos una interfaz de red necesita toobe habilitada para la nube y una interfaz debe toobe habilitada para iSCSI. DATA 0 se habilita para la nube automáticamente.
      
      ![Configuración básica de la instalación mínima del dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Haga clic en el icono de flecha de Hola. ![Icono de flecha de StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. En hello **Interfaces de red** , proporcione Hola fijo de direcciones IP para el controlador 0 y 1. Si hello DATA 0 interfaz está configurada para IPv4, hello corregido toobe de necesidad de direcciones IP proporcionada en hello formato IPv4. Si ha proporcionado un prefijo para la configuración IPv6, Hola direcciones IP fijas se rellenarán automáticamente en estos campos.

    > [!NOTE] 
    > - direcciones IP fijas de controlador de Hello necesita el toobe que liberar direcciones IP de subred de hello accesible por dirección IP del dispositivo Hola.
    > - Hola direcciones IP para el controlador de hello fijas se utilizan para dar servicio a dispositivos de toohello de las actualizaciones de Hola y por consiguiente Hola IP fija debe ser enrutables y deben poder tooconnect toohello Internet.

    ![Interfaces de red de la instalación mínima del dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Haga clic en el icono de verificación de hello ![icono de verificación de StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Se devolverá el dispositivo de toohello **inicio rápido** página.
   
   > [!NOTE]
   > Puede modificar la Hola todos los otros ajustes del dispositivo en cualquier momento mediante el acceso a hello **configurar** página.
   > 
   > 

![Vídeo disponible](./media/storsimple-complete-minimum-device-setup/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo toocomplete Hola configuración mínima del dispositivo, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).

