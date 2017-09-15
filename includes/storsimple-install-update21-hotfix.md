<!--author=alkohli last changed: 05/19/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="88e22-101">Descargar revisiones</span><span class="sxs-lookup"><span data-stu-id="88e22-101">To download hotfixes</span></span>
<span data-ttu-id="88e22-102">Realice los pasos siguientes para descargar la actualización de software desde el catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="88e22-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="88e22-103">Inicie Internet Explorer y vaya a [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="88e22-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="88e22-104">Si esta es la primera vez que utiliza el Catálogo de Microsoft Update en este equipo, haga clic en **Instalar** cuando se le solicite que instale el complemento del Catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="88e22-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="88e22-105">![Instalación del catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="88e22-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="88e22-106">En el cuadro de búsqueda del Catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de la revisión que desee descargar (por ejemplo, **3179904**) y haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="88e22-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="88e22-107">Aparecerá la lista de revisiones; por ejemplo, la **actualización acumulativa 2.2 para la serie StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="88e22-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="88e22-109">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="88e22-109">Click **Add**.</span></span> <span data-ttu-id="88e22-110">La actualización se agrega a la cesta.</span><span class="sxs-lookup"><span data-stu-id="88e22-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="88e22-111">Busque cualesquiera otras revisiones que se enumeren en la tabla anterior (**3103616**, **3146621**) y agréguelas a la cesta.</span><span class="sxs-lookup"><span data-stu-id="88e22-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span></span>
6. <span data-ttu-id="88e22-112">Haga clic en **Ver cesta**.</span><span class="sxs-lookup"><span data-stu-id="88e22-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="88e22-113">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="88e22-113">Click **Download**.</span></span> <span data-ttu-id="88e22-114">Especifique o **busque** una ubicación local en la que quiera que aparezcan las descargas.</span><span class="sxs-lookup"><span data-stu-id="88e22-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="88e22-115">Las actualizaciones se descargan en la ubicación especificada y se colocan en una subcarpeta con el mismo nombre que la actualización.</span><span class="sxs-lookup"><span data-stu-id="88e22-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="88e22-116">La carpeta también se puede copiar en un recurso compartido de red que sea accesible desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88e22-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="88e22-117">Las revisiones deben ser accesibles desde ambos controladores para detectar los posibles mensajes de error desde el controlador del mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="88e22-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="88e22-118">Instalar y comprobar las revisiones de modo normal</span><span class="sxs-lookup"><span data-stu-id="88e22-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="88e22-119">Realice los pasos siguientes para instalar y comprobar las revisiones de modo normal.</span><span class="sxs-lookup"><span data-stu-id="88e22-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="88e22-120">Si ya las ha instalado a través del Portal de Azure, puede ir directamente a la sección [Instalar y comprobar las revisiones del modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="88e22-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="88e22-121">Para instalar las revisiones, acceda a la interfaz de Windows PowerShell en la consola serie del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="88e22-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="88e22-122">Siga las instrucciones detalladas de [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console) (Uso de PuTTy para conectarse a la consola serie).</span><span class="sxs-lookup"><span data-stu-id="88e22-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="88e22-123">En el símbolo del sistema, presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="88e22-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="88e22-124">Seleccione **Opción 1** para iniciar sesión en el dispositivo con acceso completo.</span><span class="sxs-lookup"><span data-stu-id="88e22-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="88e22-125">Se recomienda instalar primero la revisión en el controlador pasivo.</span><span class="sxs-lookup"><span data-stu-id="88e22-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="88e22-126">Para instalar la revisión, en el símbolo del sistema, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="88e22-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="88e22-127">Use IP en lugar de DNS en la ruta de acceso de recurso compartido en el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="88e22-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="88e22-128">El parámetro credential se usa únicamente si tiene acceso a un recurso compartido autenticado.</span><span class="sxs-lookup"><span data-stu-id="88e22-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="88e22-129">Se recomienda que use el parámetro de credencial para obtener acceso a los recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="88e22-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="88e22-130">Incluso los recursos compartidos que están abiertos para "todos" no suelen estar abiertos a los usuarios no autenticados.</span><span class="sxs-lookup"><span data-stu-id="88e22-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="88e22-131">Indique la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="88e22-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="88e22-132">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88e22-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="88e22-133">Escriba **Y** cuando se le solicite que confirme la instalación de la revisión.</span><span class="sxs-lookup"><span data-stu-id="88e22-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="88e22-134">Si instala Update 2.2, instale solo el archivo binario precedido por 'all-hcsmdssoftwareudpate'.</span><span class="sxs-lookup"><span data-stu-id="88e22-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="88e22-135">No instale la actualización del agente de Cis y de MDS precedida por all-cismdsagentupdatebundle.</span><span class="sxs-lookup"><span data-stu-id="88e22-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="88e22-136">De lo contrario, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="88e22-136">Failure to do so will result in an error.</span></span> 

5. <span data-ttu-id="88e22-137">Supervise la actualización mediante el cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="88e22-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="88e22-138">La actualización se completará en primer lugar en el controlador pasivo.</span><span class="sxs-lookup"><span data-stu-id="88e22-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="88e22-139">Una vez actualizado el controlador pasivo, se producirá una conmutación por error, tras lo cual la actualización se aplicará en el otro controlador.</span><span class="sxs-lookup"><span data-stu-id="88e22-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="88e22-140">La actualización estará completa cuando ambos controladores se hayan actualizado.</span><span class="sxs-lookup"><span data-stu-id="88e22-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="88e22-141">La siguiente salida de ejemplo muestra la actualización en curso.</span><span class="sxs-lookup"><span data-stu-id="88e22-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="88e22-142">`RunInprogress` será `True` cuando la actualización esté en curso.</span><span class="sxs-lookup"><span data-stu-id="88e22-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="88e22-143">La siguiente salida de ejemplo indica que ha finalizado la actualización.</span><span class="sxs-lookup"><span data-stu-id="88e22-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="88e22-144">`RunInProgress` será `False` cuando se haya completado la actualización.</span><span class="sxs-lookup"><span data-stu-id="88e22-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="88e22-145">En ocasiones, el cmdlet notifica `False` cuando la actualización está todavía en curso.</span><span class="sxs-lookup"><span data-stu-id="88e22-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="88e22-146">Para garantizar que la revisión está completada, espere unos minutos, vuelva a ejecutar este comando y compruebe que `RunInProgress` es `False`.</span><span class="sxs-lookup"><span data-stu-id="88e22-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="88e22-147">Si es así, se habrá completado la revisión.</span><span class="sxs-lookup"><span data-stu-id="88e22-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="88e22-148">Cuando se complete la actualización del software, compruebe las versiones de software del sistema.</span><span class="sxs-lookup"><span data-stu-id="88e22-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="88e22-149">Escriba:</span><span class="sxs-lookup"><span data-stu-id="88e22-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="88e22-150">Verá las versiones siguientes:</span><span class="sxs-lookup"><span data-stu-id="88e22-150">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="88e22-151">Si los números de versión no cambian después de aplicar la actualización, indica que la revisión no se ha podido aplicar.</span><span class="sxs-lookup"><span data-stu-id="88e22-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="88e22-152">Si ve esto, póngase en contacto con [Soporte técnico de Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obtener más ayuda.</span><span class="sxs-lookup"><span data-stu-id="88e22-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="88e22-153">Antes de aplicar el resto de actualizaciones, debe reiniciar el controlador activo a través del cmdlet `Restart-HcsController`.</span><span class="sxs-lookup"><span data-stu-id="88e22-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="88e22-154">Repita los pasos 3 a 5 para instalar las revisiones en modo normal restantes.</span><span class="sxs-lookup"><span data-stu-id="88e22-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="88e22-155">Actualización de iSCSI (KB3146621)</span><span class="sxs-lookup"><span data-stu-id="88e22-155">The iSCSI update KB3146621</span></span>
   * <span data-ttu-id="88e22-156">Actualización de WMI (KB3103616)</span><span class="sxs-lookup"><span data-stu-id="88e22-156">The WMI update KB3103616</span></span>
3. <span data-ttu-id="88e22-157">Omita este paso si está actualizando desde la actualización 2.</span><span class="sxs-lookup"><span data-stu-id="88e22-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="88e22-158">Si está actualizando desde una versión anterior a la actualización 2, tendrá que descargar también lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="88e22-158">If you are updating from a version prior to Update 2, you will also need to download:</span></span>

    - <span data-ttu-id="88e22-159">Controlador LSI (KB3121900)</span><span class="sxs-lookup"><span data-stu-id="88e22-159">The LSI driver KB3121900</span></span>

    - <span data-ttu-id="88e22-160">Actualización de Spaceport (KB3090322)</span><span class="sxs-lookup"><span data-stu-id="88e22-160">The Spaceport update KB3090322</span></span>

    - <span data-ttu-id="88e22-161">Actualización de Storport (KB3080728)</span><span class="sxs-lookup"><span data-stu-id="88e22-161">The Storport update KB3080728</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="88e22-162">Instalar y comprobar las revisiones del modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="88e22-162">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="88e22-163">Use KB3121899 para instalar las actualizaciones de firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="88e22-163">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="88e22-164">Se trata de actualizaciones potencialmente perjudiciales y tardan unos 30 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="88e22-164">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="88e22-165">Puede elegir instalarlas en una ventana de mantenimiento planificado mediante la conexión a la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88e22-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="88e22-166">Tenga en cuenta que, si el firmware del disco ya está actualizado, no será necesario instalar estas actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="88e22-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="88e22-167">Ejecute el cmdlet `Get-HcsUpdateAvailability` desde la consola serie del dispositivo para ver si hay actualizaciones disponibles y si provocan interrupciones (modo de mantenimiento) o no (modo normal).</span><span class="sxs-lookup"><span data-stu-id="88e22-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="88e22-168">Para instalar las actualizaciones de firmware de disco, siga las instrucciones a continuación.</span><span class="sxs-lookup"><span data-stu-id="88e22-168">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="88e22-169">Active el modo de mantenimiento del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88e22-169">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="88e22-170">Tenga en cuenta que no debe usar la conexión remota de Windows PowerShell al conectarse a un dispositivo en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="88e22-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="88e22-171">En su lugar, ejecute este cmdlet en el controlador del dispositivo cuando esté conectado a través de la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88e22-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="88e22-172">Escriba:</span><span class="sxs-lookup"><span data-stu-id="88e22-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="88e22-173">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88e22-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="88e22-174">A continuación, se reiniciarán ambos controladores en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="88e22-174">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="88e22-175">Para instalar la actualización de firmware del disco, escriba:</span><span class="sxs-lookup"><span data-stu-id="88e22-175">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="88e22-176">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88e22-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="88e22-177">Supervise el progreso de la instalación con el comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="88e22-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="88e22-178">La actualización se habrá completado cuando `RunInProgress` cambie a `False`.</span><span class="sxs-lookup"><span data-stu-id="88e22-178">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="88e22-179">Una vez completada la instalación, se reiniciará el controlador en el que se haya instalado la revisión de modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="88e22-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="88e22-180">Inicie sesión como en la opción 1 con acceso completo y compruebe la versión de firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="88e22-180">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="88e22-181">Escriba:</span><span class="sxs-lookup"><span data-stu-id="88e22-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="88e22-182">Las versiones de firmware del disco esperadas son:</span><span class="sxs-lookup"><span data-stu-id="88e22-182">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="88e22-183">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88e22-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="88e22-184">Ejecute el comando `Get-HcsFirmwareVersion` en el segundo controlador para comprobar que se actualizó la versión de software.</span><span class="sxs-lookup"><span data-stu-id="88e22-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="88e22-185">A continuación, puede salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="88e22-185">You can then exit the maintenance mode.</span></span> <span data-ttu-id="88e22-186">Para ello, escriba el comando siguiente para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="88e22-186">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="88e22-187">Los controladores se reiniciarán al salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="88e22-187">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="88e22-188">Cuando las actualizaciones de firmware de disco se apliquen correctamente y el dispositivo haya salido del modo de mantenimiento, regrese al Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="88e22-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="88e22-189">Tenga en cuenta que, durante 24 horas, es posible que no aparezca en el portal la instalación de las actualizaciones en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="88e22-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

