## <a name="overview"></a><span data-ttu-id="7d2d2-101">Información general</span><span class="sxs-lookup"><span data-stu-id="7d2d2-101">Overview</span></span>

<span data-ttu-id="7d2d2-102">En este tutorial, va a completar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7d2d2-102">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="7d2d2-103">Implemente una instancia de la solución preconfigurada de supervisión remota en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="7d2d2-104">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="7d2d2-105">Configure el dispositivo para que se comunique con el equipo y la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-105">Set up your device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="7d2d2-106">Actualice el código del dispositivo de ejemplo para que se conecte a la solución de supervisión remota y envíe telemetría simulada que aparezca en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d2d2-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7d2d2-107">Prerequisites</span></span>

<span data-ttu-id="7d2d2-108">Para completar este tutorial, deberá tener una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-108">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7d2d2-109">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7d2d2-110">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="7d2d2-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="7d2d2-111">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="7d2d2-111">Required software</span></span>

<span data-ttu-id="7d2d2-112">Necesita el cliente SSH en su máquina de escritorio para poder acceder de forma remota a la línea de comandos en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="7d2d2-113">Windows no incluye ningún cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="7d2d2-114">Se recomienda usar [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="7d2d2-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="7d2d2-115">La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad de línea de comandos de SSH.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="7d2d2-116">Para más información, consulte [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH cuando se usa Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="7d2d2-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="7d2d2-117">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="7d2d2-117">Required hardware</span></span>

<span data-ttu-id="7d2d2-118">Un equipo de escritorio que permita conectarse remotamente a la línea de comandos en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="7d2d2-119">[Kit de inicio de Microsoft IoT para Raspberry Pi 3][lnk-starter-kits] o componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="7d2d2-120">En este tutorial se usan los siguientes elementos del kit:</span><span class="sxs-lookup"><span data-stu-id="7d2d2-120">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="7d2d2-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="7d2d2-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="7d2d2-122">Tarjeta MicroSD (con NOOBS)</span><span class="sxs-lookup"><span data-stu-id="7d2d2-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="7d2d2-123">Un cable USB mini</span><span class="sxs-lookup"><span data-stu-id="7d2d2-123">A USB Mini cable</span></span>
- <span data-ttu-id="7d2d2-124">Un cable Ethernet</span><span class="sxs-lookup"><span data-stu-id="7d2d2-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/