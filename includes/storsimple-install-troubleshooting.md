<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Solución de errores en actualización
**¿Qué ocurre si verá una notificación que Hola comprobaciones previas a la actualización no se han podido?**

Si se produce un error en la comprobación previa, asegúrese de que se busca en la barra de notificación detallada de hello en parte inferior de Hola de página de Hola. Esto proporciona orientación como error en la comprobación previa toowhich. Hello en la ilustración siguiente se muestra una instancia en la que aparece este tipo de notificación. En este caso, comprobación de estado del controlador de Hola y comprobación de estado del componente de hardware no han podido. En hello **estado del Hardware** sección, puede ver que ambas **controlador 0** y **controlador 1** componentes necesitan atención.

  ![Error de comprobación previa](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Necesitará toomake seguro de que ambos controladores están en línea y en buen estado. También necesitará toomake seguro de que todos los componentes de hardware de hello de dispositivo de StorSimple de Hola se muestran toobe correcto en la página de mantenimiento de Hola. A continuación, puede probar las actualizaciones de tooinstall. Si no estás problemas de componentes de hardware de toofix capaz de hello, deberá toocontact Microsoft Support para los pasos siguientes.

**¿Qué ocurre si recibe un mensaje de error "No se pudo instalar actualizaciones" y Hola recomendación es toorefer toohello actualización guía toodetermine Hola causa del error de Hola de solución de problemas?**

Una causa probable podría ser que no tiene servidores de Microsoft Update toohello de conectividad. Se trata de una comprobación manual que necesita toobe realiza. Si pierde el servidor de actualización de toohello de conectividad, el trabajo de actualización produciría un error. Puede comprobar la conectividad de hello ejecutando Hola siguientes cmdlet de la interfaz de Windows PowerShell de hello de dispositivo de StorSimple:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Ejecute el cmdlet de hello en ambos controladores.

Si ha comprobado existe conectividad de Hola y continuar toosee este problema, póngase en contacto con Microsoft Support para los pasos siguientes.

**¿Qué ocurre si ve un error de actualización al actualizar su tooUpdate dispositivo 4 y ejecutan ambos controladores de hello actualización 4?**

Actualización 4 a partir de ambos controladores Hola están ejecutando Hola la misma versión del software y si hay un error de actualización, controladores de hello no entran en modo de recuperación. Esta situación puede ocurrir si hello revisiones de software de dispositivo (actualización de pedido 1) es los controladores de Hola de tooboth aplicado correctamente pero otras revisiones aún (2 º orden ni 3rd) se aplica toobe. Controladores de Hola a partir de Update 4, pasará al modo de recuperación solo si Hola dos controladores ejecutan diferentes versiones de software. 

Si el usuario de hello ve un error de actualización cuando ejecutan ambos controladores actualización 4, se recomienda que espere unos minutos y, a continuación, vuelva a intentar la actualización. Si el reintento de hello no funciona, debe ponerse en contacto con Microsoft Support.
