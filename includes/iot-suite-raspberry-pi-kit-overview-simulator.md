## <a name="overview"></a><span data-ttu-id="c03f9-101">Información general</span><span class="sxs-lookup"><span data-stu-id="c03f9-101">Overview</span></span>

<span data-ttu-id="c03f9-102">En este tutorial, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c03f9-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="c03f9-103">Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c03f9-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="c03f9-104">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c03f9-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="c03f9-105">Configure su toocommunicate de dispositivo con el equipo y la solución de supervisión remota Hola.</span><span class="sxs-lookup"><span data-stu-id="c03f9-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="c03f9-106">Actualizar Hola ejemplo dispositivo código tooconnect toohello solución de supervisión y enviar telemetría simulada que se puede ver en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="c03f9-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c03f9-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c03f9-107">Prerequisites</span></span>

<span data-ttu-id="c03f9-108">toocomplete este tutorial, necesita una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="c03f9-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c03f9-109">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c03f9-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c03f9-110">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="c03f9-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="c03f9-111">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="c03f9-111">Required software</span></span>

<span data-ttu-id="c03f9-112">Se necesita al cliente SSH en su tooenable de máquina de escritorio tooremotely acceso Hola la línea de comandos en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="c03f9-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="c03f9-113">Windows no incluye ningún cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="c03f9-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="c03f9-114">Se recomienda usar [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="c03f9-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="c03f9-115">La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad SSH de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c03f9-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="c03f9-116">Para más información, consulte [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH cuando se usa Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="c03f9-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="c03f9-117">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="c03f9-117">Required hardware</span></span>

<span data-ttu-id="c03f9-118">Un equipo de escritorio tooenable tooconnect remotamente toohello la línea de comandos en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="c03f9-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="c03f9-119">[Kit de inicio de Microsoft IoT para Raspberry Pi 3][lnk-starter-kits] o componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="c03f9-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="c03f9-120">Este tutorial utiliza Hola siguientes elementos del kit de hello:</span><span class="sxs-lookup"><span data-stu-id="c03f9-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="c03f9-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="c03f9-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="c03f9-122">Tarjeta MicroSD (con NOOBS)</span><span class="sxs-lookup"><span data-stu-id="c03f9-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="c03f9-123">Un cable USB mini</span><span class="sxs-lookup"><span data-stu-id="c03f9-123">A USB Mini cable</span></span>
- <span data-ttu-id="c03f9-124">Un cable Ethernet</span><span class="sxs-lookup"><span data-stu-id="c03f9-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/