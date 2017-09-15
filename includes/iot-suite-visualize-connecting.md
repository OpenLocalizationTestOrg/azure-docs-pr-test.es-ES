## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="0e509-101">Ver la telemetría de dispositivo en el panel</span><span class="sxs-lookup"><span data-stu-id="0e509-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="0e509-102">El panel de la solución de supervisión remota permite ver la telemetría que los dispositivos envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0e509-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="0e509-103">En el explorador, vuelva al panel de la solución de supervisión remota, haga clic en **Dispositivos** en el panel izquierdo para navegar hasta la **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0e509-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="0e509-104">En la **lista de dispositivos**, debería ver que el estado del dispositivo es **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="0e509-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="0e509-105">Si no es así, haga clic en **Habilitar dispositivo** en el panel **Detalles del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="0e509-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![Ver el estado del dispositivo][18]
3. <span data-ttu-id="0e509-107">Haga clic en el **Panel** para volver a él, seleccione el dispositivo en la lista desplegable **Device to View** (Dispositivo para ver) para ver su telemetría.</span><span class="sxs-lookup"><span data-stu-id="0e509-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="0e509-108">La telemetría de la aplicación de ejemplo es 50 unidades para la temperatura interior, 55 unidades para la temperatura exterior y 50 unidades para la humedad.</span><span class="sxs-lookup"><span data-stu-id="0e509-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Ver la telemetría de dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="0e509-110">Invocar un método en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="0e509-110">Invoke a method on your device</span></span>
<span data-ttu-id="0e509-111">El panel de la solución de supervisión remota le permite invocar métodos en los dispositivos a través de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0e509-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="0e509-112">Por ejemplo, en la solución de supervisión remota, puede invocar un método para simular que se reinicia un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0e509-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="0e509-113">En el panel de la solución de supervisión remota, haga clic en **Devices** (Dispositivos) en el panel izquierdo para navegar a la **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0e509-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="0e509-114">Haga clic en **Device ID** (Id. de dispositivo) en el dispositivo de la **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0e509-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="0e509-115">En el panel **Detalles del dispositivo**, haga clic en **Métodos**.</span><span class="sxs-lookup"><span data-stu-id="0e509-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Métodos de dispositivo][13]
4. <span data-ttu-id="0e509-117">En el menú desplegable **Método**, seleccione **InitiateFirmwareUpdate** y, luego, en **FWPACKAGEURI**, escriba una dirección URL ficticia.</span><span class="sxs-lookup"><span data-stu-id="0e509-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="0e509-118">Haga clic en **Invocar método** para llamar al método en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0e509-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Invocar un método de dispositivo][14]
   

5. <span data-ttu-id="0e509-120">Puede ver un mensaje en la consola donde se ejecuta el código del dispositivo cuando el dispositivo controla el método.</span><span class="sxs-lookup"><span data-stu-id="0e509-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="0e509-121">Los resultados del método se agregan al historial en el portal de la solución:</span><span class="sxs-lookup"><span data-stu-id="0e509-121">The results of the method are added to the history in the solution portal:</span></span>

    ![Ver el historial de métodos][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="0e509-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e509-123">Next steps</span></span>
<span data-ttu-id="0e509-124">En el artículo [Personalización de soluciones preconfiguradas][lnk-customize] se describen algunas formas de ampliar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0e509-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="0e509-125">Entre las posibles extensiones se incluyen el uso de sensores reales y la implementación de comandos adicionales.</span><span class="sxs-lookup"><span data-stu-id="0e509-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="0e509-126">Puede obtener más información sobre los [permisos en el sitio azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="0e509-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
