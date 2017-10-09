<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de hello tooconfigure y registro
1. Obtener acceso a la interfaz de Windows PowerShell de hello en la consola serie del dispositivo de StorSimple. Vea [consola serie del dispositivo Use PuTTY tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) para obtener instrucciones. **Ser exactamente procedimiento de hello toofollow seguro o no será capaz de tooaccess consola de Hola.**
2. En la sesión de Hola que se abre, presione Intro una vez tooget un símbolo del sistema.
3. Es posible que toochoose solicitadas Hola idioma que le gustaría tener tooset en el dispositivo. Especifique el idioma de hello y, a continuación, presione ENTRAR.
   
    ![Configurar y registrar el dispositivo 1 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. En el menú de consola serie de Hola que aparece, elija toolog opción 1 en con acceso completo.
   
    ![Registrar el dispositivo 2 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Realizar Hola después de la configuración de red mínimos requeridos de pasos tooconfigure hello para el dispositivo.
   
   > [!IMPORTANT]
   > Estos pasos de configuración deben toobe realizada en el controlador activo de hello de dispositivo de Hola. menú de la consola serie de Hello indica el estado de controlador de hello en el mensaje de pancarta Hola. Si no se conectó toohello de controlador activo, desconéctese y, a continuación, conéctese controlador activo toohello.
   > 
   > 
   
   1. En el símbolo de hello, escriba su contraseña. es la contraseña predeterminada del dispositivo de Hello **Password1**.
   2. Escriba el siguiente comando de hello:
      
        `Invoke-HcsSetupWizard`
   3. Un Asistente para la instalación aparecerán toohelp configurar configuración de red de hello de dispositivo de Hola. Fuente de alimentación Hola siguiente información:
      
      * Dirección IP para la interfaz de red DATA 0
      * Máscara de subred
      * Puerta de enlace
      * Dirección IP para el servidor DNS principal
      * Dirección IP para el servidor NTP principal
      
      > [!NOTE]
      > Puede que tenga toowait durante unos minutos para la máscara de subred de Hola y toobe de configuración de DNS aplicado.
      > 
      > 
   4. De manera opcional, configure el servidor proxy web.
      
      > [!IMPORTANT]
      > Aunque la configuración del proxy web es opcional, tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí. Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
      > 
      > 
6. Presione Ctrl + C Asistente para la instalación de tooexit Hola.
7. Instalar actualizaciones de hello como sigue:
   
   1. Usar hello siguiente cmdlet tooset direcciones IP de ambos controladores hello:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. En el símbolo de hello, ejecute `Get-HcsUpdateAvailability`. Debe recibir una notificación para avisarle de que hay actualizaciones disponibles.
   3. Ejecute `Start-HcsUpdate`. Puede ejecutar este comando en cualquier nodo. Las actualizaciones se aplicarán en el primer controlador de hello, controlador Hola conmutarán por error y, a continuación, hello las actualizaciones se aplicarán en Hola otro controlador.
      
      Puede supervisar el progreso de Hola de actualización de hello ejecutando `Get-HcsUpdateStatus`.    
      
      Hello siguiente salida de ejemplo muestra hello actualización en curso.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      Después de la salida de ejemplo de Hola indica que la actualización Hola ha finalizado.
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      Esta operación puede tardar horas too11 Hola a tooapply todos hello las actualizaciones, incluidas las actualizaciones de Windows.
8. Ejecute hello siguiendo el portal de Microsoft Azure Government cmdlet toopoint Hola dispositivos toohello (porque señala toohello pública portal de Azure clásico de forma predeterminada). Ambos controladores se reiniciarán. Recomendamos que utilice dos sesiones PuTTY toosimultaneously conectar tooboth controladores para que puedan ver cuando se reinicia cada controlador.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Aparecerá un mensaje de confirmación. Acepte el predeterminado de hello (**Y**).
9. Ejecute hello después de la instalación de tooresume de cmdlet:
   
    `Invoke-HcsSetupWizard`
   
    ![Asistente para reanudar la instalación](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   Cuando se reanude el programa de instalación, el Asistente de hello serán la versión de Hola Update 2.
10. Acepte la configuración de red de Hola. Verá un mensaje de validación después de aceptar cada configuración.
11. Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira después de la primera sesión de Hola y deberá toochange TI ahora. Cuando se le solicite, proporcione una contraseña de administrador del dispositivo. Una contraseña de administrador del dispositivo válida debe tener entre 8 y 15 caracteres. Hello contraseña debe contener tres de hello siguientes: caracteres en minúsculas, mayúsculas, numéricos y especiales.
    
    <br/>![Registrar el dispositivo 5 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. paso final de Hello en el Asistente para la instalación de hello registra el dispositivo con hello el servicio StorSimple Manager. Para ello, necesita Hola clave de registro del servicio que obtuvo en [paso 2: clave de registro del servicio de Get hello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Una vez proporcionada la clave de registro de hello, deberá toowait de 2 a 3 minutos antes de registrar el dispositivo de Hola.
    
    > [!NOTE]
    > Puede presionar Ctrl + C en cualquier asistente para la instalación de tiempo tooexit Hola. Si ha especificado todas las configuraciones de red de hello (dirección IP de Data 0, máscara de subred y puerta de enlace), se conservarán las entradas.
    > 
    > 
    
    ![Progreso de registro de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Una vez registrado el dispositivo de hello, aparecerá una clave de cifrado de datos de servicio. Copie esta clave y guárdela en un lugar seguro, **Esta clave será necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello el servicio StorSimple Manager.** Consulte demasiado[seguridad de StorSimple](../articles/storsimple/storsimple-security.md) para obtener más información acerca de esta clave.
    
    ![Registrar el dispositivo 7 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > texto de hello toocopy desde la ventana de consola serie de hello, simplemente seleccione texto hello. A continuación, debe ser capaz de toopaste en el Portapapeles de Hola o cualquier editor de texto.
    > 
    > No use Ctrl + clave de cifrado de datos de servicio de C toocopy Hola. Con Ctrl + C hará que a se tooexit Hola Asistente para la instalación. Como resultado, no se cambiarán la contraseña de administrador de dispositivos de Hola y dispositivo Hola restablecerá la contraseña predeterminada de toohello.
    > 
    > 
14. Consola serie de Hola de salida.
15. Devolver toohello Portal de administración pública de Azure y completar Hola pasos:
    
    1. Haga doble clic en su hello tooaccess de servicio de administrador de StorSimple **inicio rápido** página.
    2. Haga clic en **Ver los dispositivos conectados**.
    3. En hello **dispositivos** página, compruebe que dicho dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de saludo. estado de dispositivo de Hello debe ser **Online**.
       
        ![Página de dispositivos de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        Si el estado del dispositivo de hello es **sin conexión**, espere unos minutos para hello toocome de dispositivo en línea.
       
        Si el dispositivo de hello sigue estando sin conexión después de unos minutos, deberá toomake seguro de que la red de firewall se ha configurado como se describe en [requisitos de red para el dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).
       
        Compruebe que el puerto 9354 esté abierto para comunicaciones de salida tal y como se utiliza por bus de servicio de hello para la comunicación de servicio al dispositivo de StorSimple Manager.

