---
title: aaaCreate un interno de Azure carga equilibrador - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador mediante PowerShell en el Administrador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="923c2-103">Creación del equilibrador de carga interno con PowerShell</span><span class="sxs-lookup"><span data-stu-id="923c2-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="923c2-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="923c2-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="923c2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="923c2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="923c2-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="923c2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="923c2-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="923c2-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="923c2-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="923c2-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="923c2-109">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="923c2-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="923c2-110">Hola pasos explica cómo toocreate un interno cargar equilibrador con el Administrador de recursos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="923c2-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="923c2-111">Con el Administrador de recursos de Azure, Hola elementos toocreate un equilibrador de carga interno se configuran individualmente y, a continuación, se combinan toocreate un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="923c2-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="923c2-112">Necesita toocreate y configurar Hola después objetos toodeploy un equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="923c2-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="923c2-113">Delante de la configuración de IP final: configurar la dirección IP privada de hello para el tráfico de red entrante</span><span class="sxs-lookup"><span data-stu-id="923c2-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="923c2-114">Grupo de direcciones de back-end - configurará las interfaces de red de Hola que recibirán tráfico con equilibrio de carga de hello procedentes de grupo de direcciones IP de front-end</span><span class="sxs-lookup"><span data-stu-id="923c2-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="923c2-115">Reglas de equilibrio de carga: equilibrador de carga de origen y configuración del puerto local para saludo.</span><span class="sxs-lookup"><span data-stu-id="923c2-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="923c2-116">Sondea - configura el sondeo de estado de mantenimiento de Hola para instancias de máquina Virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="923c2-117">Reglas NAT de entrada: se configura el acceso de toodirectly de reglas de puerto de hello entre instancias de máquina Virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="923c2-118">Para obtener más información acerca de los componentes del equilibrador de carga con el Administrador de recursos de Azure en [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="923c2-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="923c2-119">Hello pasos siguientes se explica cómo tooconfigure un equilibrador de carga entre dos máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="923c2-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="923c2-120">El programa de instalación PowerShell toouse el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="923c2-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="923c2-121">Asegúrese de que tiene Hola última versión de producción de hello Azure módulo de PowerShell y tengan PowerShell configurar correctamente tooaccess su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="923c2-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="923c2-122">Paso 1</span><span class="sxs-lookup"><span data-stu-id="923c2-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="923c2-123">Paso 2</span><span class="sxs-lookup"><span data-stu-id="923c2-123">Step 2</span></span>

<span data-ttu-id="923c2-124">Compruebe las suscripciones de hello para la cuenta de hello</span><span class="sxs-lookup"><span data-stu-id="923c2-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="923c2-125">Es posible que tooAuthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="923c2-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="923c2-126">Paso 3</span><span class="sxs-lookup"><span data-stu-id="923c2-126">Step 3</span></span>

<span data-ttu-id="923c2-127">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="923c2-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="923c2-128">Creación de un grupo de recursos para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="923c2-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="923c2-129">Creación de un grupo de recursos (omitir este paso si se usa un grupo de recursos existente)</span><span class="sxs-lookup"><span data-stu-id="923c2-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="923c2-130">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="923c2-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="923c2-131">Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="923c2-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="923c2-132">Asegúrese de que todos los comandos toocreate que se va a usar un equilibrador de carga Hola mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="923c2-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="923c2-133">Hola ejemplo anterior crea un grupo de recursos denominado "NRP-RG" y la ubicación "West US".</span><span class="sxs-lookup"><span data-stu-id="923c2-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="923c2-134">Creación de una red virtual y una dirección IP privada para el grupo de IP front-end</span><span class="sxs-lookup"><span data-stu-id="923c2-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="923c2-135">Crea una subred de red virtual de Hola y asigna toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="923c2-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="923c2-136">Cree una red virtual:</span><span class="sxs-lookup"><span data-stu-id="923c2-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="923c2-137">Crea la red virtual de Hola y agrega la red virtual de hello subred toohello lb subred ser NRPVNet y asigna toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="923c2-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="923c2-138">Creación de un grupo de direcciones IP front-end y un grupo de direcciones back-end</span><span class="sxs-lookup"><span data-stu-id="923c2-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="923c2-139">Cómo configurar un grupo IP de front-end para Hola entrante cargar tráfico de red de equilibrador y tráfico de equilibrio de carga de back-end dirección grupo tooreceive Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="923c2-140">Paso 1</span><span class="sxs-lookup"><span data-stu-id="923c2-140">Step 1</span></span>

<span data-ttu-id="923c2-141">Cree un grupo IP de front-end con la dirección IP privada de hello 10.0.2.5 para hello subred 10.0.2.0/24 que será el extremo del tráfico de red entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="923c2-142">Paso 2</span><span class="sxs-lookup"><span data-stu-id="923c2-142">Step 2</span></span>

<span data-ttu-id="923c2-143">Configurar un grupo de direcciones de back-end utiliza tooreceive el tráfico entrante de grupo de direcciones IP de front-end:</span><span class="sxs-lookup"><span data-stu-id="923c2-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="923c2-144">Creación de reglas de equilibrio de carga, reglas NAT, sondeos y el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="923c2-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="923c2-145">Después de crear el grupo de direcciones IP de front-end de Hola y el grupo de direcciones de back-end de hello, necesitará las reglas de hello toocreate que pertenecerán el recurso de equilibrador de carga de toohello:</span><span class="sxs-lookup"><span data-stu-id="923c2-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="923c2-146">Paso 1</span><span class="sxs-lookup"><span data-stu-id="923c2-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="923c2-147">ejemplo de Hola anterior está creando Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="923c2-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="923c2-148">Regla NAT que todos los entrantes tráfico tooport 3441 irá tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="923c2-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="923c2-149">una segunda regla NAT que todos los entrantes tráfico tooport 3442 irá tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="923c2-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="923c2-150">una regla de equilibrador de carga que se cargará equilibrar todo el tráfico entrante en el puerto de puerto público 80 toolocal 80 en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="923c2-151">una regla de sondeo que comprobará el estado de mantenimiento de Hola de ruta de acceso "HealthProbe.aspx"</span><span class="sxs-lookup"><span data-stu-id="923c2-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="923c2-152">Paso 2</span><span class="sxs-lookup"><span data-stu-id="923c2-152">Step 2</span></span>

<span data-ttu-id="923c2-153">Crear el equilibrador de carga de hello sumar todos los objetos (reglas NAT, reglas de equilibrador de carga, las configuraciones de sondeo):</span><span class="sxs-lookup"><span data-stu-id="923c2-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="923c2-154">Creación de interfaces de red</span><span class="sxs-lookup"><span data-stu-id="923c2-154">Create network interfaces</span></span>

<span data-ttu-id="923c2-155">Después de crear el equilibrador de carga interno de hello, debe definir qué interfaces de red va a recibir Hola entrante con equilibrio de carga tráfico de red, las reglas de NAT y sondeo.</span><span class="sxs-lookup"><span data-stu-id="923c2-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="923c2-156">interfaz de red de Hello en este caso se configura individualmente y se puede asignar máquinas virtuales de tooa más adelante.</span><span class="sxs-lookup"><span data-stu-id="923c2-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="923c2-157">Paso 1</span><span class="sxs-lookup"><span data-stu-id="923c2-157">Step 1</span></span>

<span data-ttu-id="923c2-158">Obtener recursos de hello virtuales interfaces de red de toocreate de red y la subred:</span><span class="sxs-lookup"><span data-stu-id="923c2-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="923c2-159">Este paso crea una interfaz de red que pertenecerán toohello grupo de back-end de equilibradores de carga y asociar la primera regla NAT de Hola para RDP para esta interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="923c2-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="923c2-160">Paso 2</span><span class="sxs-lookup"><span data-stu-id="923c2-160">Step 2</span></span>

<span data-ttu-id="923c2-161">Cree una segunda interfaz de red llamada LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="923c2-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="923c2-162">Este paso crea una segunda interfaz de red, asignar toohello mismo equilibrador de carga volver Finalizar grupo y asociar la segunda regla NAT Hola creado para RDP:</span><span class="sxs-lookup"><span data-stu-id="923c2-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="923c2-163">resultado final de Hello mostrará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="923c2-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="923c2-164">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="923c2-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="923c2-165">Paso 3</span><span class="sxs-lookup"><span data-stu-id="923c2-165">Step 3</span></span>

<span data-ttu-id="923c2-166">Usar comandos hello AzureRmVMNetworkInterface agregar hello tooassign NIC virtual tooa máquina.</span><span class="sxs-lookup"><span data-stu-id="923c2-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="923c2-167">Puede encontrar Hola toocreate instrucciones paso a paso una máquina virtual y asigne tooa NIC siguiendo Hola documentación: [crear una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="923c2-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="923c2-168">Agregar la interfaz de red de Hola</span><span class="sxs-lookup"><span data-stu-id="923c2-168">Add hello network interface</span></span>

<span data-ttu-id="923c2-169">Si ya tiene una máquina virtual creada, puede agregar la interfaz de red de Hola con hello siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="923c2-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="923c2-170">Paso 1</span><span class="sxs-lookup"><span data-stu-id="923c2-170">Step 1</span></span>

<span data-ttu-id="923c2-171">Cargar recursos de equilibrador de carga de hello en una variable (si aún no lo ha hecho todavía).</span><span class="sxs-lookup"><span data-stu-id="923c2-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="923c2-172">variable de saludo que se utiliza es $lb llamado y Hola uso mismos nombres de recurso de equilibrador de carga de hello creados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="923c2-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="923c2-173">Paso 2</span><span class="sxs-lookup"><span data-stu-id="923c2-173">Step 2</span></span>

<span data-ttu-id="923c2-174">Variable de tooa de configuración de carga Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="923c2-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="923c2-175">Paso 3</span><span class="sxs-lookup"><span data-stu-id="923c2-175">Step 3</span></span>

<span data-ttu-id="923c2-176">Cargar la interfaz de red de hello ya creado en una variable.</span><span class="sxs-lookup"><span data-stu-id="923c2-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="923c2-177">nombre de variable de Hello utilizado es $ tarjeta NIC.</span><span class="sxs-lookup"><span data-stu-id="923c2-177">hello variable name used is $nic.</span></span> <span data-ttu-id="923c2-178">nombre de la interfaz de red Hello usa es Hola igual de ejemplo de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="923c2-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="923c2-179">Paso 4</span><span class="sxs-lookup"><span data-stu-id="923c2-179">Step 4</span></span>

<span data-ttu-id="923c2-180">Cambiar configuración de back-end de hello en la interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="923c2-181">Paso 5</span><span class="sxs-lookup"><span data-stu-id="923c2-181">Step 5</span></span>

<span data-ttu-id="923c2-182">Guardar el objeto de interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="923c2-183">Después de una interfaz de red se agrega el grupo de back-end de equilibradores de carga de toohello, comienza a recibir tráfico de red en función de las reglas para ese recurso de equilibrador de carga de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="923c2-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="923c2-184">Actualización de un equilibrador de carga existente</span><span class="sxs-lookup"><span data-stu-id="923c2-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="923c2-185">Paso 1</span><span class="sxs-lookup"><span data-stu-id="923c2-185">Step 1</span></span>
<span data-ttu-id="923c2-186">Con el equilibrador de carga de Hola de ejemplo de Hola anterior, asignar $slb mediante Get-AzureRmLoadBalancer de toovariable de objeto de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="923c2-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="923c2-187">Paso 2</span><span class="sxs-lookup"><span data-stu-id="923c2-187">Step 2</span></span>

<span data-ttu-id="923c2-188">En el siguiente ejemplo de Hola, agregará una nueva regla de NAT de entrada mediante el puerto 81 de front-end de Hola y puerto 8181 para la copia de hello finalizar equilibrador de carga existente de grupo tooan</span><span class="sxs-lookup"><span data-stu-id="923c2-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="923c2-189">Paso 3</span><span class="sxs-lookup"><span data-stu-id="923c2-189">Step 3</span></span>

<span data-ttu-id="923c2-190">Guardar configuración nueva de hello mediante Set-AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="923c2-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="923c2-191">Elimine un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="923c2-191">Remove a load balancer</span></span>

<span data-ttu-id="923c2-192">Usar Hola comando Remove-AzureRmLoadBalancer toodelete un equilibrador de carga creada anteriormente con el nombre "NRP-LB" en un grupo de recursos denominado "NRP-RG"</span><span class="sxs-lookup"><span data-stu-id="923c2-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="923c2-193">Puede usar Hola opcional cambiar - Force tooavoid Hola para su eliminación.</span><span class="sxs-lookup"><span data-stu-id="923c2-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="923c2-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="923c2-194">Next steps</span></span>

[<span data-ttu-id="923c2-195">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="923c2-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="923c2-196">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="923c2-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
