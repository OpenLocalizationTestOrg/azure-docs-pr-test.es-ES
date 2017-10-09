#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="2c5d7-101">toostop e inicie una aplicación en la nube</span><span class="sxs-lookup"><span data-stu-id="2c5d7-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="2c5d7-102">toostop un dispositivo en la nube, vaya toohello máquina virtual para su dispositivo en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="2c5d7-103">![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="2c5d7-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="2c5d7-104">En la barra de comandos de hello, haga clic en **detener**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-104">From hello command bar, click **Stop**.</span></span>

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="2c5d7-106">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="2c5d7-108">Cuando detiene una máquina virtual, esta se desasigna.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="2c5d7-109">Mientras se está deteniendo el dispositivo de nube de hello, su estado es **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="2c5d7-110">Cuando se haya detenido el dispositivo de nube de hello, su estado es **detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="2c5d7-112">Una vez que se detiene una máquina virtual, haga clic en **iniciar** (botón esté disponible) toostart Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="2c5d7-113">Después de dispositivo de hello en la nube se ha iniciado, su estado es **iniciado**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="2c5d7-115">Usar hello después cmdlets toostop e iniciar una aplicación de nube.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="2c5d7-116">toorestart un dispositivo de nube</span><span class="sxs-lookup"><span data-stu-id="2c5d7-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="2c5d7-117">toorestart un dispositivo en la nube, vaya toohello máquina virtual para su dispositivo en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="2c5d7-118">En la barra de comandos de hello, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="2c5d7-119">Cuando se le pida, confirme Hola reinicio.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="2c5d7-120">Cuando esté listo para toouse aparato de nube de hello, su estado es **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Máquina virtual de StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="2c5d7-122">Usar hello siguiente cmdlet toorestart un dispositivo de nube.</span><span class="sxs-lookup"><span data-stu-id="2c5d7-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

