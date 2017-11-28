<!--author=alkohli last changed: 01/18/17 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="537ed-101">Para instalar actualizaciones mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="537ed-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="537ed-102">Vaya a su Administrador de dispositivos de StorSimple y seleccione **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="537ed-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="537ed-103">En la lista de dispositivos conectados al servicio, seleccione y haga clic en el dispositivo que desea actualizar.</span><span class="sxs-lookup"><span data-stu-id="537ed-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate1m.png) 

2. <span data-ttu-id="537ed-105">En la hoja **Configuración**, haga clic en **Actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="537ed-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate2m.png)  

3. <span data-ttu-id="537ed-107">Verá un mensaje si hay actualizaciones de software disponibles.</span><span class="sxs-lookup"><span data-stu-id="537ed-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="537ed-108">Para buscar actualizaciones, también puede hacer clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="537ed-108">To check for updates, you can also click **Scan**.</span></span>

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate3m1.png)

    <span data-ttu-id="537ed-110">Se le notificará cuando se inicie el examen y se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="537ed-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate5m.png)

4. <span data-ttu-id="537ed-112">Una vez examinadas las actualizaciones, haga clic en **Descargar actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="537ed-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate6m.png)

5. <span data-ttu-id="537ed-114">En la hoja **Nuevas actualizaciones**, revise la información y, una vez descargadas las actualizaciones, debe confirmar la instalación.</span><span class="sxs-lookup"><span data-stu-id="537ed-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="537ed-115">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="537ed-115">Click **OK**.</span></span>

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate7m.png)

6. <span data-ttu-id="537ed-117">Se le notificará cuando se inicie la carga y se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="537ed-117">You are notified when the upload starts and completes successfully.</span></span>

     ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate8m.png)

5. <span data-ttu-id="537ed-119">En la hoja **Actualizaciones del dispositivo**, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="537ed-119">In the **Device updates** blade, click **Install**.</span></span>

     ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate11m1.png)   

6. <span data-ttu-id="537ed-121">En la hoja **Nuevas actualizaciones**, se le advertirá de que la actualización puede ser perjudicial.</span><span class="sxs-lookup"><span data-stu-id="537ed-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="537ed-122">Puesto que la matriz virtual es un dispositivo de un solo nodo, el dispositivo se reiniciará una vez actualizado.</span><span class="sxs-lookup"><span data-stu-id="537ed-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="537ed-123">Se interrumpirá cualquier E/S en curso.</span><span class="sxs-lookup"><span data-stu-id="537ed-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="537ed-124">Haga clic en **Aceptar** para instalar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="537ed-124">Click **OK** to install the updates.</span></span> 

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate12m.png) 

7. <span data-ttu-id="537ed-126">Se le notificará cuando se inicie el trabajo de instalación.</span><span class="sxs-lookup"><span data-stu-id="537ed-126">You are notified when the install job starts.</span></span> 

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate13m.png)

8.  <span data-ttu-id="537ed-128">Cuando el trabajo de instalación finalice correctamente, haga clic en el vínculo **Ver trabajo**, en la hoja **Actualizaciones del dispositivo**, para supervisar la instalación.</span><span class="sxs-lookup"><span data-stu-id="537ed-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate15m1.png)

    <span data-ttu-id="537ed-130">Esto le lleva a la hoja **Instalar actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="537ed-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="537ed-131">Puede ver información detallada sobre el trabajo aquí.</span><span class="sxs-lookup"><span data-stu-id="537ed-131">You can view detailed information about the job here.</span></span>

    ![actualizar dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate16m1.png)

9. <span data-ttu-id="537ed-133">Una vez instaladas correctamente las actualizaciones, verá un mensaje que lo indica en la hoja **Actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="537ed-133">After the updates are successfully installed, you see a message to this effect in the **Device updates** blade.</span></span> 