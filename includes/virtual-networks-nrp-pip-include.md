## <a name="public-ip-address"></a><span data-ttu-id="bb02d-101">Dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="bb02d-101">Public IP address</span></span>
<span data-ttu-id="bb02d-102">Un recurso de dirección IP pública le proporciona una dirección IP de Internet reservada o dinámica.</span><span class="sxs-lookup"><span data-stu-id="bb02d-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="bb02d-103">Aunque puede crear una dirección IP pública como un objeto independiente, necesita tooassociate se tooanother objeto tooactually usar dirección Hola.</span><span class="sxs-lookup"><span data-stu-id="bb02d-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="bb02d-104">Puede asociar un equilibrador de carga de tooa de dirección IP público, puerta de enlace de aplicaciones o una NIC tooprovide Internet acceder a toothose los recursos.</span><span class="sxs-lookup"><span data-stu-id="bb02d-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="bb02d-105">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bb02d-105">Property</span></span> | <span data-ttu-id="bb02d-106">Descripción</span><span class="sxs-lookup"><span data-stu-id="bb02d-106">Description</span></span> | <span data-ttu-id="bb02d-107">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb02d-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb02d-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="bb02d-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="bb02d-109">Define si la dirección IP de hello es *estático* o *dinámica*.</span><span class="sxs-lookup"><span data-stu-id="bb02d-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="bb02d-110">estática, dinámica</span><span class="sxs-lookup"><span data-stu-id="bb02d-110">static, dynamic</span></span> |
| <span data-ttu-id="bb02d-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="bb02d-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="bb02d-112">Define Hola inactivo tiempo de espera, con un valor predeterminado de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="bb02d-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="bb02d-113">Si no se recibe ningún paquete más de una sesión específica dentro de este tiempo, la sesión Hola terminó.</span><span class="sxs-lookup"><span data-stu-id="bb02d-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="bb02d-114">cualquier valor entre 4 y 30</span><span class="sxs-lookup"><span data-stu-id="bb02d-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="bb02d-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="bb02d-115">**ipAddress**</span></span> |<span data-ttu-id="bb02d-116">Dirección IP asignada tooobject.</span><span class="sxs-lookup"><span data-stu-id="bb02d-116">IP address assigned tooobject.</span></span> <span data-ttu-id="bb02d-117">Se trata de una propiedad de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="bb02d-117">This is a read-only property.</span></span> |<span data-ttu-id="bb02d-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="bb02d-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="bb02d-119">Configuración de DNS</span><span class="sxs-lookup"><span data-stu-id="bb02d-119">DNS settings</span></span>
<span data-ttu-id="bb02d-120">Las direcciones IP públicas tienen un objeto secundario denominado **dnsSettings** que contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb02d-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="bb02d-121">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bb02d-121">Property</span></span> | <span data-ttu-id="bb02d-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="bb02d-122">Description</span></span> | <span data-ttu-id="bb02d-123">Valores de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb02d-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb02d-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="bb02d-124">**domainNameLabel**</span></span> |<span data-ttu-id="bb02d-125">Nombre de host usado para la resolución de nombres.</span><span class="sxs-lookup"><span data-stu-id="bb02d-125">Host named used for name resolution.</span></span> |<span data-ttu-id="bb02d-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="bb02d-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="bb02d-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="bb02d-127">**fqdn**</span></span> |<span data-ttu-id="bb02d-128">Nombre completo para la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="bb02d-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="bb02d-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="bb02d-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="bb02d-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="bb02d-130">**reverseFqdn**</span></span> |<span data-ttu-id="bb02d-131">Nombre de dominio completo que resuelve la dirección IP de toohello y está registrado en DNS como un registro PTR.</span><span class="sxs-lookup"><span data-stu-id="bb02d-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="bb02d-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bb02d-132">www.contoso.com.</span></span> |

<span data-ttu-id="bb02d-133">Dirección IP pública de ejemplo en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="bb02d-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="bb02d-134">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bb02d-134">Additional resources</span></span>
* <span data-ttu-id="bb02d-135">Obtener más información sobre [direcciones IP públicas](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="bb02d-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="bb02d-136">Obtenga más información sobre las [direcciones IP públicas de nivel de instancia](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="bb02d-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="bb02d-137">Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) para la dirección IP pública direcciones.</span><span class="sxs-lookup"><span data-stu-id="bb02d-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

