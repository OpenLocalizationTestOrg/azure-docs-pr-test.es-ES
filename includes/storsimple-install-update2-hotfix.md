<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="9ab6c-101">revisiones de toodownload</span><span class="sxs-lookup"><span data-stu-id="9ab6c-101">toodownload hotfixes</span></span>
<span data-ttu-id="9ab6c-102">Realizar Hola tras la actualización de software de pasos toodownload Hola de Hola catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="9ab6c-103">Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9ab6c-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="9ab6c-104">Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="9ab6c-105">![Instalación del catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="9ab6c-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="9ab6c-106">En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de Hola que desee toodownload, por ejemplo **3121901**y, a continuación, haga clic en **búsqueda**.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="9ab6c-107">Hello revisión aparece listado, por ejemplo, **acumulativa 2.0 de actualización de agrupación de Software para StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="9ab6c-109">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-109">Click **Add**.</span></span> <span data-ttu-id="9ab6c-110">actualización de Hola se agrega toohello cesta.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="9ab6c-111">Busque las revisiones adicionales enumerados en la tabla Hola anterior (**3121900**, **3080728**, **3090322**, y **3121899**) y agregue cada uno en el caso de la cesta de compras de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-111">Search for any additional hotfixes listed in hello table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each hello basket.</span></span>
6. <span data-ttu-id="9ab6c-112">Haga clic en **Ver cesta**.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="9ab6c-113">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-113">Click **Download**.</span></span> <span data-ttu-id="9ab6c-114">Especifique o **examinar** tooa ubicación local donde desee Hola descarga tooappear.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="9ab6c-115">Hello las actualizaciones se descargan toohello ubicación especificada y se coloca en una subcarpeta con el mismo nombre como actualización de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="9ab6c-116">carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab6c-117">las revisiones de Hello deben ser accesibles desde ambos toodetect controladores los posible mensajes de error del controlador del mismo nivel de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="9ab6c-118">tooinstall y comprobar las revisiones de modo normal</span><span class="sxs-lookup"><span data-stu-id="9ab6c-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="9ab6c-119">Realizar Hola siguiendo los pasos tooinstall y comprobar las revisiones de modo normal.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="9ab6c-120">Si ha instalado ya usando Hola Portal de Azure, pase demasiado[instalar y comprobar las revisiones de modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="9ab6c-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="9ab6c-121">tooinstall Hola revisiones, interfaz de Windows PowerShell de Hola de acceso en la consola serie del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="9ab6c-122">Siga Hola detallada instrucciones [consola serie de uso PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="9ab6c-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="9ab6c-123">En el símbolo de hello, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="9ab6c-124">Seleccione **opción 1** toolog en toohello dispositivo con acceso completo.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="9ab6c-125">revisión de hello tooinstall, en hello símbolo, escriba:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="9ab6c-126">Use IP en lugar de DNS en ruta de acceso de recurso compartido en hello por encima del comando.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="9ab6c-127">parámetro de credencial de Hola se usa únicamente si tiene acceso a un recurso compartido de autenticado.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="9ab6c-128">Se recomienda que se utilizan recursos compartidos tooaccess de parámetro de credencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="9ab6c-129">Incluso los recursos compartidos que están abiertos demasiado "todos" suelen no abra toounauthenticated a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="9ab6c-130">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="9ab6c-131">Tipo de **Y** cuando tooconfirm solicitada Hola instalación de la revisión.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="9ab6c-132">Supervisar actualizaciones de hello mediante hello `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="9ab6c-133">Hello siguiente salida de ejemplo muestra hello actualización en curso.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="9ab6c-134">Hola `RunInprogress` será `True` cuando actualización Hola está en curso.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="9ab6c-135">Después de la salida de ejemplo de Hola indica que la actualización Hola ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="9ab6c-136">Hola `RunInProgress` será `False` cuando se complete la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9ab6c-137">En ocasiones, Hola cmdlet informes `False` cuando actualización Hola aún está en curso.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="9ab6c-138">tooensure que Hola revisión esté completa, espere unos minutos, vuelva a ejecutar este comando y compruebe que hello `RunInProgress` es `False`.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="9ab6c-139">Si es así, se completó la revisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-139">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="9ab6c-140">Después de software de hello actualización es completa, repita los pasos 3 a 5 tooinstall y monitor Hola agente SaaS y MDS.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-140">After hello software update is complete, repeat steps 3-5 tooinstall and monitor hello SaaS agent and MDS agent .</span></span> <span data-ttu-id="9ab6c-141">Asegúrese de que `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` se instala antes que `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="9ab6c-142">Compruebe que las versiones de software de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-142">Verify hello system software versions.</span></span> <span data-ttu-id="9ab6c-143">Escriba:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="9ab6c-144">Debería ver Hola siguientes versiones:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-144">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="9ab6c-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="9ab6c-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="9ab6c-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="9ab6c-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="9ab6c-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="9ab6c-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="9ab6c-148">Si los números de versión de hello no cambian después de aplicar la actualización de hello, indica que esa revisión Hola error tooapply.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="9ab6c-149">Si ve esto, póngase en contacto con [Soporte técnico de Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obtener más ayuda.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="9ab6c-150">Repita los pasos 3 a 5 tooinstall Hola restantes revisiones de modo normal.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-150">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="9ab6c-151">Hola controlador LSI - KB3121900</span><span class="sxs-lookup"><span data-stu-id="9ab6c-151">hello LSI driver - KB3121900</span></span>
   * <span data-ttu-id="9ab6c-152">Hola Storport update - KB3080728</span><span class="sxs-lookup"><span data-stu-id="9ab6c-152">hello Storport update - KB3080728</span></span>
   * <span data-ttu-id="9ab6c-153">Hola actualización Spaceport - KB3090322</span><span class="sxs-lookup"><span data-stu-id="9ab6c-153">hello Spaceport update - KB3090322</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="9ab6c-154">tooinstall y comprobar las revisiones de modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="9ab6c-154">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="9ab6c-155">Usar actualizaciones de firmware de disco de KB3121899 tooinstall.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-155">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="9ab6c-156">Estas son actualizaciones potencialmente perjudiciales y toman toocomplete aproximadamente 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-156">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="9ab6c-157">Puede elegir tooinstall en una ventana de mantenimiento planificado mediante la consola serie del dispositivo toohello conexión.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-157">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="9ab6c-158">Tenga en cuenta que si el firmware del disco ya está actualizado, no será necesario tooinstall estas actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-158">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="9ab6c-159">Ejecute hello `Get-HcsUpdateAvailability` cmdlet impide Hola dispositivo consola serie toocheck si las actualizaciones están disponibles y si Hola actualiza son perjudiciales (modo de mantenimiento) o no perjudiciales (modo normal) las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-159">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="9ab6c-160">las actualizaciones de firmware de disco de tooinstall hello, siga estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-160">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="9ab6c-161">Coloque el dispositivo Hola Hola en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-161">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="9ab6c-162">Tenga en cuenta que no debe usar comunicación remota de Windows PowerShell cuando se conecta el dispositivo de tooa en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-162">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="9ab6c-163">En su lugar, ejecute este cmdlet en el controlador de dispositivo de hello cuando se conecta a través de la consola serie del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-163">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="9ab6c-164">Escriba:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="9ab6c-165">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="9ab6c-166">A continuación, reinicie ambos controladores hello en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-166">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="9ab6c-167">actualización de firmware de disco de tooinstall hello, tipo:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-167">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="9ab6c-168">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="9ab6c-169">Progreso de instalación de Hola de monitor mediante `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-169">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="9ab6c-170">Hello actualización está completa cuando hello `RunInProgress` cambia demasiado`False`.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-170">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="9ab6c-171">Una vez completada la instalación de hello, reinicia el controlador de hello en qué Hola se ha instalado la revisión del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-171">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="9ab6c-172">Inicie sesión como opción 1 con acceso completo y comprobar la versión de firmware del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-172">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="9ab6c-173">Escriba:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="9ab6c-174">Hola espera versiones de firmware de disco son:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-174">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="9ab6c-175">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
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
   
    <span data-ttu-id="9ab6c-176">Ejecute hello `Get-HcsFirmwareVersion` comando hello segundo controlador tooverify que Hola versión del software se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-176">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="9ab6c-177">A continuación, puede salir del modo de mantenimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-177">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="9ab6c-178">toodo por lo tanto, escriba Hola siguiente comando para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9ab6c-178">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="9ab6c-179">controladores de Hello reiniciar al salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-179">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="9ab6c-180">Después de firmware del disco Hola correctamente se aplican las actualizaciones y dispositivo Hola ha salido del modo de mantenimiento, devuelto toohello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-180">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="9ab6c-181">Tenga en cuenta ese portal hello no es posible que muestre que instala actualizaciones de modo de mantenimiento de Hola durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9ab6c-181">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

