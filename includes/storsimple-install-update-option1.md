<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>revisiones de toodownload
Realizar Hola después de la actualización de software de pasos toodownload Hola.

1. Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.
    ![Instalación del catálogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de Hola que desee toodownload, por ejemplo **3063418**y, a continuación, haga clic en **búsqueda**.
4. Verá hello **actualización del dispositivo StorSimple actualización 1.2** agrupación. Haga clic en **Agregar**. actualización de Hola se agregarán toohello cesta.
5. Busque las revisiones adicionales enumerados en la tabla Hola anterior (**3043005** y **3063416**) y agregue cada cesta Hola.
6. Haga clic en **Ver cesta**.
   
    ![Ver cesta](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Haga clic en **Descargar**. Especifique o **examinar** tooa ubicación local donde desee Hola descarga tooappear. Hello las actualizaciones se descargan toohello ubicación especificada y se coloca en una subcarpeta con el mismo nombre como actualización de Hola de Hola. carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.

> [!NOTE]
> las revisiones de Hello deben ser accesibles desde ambos toodetect controladores los posible mensajes de error del controlador del mismo nivel de Hola.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall y comprobar las revisiones de modo normal
Realizar Hola siguiendo los pasos tooinstall y comprobar las revisiones de modo normal de Hola. Si ha instalado ya usando Hola Portal de Azure, pase demasiado[instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall Hola de actualización de software, interfaz de Windows PowerShell de Hola de acceso en la consola serie del dispositivo de StorSimple. Siga Hola detallada instrucciones [consola serie de uso PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). En el símbolo de hello, presione **ENTRAR**.
2. Seleccione **opción 1** toolog en toohello dispositivo con acceso completo.
3. paquete de actualización de saludo de la tooinstall en hello símbolo, escriba:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Use IP en lugar de DNS en ruta de acceso de recurso compartido en hello por encima del comando. parámetro de credencial de Hola se usa únicamente si tiene acceso a un recurso compartido de autenticado.
   
    Se recomienda que se utilizan recursos compartidos tooaccess de parámetro de credencial de Hola. Incluso los recursos compartidos que están abiertos demasiado "todos" suelen no abra toounauthenticated a los usuarios.
   
    A continuación se muestra una salida de ejemplo.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Tipo de **Y** cuando tooconfirm solicitada Hola instalación de la revisión.
5. Supervisar actualizaciones de hello mediante hello `Get-HcsUpdateStatus` cmdlet.
   
    Hello siguiente salida de ejemplo muestra hello actualización en curso. Hola `RunInprogress` será `True` cuando actualización Hola está en curso.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Después de la salida de ejemplo de Hola indica que la actualización Hola ha finalizado. Hola `RunInProgress` será `False` cuando se complete la actualización de Hola.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > En ocasiones, Hola cmdlet informes `False` cuando actualización Hola aún está en curso. tooensure que Hola revisión esté completa, espere unos minutos, vuelva a ejecutar este comando y compruebe que hello `RunInProgress` es `False`. Si es así, se completó la revisión de Hola.
   > 
   > 
6. Una vez completada la actualización de software de hello, compruebe que las versiones de software de sistema de Hola. Escriba el siguiente comando de hello:
   
    `Get-HcsSystem`
   
    Debería ver Hola siguientes versiones:
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Si los números de versión de hello no cambian después de aplicar la actualización de hello, indica que esa revisión Hola error tooapply. Si ve esto, póngase en contacto con [Soporte técnico de Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obtener más ayuda.
7. Repita los pasos 3 a 5 tooinstall Hola restantes revisiones de modo normal (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall y comprobar las revisiones de modo de mantenimiento
Usar actualizaciones de firmware de disco de KB3063416 tooinstall. Estas son actualizaciones potencialmente perjudiciales y tardar alrededor de 30 y 45 minutos toocomplete. Puede elegir tooinstall en una ventana de mantenimiento planificado mediante la consola serie del dispositivo toohello conexión.

las actualizaciones de firmware de disco de tooinstall hello, siga estas instrucciones Hola.

1. Coloque el dispositivo de hello en modo de mantenimiento. Tenga en cuenta que no debe usar comunicación remota de Windows PowerShell cuando se conecta el dispositivo de tooa en modo de mantenimiento. Este cmdlet en el controlador de dispositivo de hello cuando se conecta a través de la consola serie del dispositivo Hola necesitará toorun. Escriba:
   
    `Enter-HcsMaintenanceMode`
   
    A continuación se muestra una salida de ejemplo.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    A continuación, reinicie ambos controladores hello en modo de mantenimiento.
2. actualización de firmware de disco de tooinstall hello, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    A continuación se muestra una salida de ejemplo.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Progreso de instalación de Hola de monitor mediante `Get-HcsUpdateStatus` comando. Hello actualización está completa cuando hello `RunInProgress` cambia demasiado`False`.
4. Una vez completada la instalación de hello, se reiniciará el controlador de hello en el que se instaló revisiones de modo de mantenimiento de Hola. Inicie sesión como opción 1 con acceso completo y comprobar la versión de firmware del disco de Hola. Escriba:
   
   `Get-HcsFirmwareVersion`
   
   Hola espera versiones de firmware de disco son:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Ejecute hello `Get-HcsFirmwareVersion` comando hello segundo controlador tooverify que Hola versión del software se ha actualizado. A continuación, puede salir del modo de mantenimiento de Hola. Escriba el siguiente comando para cada controlador de dispositivo de hello:
   
   `Exit-HcsMaintenanceMode`
5. controladores de Hello reiniciar al salir del modo de mantenimiento. Después de firmware del disco Hola correctamente se aplican las actualizaciones y dispositivo Hola ha salido del modo de mantenimiento, devuelto toohello portal de Azure clásico. Tenga en cuenta ese portal hello no es posible que muestre que instala actualizaciones de modo de mantenimiento de Hola durante 24 horas.

