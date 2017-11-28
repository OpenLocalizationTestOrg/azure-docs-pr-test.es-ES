<!--author=alkohli last changed: 07/07/17-->

#### <a name="to-install-an-update-from-the-azure-portal"></a><span data-ttu-id="9fea2-101">Instalar una actualización desde el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9fea2-101">To install an update from the Azure portal</span></span>

1. <span data-ttu-id="9fea2-102">En la página de servicio de StorSimple, seleccione el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9fea2-102">On the StorSimple service page, select your device.</span></span>

    ![Selección del dispositivo](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="9fea2-104">Vaya a **Configuración del dispositivo** > **Actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="9fea2-104">Navigate to **Device settings** > **Device updates**.</span></span>

    ![Haga clic en Actualizaciones del dispositivo.](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="9fea2-106">Aparecerá una notificación si hay nuevas actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9fea2-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="9fea2-107">O bien, en la hoja **Actualizaciones del dispositivo**, haga clic en **Buscar actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fea2-107">Alternatively, in the **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="9fea2-108">Se crea un trabajo para buscar las actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9fea2-108">A job is created to scan for available updates.</span></span> <span data-ttu-id="9fea2-109">Se le notificará cuando el trabajo se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="9fea2-109">You are notified when the job completes successfully.</span></span>

    ![Haga clic en Actualizaciones del dispositivo.](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="9fea2-111">Se recomienda revisar las notas de la versión antes de aplicar una actualización en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9fea2-111">We recommend that you review the release notes before you apply an update on your device.</span></span> <span data-ttu-id="9fea2-112">Para aplicar las actualizaciones, haga clic en **Instalar actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fea2-112">To apply updates, click **Install updates**.</span></span> <span data-ttu-id="9fea2-113">En la hoja **Confirmar actualizaciones normales**, revise los requisitos previos que debe completar antes de aplicar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9fea2-113">In the **Confirm regular updates** blade, review the prerequisites to complete before you apply updates.</span></span> <span data-ttu-id="9fea2-114">Seleccione la casilla para indicar que está listo para actualizar el dispositivo y, a continuación, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="9fea2-114">Select the checkbox to indicate that you are ready to update the device and then click **Install**.</span></span>

    ![Haga clic en Actualizaciones del dispositivo.](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="9fea2-116">Ahora se inicia un conjunto de comprobaciones previas.</span><span class="sxs-lookup"><span data-stu-id="9fea2-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="9fea2-117">Estas comprobaciones incluyen:</span><span class="sxs-lookup"><span data-stu-id="9fea2-117">These checks include:</span></span>
   
   * <span data-ttu-id="9fea2-118">**Comprobaciones del estado del controlador** para comprobar que los controladores del dispositivo están en buen estado y en línea.</span><span class="sxs-lookup"><span data-stu-id="9fea2-118">**Controller health checks** to verify that both the device controllers are healthy and online.</span></span>
   * <span data-ttu-id="9fea2-119">**Comprobaciones de mantenimiento de componentes de hardware** para comprobar que todos los componentes de hardware del dispositivo StorSimple están en buen estado.</span><span class="sxs-lookup"><span data-stu-id="9fea2-119">**Hardware component health checks** to verify that all the hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="9fea2-120">**Comprobaciones de DATA 0** para comprobar DATA 0 está habilitado en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9fea2-120">**DATA 0 checks** to verify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="9fea2-121">Si la interfaz no está habilitada, tendrá que habilitarla y, después, volver a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="9fea2-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="9fea2-122">La actualización se descargará e instalará solo si todas las comprobaciones se completan correctamente.</span><span class="sxs-lookup"><span data-stu-id="9fea2-122">The update is downloaded and installed only if all the checks are successfully completed.</span></span> <span data-ttu-id="9fea2-123">Recibirá una notificación cuando las comprobaciones están en curso.</span><span class="sxs-lookup"><span data-stu-id="9fea2-123">You are notified when the checks are in progress.</span></span> <span data-ttu-id="9fea2-124">Si se produce un error en la comprobación previa, se le indicarán las causas del error.</span><span class="sxs-lookup"><span data-stu-id="9fea2-124">If the prechecks fail, then you will be provided with the reasons for failure.</span></span> <span data-ttu-id="9fea2-125">Resuelva estos problemas e intente realizar de nuevo la operación.</span><span class="sxs-lookup"><span data-stu-id="9fea2-125">Address those issues and then retry the operation.</span></span> <span data-ttu-id="9fea2-126">Puede que necesite ponerse en contacto con el soporte técnico de Microsoft si no puede resolver estos problemas por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="9fea2-126">You may need to contact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="9fea2-127">Una vez realizadas correctamente las comprobaciones previas, se crea un trabajo de actualización.</span><span class="sxs-lookup"><span data-stu-id="9fea2-127">After the prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="9fea2-128">Recibirá una notificación cuando el trabajo de actualización esté correctamente creado.</span><span class="sxs-lookup"><span data-stu-id="9fea2-128">You are notified when the update job is successfully created.</span></span>
   
    ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="9fea2-130">La actualización se aplica en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9fea2-130">The update is then applied on your device.</span></span>

9. <span data-ttu-id="9fea2-131">La actualización tarda unas horas en completarse.</span><span class="sxs-lookup"><span data-stu-id="9fea2-131">The update takes a few hours to complete.</span></span> <span data-ttu-id="9fea2-132">Seleccione el trabajo de actualización y haga clic en **Detalles** para ver los detalles del trabajo en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="9fea2-132">Select the update job and click **Details** to view the details of the job at any time.</span></span>

    ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="9fea2-134">También puede supervisar el progreso del trabajo de actualización desde **Configuración del dispositivo > Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="9fea2-134">You can also monitor the progress of the update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="9fea2-135">En la hoja **Trabajos**, puede ver el progreso de la actualización.</span><span class="sxs-lookup"><span data-stu-id="9fea2-135">On the **Jobs** blade, you can see the update progress.</span></span>

     ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="9fea2-137">Una vez completado el trabajo, vaya a **Configuración del dispositivo > Actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="9fea2-137">After the job is complete, navigate to the **Device settings > Device updates**.</span></span> <span data-ttu-id="9fea2-138">La versión del software ya debería estar actualizada.</span><span class="sxs-lookup"><span data-stu-id="9fea2-138">The software version should now be updated.</span></span>

    ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update9.png)

