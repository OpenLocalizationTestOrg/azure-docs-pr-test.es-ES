## <a name="view-the-telemetry"></a><span data-ttu-id="6ffc2-101">Visualización de la telemetría</span><span class="sxs-lookup"><span data-stu-id="6ffc2-101">View the telemetry</span></span>

<span data-ttu-id="6ffc2-102">Raspberry Pi ahora está enviando telemetría a la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="6ffc2-103">Puede verla en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="6ffc2-104">También puede enviar mensajes a su Raspberry Pi desde el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="6ffc2-105">Vaya al panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="6ffc2-106">Seleccione el dispositivo en la lista desplegable **Dispositivo que se visualizará**.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="6ffc2-107">La telemetría de Raspberry Pi se muestra en el panel.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Mostrar telemetría desde Raspberry Pi][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="6ffc2-109">Actuación en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="6ffc2-109">Act on the device</span></span>

<span data-ttu-id="6ffc2-110">En el panel de soluciones, puede invocar métodos en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="6ffc2-111">Cuando Raspberry Pi se conecta a la solución de supervisión remota, envía información acerca de los métodos que admite.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="6ffc2-112">En el panel de soluciones, haga clic en **Dispositivos** para visitar la página **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="6ffc2-113">Seleccione su Raspberry Pi en la **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="6ffc2-114">A continuación, elija **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="6ffc2-114">Then choose **Methods**:</span></span>

    ![Lista de dispositivos en el panel][img-list-devices]

- <span data-ttu-id="6ffc2-116">En la página **Invocar método**, elija **LightBlink** en la lista desplegable **Método**.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="6ffc2-117">Elija **Invocar método**.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="6ffc2-118">El simulador imprime un mensaje en la consola de Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="6ffc2-119">La aplicación en Raspberry Pi envía una confirmación de vuelta al panel de soluciones:</span><span class="sxs-lookup"><span data-stu-id="6ffc2-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Mostrar el historial de métodos][img-method-history]

- <span data-ttu-id="6ffc2-121">Puede activar el LED y desactivarlo mediante el método **ChangeLightStatus** con un valor de **LightStatusValue** establecido en **1** para activado o **0** para desactivado.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="6ffc2-122">Si deja la solución de supervisión remota ejecutándose en su cuenta de Azure, se le cobra por el tiempo que se ejecute.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="6ffc2-123">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="6ffc2-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="6ffc2-124">Elimine la solución preconfigurada de su cuenta de Azure cuando haya terminado de usarla.</span><span class="sxs-lookup"><span data-stu-id="6ffc2-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md