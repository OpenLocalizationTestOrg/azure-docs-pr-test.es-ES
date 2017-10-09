<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="e33a0-101">tootake una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="e33a0-101">tootake a backup</span></span>

1. <span data-ttu-id="e33a0-102">Servicio de administrador de dispositivos de StorSimple de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="e33a0-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e33a0-103">En la lista tabular de Hola de dispositivos, seleccione y haga clic en el dispositivo y, a continuación, haga clic en **toda la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="e33a0-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="e33a0-104">Hola **configuración** hoja, vaya demasiado**configuración > Administrar > directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e33a0-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="e33a0-106">Hola **directiva de copia de seguridad** hoja, haga clic en **+ Agregar directiva**.</span><span class="sxs-lookup"><span data-stu-id="e33a0-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="e33a0-108">Hola **Crear directiva de copia de seguridad** hoja, un nombre que contenga entre 3 y 150 caracteres de la directiva de copia de seguridad de alimentación.</span><span class="sxs-lookup"><span data-stu-id="e33a0-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="e33a0-109">Seleccione Hola volúmenes toobe copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e33a0-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="e33a0-110">Si selecciona más de un volumen, estos volúmenes están agrupado toocreate conjuntamente una copia de seguridad coherente tras bloqueo.</span><span class="sxs-lookup"><span data-stu-id="e33a0-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="e33a0-112">En la hoja **Agregar la primera programación**:</span><span class="sxs-lookup"><span data-stu-id="e33a0-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="e33a0-113">Seleccione el tipo de saludo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e33a0-113">Select hello type of backup.</span></span> <span data-ttu-id="e33a0-114">Para restauraciones más rápidas, seleccione instantánea **local**.</span><span class="sxs-lookup"><span data-stu-id="e33a0-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="e33a0-115">Para lograr resistencia de datos, seleccione instantánea **en la nube**.</span><span class="sxs-lookup"><span data-stu-id="e33a0-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="e33a0-116">Especifique la frecuencia de copia de seguridad de hello en minutos, horas, días o semanas.</span><span class="sxs-lookup"><span data-stu-id="e33a0-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="e33a0-117">Seleccione un tiempo de retención.</span><span class="sxs-lookup"><span data-stu-id="e33a0-117">Select a retention time.</span></span> <span data-ttu-id="e33a0-118">Opciones de retención de Hello dependen de la frecuencia de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e33a0-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="e33a0-119">Por ejemplo, para una directiva diaria, retención de hello puede especificarse en semanas, mientras que la retención de una directiva mensual es en meses.</span><span class="sxs-lookup"><span data-stu-id="e33a0-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="e33a0-120">Seleccione Hola a partir de fecha y hora para la directiva de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e33a0-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="e33a0-121">Haga clic en **Aceptar** directiva de copia de seguridad de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="e33a0-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="e33a0-123">Haga clic en **crear** creación de directiva de copia de seguridad de toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="e33a0-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="e33a0-124">Se le notificará cuando la directiva de copia de seguridad de Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="e33a0-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="e33a0-125">También se actualiza la lista de Hola de directivas de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e33a0-125">hello list of backup policies is also updated.</span></span>
      
      ![Agregar directiva de copia de seguridad](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="e33a0-127">Ahora dispone de una directiva de copia de seguridad que creará copias de seguridad programadas de los datos del volumen.</span><span class="sxs-lookup"><span data-stu-id="e33a0-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




