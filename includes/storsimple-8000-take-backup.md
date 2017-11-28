<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="b456b-101">Para realizar una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b456b-101">To take a backup</span></span>

1. <span data-ttu-id="b456b-102">Vaya al servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="b456b-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="b456b-103">En la lista tabular de dispositivos, seleccione y haga clic en su dispositivo y después en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="b456b-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="b456b-104">En la hoja **Configuración**, vaya a **Configuración > Administrar > Directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b456b-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="b456b-106">En la hoja **Directiva de copia de seguridad**, haga clic en **+ Agregar directiva**.</span><span class="sxs-lookup"><span data-stu-id="b456b-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="b456b-108">En la hoja **Crear directiva de copia de seguridad** proporcione un nombre que tenga entre 3 y 150 caracteres para la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="b456b-109">Seleccione los volúmenes de los que se va a hacer la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="b456b-110">Si selecciona más de un volumen, estos volúmenes se agruparán para crear una copia de seguridad preparada para bloqueos.</span><span class="sxs-lookup"><span data-stu-id="b456b-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="b456b-112">En la hoja **Agregar la primera programación**:</span><span class="sxs-lookup"><span data-stu-id="b456b-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="b456b-113">Seleccione el tipo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-113">Select the type of backup.</span></span> <span data-ttu-id="b456b-114">Para restauraciones más rápidas, seleccione instantánea **local**.</span><span class="sxs-lookup"><span data-stu-id="b456b-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="b456b-115">Para lograr resistencia de datos, seleccione instantánea **en la nube**.</span><span class="sxs-lookup"><span data-stu-id="b456b-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="b456b-116">Especifique la frecuencia de copia de seguridad en minutos, horas, días o semanas.</span><span class="sxs-lookup"><span data-stu-id="b456b-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="b456b-117">Seleccione un tiempo de retención.</span><span class="sxs-lookup"><span data-stu-id="b456b-117">Select a retention time.</span></span> <span data-ttu-id="b456b-118">Las opciones de retención dependen de la frecuencia de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="b456b-119">Por ejemplo, para una directiva diaria, la retención puede especificarse en semanas, mientras que la retención de una directiva mensual es en meses.</span><span class="sxs-lookup"><span data-stu-id="b456b-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="b456b-120">Seleccione la fecha y hora de inicio para la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="b456b-121">Haga clic en **Aceptar** para crear la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-121">Click **OK** to create the backup policy.</span></span>

        ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="b456b-123">Haga clic en **Crear** para iniciar la creación de directivas de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="b456b-124">Recibirá una notificación cuando la directiva de copia de seguridad se haya creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b456b-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="b456b-125">También se actualiza la lista de directivas de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b456b-125">The list of backup policies is also updated.</span></span>
      
      ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="b456b-127">Ahora dispone de una directiva de copia de seguridad que creará copias de seguridad programadas de los datos del volumen.</span><span class="sxs-lookup"><span data-stu-id="b456b-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




