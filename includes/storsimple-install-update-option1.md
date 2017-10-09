<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="2b444-101">revisiones de toodownload</span><span class="sxs-lookup"><span data-stu-id="2b444-101">toodownload hotfixes</span></span>
<span data-ttu-id="2b444-102">Realizar Hola después de la actualización de software de pasos toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-102">Perform hello following steps toodownload hello software update.</span></span>

1. <span data-ttu-id="2b444-103">Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2b444-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="2b444-104">Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="2b444-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="2b444-105">![Instalación del catálogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="2b444-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="2b444-106">En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de Hola que desee toodownload, por ejemplo **3063418**y, a continuación, haga clic en **búsqueda**.</span><span class="sxs-lookup"><span data-stu-id="2b444-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="2b444-107">Verá hello **actualización del dispositivo StorSimple actualización 1.2** agrupación.</span><span class="sxs-lookup"><span data-stu-id="2b444-107">You will see hello **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="2b444-108">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2b444-108">Click **Add**.</span></span> <span data-ttu-id="2b444-109">actualización de Hola se agregarán toohello cesta.</span><span class="sxs-lookup"><span data-stu-id="2b444-109">hello update will be added toohello basket.</span></span>
5. <span data-ttu-id="2b444-110">Busque las revisiones adicionales enumerados en la tabla Hola anterior (**3043005** y **3063416**) y agregue cada cesta Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-110">Search for any additional hotfixes listed in hello table above (**3043005** and **3063416**), and add each hello basket.</span></span>
6. <span data-ttu-id="2b444-111">Haga clic en **Ver cesta**.</span><span class="sxs-lookup"><span data-stu-id="2b444-111">Click **View Basket**.</span></span>
   
    ![Ver cesta](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="2b444-113">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="2b444-113">Click **Download**.</span></span> <span data-ttu-id="2b444-114">Especifique o **examinar** tooa ubicación local donde desee Hola descarga tooappear.</span><span class="sxs-lookup"><span data-stu-id="2b444-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="2b444-115">Hello las actualizaciones se descargan toohello ubicación especificada y se coloca en una subcarpeta con el mismo nombre como actualización de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="2b444-116">carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="2b444-117">las revisiones de Hello deben ser accesibles desde ambos toodetect controladores los posible mensajes de error del controlador del mismo nivel de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="2b444-118">tooinstall y comprobar las revisiones de modo normal</span><span class="sxs-lookup"><span data-stu-id="2b444-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="2b444-119">Realizar Hola siguiendo los pasos tooinstall y comprobar las revisiones de modo normal de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-119">Perform hello following steps tooinstall and verify hello regular-mode hotfixes.</span></span> <span data-ttu-id="2b444-120">Si ha instalado ya usando Hola Portal de Azure, pase demasiado[instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="2b444-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="2b444-121">tooinstall Hola de actualización de software, interfaz de Windows PowerShell de Hola de acceso en la consola serie del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2b444-121">tooinstall hello software update, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="2b444-122">Siga Hola detallada instrucciones [consola serie de uso PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="2b444-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="2b444-123">En el símbolo de hello, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="2b444-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="2b444-124">Seleccione **opción 1** toolog en toohello dispositivo con acceso completo.</span><span class="sxs-lookup"><span data-stu-id="2b444-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="2b444-125">paquete de actualización de saludo de la tooinstall en hello símbolo, escriba:</span><span class="sxs-lookup"><span data-stu-id="2b444-125">tooinstall hello update package, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="2b444-126">Use IP en lugar de DNS en ruta de acceso de recurso compartido en hello por encima del comando.</span><span class="sxs-lookup"><span data-stu-id="2b444-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="2b444-127">parámetro de credencial de Hola se usa únicamente si tiene acceso a un recurso compartido de autenticado.</span><span class="sxs-lookup"><span data-stu-id="2b444-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="2b444-128">Se recomienda que se utilizan recursos compartidos tooaccess de parámetro de credencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="2b444-129">Incluso los recursos compartidos que están abiertos demasiado "todos" suelen no abra toounauthenticated a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="2b444-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="2b444-130">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2b444-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="2b444-131">Tipo de **Y** cuando tooconfirm solicitada Hola instalación de la revisión.</span><span class="sxs-lookup"><span data-stu-id="2b444-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="2b444-132">Supervisar actualizaciones de hello mediante hello `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2b444-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="2b444-133">Hello siguiente salida de ejemplo muestra hello actualización en curso.</span><span class="sxs-lookup"><span data-stu-id="2b444-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="2b444-134">Hola `RunInprogress` será `True` cuando actualización Hola está en curso.</span><span class="sxs-lookup"><span data-stu-id="2b444-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="2b444-135">Después de la salida de ejemplo de Hola indica que la actualización Hola ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="2b444-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="2b444-136">Hola `RunInProgress` será `False` cuando se complete la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="2b444-137">En ocasiones, Hola cmdlet informes `False` cuando actualización Hola aún está en curso.</span><span class="sxs-lookup"><span data-stu-id="2b444-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="2b444-138">tooensure que Hola revisión esté completa, espere unos minutos, vuelva a ejecutar este comando y compruebe que hello `RunInProgress` es `False`.</span><span class="sxs-lookup"><span data-stu-id="2b444-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="2b444-139">Si es así, se completó la revisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-139">If it is, then hello hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="2b444-140">Una vez completada la actualización de software de hello, compruebe que las versiones de software de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-140">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="2b444-141">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2b444-141">Type hello following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="2b444-142">Debería ver Hola siguientes versiones:</span><span class="sxs-lookup"><span data-stu-id="2b444-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="2b444-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="2b444-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="2b444-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="2b444-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="2b444-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="2b444-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="2b444-146">Si los números de versión de hello no cambian después de aplicar la actualización de hello, indica que esa revisión Hola error tooapply.</span><span class="sxs-lookup"><span data-stu-id="2b444-146">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="2b444-147">Si ve esto, póngase en contacto con [Soporte técnico de Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obtener más ayuda.</span><span class="sxs-lookup"><span data-stu-id="2b444-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="2b444-148">Repita los pasos 3 a 5 tooinstall Hola restantes revisiones de modo normal (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="2b444-148">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="2b444-149">tooinstall y comprobar las revisiones de modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="2b444-149">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="2b444-150">Usar actualizaciones de firmware de disco de KB3063416 tooinstall.</span><span class="sxs-lookup"><span data-stu-id="2b444-150">Use KB3063416 tooinstall disk firmware updates.</span></span> <span data-ttu-id="2b444-151">Estas son actualizaciones potencialmente perjudiciales y tardar alrededor de 30 y 45 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2b444-151">These are disruptive updates and take around 30-45 minutes toocomplete.</span></span> <span data-ttu-id="2b444-152">Puede elegir tooinstall en una ventana de mantenimiento planificado mediante la consola serie del dispositivo toohello conexión.</span><span class="sxs-lookup"><span data-stu-id="2b444-152">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="2b444-153">las actualizaciones de firmware de disco de tooinstall hello, siga estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-153">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="2b444-154">Coloque el dispositivo de hello en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="2b444-154">Place hello device in Maintenance mode.</span></span> <span data-ttu-id="2b444-155">Tenga en cuenta que no debe usar comunicación remota de Windows PowerShell cuando se conecta el dispositivo de tooa en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="2b444-155">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="2b444-156">Este cmdlet en el controlador de dispositivo de hello cuando se conecta a través de la consola serie del dispositivo Hola necesitará toorun.</span><span class="sxs-lookup"><span data-stu-id="2b444-156">You will need toorun this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="2b444-157">Escriba:</span><span class="sxs-lookup"><span data-stu-id="2b444-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="2b444-158">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2b444-158">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="2b444-159">A continuación, reinicie ambos controladores hello en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="2b444-159">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="2b444-160">actualización de firmware de disco de tooinstall hello, tipo:</span><span class="sxs-lookup"><span data-stu-id="2b444-160">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="2b444-161">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2b444-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="2b444-162">Progreso de instalación de Hola de monitor mediante `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="2b444-162">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="2b444-163">Hello actualización está completa cuando hello `RunInProgress` cambia demasiado`False`.</span><span class="sxs-lookup"><span data-stu-id="2b444-163">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="2b444-164">Una vez completada la instalación de hello, se reiniciará el controlador de hello en el que se instaló revisiones de modo de mantenimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-164">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="2b444-165">Inicie sesión como opción 1 con acceso completo y comprobar la versión de firmware del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-165">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="2b444-166">Escriba:</span><span class="sxs-lookup"><span data-stu-id="2b444-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="2b444-167">Hola espera versiones de firmware de disco son:</span><span class="sxs-lookup"><span data-stu-id="2b444-167">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="2b444-168">Ejecute hello `Get-HcsFirmwareVersion` comando hello segundo controlador tooverify que Hola versión del software se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="2b444-168">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="2b444-169">A continuación, puede salir del modo de mantenimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b444-169">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="2b444-170">Escriba el siguiente comando para cada controlador de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="2b444-170">Type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="2b444-171">controladores de Hello reiniciar al salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="2b444-171">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="2b444-172">Después de firmware del disco Hola correctamente se aplican las actualizaciones y dispositivo Hola ha salido del modo de mantenimiento, devuelto toohello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="2b444-172">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="2b444-173">Tenga en cuenta ese portal hello no es posible que muestre que instala actualizaciones de modo de mantenimiento de Hola durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="2b444-173">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

