<!--author=SharS last changed: 06/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de hello tooconfigure y registro
1. Obtener acceso a la interfaz de Windows PowerShell de hello en la consola serie del dispositivo de StorSimple. Vea [consola serie del dispositivo Use PuTTY tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) para obtener instrucciones. **Ser exactamente procedimiento de hello toofollow seguro o no será capaz de tooaccess consola de Hola.**
2. En la sesión de Hola que se abre, presione **ENTRAR** una vez tooget un símbolo del sistema.
3. Es posible que toochoose solicitadas Hola idioma que le gustaría tener tooset en el dispositivo. Especificar el idioma de hello y, a continuación, presione **ENTRAR**.
   
    ![Configurar y registrar el dispositivo 1 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. En el menú de consola serie de Hola que aparece, elija toolog opción 1 en con acceso completo.
   
    ![Registrar el dispositivo 2 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Realizar Hola después de la configuración de red mínimos requeridos de pasos tooconfigure hello para el dispositivo.
   
   > [!IMPORTANT]
   > Estos pasos de configuración deben toobe realizada en el controlador activo de hello de dispositivo de Hola. menú de la consola serie de Hello indica el estado de controlador de hello en el mensaje de pancarta Hola. Si no se conectó toohello de controlador activo, desconéctese y, a continuación, conéctese controlador activo toohello.
   
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
    
   4. De manera opcional, configure el servidor proxy web.
      
      > [!IMPORTANT]
      > Aunque la configuración del proxy web es opcional, tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí. Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
     
6. Presione Ctrl + C Asistente para la instalación de tooexit Hola.
8. Ejecute hello siguiendo el portal de Microsoft Azure Government cmdlet toopoint Hola dispositivos toohello (porque señala toohello pública portal de Azure clásico de forma predeterminada). Ambos controladores se reiniciarán. Recomendamos que utilice dos sesiones PuTTY toosimultaneously conectar tooboth controladores para que puedan ver cuando se reinicia cada controlador.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Aparecerá un mensaje de confirmación. Acepte el predeterminado de hello (**Y**).
9. Ejecute hello después de la instalación de tooresume de cmdlet:
   
    `Invoke-HcsSetupWizard`
   
    ![Asistente para reanudar la instalación](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
10. Acepte la configuración de red de Hola. Verá un mensaje de validación después de aceptar cada configuración.
11. Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira después de la primera sesión de Hola y deberá toochange TI ahora. Cuando se le solicite, proporcione una contraseña de administrador del dispositivo. Una contraseña de administrador del dispositivo válida debe tener entre 8 y 15 caracteres. Hello contraseña debe contener tres de hello siguientes: caracteres en minúsculas, mayúsculas, numéricos y especiales.
    
    <br/>![Registrar el dispositivo 5 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. paso final de Hello en el Asistente para la instalación de hello registra el dispositivo con hello servicio Administrador de dispositivos de StorSimple. Para ello, necesita Hola clave de registro del servicio que obtuvo en [paso 2: clave de registro del servicio de Get hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Una vez proporcionada la clave de registro de hello, deberá toowait de 2 a 3 minutos antes de registrar el dispositivo de Hola.
    
    > [!NOTE]
    > Puede presionar Ctrl + C en cualquier asistente para la instalación de tiempo tooexit Hola. Si ha especificado todas las configuraciones de red de hello (dirección IP de Data 0, máscara de subred y puerta de enlace), se conservarán las entradas.
    
    ![Progreso de registro de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Una vez registrado el dispositivo de hello, aparecerá una clave de cifrado de datos de servicio. Copie esta clave y guárdela en un lugar seguro, **Esta clave es necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello servicio Administrador de dispositivos de StorSimple.** Consulte demasiado[seguridad de StorSimple](../articles/storsimple/storsimple-8000-security.md) para obtener más información acerca de esta clave.
    
    ![Registrar el dispositivo 7 de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)
    > [!IMPORTANT]
    > texto de hello toocopy desde la ventana de consola serie de hello, simplemente seleccione texto hello. A continuación, debe ser capaz de toopaste en el Portapapeles de Hola o cualquier editor de texto.
    > 
    > No utilice **Ctrl + C** clave de cifrado de datos del servicio de toocopy Hola. Usar **Ctrl + C** hará que Asistente para la instalación de tooexit Hola. Como resultado, no se cambiarán la contraseña de administrador de dispositivos de Hola y dispositivo Hola restablecerá la contraseña predeterminada de toohello.
    
14. Consola serie de Hola de salida.
15. Devolver toohello Portal de administración pública de Azure y completar Hola pasos:
    
    1. Servicio de administrador de dispositivos de StorSimple de tooyour go.
    2. Haga clic en **Dispositivos**. En la lista Hola de dispositivos, identifique el dispositivo de Hola que son ddeploying. Compruebe que dicho dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de Hola. estado de dispositivo de Hello debe ser **Online**.
            
        Si el estado del dispositivo de hello es **sin conexión**, espere unos minutos para hello toocome de dispositivo en línea.
       
        Si el dispositivo de hello sigue estando sin conexión después de unos minutos, deberá toomake seguro de que la red de firewall se ha configurado como se describe en [requisitos de red para el dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).
       
        Compruebe que el puerto 9354 esté abierto para comunicaciones de salida tal y como se utiliza por bus de servicio de hello para la comunicación de servicio al dispositivo de administrador de dispositivos de StorSimple.

