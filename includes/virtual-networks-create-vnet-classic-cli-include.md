## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="217d3-101">¿Cómo toocreate una red virtual clásica con CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="217d3-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="217d3-102">Puede usar hello Azure CLI toomanage los recursos de Azure Hola desde línea de comandos desde cualquier equipo que ejecute Windows, Linux y OSX.</span><span class="sxs-lookup"><span data-stu-id="217d3-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="217d3-103">toocreate una red virtual mediante el uso de hello CLI de Azure, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="217d3-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="217d3-104">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../articles/cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="217d3-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="217d3-105">Ejecute hello **crear red virtual de red de azure** comandos toocreate una red virtual y una subred, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="217d3-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="217d3-106">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="217d3-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="217d3-107">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="217d3-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="217d3-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="217d3-108">**--vnet**.</span></span> <span data-ttu-id="217d3-109">Nombre de hello toobe de red virtual creado.</span><span class="sxs-lookup"><span data-stu-id="217d3-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="217d3-110">En este escenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="217d3-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="217d3-111">**-e (o --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="217d3-112">Espacio de direcciones de red virtual.</span><span class="sxs-lookup"><span data-stu-id="217d3-112">VNet address space.</span></span> <span data-ttu-id="217d3-113">En este escenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="217d3-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="217d3-114">**-i (o -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="217d3-115">Máscara de red en formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="217d3-115">Network mask in CIDR format.</span></span> <span data-ttu-id="217d3-116">En este escenario, *16*.</span><span class="sxs-lookup"><span data-stu-id="217d3-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="217d3-117">**-n (o --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="217d3-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="217d3-118">Nombre de la primera subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="217d3-118">Name of hello first subnet.</span></span> <span data-ttu-id="217d3-119">En este escenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="217d3-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="217d3-120">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="217d3-121">Dirección IP inicial de la subred o el espacio de direcciones de la subred.</span><span class="sxs-lookup"><span data-stu-id="217d3-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="217d3-122">En este escenario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="217d3-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="217d3-123">**-r (o --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="217d3-124">Máscara de red en formato CIDR para subred.</span><span class="sxs-lookup"><span data-stu-id="217d3-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="217d3-125">En este escenario, *24*.</span><span class="sxs-lookup"><span data-stu-id="217d3-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="217d3-126">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-126">**-l (or --location)**.</span></span> <span data-ttu-id="217d3-127">Región de Azure donde se creará Hola red virtual.</span><span class="sxs-lookup"><span data-stu-id="217d3-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="217d3-128">En este escenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="217d3-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="217d3-129">Ejecute hello **crear subredes de red virtual de red de azure** comando toocreate una subred tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="217d3-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="217d3-130">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="217d3-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="217d3-131">Este es el resultado de hello esperada en comando hello anterior:</span><span class="sxs-lookup"><span data-stu-id="217d3-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="217d3-132">**-t (o --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="217d3-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="217d3-133">Nombre de red virtual donde se creará la subred de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="217d3-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="217d3-134">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="217d3-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="217d3-135">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-135">**-n (or --name)**.</span></span> <span data-ttu-id="217d3-136">Nombre de subred nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="217d3-136">Name of hello new subnet.</span></span> <span data-ttu-id="217d3-137">En este escenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="217d3-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="217d3-138">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="217d3-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="217d3-139">Bloque CIDR de subred.</span><span class="sxs-lookup"><span data-stu-id="217d3-139">Subnet CIDR block.</span></span> <span data-ttu-id="217d3-140">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="217d3-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="217d3-141">Ejecute hello **mostrar de la red virtual de red de azure** comando Propiedades de hello tooview de red virtual nueva hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="217d3-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="217d3-142">Este es el resultado de hello esperada en comando hello anterior:</span><span class="sxs-lookup"><span data-stu-id="217d3-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

