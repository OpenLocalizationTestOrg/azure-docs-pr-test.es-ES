<!--author=SharS last changed: 9/17/15-->

#### <a name="to-connect-through-the-serial-console"></a><span data-ttu-id="977f0-101">Para conectarse a través de la consola serie</span><span class="sxs-lookup"><span data-stu-id="977f0-101">To connect through the serial console</span></span>
1. <span data-ttu-id="977f0-102">Conecte el cable serie al dispositivo (directamente o a través de un adaptador USB-serie).</span><span class="sxs-lookup"><span data-stu-id="977f0-102">Connect your serial cable to the device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="977f0-103">Abra el **Panel de control** y, a continuación, abra el **Administrador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="977f0-103">Open the **Control Panel**, and then open the **Device Manager**.</span></span>
3. <span data-ttu-id="977f0-104">Identifique el puerto COM como se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="977f0-104">Identify the COM port as shown in the following illustration.</span></span>
   
     ![Conexión a través de la consola serie](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="977f0-106">Inicie PuTTY.</span><span class="sxs-lookup"><span data-stu-id="977f0-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="977f0-107">En el panel derecho, cambie el **Tipo de conexión** a **Serie**.</span><span class="sxs-lookup"><span data-stu-id="977f0-107">In the right pane, change the **Connection type** to **Serial**.</span></span>
6. <span data-ttu-id="977f0-108">En el panel derecho, escriba el puerto COM adecuado.</span><span class="sxs-lookup"><span data-stu-id="977f0-108">In the right pane, type the appropriate COM port.</span></span> <span data-ttu-id="977f0-109">Asegúrese de que los parámetros de configuración en serie se establecen como sigue:</span><span class="sxs-lookup"><span data-stu-id="977f0-109">Make sure that the serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="977f0-110">Velocidad: 115.200</span><span class="sxs-lookup"><span data-stu-id="977f0-110">Speed: 115,200</span></span>
   * <span data-ttu-id="977f0-111">Bits de datos: 8</span><span class="sxs-lookup"><span data-stu-id="977f0-111">Data bits: 8</span></span>
   * <span data-ttu-id="977f0-112">Bits de parada: 1</span><span class="sxs-lookup"><span data-stu-id="977f0-112">Stop bits: 1</span></span>
   * <span data-ttu-id="977f0-113">Paridad: ninguno</span><span class="sxs-lookup"><span data-stu-id="977f0-113">Parity: None</span></span>
   * <span data-ttu-id="977f0-114">Control de flujo: ninguno</span><span class="sxs-lookup"><span data-stu-id="977f0-114">Flow control: None</span></span>
     
     <span data-ttu-id="977f0-115">Esta configuración se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="977f0-115">These settings are shown in the following illustration.</span></span>
     
     ![Configuración de PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="977f0-117">Si la opción de control de flujo predeterminado no funciona, pruebe a establecer el control de flujo en XON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="977f0-117">If the default flow control setting does not work, try setting the flow control to XON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="977f0-118">Haga clic en **Abrir** para iniciar una sesión en serie.</span><span class="sxs-lookup"><span data-stu-id="977f0-118">Click **Open** to start a serial session.</span></span>

