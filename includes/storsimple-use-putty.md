<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="076ac-101">tooconnect a través de la consola serie Hola</span><span class="sxs-lookup"><span data-stu-id="076ac-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="076ac-102">Conecte el cable serie toohello dispositivo (directamente o a través de un adaptador USB-serie).</span><span class="sxs-lookup"><span data-stu-id="076ac-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="076ac-103">Abra hello **el Panel de Control**y, a continuación, abra hello **el Administrador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="076ac-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="076ac-104">Identifique el puerto de hello COM como se muestra en hello siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="076ac-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Conexión a través de la consola serie](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="076ac-106">Inicie PuTTY.</span><span class="sxs-lookup"><span data-stu-id="076ac-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="076ac-107">En el panel derecho de hello, cambie hello **tipo de conexión** demasiado**serie**.</span><span class="sxs-lookup"><span data-stu-id="076ac-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="076ac-108">En el panel derecho de hello, escriba el puerto COM correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="076ac-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="076ac-109">Asegúrese de que los parámetros de configuración de serie de hello están establecidos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="076ac-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="076ac-110">Velocidad: 115.200</span><span class="sxs-lookup"><span data-stu-id="076ac-110">Speed: 115,200</span></span>
   * <span data-ttu-id="076ac-111">Bits de datos: 8</span><span class="sxs-lookup"><span data-stu-id="076ac-111">Data bits: 8</span></span>
   * <span data-ttu-id="076ac-112">Bits de parada: 1</span><span class="sxs-lookup"><span data-stu-id="076ac-112">Stop bits: 1</span></span>
   * <span data-ttu-id="076ac-113">Paridad: ninguno</span><span class="sxs-lookup"><span data-stu-id="076ac-113">Parity: None</span></span>
   * <span data-ttu-id="076ac-114">Control de flujo: ninguno</span><span class="sxs-lookup"><span data-stu-id="076ac-114">Flow control: None</span></span>
     
     <span data-ttu-id="076ac-115">Esta configuración se muestra en hello siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="076ac-115">These settings are shown in hello following illustration.</span></span>
     
     ![Configuración de PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="076ac-117">Si la configuración de control de flujo de hello predeterminada no funciona, intente establecer control de flujo de hello tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="076ac-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="076ac-118">Haga clic en **abiertos** toostart una sesión serie.</span><span class="sxs-lookup"><span data-stu-id="076ac-118">Click **Open** toostart a serial session.</span></span>

