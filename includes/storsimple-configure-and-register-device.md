<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de hello tooconfigure y registro
1. Obtener acceso a la interfaz de Windows PowerShell de hello en la consola serie del dispositivo de StorSimple. Vea [consola serie del dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obtener instrucciones. **Ser exactamente procedimiento de hello toofollow seguro o no será capaz de tooaccess consola de Hola.**
2. En la sesión de Hola que se abre, presione Intro una vez tooget un símbolo del sistema. 
3. Es posible que toochoose solicitadas Hola idioma que le gustaría tener tooset en el dispositivo. Especifique el idioma de hello y, a continuación, presione ENTRAR. 
   
    ![Configurar y registrar el dispositivo 1 de StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. En el menú de consola serie de Hola que aparece, elija toolog opción 1 en con acceso completo. 
   
    ![Registrar el dispositivo 2 de StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Complete los pasos 5-12 de valores de configuración de red mínimos requeridos de hello tooconfigure para el dispositivo. **Estos pasos de configuración deben toobe realizada en el controlador activo de hello de dispositivo de Hola.** menú de la consola serie de Hello indica el estado de controlador de hello en el mensaje de pancarta Hola. Si no está conectado toohello controlador activo, desconéctese y, a continuación, conéctese toohello de controlador activo.
5. En el símbolo de hello, escriba su contraseña. es la contraseña predeterminada del dispositivo de Hello **Password1**.
6. Escriba el siguiente comando de hello:
   
     `Invoke-HcsSetupWizard` 
7. Un Asistente para la instalación aparecerán toohelp configurar configuración de red de hello de dispositivo de Hola. Fuente de alimentación Hola Hola siguiente información: 
   
   * Dirección IP de interfaz de red 0 datos Hola
   * Máscara de subred
   * Puerta de enlace
   * Dirección IP para el servidor DNS principal
   * Dirección IP para el servidor NTP principal
     
     > [!NOTE]
     > Puede que tenga toowait durante unos minutos para la máscara de subred de Hola y Hola DNS configuración toobe aplicado. Si se produce un "hello dispositivo no está listo." mensaje de error, comprobación de conexión de red física de hello en hello datos interfaz de red 0 de su controlador activo.
     > 
     > 
8. (Opcional) Configure el servidor proxy web. Aunque la configuración del proxy web es opcional, **tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí**. Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). Si experimenta problemas durante este paso, consulte instrucciones de tootroubleshooting para [errores durante la configuración del proxy web](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > Puede presionar Ctrl + C en cualquier asistente para la instalación de tiempo tooexit Hola. Se conservarán todos los valores de configuración que aplicó antes de emitir este comando.

1. Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira después de la primera sesión de Hola y deberá toochange para las sesiones posteriores. Cuando se le solicite, proporcione una contraseña de administrador del dispositivo. Una contraseña de administrador del dispositivo válida debe tener entre 8 y 15 caracteres. contraseña de Hello debe contener una combinación de caracteres en minúsculas, caracteres en mayúsculas, números y caracteres especiales.
2. También se establece la contraseña de administrador de instantáneas StorSimple Hola aquí. Use esta contraseña para autenticar un dispositivo con el host de Windows que ejecuta StorSimple Snapshot Manager. Cuando se le solicite, proporcione una contraseña de carácter 14 too15. Hello contraseña debe contener una combinación de tres de hello siguientes: caracteres en minúsculas, mayúsculas, numéricos y especiales. 
   
   ![Registrar el dispositivo 4 de StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Puede restablecer la contraseña de administrador de instantáneas StorSimple Hola de interfaz de servicio de administrador de StorSimple de Hola. Para obtener instrucciones detalladas, vaya demasiado[cambiar contraseñas de StorSimple de hello mediante Hola servicio StorSimple Manager](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot problemas durante este paso, consulte instrucciones de tootroubleshooting para [errores relacionados con toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. paso final de Hello en el Asistente para la instalación de hello registra el dispositivo con hello el servicio StorSimple Manager. Para ello, necesitará la clave de registro del servicio Hola que obtuvo en el paso 2. Una vez proporcionada la clave de registro de hello, deberá toowait de 2 a 3 minutos antes de registrar el dispositivo de Hola.
   
   tootroubleshoot cualquier error de registro de los dispositivos posibles, consulte demasiado[errores durante el registro de dispositivo](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Para obtener la solución de problemas, también puede hacer referencia demasiado[ejemplo paso a paso de solución de problemas](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Una vez registrado el dispositivo de hello, aparecerá una clave de cifrado de datos de servicio. Copie esta clave y guárdela en un lugar seguro,
   
   > [!WARNING]
   > Esta clave será necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello el servicio StorSimple Manager. Consulte demasiado[seguridad de StorSimple](../articles/storsimple/storsimple-security.md) para obtener más información acerca de esta clave.
   > 
   > 
   
    ![Registrar el dispositivo 6 de StorSimple](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    texto de hello toocopy desde la ventana de consola serie de hello, simplemente seleccione texto hello. A continuación, debe ser capaz de toopaste en el Portapapeles de Hola o cualquier editor de texto. No use Ctrl + clave de cifrado de datos de servicio de C toocopy Hola. Con Ctrl + C hará que a se tooexit Hola Asistente para la instalación. Como resultado, no se cambiarán contraseña de administrador de dispositivos de Hola y la contraseña de administrador de instantáneas StorSimple hello y dispositivo Hola volverá toohello contraseñas de forma predeterminada.
5. Consola serie de Hola de salida.
6. Devolver toohello portal de Azure clásico y complete Hola pasos:
   
   1. Haga doble clic en su hello tooaccess de servicio de administrador de StorSimple **inicio rápido** página.
   2. Haga clic en **Ver los dispositivos conectados**.
   3. En hello **dispositivos** página, compruebe que dicho dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de saludo. estado de dispositivo de Hello debe ser **Online**. Si el estado del dispositivo de hello es **sin conexión**, espere unos minutos para hello toocome de dispositivo en línea.
   
   ![Página de dispositivos de StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Después de hello dispositivo está en línea, conecte los cables de red de Hola que tenía desconectado en principio Hola de este paso.
   > 
   > 

Después de dispositivo de Hola se ha registrado correctamente y no esté en línea, puede ejecutar hello `Test-HcsmConnection -Verbose` tooensure que Hola conectividad de red es correcto. Para hello detallados de uso de este cmdlet, vaya demasiado[referencia de cmdlet de Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Vídeo disponible](./media/storsimple-configure-and-register-device/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo tooconfigure y registrar el dispositivo a través de Windows PowerShell para StorSimple, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

