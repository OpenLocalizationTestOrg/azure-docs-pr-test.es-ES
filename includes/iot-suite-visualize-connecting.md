## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="ead1f-101">Vista de telemetría de dispositivo en el panel de Hola</span><span class="sxs-lookup"><span data-stu-id="ead1f-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="ead1f-102">panel de Hola Hola habilita solución telemetría hello tooview tooIoT concentrador de envío de los dispositivos de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="ead1f-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="ead1f-103">En el explorador, el valor devuelto toohello panel de solución supervisión remoto, haga clic en **dispositivos** en hello panel izquierdo toonavigate toohello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ead1f-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="ead1f-104">Hola **lista de dispositivos**, debería ver que Hola estado del dispositivo es **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="ead1f-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="ead1f-105">Si no es así, haga clic en **Habilitar dispositivo** en hello **detalles del dispositivo** panel.</span><span class="sxs-lookup"><span data-stu-id="ead1f-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Ver el estado del dispositivo][18]
3. <span data-ttu-id="ead1f-107">Haga clic en **panel** tooreturn toohello panel, seleccione el dispositivo en hello **tooView dispositivo** tooview de la lista desplegable la telemetría.</span><span class="sxs-lookup"><span data-stu-id="ead1f-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="ead1f-108">Hola la telemetría de aplicación de ejemplo de Hola es 50 unidades de temperatura interna, 55 unidades de temperatura externo y las 50 unidades de humedad.</span><span class="sxs-lookup"><span data-stu-id="ead1f-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Ver la telemetría de dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="ead1f-110">Invocar un método en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="ead1f-110">Invoke a method on your device</span></span>
<span data-ttu-id="ead1f-111">panel de Hello en la solución de supervisión remoto hello permite tooinvoke métodos en los dispositivos a través del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ead1f-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="ead1f-112">Por ejemplo, en hello remoto de solución de supervisión puede invocar un toosimulate método reiniciar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ead1f-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="ead1f-113">En hello remoto solución panel de supervisión, haga clic en **dispositivos** en hello panel izquierdo toonavigate toohello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ead1f-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="ead1f-114">Haga clic en **Id. de dispositivo** para el dispositivo en hello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ead1f-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="ead1f-115">Hola **detalles del dispositivo** del panel, haga clic en **métodos**.</span><span class="sxs-lookup"><span data-stu-id="ead1f-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Métodos de dispositivo][13]
4. <span data-ttu-id="ead1f-117">Hola **método** lista desplegable, seleccione **InitiateFirmwareUpdate**y, a continuación, en **FWPACKAGEURI** escriba una dirección URL ficticia.</span><span class="sxs-lookup"><span data-stu-id="ead1f-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="ead1f-118">Haga clic en **invocar método** toocall método de hello en dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="ead1f-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Invocar un método de dispositivo][14]
   

5. <span data-ttu-id="ead1f-120">Verá un mensaje en la consola de Hola que se ejecute el código de dispositivo cuando el dispositivo de hello controla método hello.</span><span class="sxs-lookup"><span data-stu-id="ead1f-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="ead1f-121">resultados de Hello del método hello se agregan toohello historial en el portal de solución de hello:</span><span class="sxs-lookup"><span data-stu-id="ead1f-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Ver el historial de métodos][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="ead1f-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ead1f-123">Next steps</span></span>
<span data-ttu-id="ead1f-124">artículo de Hello [personalizar soluciones preconfiguradas] [ lnk-customize] describe algunas maneras puede extender este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ead1f-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="ead1f-125">Entre las posibles extensiones se incluyen el uso de sensores reales y la implementación de comandos adicionales.</span><span class="sxs-lookup"><span data-stu-id="ead1f-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="ead1f-126">Puede aprender más acerca de hello [permisos en el sitio de hello azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="ead1f-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
