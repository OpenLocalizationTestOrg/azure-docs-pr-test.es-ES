#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="7686f-101">toostop e inicie un dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="7686f-101">toostop and start a virtual device</span></span>
<span data-ttu-id="7686f-102">toostop un dispositivo virtual, haga clic en su nombre y, a continuación, haga clic en **apagado**.</span><span class="sxs-lookup"><span data-stu-id="7686f-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="7686f-103">Mientras se está cerrando el dispositivo virtual hello, su estado es **detener**.</span><span class="sxs-lookup"><span data-stu-id="7686f-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="7686f-104">Cuando se haya detenido el dispositivo virtual hello, su estado es **detenido**.</span><span class="sxs-lookup"><span data-stu-id="7686f-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="7686f-105">Usar hello después cmdlets toostop e iniciar un dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="7686f-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="7686f-106">toorestart un dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="7686f-106">toorestart a virtual device</span></span>
<span data-ttu-id="7686f-107">Cuando se ejecuta un dispositivo virtual y desea toorestart, haga clic en su nombre y, a continuación, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="7686f-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="7686f-108">Mientras se está reiniciando el dispositivo virtual hello, su estado es **reiniciando**.</span><span class="sxs-lookup"><span data-stu-id="7686f-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="7686f-109">Cuando esté listo para toouse dispositivo virtual hello, su estado es **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="7686f-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="7686f-110">Usar hello siguiente cmdlet toorestart un dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="7686f-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

