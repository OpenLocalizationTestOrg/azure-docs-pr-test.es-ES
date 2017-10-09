<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Paso 1: Autorizar una clave de cifrado de dispositivo toochange Hola servicio datos Hola portal de Azure clásico
Por lo general, Administrador de dispositivos de hello solicitará que Administrador de servicio de hello autorizar un claves de cifrado de datos del servicio de toochange de dispositivo. Administrador de servicios de Hello autorizará, a continuación, una clave de hello dispositivos toochange Hola.

Este paso se realiza en hello portal de Azure clásico. Administrador de servicios de Hello puede seleccionar un dispositivo en una lista de dispositivos de hello toobe elegible autorizado. dispositivo de Hello es, a continuación, el proceso de cambio de clave de cifrado de datos del servicio de toostart autorizados Hola.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>¿Los dispositivos que pueden autorizarse claves de cifrado de datos de servicio de toochange?
Un dispositivo debe cumplir Hola siguiendo criterios antes de cambios de clave de cifrado de datos de servicio de tooinitiate autorizados:

* dispositivo de Hello debe estar en línea toobe apto para la autorización de cambio de clave de cifrado de datos de servicio.
* Puede autorizar Hola mismo dispositivo nuevo después de 30 minutos si el cambio de la clave de hello no haya iniciado.
* Puede autorizar a un dispositivo distinto, siempre que no ha iniciado cambio de clave de hello hello de dispositivo autorizado anteriormente. Después de que se ha autorizado el nuevo dispositivo de hello, dispositivo antiguo de hello no puede iniciar el cambio de Hola.
* No se puede autorizar a un dispositivo mientras está en curso Hola sustitución de la clave de cifrado de datos del servicio de Hola.
* Puede autorizar a un dispositivo cuando algunos de los dispositivos de hello registrados con el servicio de Hola han sustituido el cifrado Hola mientras que otros no. En tales casos, los dispositivos aptos Hola son aquellos que han completado el cambio de clave de cifrado de datos de servicio de Hola Hola.

> [!NOTE]
> Hola portal de Azure clásico, StorSimple dispositivos virtuales no se muestran en la lista de Hola de dispositivos que pueden estar autorizado cambio de clave toostart Hola.
> 
> 

Realizar Hola siguiendo los pasos tooselect y autorice un dispositivo tooinitiate Hola servicio cambio cifrado de datos clave.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize una clave de hello de dispositivo toochange
1. En la página del panel de servicio de hello, haga clic en **cambiar clave de cifrado de datos de servicio**.
   
    ![Cambiar clave de cifrado del servicio](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. Hola **la clave de cifrado de datos del servicio de cambio** diálogo cuadro, seleccione y autorice un dispositivo tooinitiate Hola servicio cambio cifrado de datos clave. lista desplegable de Hello tiene todos los dispositivos aptos Hola que se pueden autorizar.
3. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Paso 2: Usar Windows PowerShell para el cambio clave del cifrado de datos de StorSimple tooinitiate Hola servicio
Este paso se realiza en hello Windows PowerShell para StorSimple interfaz en hello había autorizado dispositivo StorSimple.

> [!NOTE]
> Puede realizarse ninguna operación en hello portal de Azure clásico de su servicio StorSimple Manager hasta que se complete la sustitución de claves de Hola.
> 
> 

Si usas la interfaz de Windows PowerShell de hello dispositivo consola serie tooconnect toohello, realizar Hola pasos.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>cambiar la clave de cifrado de datos del servicio de tooinitiate Hola
1. Seleccione la opción 1 toolog en con acceso completo.
2. En hello símbolo del sistema, escriba:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Una vez Hola cmdlet se haya completado correctamente, obtendrá una nueva clave de cifrado de datos del servicio. Copie y guarde esta clave para usarla en el paso 3 de este proceso. Esta clave será usa tooupdate Hola todos los restantes dispositivos registrados con el servicio StorSimple Manager Hola.
   
   > [!NOTE]
   > Este proceso debe iniciarse en las cuatro horas siguientes a la autorización de un dispositivo de StorSimple.
   > 
   > 
   
   Esta nueva clave, a continuación, se envía toohello servicio toobe insertada tooall Hola los dispositivos que están registrados con el servicio de Hola. A continuación, aparecerá una alerta en panel de servicio de Hola. servicio de Hola se deshabilitará todas las operaciones de hello en los dispositivos de hello registrado y Administrador de dispositivos de hello deberá, a continuación, clave de cifrado de datos de servicio de tooupdate hello en hello otros dispositivos. Sin embargo, hello E/s (hosts que envían datos en la nube toohello) no se interrumpirán.
   
   Si tiene un único dispositivo registrado servicio tooyour, proceso de sustitución de hello ahora está completa y puede omitir el paso siguiente de Hola. Si tiene varios dispositivos registrados tooyour servicio, continúe toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Paso 3: Actualizar la clave de cifrado de datos de servicio de hello en otros dispositivos de StorSimple
Estos pasos deben realizarse en la interfaz de Windows PowerShell de hello del dispositivo StorSimple si tiene varios dispositivos registrados tooyour el servicio StorSimple Manager. clave de Hola que obtuvo en el paso 2: usar Windows PowerShell para el cambio clave del cifrado de datos de StorSimple tooinitiate Hola servicio debe ser usado tooupdate todos Hola restantes registrado con el servicio StorSimple Manager hello de dispositivo de StorSimple.

Realizar Hola siguiendo el cifrado de datos de servicio de pasos tooupdate hello en el dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>clave de cifrado de datos del servicio de tooupdate Hola
1. Usar Windows PowerShell para StorSimple tooconnect toohello consola. Seleccione la opción 1 toolog en con acceso completo.
2. En hello símbolo del sistema, escriba:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Proporcione la clave de cifrado de datos de servicio de Hola que obtuvo en [paso 2: usar Windows PowerShell para el cambio clave del cifrado de datos de StorSimple tooinitiate Hola servicio](#to-initiate-the-service-data-encryption-key-change).

