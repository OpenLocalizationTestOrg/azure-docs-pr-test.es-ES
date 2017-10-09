<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>actualizaciones del modo de mantenimiento tooinstall a través de Windows PowerShell para StorSimple
1. Si aún no lo ha hecho lo ha hecho, tener acceso a consola serie del dispositivo de Hola y seleccione la opción 1, **iniciar sesión con acceso completo**. 
2. Escriba la contraseña de Hola. es la contraseña predeterminada de Hello **Password1**.
3. En hello símbolo del sistema, escriba:
   
     `Get-HcsUpdateAvailability` 
4. Se le notificará si hay actualizaciones disponibles y si las actualizaciones de hello son perjudiciales o no perjudiciales. tooapply actualizaciones potencialmente perjudiciales, necesita tooput Hola dispositivo en modo de mantenimiento. Para obtener instrucciones al respecto, consulte [Paso 2: Acceso al modo de mantenimiento](../articles/storsimple/storsimple-update-device.md#step2).
5. Cuando el dispositivo está en modo de mantenimiento, en hello símbolo del sistema, escriba:`Start-HcsUpdate`
6. Se le pedirá confirmación. Después de confirmar las actualizaciones de hello, se instalará en el controlador de Hola que está accediendo actualmente. Después de instalar actualizaciones de hello, controlador de Hola se reiniciará. 
7. Supervisar el estado de Hola de actualizaciones. Escriba:
   
    `Get-HcsUpdateStatus`
   
    Si hello `RunInProgress` es `True`, actualización de hello aún está en curso. Si `RunInProgress` es `False`, indica que ha completado la actualización Hola.  
8. Cuando Hola actualización está instalada en el controlador actual de Hola y haya reiniciado, conectar toohello otro controlador y realizar los pasos del 1 al 6.
9. Una vez actualizados ambos controladores, salga del modo de mantenimiento. Consulte [Paso 4: Salida del modo de mantenimiento](../articles/storsimple/storsimple-update-device.md#step4) para obtener instrucciones.

