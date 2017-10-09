<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a>revisiones de toodownload
Realizar Hola tras la actualización de software de pasos toodownload Hola de Hola catálogo de Microsoft Update.

1. Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.
    ![Instalación del catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de Hola que desee toodownload, por ejemplo **3186843**y, a continuación, haga clic en **búsqueda**.
   
    Hello revisión aparece listado, por ejemplo, **acumulativa 3.0 de actualización de agrupación de Software para StorSimple 8000 Series**.
   
    ![Búsqueda de catálogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Haga clic en **Agregar**. actualización de Hola se agrega toohello cesta.
5. Busque las revisiones adicionales enumerados en la tabla Hola anterior (**3186859**) y agregue cada cesta toohello.
6. Haga clic en **Ver cesta**.
7. Haga clic en **Descargar**. Especifique o **examinar** tooa ubicación local donde desee Hola descarga tooappear. Hello las actualizaciones se descargan toohello ubicación especificada y se coloca en una subcarpeta con el mismo nombre como actualización de Hola de Hola. carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.

> [!NOTE]
> las revisiones de Hello deben ser accesibles desde ambos toodetect controladores los posible mensajes de error del controlador del mismo nivel de Hola.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall y comprobar las revisiones de modo normal
Realizar Hola siguiendo los pasos tooinstall y comprobar las revisiones de modo normal. Si ha instalado ya usando Hola Portal de Azure, pase demasiado[instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall Hola revisiones, interfaz de Windows PowerShell de Hola de acceso en la consola serie del dispositivo de StorSimple. Siga Hola detallada instrucciones [consola serie de uso PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). En el símbolo de hello, presione **ENTRAR**.
2. Seleccione **opción 1** toolog en toohello dispositivo con acceso completo. Se recomienda que instale Hola revisión en el controlador pasivo hello en primer lugar.
3. revisión de hello tooinstall, en hello símbolo, escriba:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Use IP en lugar de DNS en ruta de acceso de recurso compartido en hello por encima del comando. parámetro de credencial de Hola se usa únicamente si tiene acceso a un recurso compartido de autenticado.
   
    Se recomienda que se utilizan recursos compartidos tooaccess de parámetro de credencial de Hola. Incluso los recursos compartidos que están abiertos demasiado "todos" suelen no abra toounauthenticated a los usuarios.
   
    Fuente de alimentación Hola contraseña cuando se le solicite.
   
    A continuación se muestra una salida de ejemplo.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Tipo de **Y** cuando tooconfirm solicitada Hola instalación de la revisión.
5. Supervisar actualizaciones de hello mediante hello `Get-HcsUpdateStatus` cmdlet. actualización de Hola primero se completará en el controlador pasivo Hola. Una vez que se actualiza el controlador pasivo hello, habrá una conmutación por error y actualización de hello, a continuación, se aplicará en Hola otro controlador. actualización de Hello está completa cuando se actualizan ambos controladores Hola.
   
    Hello siguiente salida de ejemplo muestra hello actualización en curso. Hola `RunInprogress` será `True` cuando actualización Hola está en curso.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Después de la salida de ejemplo de Hola indica que la actualización Hola ha finalizado. Hola `RunInProgress` será `False` cuando se complete la actualización de Hola.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > En ocasiones, Hola cmdlet informes `False` cuando actualización Hola aún está en curso. tooensure que Hola revisión esté completa, espere unos minutos, vuelva a ejecutar este comando y compruebe que hello `RunInProgress` es `False`. Si es así, se completó la revisión de Hola.

1. Una vez completada la actualización de software de hello, compruebe que las versiones de software de sistema de Hola. Escriba:
   
    `Get-HcsSystem`
   
    Debería ver Hola siguientes versiones:
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     Si los números de versión de hello no cambian después de aplicar la actualización de hello, indica que esa revisión Hola error tooapply. Si ve esto, póngase en contacto con [Soporte técnico de Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obtener más ayuda.
     
     > [!IMPORTANT]
     > Debe reiniciar el controlador activo de Hola a través de hello `Restart-HcsController` cmdlet antes de aplicar Hola actualizaciones restantes. 
     > 
     > 
2. Repita los pasos 3 a 5 controlador de hello LSI tooinstall y revisión de firmware **KB3186859**. Después de instala la revisión de hello, usar hello `Get-HcsSystem` cmdlet. versión de Hola LSI debe ser:
   
   * `Lsisas2Version: 2.0.78.00`
3. Repita los pasos 3 a 5 tooinstall Hola Storport y actualización de Spaceport **KB3121261**.
4. Si está actualizando desde Update 2 o una versión anterior, también necesitará toodownload:
   
   * Corrección de iSCSI mediante KB3146621
   * Corrección de WMI mediante KB3103616

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall y comprobar las revisiones de modo de mantenimiento
Usar actualizaciones de firmware de disco de KB3121899 tooinstall. Estas son actualizaciones potencialmente perjudiciales y toman toocomplete aproximadamente 30 minutos. Puede elegir tooinstall en una ventana de mantenimiento planificado mediante la consola serie del dispositivo toohello conexión.

Tenga en cuenta que si el firmware del disco ya está actualizado, no será necesario tooinstall estas actualizaciones. Ejecute hello `Get-HcsUpdateAvailability` cmdlet impide Hola dispositivo consola serie toocheck si las actualizaciones están disponibles y si Hola actualiza son perjudiciales (modo de mantenimiento) o no perjudiciales (modo normal) las actualizaciones.

las actualizaciones de firmware de disco de tooinstall hello, siga estas instrucciones Hola.

1. Coloque el dispositivo Hola Hola en modo de mantenimiento. Tenga en cuenta que no debe usar comunicación remota de Windows PowerShell cuando se conecta el dispositivo de tooa en modo de mantenimiento. En su lugar, ejecute este cmdlet en el controlador de dispositivo de hello cuando se conecta a través de la consola serie del dispositivo de Hola. Escriba:
   
    `Enter-HcsMaintenanceMode`
   
    A continuación se muestra una salida de ejemplo.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Progreso de instalación de Hola de monitor mediante `Get-HcsUpdateStatus` comando. Hello actualización está completa cuando hello `RunInProgress` cambia demasiado`False`.
4. Una vez completada la instalación de hello, reinicia el controlador de hello en qué Hola se ha instalado la revisión del modo de mantenimiento. Inicie sesión como opción 1 con acceso completo y comprobar la versión de firmware del disco de Hola. Escriba:
   
   `Get-HcsFirmwareVersion`
   
   Hola espera versiones de firmware de disco son:
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   A continuación se muestra una salida de ejemplo.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    Ejecute hello `Get-HcsFirmwareVersion` comando hello segundo controlador tooverify que Hola versión del software se ha actualizado. A continuación, puede salir del modo de mantenimiento de Hola. toodo por lo tanto, escriba Hola siguiente comando para cada controlador de dispositivo:
   
   `Exit-HcsMaintenanceMode`
5. controladores de Hello reiniciar al salir del modo de mantenimiento. Después de firmware del disco Hola correctamente se aplican las actualizaciones y dispositivo Hola ha salido del modo de mantenimiento, devuelto toohello portal de Azure clásico. Tenga en cuenta ese portal hello no es posible que muestre que instala actualizaciones de modo de mantenimiento de Hola durante 24 horas.

