## <a name="view-hello-telemetry"></a><span data-ttu-id="0c515-101">Vista Hola telemetría</span><span class="sxs-lookup"><span data-stu-id="0c515-101">View hello telemetry</span></span>

<span data-ttu-id="0c515-102">Hola frambuesa Pi ahora está enviando la solución de supervisión remota de telemetría toohello.</span><span class="sxs-lookup"><span data-stu-id="0c515-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="0c515-103">Puede ver la telemetría de hello en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c515-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="0c515-104">También puede enviar mensajes tooyour frambuesa Pi desde el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c515-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="0c515-105">Vaya a Panel de solución toohello.</span><span class="sxs-lookup"><span data-stu-id="0c515-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="0c515-106">Seleccione el dispositivo en hello **tooView dispositivo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="0c515-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="0c515-107">telemetría Hola de hello frambuesa Pi muestra en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c515-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Mostrar la telemetría de hello frambuesa Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="0c515-109">Actuar en dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="0c515-109">Act on hello device</span></span>

<span data-ttu-id="0c515-110">En el panel de la solución de hello, puede invocar métodos en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="0c515-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="0c515-111">Cuando Hola frambuesa Pi conecta toohello solución de supervisión remoto, se enviará información acerca de los métodos de hello es compatible con.</span><span class="sxs-lookup"><span data-stu-id="0c515-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="0c515-112">En el panel de la solución de hello, haga clic en **dispositivos** toovisit hello **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="0c515-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="0c515-113">Seleccione el instalador de plataforma de frambuesa Hola **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0c515-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="0c515-114">A continuación, elija **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="0c515-114">Then choose **Methods**:</span></span>

    ![Lista de dispositivos en el panel][img-list-devices]

- <span data-ttu-id="0c515-116">En hello **invocar método** página, elija **LightBlink** en hello **método** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="0c515-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="0c515-117">Elija **Invocar método**.</span><span class="sxs-lookup"><span data-stu-id="0c515-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="0c515-118">simulador de Hello imprime un mensaje en la consola de hello en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="0c515-118">hello simulator prints a message in hello console on hello Raspberry Pi.</span></span> <span data-ttu-id="0c515-119">aplicación de Hello en hello frambuesa Pi envía un panel de solución de toohello espera de confirmación:</span><span class="sxs-lookup"><span data-stu-id="0c515-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Mostrar el historial de métodos][img-method-history]

- <span data-ttu-id="0c515-121">Puede cambiar los LED de Hola activar y desactivar mediante hello **ChangeLightStatus** método con un **LightStatusValue** establecido demasiado**1** para en o **0** para desactivar.</span><span class="sxs-lookup"><span data-stu-id="0c515-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="0c515-122">Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="0c515-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="0c515-123">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="0c515-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="0c515-124">Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.</span><span class="sxs-lookup"><span data-stu-id="0c515-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md