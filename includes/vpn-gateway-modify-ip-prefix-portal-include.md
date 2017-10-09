### <span data-ttu-id="d8b25-101"><a name="noconnection"></a>prefijos de direcciones en la IP de la puerta de enlace de red local toomodify - no hay ninguna conexión de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="d8b25-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="d8b25-102">prefijos de dirección adicional tooadd:</span><span class="sxs-lookup"><span data-stu-id="d8b25-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="d8b25-103">En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d8b25-104">Agregar espacio de direcciones IP de Hola Hola *agregar otro intervalo de direcciones* cuadro.</span><span class="sxs-lookup"><span data-stu-id="d8b25-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="d8b25-105">Haga clic en **guardar** toosave la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8b25-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="d8b25-106">prefijos de direcciones de tooremove:</span><span class="sxs-lookup"><span data-stu-id="d8b25-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="d8b25-107">En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d8b25-108">Haga clic en hello **'...'** en la línea de Hola que contiene el prefijo de hello desea tooremove.</span><span class="sxs-lookup"><span data-stu-id="d8b25-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="d8b25-109">Haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-109">Click **Remove**.</span></span>
4. <span data-ttu-id="d8b25-110">Haga clic en **guardar** toosave la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8b25-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="d8b25-111"><a name="withconnection"></a>toomodify red local puerta de enlace prefijos de direcciones IP: conexión de puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="d8b25-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="d8b25-112">Si tiene una conexión de puerta de enlace y desea tooadd o quitar prefijos de direcciones IP de hello contenidos en la puerta de enlace de red local, deberá hello toodo siguiendo los pasos en orden.</span><span class="sxs-lookup"><span data-stu-id="d8b25-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="d8b25-113">Esto tendrá como resultado un tiempo de inactividad para la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="d8b25-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="d8b25-114">Cuando se modifica prefijos de direcciones IP, no es necesario puerta de enlace VPN toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b25-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="d8b25-115">Solo necesita conexión de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="d8b25-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="d8b25-116">1. Quitar conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b25-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="d8b25-117">En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **conexiones**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="d8b25-118">Haga clic en hello **...**  en línea hello para cada conexión, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="d8b25-119">Haga clic en **guardar** toosave la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8b25-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="d8b25-120">2. Modifique los prefijos de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b25-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="d8b25-121">prefijos de dirección adicional tooadd:</span><span class="sxs-lookup"><span data-stu-id="d8b25-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="d8b25-122">En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d8b25-123">Agregar espacio de direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b25-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="d8b25-124">Haga clic en **guardar** toosave la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8b25-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="d8b25-125">prefijos de direcciones de tooremove:</span><span class="sxs-lookup"><span data-stu-id="d8b25-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="d8b25-126">En los recursos de la puerta de enlace de red Local, en Hola Hola **configuración** sección, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="d8b25-127">Haga clic en hello **...**  en la línea de Hola que contiene el prefijo de hello desea tooremove.</span><span class="sxs-lookup"><span data-stu-id="d8b25-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="d8b25-128">Haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-128">Click **Remove**.</span></span>
4. <span data-ttu-id="d8b25-129">Haga clic en **guardar** toosave la configuración.</span><span class="sxs-lookup"><span data-stu-id="d8b25-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="d8b25-130">3. Vuelva a crear la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8b25-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="d8b25-131">Navegue toohello puerta de enlace de red Virtual para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="d8b25-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="d8b25-132">(No Hola puerta de enlace de red Local.)</span><span class="sxs-lookup"><span data-stu-id="d8b25-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="d8b25-133">En hello puerta de enlace de red Virtual, en hello **configuración** sección, haga clic en **conexiones**.</span><span class="sxs-lookup"><span data-stu-id="d8b25-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="d8b25-134">Haga clic en hello **+ agregar** tooopen hello **Agregar conexión** hoja.</span><span class="sxs-lookup"><span data-stu-id="d8b25-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="d8b25-135">Vuelva a crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="d8b25-135">Recreate your connection.</span></span>
5. <span data-ttu-id="d8b25-136">Haga clic en **Aceptar** conexión de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d8b25-136">Click **OK** toocreate hello connection.</span></span>
