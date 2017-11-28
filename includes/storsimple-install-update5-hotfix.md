<!--author=alkohli last changed: 08/21/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="981f0-101">Descargar revisiones</span><span class="sxs-lookup"><span data-stu-id="981f0-101">To download hotfixes</span></span>

<span data-ttu-id="981f0-102">Realice los pasos siguientes para descargar la actualización de software desde el catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="981f0-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="981f0-103">Inicie Internet Explorer y vaya a [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="981f0-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="981f0-104">Si esta es la primera vez que utiliza el Catálogo de Microsoft Update en este equipo, haga clic en **Instalar** cuando se le solicite que instale el complemento del Catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="981f0-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Instalación del catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="981f0-106">En el cuadro de búsqueda del Catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de la revisión que desee descargar (por ejemplo, **4037264**) y haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="981f0-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="981f0-107">Aparece la lista de revisiones; por ejemplo, la **actualización acumulativa 5.0 para la serie StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="981f0-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="981f0-109">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="981f0-109">Click **Download**.</span></span> <span data-ttu-id="981f0-110">Especifique o **busque** una ubicación local en la que quiera que aparezcan las descargas.</span><span class="sxs-lookup"><span data-stu-id="981f0-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="981f0-111">Haga clic en los archivos que va a descargar en la ubicación y carpeta especificadas.</span><span class="sxs-lookup"><span data-stu-id="981f0-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="981f0-112">La carpeta también se puede copiar en un recurso compartido de red que sea accesible desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="981f0-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="981f0-113">Busque las revisiones adicionales que se enumeran en la tabla anterior (**4037266**) y descargue los archivos correspondientes a las carpetas específicas, como se muestra en dicha tabla.</span><span class="sxs-lookup"><span data-stu-id="981f0-113">Search for any additional hotfixes listed in the table above (**4037266**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="981f0-114">Las revisiones deben ser accesibles desde ambos controladores para detectar los posibles mensajes de error desde el controlador del mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="981f0-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="981f0-115">Las revisiones deben copiarse en tres carpetas separadas.</span><span class="sxs-lookup"><span data-stu-id="981f0-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="981f0-116">Por ejemplo, la actualización del software o Cis o agente MDS se puede copiar en la carpeta _FirstOrderUpdate_, las restantes actualizaciones que no provocan interrupciones se pueden copiar en la carpeta _SecondOrderUpdate_ y las actualizaciones del modo de mantenimiento en la carpeta _ThirdOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="981f0-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="981f0-117">Instalar y comprobar las revisiones de modo normal</span><span class="sxs-lookup"><span data-stu-id="981f0-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="981f0-118">Realice los pasos siguientes para instalar y comprobar las revisiones de modo normal.</span><span class="sxs-lookup"><span data-stu-id="981f0-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="981f0-119">Si ya las ha instalado a través de Azure Portal, puede ir directamente a la sección [Instalar y comprobar las revisiones del modo de mantenimiento](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="981f0-119">If you already installed them using the Azure portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="981f0-120">Para instalar las revisiones, acceda a la interfaz de Windows PowerShell en la consola serie del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="981f0-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="981f0-121">Siga las instrucciones detalladas de [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console) (Uso de PuTTy para conectarse a la consola serie).</span><span class="sxs-lookup"><span data-stu-id="981f0-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="981f0-122">En el símbolo del sistema, presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="981f0-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="981f0-123">Seleccione **Opción 1** para iniciar sesión en el dispositivo con acceso completo.</span><span class="sxs-lookup"><span data-stu-id="981f0-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="981f0-124">Se recomienda instalar primero la revisión en el controlador pasivo.</span><span class="sxs-lookup"><span data-stu-id="981f0-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="981f0-125">Para instalar la revisión, en el símbolo del sistema, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="981f0-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="981f0-126">Use IP en lugar de DNS en la ruta de acceso de recurso compartido en el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="981f0-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="981f0-127">El parámetro credential se usa únicamente si tiene acceso a un recurso compartido autenticado.</span><span class="sxs-lookup"><span data-stu-id="981f0-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="981f0-128">Se recomienda que use el parámetro de credencial para obtener acceso a los recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="981f0-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="981f0-129">Incluso los recursos compartidos que están abiertos para "todos" no suelen estar abiertos a los usuarios no autenticados.</span><span class="sxs-lookup"><span data-stu-id="981f0-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
4. <span data-ttu-id="981f0-130">Indique la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="981f0-130">Supply the password when prompted.</span></span> <span data-ttu-id="981f0-131">A continuación se muestra una salida de ejemplo para instalar las actualizaciones de primer orden.</span><span class="sxs-lookup"><span data-stu-id="981f0-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="981f0-132">Para la actualización de primer orden, es preciso que apunte al archivo concreto.</span><span class="sxs-lookup"><span data-stu-id="981f0-132">For the first order update, you need to point to the specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="981f0-133">Debe instalar primero _HcsSoftwareUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="981f0-133">You should install the _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="981f0-134">Una vez finalizada la instalación, instale _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="981f0-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="981f0-135">Escriba **Y** cuando se le solicite que confirme la instalación de la revisión.</span><span class="sxs-lookup"><span data-stu-id="981f0-135">Type **Y** when prompted to confirm the hotfix installation.</span></span>
6. <span data-ttu-id="981f0-136">Supervise la actualización mediante el cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="981f0-136">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="981f0-137">La actualización se completará en primer lugar en el controlador pasivo.</span><span class="sxs-lookup"><span data-stu-id="981f0-137">The update will first complete on the passive controller.</span></span> <span data-ttu-id="981f0-138">Una vez actualizado el controlador pasivo, se producirá una conmutación por error, tras lo cual la actualización se aplicará en el otro controlador.</span><span class="sxs-lookup"><span data-stu-id="981f0-138">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="981f0-139">La actualización estará completa cuando ambos controladores se hayan actualizado.</span><span class="sxs-lookup"><span data-stu-id="981f0-139">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="981f0-140">La siguiente salida de ejemplo muestra la actualización en curso.</span><span class="sxs-lookup"><span data-stu-id="981f0-140">The following sample output shows the update in progress.</span></span> <span data-ttu-id="981f0-141">`RunInprogress` es `True` cuando la actualización está en curso.</span><span class="sxs-lookup"><span data-stu-id="981f0-141">The `RunInprogress` is `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="981f0-142">La siguiente salida de ejemplo indica que ha finalizado la actualización.</span><span class="sxs-lookup"><span data-stu-id="981f0-142">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="981f0-143">`RunInProgress` es `False` cuando la actualización ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="981f0-143">The `RunInProgress` is `False` when the update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="981f0-144">En ocasiones, el cmdlet notifica `False` cuando la actualización está todavía en curso.</span><span class="sxs-lookup"><span data-stu-id="981f0-144">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="981f0-145">Para garantizar que la revisión está completada, espere unos minutos, vuelva a ejecutar este comando y compruebe que `RunInProgress` es `False`.</span><span class="sxs-lookup"><span data-stu-id="981f0-145">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="981f0-146">Si es así, se habrá completado la revisión.</span><span class="sxs-lookup"><span data-stu-id="981f0-146">If it is, then the hotfix has completed.</span></span>

7. <span data-ttu-id="981f0-147">Cuando se complete la actualización del software, compruebe las versiones de software del sistema.</span><span class="sxs-lookup"><span data-stu-id="981f0-147">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="981f0-148">Escriba:</span><span class="sxs-lookup"><span data-stu-id="981f0-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="981f0-149">Verá las versiones siguientes:</span><span class="sxs-lookup"><span data-stu-id="981f0-149">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="981f0-150">Si el número de versión no cambia después de aplicar la actualización, indica que la revisión no se ha podido aplicar.</span><span class="sxs-lookup"><span data-stu-id="981f0-150">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="981f0-151">Si ve esto, póngase en contacto con [Soporte técnico de Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) para obtener más ayuda.</span><span class="sxs-lookup"><span data-stu-id="981f0-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="981f0-152">Antes de aplicar la siguiente actualización, debe reiniciar el controlador activo a través del cmdlet `Restart-HcsController`.</span><span class="sxs-lookup"><span data-stu-id="981f0-152">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
8. <span data-ttu-id="981f0-153">Repita los pasos del 3 al 6 para instalar el agente _CisMDSAgentupdate.exe_ descargado en la carpeta _FirstOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="981f0-153">Repeat steps 3-6 to install the _CisMDSAgentupdate.exe_ agent downloaded to your _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="981f0-154">Repita los pasos del 3 al 6 para instalar las actualizaciones de segundo orden.</span><span class="sxs-lookup"><span data-stu-id="981f0-154">Repeat steps 3-6 to install the second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="981f0-155">Para las actualizaciones de segundo orden, se pueden instalar varias actualizaciones con solo ejecutar `Start-HcsHotfix cmdlet` y apuntar a la carpeta en que se encuentran las actualizaciones de segundo orden.</span><span class="sxs-lookup"><span data-stu-id="981f0-155">For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located.</span></span> <span data-ttu-id="981f0-156">El cmdlet ejecutará todas las actualizaciones disponibles en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="981f0-156">The cmdlet will execute all the updates available in the folder.</span></span> <span data-ttu-id="981f0-157">Si una actualización ya está instalada, la lógica de la actualización la detectará y no aplicará esa actualización.</span><span class="sxs-lookup"><span data-stu-id="981f0-157">If an update is already installed, the update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="981f0-158">Después de instalar las revisiones, use el cmdlet `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="981f0-158">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="981f0-159">Las versiones deben ser:</span><span class="sxs-lookup"><span data-stu-id="981f0-159">The versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="981f0-160">Instalar y comprobar las revisiones del modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="981f0-160">To install and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="981f0-161">Use KB4037263 para instalar las actualizaciones de firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="981f0-161">Use KB4037263 to install disk firmware updates.</span></span> <span data-ttu-id="981f0-162">Se trata de actualizaciones potencialmente perjudiciales y tardan unos 30 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="981f0-162">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="981f0-163">Puede elegir instalarlas en una ventana de mantenimiento planificado mediante la conexión a la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="981f0-163">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="981f0-164">Si el firmware del disco ya está actualizado, no será necesario instalar estas actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="981f0-164">If your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="981f0-165">Ejecute el cmdlet `Get-HcsUpdateAvailability` desde la consola serie del dispositivo para ver si hay actualizaciones disponibles y si provocan interrupciones (modo de mantenimiento) o no (modo normal).</span><span class="sxs-lookup"><span data-stu-id="981f0-165">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="981f0-166">Para instalar las actualizaciones de firmware de disco, siga las instrucciones a continuación.</span><span class="sxs-lookup"><span data-stu-id="981f0-166">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="981f0-167">Active el modo de mantenimiento del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="981f0-167">Place the device in the maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="981f0-168">No use la conexión remota de Windows PowerShell al conectarse a un dispositivo en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="981f0-168">Do not use Windows PowerShell remoting when connecting to a device in maintenance mode.</span></span> <span data-ttu-id="981f0-169">En su lugar, ejecute este cmdlet en el controlador del dispositivo cuando esté conectado a través de la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="981f0-169">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span>

    <span data-ttu-id="981f0-170">Para colocar el controlador en modo de mantenimiento, escriba:</span><span class="sxs-lookup"><span data-stu-id="981f0-170">To place the controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="981f0-171">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="981f0-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="981f0-172">A continuación, se reiniciarán ambos controladores en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="981f0-172">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="981f0-173">Para instalar la actualización de firmware del disco, escriba:</span><span class="sxs-lookup"><span data-stu-id="981f0-173">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="981f0-174">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="981f0-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="981f0-175">Supervise el progreso de la instalación con el comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="981f0-175">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="981f0-176">La actualización se habrá completado cuando `RunInProgress` cambie a `False`.</span><span class="sxs-lookup"><span data-stu-id="981f0-176">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="981f0-177">Una vez completada la instalación, se reiniciará el controlador en el que se haya instalado la revisión de modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="981f0-177">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="981f0-178">Inicie sesión como en la opción 1 con acceso completo y compruebe la versión de firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="981f0-178">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="981f0-179">Escriba:</span><span class="sxs-lookup"><span data-stu-id="981f0-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="981f0-180">Las versiones de firmware del disco esperadas son:</span><span class="sxs-lookup"><span data-stu-id="981f0-180">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="981f0-181">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="981f0-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="981f0-182">Ejecute el comando `Get-HcsFirmwareVersion` en el segundo controlador para comprobar que se actualizó la versión de software.</span><span class="sxs-lookup"><span data-stu-id="981f0-182">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="981f0-183">A continuación, puede salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="981f0-183">You can then exit the maintenance mode.</span></span> <span data-ttu-id="981f0-184">Para ello, escriba el comando siguiente para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="981f0-184">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="981f0-185">Los controladores se reiniciarán al salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="981f0-185">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="981f0-186">Cuando las actualizaciones de firmware de disco se apliquen correctamente y el dispositivo haya salido del modo de mantenimiento, regrese a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="981f0-186">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure portal.</span></span> <span data-ttu-id="981f0-187">Tenga en cuenta que, durante 24 horas, es posible que no aparezca en el portal la instalación de las actualizaciones en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="981f0-187">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

