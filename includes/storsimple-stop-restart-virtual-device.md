#### <a name="to-stop-and-start-a-virtual-device"></a><span data-ttu-id="78d55-101">Para detener e iniciar un dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="78d55-101">To stop and start a virtual device</span></span>
<span data-ttu-id="78d55-102">Para detener un dispositivo virtual, haga clic en su nombre y, a continuación, haga clic en **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="78d55-102">To stop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="78d55-103">Mientras se está cerrando el dispositivo virtual, su estado es **Deteniéndose**.</span><span class="sxs-lookup"><span data-stu-id="78d55-103">While the virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="78d55-104">Una vez detenido el dispositivo virtual, su estado es **Detenido**.</span><span class="sxs-lookup"><span data-stu-id="78d55-104">After the virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="78d55-105">Use los siguientes cmdlets para detener e iniciar un dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="78d55-105">Use the following cmdlets to stop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-virtual-device"></a><span data-ttu-id="78d55-106">Para reiniciar un dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="78d55-106">To restart a virtual device</span></span>
<span data-ttu-id="78d55-107">Cuando se ejecuta un dispositivo virtual y desea reiniciarlo, haga clic en su nombre y, a continuación, haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="78d55-107">When a virtual device is running and you want to restart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="78d55-108">Mientras se reinicia el dispositivo virtual, su estado es **Reiniciando**.</span><span class="sxs-lookup"><span data-stu-id="78d55-108">While the virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="78d55-109">Cuando el dispositivo virtual está listo para su uso, su estado es **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="78d55-109">When the virtual device is ready for you to use, its status is **Running**.</span></span>

<span data-ttu-id="78d55-110">Use el siguiente cmdlet para reiniciar un dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="78d55-110">Use the following cmdlet to restart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

