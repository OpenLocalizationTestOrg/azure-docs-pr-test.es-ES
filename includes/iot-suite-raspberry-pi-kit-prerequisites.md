## <a name="prerequisites"></a><span data-ttu-id="b6411-101">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b6411-101">Prerequisites</span></span>

<span data-ttu-id="b6411-102">Para completar este tutorial, deberá tener una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6411-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b6411-103">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b6411-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b6411-104">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="b6411-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="b6411-105">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="b6411-105">Required software</span></span>

<span data-ttu-id="b6411-106">Necesita el cliente SSH en su máquina de escritorio para poder acceder de forma remota a la línea de comandos en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b6411-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="b6411-107">Windows no incluye ningún cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="b6411-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="b6411-108">Se recomienda usar [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="b6411-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="b6411-109">La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad de línea de comandos de SSH.</span><span class="sxs-lookup"><span data-stu-id="b6411-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="b6411-110">Para más información, consulte [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH cuando se usa Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="b6411-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="b6411-111">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="b6411-111">Required hardware</span></span>

<span data-ttu-id="b6411-112">Un equipo de escritorio que permita conectarse remotamente a la línea de comandos en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b6411-112">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="b6411-113">[Kit de inicio de Microsoft IoT para Raspberry Pi 3][lnk-starter-kits] o componentes equivalentes.</span><span class="sxs-lookup"><span data-stu-id="b6411-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="b6411-114">En este tutorial se usan los siguientes elementos del kit:</span><span class="sxs-lookup"><span data-stu-id="b6411-114">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="b6411-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="b6411-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="b6411-116">Tarjeta MicroSD (con NOOBS)</span><span class="sxs-lookup"><span data-stu-id="b6411-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="b6411-117">Un cable USB mini</span><span class="sxs-lookup"><span data-stu-id="b6411-117">A USB Mini cable</span></span>
- <span data-ttu-id="b6411-118">Un cable Ethernet</span><span class="sxs-lookup"><span data-stu-id="b6411-118">An Ethernet cable</span></span>
- <span data-ttu-id="b6411-119">Sensor de BME280</span><span class="sxs-lookup"><span data-stu-id="b6411-119">BME280 sensor</span></span>
- <span data-ttu-id="b6411-120">Placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="b6411-120">Breadboard</span></span>
- <span data-ttu-id="b6411-121">Cables de puente</span><span class="sxs-lookup"><span data-stu-id="b6411-121">Jumper wires</span></span>
- <span data-ttu-id="b6411-122">Resistencias</span><span class="sxs-lookup"><span data-stu-id="b6411-122">Resistors</span></span>
- <span data-ttu-id="b6411-123">LED</span><span class="sxs-lookup"><span data-stu-id="b6411-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/