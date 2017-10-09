<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de hello tooconfigure y registro
1. Obtener acceso a la interfaz de Windows PowerShell de hello en la consola serie del dispositivo de StorSimple. Vea [consola serie del dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obtener instrucciones. **Ser exactamente procedimiento de hello toofollow seguro o no será capaz de tooaccess consola de Hola.**
2. En la sesión de Hola que se abre, presione Intro una vez tooget un símbolo del sistema. 
3. Es posible que toochoose solicitadas Hola idioma que le gustaría tener tooset en el dispositivo. Especifique el idioma de hello y, a continuación, presione ENTRAR. 
   
    ![Configurar y registrar el dispositivo 1 de StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. En el menú de consola serie de Hola que aparece, elija toolog opción 1 en con acceso completo. 
   
    ![Registrar el dispositivo 2 de StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Complete los pasos 5-12 de valores de configuración de red mínimos requeridos de hello tooconfigure para el dispositivo. **Estos pasos de configuración deben toobe realizada en el controlador activo de hello de dispositivo de Hola.** menú de la consola serie de Hello indica el estado de controlador de hello en el mensaje de pancarta Hola. Si no está conectado toohello controlador activo, desconéctese y, a continuación, conéctese toohello de controlador activo.
5. En el símbolo de hello, escriba su contraseña. es la contraseña predeterminada del dispositivo de Hello **Password1**.
6. Hola de tipo siguiente comando: `Invoke-HcsSetupWizard`. 
7. Un Asistente para la instalación aparecerán toohelp configurar configuración de red de hello de dispositivo de Hola. Fuente de alimentación Hola Hola siguiente información: 
   
   * Dirección IP de interfaz de red 0 datos Hola
   * Máscara de subred
   * Puerta de enlace
   * Dirección IP para el servidor DNS principal
     
        Tenga en cuenta que sistema hello es validar la configuración de red después de cada paso en el proceso de Hola.
     
     > [!NOTE]
     > Puede que tenga toowait durante unos minutos para la máscara de subred de Hola y Hola DNS configuración toobe aplicado. Si recibe un mensaje de error de "Comprobación de hello red conectividad tooData 0", compruebe la conexión de red física de hello en hello datos interfaz de red 0 de su controlador activo.
     > 
     > 
8. (Opcional) Configure el servidor proxy web. Aunque la configuración del proxy web es opcional, **tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí**. Para obtener más información, consulte demasiado[configurar el proxy web para el dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Configure un servidor NTP principal para el dispositivo. Se requieren servidores NTP, dado que el dispositivo debe sincronizar la hora para que pueda autenticarse con los proveedores de servicios en la nube. Asegúrese de que su red permite toopass de tráfico NTP desde su toohello de centro de datos Internet. Si esto no es posible, especifique un servidor NTP interno. 
10. Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira después de la primera sesión de Hola y deberá toochange TI ahora. Cuando se le solicite, proporcione una contraseña de administrador del dispositivo. Una contraseña de administrador del dispositivo válida debe tener entre 8 y 15 caracteres. Hello contraseña debe contener tres de hello siguientes: caracteres en minúsculas, mayúsculas, numéricos y especiales.
    
    <br/>![Registrar el dispositivo 5 de StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. paso final de Hello en el Asistente para la instalación de hello registra el dispositivo con hello el servicio StorSimple Manager. Para ello, necesitará la clave de registro del servicio Hola que obtuvo en el paso 2. Una vez proporcionada la clave de registro de hello, deberá toowait de 2 a 3 minutos antes de registrar el dispositivo de Hola.
    
    > [!NOTE]
    > Puede presionar Ctrl + C en cualquier asistente para la instalación de tiempo tooexit Hola. Si ha especificado todas las configuraciones de red de hello (dirección IP de Data 0, máscara de subred y puerta de enlace), se conservarán las entradas.
    > 
    > 
    
    ![Registrar el dispositivo 6 de StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Una vez registrado el dispositivo de hello, aparecerá una clave de cifrado de datos de servicio. Copie esta clave y guárdela en un lugar seguro, **Esta clave será necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello el servicio StorSimple Manager.** Consulte demasiado[seguridad de StorSimple](../articles/storsimple/storsimple-security.md) para obtener más información acerca de esta clave.
    
    ![Registrar el dispositivo 7 de StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > texto de hello toocopy desde la ventana de consola serie de hello, simplemente seleccione texto hello. A continuación, debe ser capaz de toopaste en el Portapapeles de Hola o cualquier editor de texto. No use Ctrl + clave de cifrado de datos de servicio de C toocopy Hola. Con Ctrl + C hará que a se tooexit Hola Asistente para la instalación. Como resultado, no se cambiarán la contraseña de administrador de dispositivos de Hola y dispositivo Hola restablecerá la contraseña predeterminada de toohello.
    > 
    > 
13. Consola serie de Hola de salida.
14. Devolver toohello portal de Azure clásico y complete Hola pasos:
    
    1. Haga doble clic en su hello tooaccess de servicio de administrador de StorSimple **inicio rápido** página.
    2. Haga clic en **Ver los dispositivos conectados**.
    3. En hello **dispositivos** página, compruebe que dicho dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de saludo. estado de dispositivo de Hello debe ser **Online**.
       
        ![Página de dispositivos de StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Si el estado del dispositivo de hello es **sin conexión**, espere unos minutos para hello toocome de dispositivo en línea. 
       
        Si el dispositivo de hello sigue estando sin conexión después de unos minutos, deberá toomake seguro de que la red de firewall se ha configurado como se describe en [requisitos de red para el dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Compruebe que el puerto 9354 esté abierto para comunicaciones de salida tal y como se utiliza por bus de servicio de hello para la comunicación de servicio al dispositivo de StorSimple Manager.

