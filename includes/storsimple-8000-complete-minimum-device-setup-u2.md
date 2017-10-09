<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>instalación de dispositivo de StorSimple mínima de toocomplete Hola

   > [!NOTE]
   > No se puede cambiar el nombre del dispositivo de hello una vez completada la instalación mínima del dispositivo de Hola.
   
1. Desde la lista tabular de Hola de los dispositivos de hello **dispositivos** hoja, seleccione y haga clic en el dispositivo. Hola dispositivo está en un **listo tooset seguridad** estado. Hola **Configurar dispositivo** abrirá la hoja.

     ![Interfaces de red de la instalación mínima del dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. Hola **Configurar dispositivo** hoja:
   
   1. Proporcione un **nombre descriptivo** para el dispositivo. nombre de dispositivo predeterminado de Hello refleja información como el modelo de dispositivo de Hola y número de serie. Puede asignar un nombre descriptivo de la too64 caracteres toomanage el dispositivo.
   2. Conjunto hello **zona horaria** basadas en ubicación geográfica de hello en qué Hola se va a implementar el dispositivo. El dispositivo usa esta zona horaria para todas las operaciones programadas.
   3. En hello **DATA 0 configuración**:

       1. Los datos de muestra de interfaz de red como habilitado con hello de 0 de red configuradas (IP, subred, puerta de enlace) a través del Asistente para la instalación de Hola. DATOS 0 también se habilita automáticamente para la nube y para iSCSI.

       2. Proporcionan Hola fijos direcciones IP para el controlador 0 y 1. **direcciones IP fijas de controlador de Hello necesita el toobe que liberar direcciones IP de subred de hello accesible por dirección IP del dispositivo Hola.** Si hello DATA 0 interfaz está configurada para IPv4, hello corregido toobe de necesidad de direcciones IP proporcionada en hello formato IPv4. Si ha proporcionado un prefijo para la configuración IPv6, Hola direcciones IP fijas se rellenan automáticamente en estos campos.

            ![Interfaces de red de la instalación mínima del dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Hola direcciones IP para el controlador de hello fijas se usan para atender toohello dispositivo de hello las actualizaciones. Por lo tanto, Hola IP fija debe ser enrutables y deben poder tooconnect toohello Internet. Puede comprobar que el controlador fijo direcciones IP sean enrutables mediante el uso de hello [Test-HcsmConnection] [ Test] cmdlet. Hola siguiente ejemplo muestra fija del controlador direcciones IP es toohello enrutado Internet y puede tener acceso a Hola servidores de Microsoft Update.

            ![Test-HcsmConnection que muestra direcciones IP enrutables](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Haga clic en **Aceptar**. configuración de dispositivo de Hello comienza. Cuando se completa la configuración del dispositivo hello, se le notificará. Hola cambios de estado de dispositivo demasiado**en línea** en hello **dispositivos** hoja.

    ![Interfaces de red de la instalación mínima del dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
