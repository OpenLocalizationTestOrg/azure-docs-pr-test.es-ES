<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>instalación de dispositivo de StorSimple mínima de toocomplete Hola
1. Seleccionar dispositivo de Hola y haga clic en **inicio rápido**. Haga clic en **completar el programa de instalación de dispositivo** Asistente de dispositivo de configuración de toostart Hola.
2. En el Asistente de dispositivo de configuración de hello **configuración básica** diálogo cuadro, Hola siguientes:
   
   1. Proporcione un **nombre descriptivo** para el dispositivo. nombre de dispositivo predeterminado de Hello refleja información como el modelo de dispositivo de Hola y número de serie. Puede asignar un nombre descriptivo de la too64 caracteres toomanage el dispositivo.
   2. Conjunto hello **zona horaria** basadas en ubicación geográfica de hello en qué Hola se va a implementar el dispositivo. El dispositivo usará esta zona horaria para todas las operaciones programadas.
   3. En **Configuración DNS**, proporcione una dirección para el **Servidor DNS secundario**. Si usas IPv6, campo Hola se rellenará según Hola prefijo de IPv6 proporcionado en la interfaz de Windows PowerShell de Hola. 
      Si no está configurado el servidor DNS secundario de hello, es posible no que permiten toosave la configuración del dispositivo.
   4. En Interfaces habilitadas para iSCSI, habilite al menos una red para iSCSI. Al menos una interfaz de red necesita toobe habilitada para la nube y una interfaz debe toobe habilitada para iSCSI. DATA 0 se habilita para la nube automáticamente.
      
      ![Configuración básica de la instalación mínima del dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Haga clic en el icono de flecha de Hola. ![Icono de flecha de StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. Hola **Interfaces de red** diálogo cuadro, proporcione Hola fijo de direcciones IP para el controlador 0 y 1. **direcciones IP fijas de controlador de Hello necesita el toobe que liberar direcciones IP de subred de hello accesible por dirección IP del dispositivo Hola.** Si hello DATA 0 interfaz está configurada para IPv4, hello corregido toobe de necesidad de direcciones IP proporcionada en hello formato IPv4. Si ha proporcionado un prefijo para la configuración IPv6, Hola direcciones IP fijas se rellenarán automáticamente en estos campos.

    ![Interfaces de red de la instalación mínima del dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Hola direcciones IP para el controlador de hello fijas se utilizan para dar servicio a dispositivos de toohello de las actualizaciones de Hola y por consiguiente Hola IP fija debe ser enrutables y deben poder tooconnect toohello Internet. Puede comprobar que el controlador fijo direcciones IP sean enrutables mediante el uso de hello [Test-HcsmConnection] [ Test] cmdlet. Hola siguiente ejemplo muestra fija del controlador direcciones IP es toohello enrutado Internet y puede tener acceso a Hola servidores de Microsoft Update. 

     ![Test-HcsmConnection que muestra direcciones IP enrutables](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Haga clic en el icono de verificación de hello ![icono de verificación de StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Se devolverá el dispositivo de toohello **inicio rápido** página.
   
   > [!NOTE]
   > Puede modificar la Hola todos los otros ajustes del dispositivo en cualquier momento mediante el acceso a hello **configurar** página.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx