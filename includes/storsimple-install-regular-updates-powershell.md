<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>tooinstall actualizaciones periódicas a través de Windows PowerShell para StorSimple
1. Abra la consola serie del dispositivo de Hola y seleccione la opción 1, **iniciar sesión con acceso completo**. Escriba la contraseña de Hola. es la contraseña predeterminada de Hello *Password1*. 
2. En hello símbolo del sistema, escriba:
   
     `Get-HcsUpdateAvailability`
   
    Se le notificará si hay actualizaciones disponibles y si las actualizaciones de hello son perjudiciales o no perjudiciales.
3. En hello símbolo del sistema, escriba:
   
     `Start-HcsUpdate`
   
    se iniciará el proceso de actualización de Hola.

> [!IMPORTANT]
> * Este comando aplica sólo tooregular actualizaciones. Este comando se ejecuta en un solo controlador, pero se actualizarán ambos controladores. 
> * Puede que observe una conmutación por error del controlador durante el proceso de actualización de hello; Sin embargo, Hola conmutación por error no afectará a la disponibilidad del sistema o la operación.
> 
> 

