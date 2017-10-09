<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall revisiones normales mediante Windows PowerShell para StorSimple
1. Conecte la consola serie del dispositivo toohello. Para obtener más información, consulte [paso 1: conectar la consola serie toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. En el menú de consola serie de hello, seleccione la opción 1, **iniciar sesión con acceso completo**. Escriba la contraseña de Hola. es la contraseña predeterminada de Hello **Password1**.
3. En hello símbolo del sistema, escriba:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Este comando aplica solo tooregular las revisiones. Este comando se ejecuta en un solo controlador, pero se actualizarán ambos controladores.
    > Puede que observe una conmutación por error del controlador durante el proceso de actualización de hello; Sin embargo, Hola conmutación por error no afectará a la disponibilidad del sistema o la operación.

4. Cuando se le solicite, proporcione Hola ruta de acceso toohello carpeta compartida de red que contiene los archivos de revisión de Hola.
5. Se le pedirá confirmación. Tipo de **Y** tooproceed con la instalación de revisión de Hola.

