## <a name="traffic-manager-profile"></a><span data-ttu-id="3600f-101">Perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="3600f-101">Traffic Manager Profile</span></span>
<span data-ttu-id="3600f-102">El Administrador de tráfico y su recurso de extremo secundario permiten tooendpoints de enrutamiento de DNS en Azure y fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="3600f-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="3600f-103">Esta distribución de tráfico se rige por los métodos de directivas de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="3600f-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="3600f-104">Traffic manager también permite supervisa toobe de estado de punto de conexión y tráfico desviado adecuadamente basadas en el estado de saludo de un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="3600f-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="3600f-105">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3600f-105">Property</span></span> | <span data-ttu-id="3600f-106">Descripción</span><span class="sxs-lookup"><span data-stu-id="3600f-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3600f-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="3600f-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="3600f-108">los valores posibles son *Performance*, *Weighted* y *Priority*</span><span class="sxs-lookup"><span data-stu-id="3600f-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="3600f-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="3600f-109">**dnsConfig**</span></span> |<span data-ttu-id="3600f-110">FQDN para el perfil de Hola</span><span class="sxs-lookup"><span data-stu-id="3600f-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="3600f-111">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="3600f-111">**Protocol**</span></span> |<span data-ttu-id="3600f-112">protocolo de supervisión, los valores posibles son *HTTP* y *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="3600f-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="3600f-113">**Puerto**</span><span class="sxs-lookup"><span data-stu-id="3600f-113">**Port**</span></span> |<span data-ttu-id="3600f-114">puerto de supervisión</span><span class="sxs-lookup"><span data-stu-id="3600f-114">monitoring port</span></span> |
| <span data-ttu-id="3600f-115">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="3600f-115">**Path**</span></span> |<span data-ttu-id="3600f-116">ruta de acceso de supervisión</span><span class="sxs-lookup"><span data-stu-id="3600f-116">monitoring path</span></span> |
| <span data-ttu-id="3600f-117">**Extremos**</span><span class="sxs-lookup"><span data-stu-id="3600f-117">**Endpoints**</span></span> |<span data-ttu-id="3600f-118">contenedor de recursos de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="3600f-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="3600f-119">Extremo</span><span class="sxs-lookup"><span data-stu-id="3600f-119">Endpoint</span></span>
<span data-ttu-id="3600f-120">Un extremo es un recurso secundario de un perfil de Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="3600f-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="3600f-121">Representa un servicio o se distribuye el tráfico de usuario de web extremo toowhich basándose en la directiva de hello configurado en hello recursos de perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="3600f-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="3600f-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3600f-122">Property</span></span> | <span data-ttu-id="3600f-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="3600f-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3600f-124">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="3600f-124">**Type**</span></span> |<span data-ttu-id="3600f-125">Hola tipo de punto de conexión de hello, los valores posibles son *punto final de Azure*, *extremo externo*, y *extremo anidados*</span><span class="sxs-lookup"><span data-stu-id="3600f-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="3600f-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="3600f-126">**targetResourceId**</span></span> |<span data-ttu-id="3600f-127">dirección IP pública de servicio o punto de conexión web.</span><span class="sxs-lookup"><span data-stu-id="3600f-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="3600f-128">Puede tratarse de un extremo de Azure o uno externo.</span><span class="sxs-lookup"><span data-stu-id="3600f-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="3600f-129">**Peso**</span><span class="sxs-lookup"><span data-stu-id="3600f-129">**Weight**</span></span> |<span data-ttu-id="3600f-130">ponderación del punto de conexión usada en la administración del tráfico.</span><span class="sxs-lookup"><span data-stu-id="3600f-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="3600f-131">**Prioridad**</span><span class="sxs-lookup"><span data-stu-id="3600f-131">**Priority**</span></span> |<span data-ttu-id="3600f-132">prioridad de punto de conexión de hello, toodefine usa una acción de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="3600f-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="3600f-133">Ejemplo de Administrador de tráfico en formato Json:</span><span class="sxs-lookup"><span data-stu-id="3600f-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="3600f-134">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3600f-134">Additional resources</span></span>
<span data-ttu-id="3600f-135">Para más información, lea la [documentación de API de REST para el Administrador de tráfico](https://msdn.microsoft.com/library/azure/mt163664.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3600f-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

