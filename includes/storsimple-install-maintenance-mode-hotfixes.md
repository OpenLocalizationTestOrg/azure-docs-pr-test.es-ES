<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall revisiones de modo de mantenimiento mediante Windows PowerShell para StorSimple
> [!IMPORTANT]
> En el modo de mantenimiento, primero es necesario tooapply Hola revisión en un controlador y, a continuación, en Hola otro controlador.
> 
> 

1. Coloque el dispositivo de hello en modo de mantenimiento. Vea [paso 2: modo de mantenimiento escriba](../articles/storsimple/storsimple-update-device.md#step2) para obtener instrucciones sobre cómo tooenter modo de mantenimiento.
2. revisión de hello tooapply, tipo:
   
     `Start-HcsHotfix` 
3. Cuando se le solicite, proporcione Hola ruta de acceso toohello carpeta compartida de red que contiene los archivos de revisión de Hola.
4. Se le pedirá confirmación. Tipo de **Y** tooproceed con la instalación de revisión de Hola.
5. Una vez aplicada Hola revisión en un controlador, toohello de inicio de sesión otro controlador. Aplique la revisión de Hola que hizo controlador anterior Hola.
6. Después de aplican las revisiones de hello, salga del modo de mantenimiento. Consulte [Paso 4: Salida del modo de mantenimiento](../articles/storsimple/storsimple-update-device.md#step4) para obtener instrucciones.

