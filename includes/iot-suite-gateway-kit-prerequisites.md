## <a name="prerequisites"></a><span data-ttu-id="d30c3-101">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d30c3-101">Prerequisites</span></span>

<span data-ttu-id="d30c3-102">Para completar este tutorial, deberá tener una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="d30c3-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d30c3-103">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d30c3-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d30c3-104">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="d30c3-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="d30c3-105">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="d30c3-105">Required software</span></span>

<span data-ttu-id="d30c3-106">Necesita el cliente SSH en su máquina de escritorio para poder acceder de forma remota a la línea de comandos en su Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d30c3-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Intel NUC.</span></span>

- <span data-ttu-id="d30c3-107">Windows no incluye ningún cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="d30c3-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="d30c3-108">Se recomienda usar [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="d30c3-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="d30c3-109">La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad de línea de comandos de SSH.</span><span class="sxs-lookup"><span data-stu-id="d30c3-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span>

### <a name="required-hardware"></a><span data-ttu-id="d30c3-110">Requisitos de hardware</span><span class="sxs-lookup"><span data-stu-id="d30c3-110">Required hardware</span></span>

<span data-ttu-id="d30c3-111">Un equipo de escritorio que permita conectarse remotamente a la línea de comandos en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d30c3-111">A desktop computer to enable you to connect remotely to the command line on the Intel NUC.</span></span>

<span data-ttu-id="d30c3-112">[Kit de puerta de enlace comercial de IoT][lnk-starter-kits].</span><span class="sxs-lookup"><span data-stu-id="d30c3-112">[IoT Commercial Gateway Kit][lnk-starter-kits].</span></span> <span data-ttu-id="d30c3-113">En este tutorial se usan los siguientes elementos del kit:</span><span class="sxs-lookup"><span data-stu-id="d30c3-113">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="d30c3-114">Intel® NUC Kit DE3815TYKE con 4 GB de memoria y tarjeta de expansión Bluetooth</span><span class="sxs-lookup"><span data-stu-id="d30c3-114">Intel® NUC Kit DE3815TYKE with 4G Memory and Bluetooth expansion card</span></span>
- <span data-ttu-id="d30c3-115">Adaptador de corriente</span><span class="sxs-lookup"><span data-stu-id="d30c3-115">Power adaptor</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/