---
title: aaaCreate un orientado a Internet de Azure carga equilibrador - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una conexión a Internet equilibrador de carga en el Administrador de recursos mediante el uso de PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="bfabe-103"><a name="get-started"></a>Creación de un equilibrador de carga orientado a Internet en Resource Manager mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfabe-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfabe-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bfabe-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="bfabe-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfabe-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="bfabe-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bfabe-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="bfabe-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="bfabe-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bfabe-108">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="bfabe-109">También puede [Obtenga información acerca de cómo toocreate una conexión a Internet el equilibrador de carga utilizando el modelo de implementación clásica de hello](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bfabe-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="bfabe-110">Implementar soluciones de hello mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfabe-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="bfabe-111">Hola procedimientos siguientes explica cómo toocreate una conexión a Internet el equilibrador de carga mediante el Administrador de recursos de Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfabe-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="bfabe-112">Con el Administrador de recursos de Azure, cada recurso se crea y configura individualmente y, a continuación, reunir toocreate un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfabe-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="bfabe-113">Debe crear y configurar Hola después objetos toodeploy un equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="bfabe-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="bfabe-114">Configuración de direcciones IP front-end: contiene direcciones IP públicas (PIP) para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="bfabe-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="bfabe-115">Grupo de direcciones de back-end: contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfabe-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="bfabe-116">Las reglas de equilibrio de carga: contiene reglas que se asignan a un puerto público en el puerto de tooa de equilibrador de carga de hello en grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="bfabe-117">Reglas NAT de entrada: contiene reglas que se asignan a un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="bfabe-118">Sondeos: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquina virtual en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="bfabe-119">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bfabe-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="bfabe-120">Configurar PowerShell toouse el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="bfabe-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="bfabe-121">Asegúrese de que dispone de hello última versión de producción del módulo de Azure Resource Manager Hola de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bfabe-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="bfabe-122">Inicie sesión en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bfabe-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="bfabe-123">Escriba sus credenciales cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="bfabe-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="bfabe-124">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="bfabe-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="bfabe-125">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfabe-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="bfabe-126">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bfabe-126">Create a resource group.</span></span> <span data-ttu-id="bfabe-127">(Si utiliza un grupo de recursos existente, puede omitir este paso).</span><span class="sxs-lookup"><span data-stu-id="bfabe-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="bfabe-128">Crear una red virtual y una dirección IP pública para el grupo de direcciones IP de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="bfabe-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="bfabe-129">Cree una subred y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="bfabe-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="bfabe-130">Crear un Azure público recurso de dirección IP, denominado **PublicIP**, toobe utilizado por un grupo IP front-end con el nombre DNS de hello **loadbalancernrp.westus.cloudapp.azure.com**. Hola siguiente comando usa Hola tipo de asignación estático.</span><span class="sxs-lookup"><span data-stu-id="bfabe-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="bfabe-131">equilibrador de carga de Hello usa la etiqueta de Hola de dominio de la dirección IP pública de hello como prefijo para su FQDN.</span><span class="sxs-lookup"><span data-stu-id="bfabe-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="bfabe-132">Esto es diferente del modelo de implementación clásica de hello, que utiliza el servicio de nube de hello como Hola FQDN del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfabe-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="bfabe-133">En este ejemplo, hello FQDN es **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="bfabe-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="bfabe-134">Creación de un grupo de direcciones IP front-end y un grupo de direcciones back-end</span><span class="sxs-lookup"><span data-stu-id="bfabe-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="bfabe-135">Cree un grupo IP front-end denominado **front-end de LB** que usa hello **PublicIp** recursos.</span><span class="sxs-lookup"><span data-stu-id="bfabe-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="bfabe-136">Cree un grupo de direcciones de back-end llamado **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="bfabe-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="bfabe-137">Creación de reglas NAT, una regla de equilibrador de carga, un sondeo y un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="bfabe-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="bfabe-138">Este ejemplo crea Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bfabe-138">This example creates hello following items:</span></span>

* <span data-ttu-id="bfabe-139">Un tootranslate de regla NAT entrante todos tráfico en puerto 3441 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="bfabe-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="bfabe-140">Un tootranslate de regla NAT entrante todos tráfico en puerto 3442 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="bfabe-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="bfabe-141">Un estado de mantenimiento de sondeo regla toocheck hello en una página denominada **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="bfabe-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="bfabe-142">Un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="bfabe-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="bfabe-143">Un equilibrador de carga que usa todos estos objetos.</span><span class="sxs-lookup"><span data-stu-id="bfabe-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="bfabe-144">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bfabe-144">Use these steps:</span></span>

1. <span data-ttu-id="bfabe-145">Crear hello las reglas NAT.</span><span class="sxs-lookup"><span data-stu-id="bfabe-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="bfabe-146">Cree un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="bfabe-146">Create a health probe.</span></span> <span data-ttu-id="bfabe-147">Hay dos tooconfigure formas un sondeo:</span><span class="sxs-lookup"><span data-stu-id="bfabe-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="bfabe-148">Sondeo HTTP</span><span class="sxs-lookup"><span data-stu-id="bfabe-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="bfabe-149">Sondeo TCP</span><span class="sxs-lookup"><span data-stu-id="bfabe-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="bfabe-150">Cree una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfabe-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="bfabe-151">Crea el equilibrador de carga de hello mediante objetos de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bfabe-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="bfabe-152">Cree tarjetas NIC</span><span class="sxs-lookup"><span data-stu-id="bfabe-152">Create NICs</span></span>

<span data-ttu-id="bfabe-153">Crear interfaces de red (o modificar los existentes) y después asociar reglas de tooNAT, reglas de equilibrador de carga y sondeos:</span><span class="sxs-lookup"><span data-stu-id="bfabe-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="bfabe-154">Obtener la red virtual de hello y una subred de red virtual, donde hello NIC necesitan toobe creado.</span><span class="sxs-lookup"><span data-stu-id="bfabe-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="bfabe-155">Cree una NIC denominada **nic1 de carga equilibrada puede**y lo asocia a la primera regla NAT de Hola y el grupo de direcciones de back-end de primer (y único) de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="bfabe-156">Cree una NIC denominada **nic2 de carga equilibrada puede**y lo asocia a la segunda regla NAT de Hola y el grupo de direcciones de back-end de primer (y único) de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="bfabe-157">Compruebe Hola NIC.</span><span class="sxs-lookup"><span data-stu-id="bfabe-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="bfabe-158">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="bfabe-158">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
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
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="bfabe-159">Hola de uso `Add-AzureRmVMNetworkInterface` cmdlet tooassign Hola NIC toodifferent máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bfabe-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="bfabe-160">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bfabe-160">Create a virtual machine</span></span>

<span data-ttu-id="bfabe-161">Para instrucciones sobre cómo crear una máquina virtual y asignar una NIC, consulte el artículo sobre cómo [crear una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bfabe-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="bfabe-162">Agregar equilibrador de carga de toohello de interfaz de red de Hola</span><span class="sxs-lookup"><span data-stu-id="bfabe-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="bfabe-163">Recuperar el equilibrador de carga de Hola de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfabe-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="bfabe-164">Cargar recursos de equilibrador de carga de hello en una variable (si aún no lo ha hecho todavía).</span><span class="sxs-lookup"><span data-stu-id="bfabe-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="bfabe-165">Hola variable se denomina **$lb**. Usar hello mismos nombres de recurso de equilibrador de carga de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bfabe-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="bfabe-166">Variable de tooa de configuración de back-end de Hola de carga.</span><span class="sxs-lookup"><span data-stu-id="bfabe-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="bfabe-167">Cargar la interfaz de red de hello ya creado en una variable.</span><span class="sxs-lookup"><span data-stu-id="bfabe-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="bfabe-168">nombre de variable de Hello es **$nic**.</span><span class="sxs-lookup"><span data-stu-id="bfabe-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="bfabe-169">Hello nombre de la interfaz de red es Hola misma de hello ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="bfabe-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="bfabe-170">Cambiar configuración de back-end de hello en la interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="bfabe-171">Guardar el objeto de interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfabe-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="bfabe-172">Después de una interfaz de red se agrega el grupo de back-end de equilibradores de carga de toohello, comienza a recibir tráfico de red en función de reglas de equilibrio de carga de Hola para ese recurso de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfabe-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="bfabe-173">Actualización de un equilibrador de carga existente</span><span class="sxs-lookup"><span data-stu-id="bfabe-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="bfabe-174">Equilibrador de carga mediante el uso de Hola Hola ejemplo anterior, asigne una variable de toohello del objeto de equilibrador de carga **$slb** utilizando `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="bfabe-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="bfabe-175">En el siguiente ejemplo de Hola, agregará una regla NAT de entrada--mediante el puerto 81 en grupo de servidores front-end de Hola y puerto 8181 para grupo de back-end de hello--tooan equilibrador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="bfabe-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="bfabe-176">Guardar la nueva configuración de hello mediante `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="bfabe-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="bfabe-177">Elimine un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="bfabe-177">Remove a load balancer</span></span>

<span data-ttu-id="bfabe-178">Use el comando de hello `Remove-AzureLoadBalancer` toodelete un equilibrador de carga previamente creada denominado **NRP LB** en un grupo de recursos denominado **NRP RG**.</span><span class="sxs-lookup"><span data-stu-id="bfabe-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="bfabe-179">Puede usar el modificador opcional hello **-Force** tooavoid mensaje de Hola para su eliminación.</span><span class="sxs-lookup"><span data-stu-id="bfabe-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfabe-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfabe-180">Next steps</span></span>

[<span data-ttu-id="bfabe-181">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="bfabe-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="bfabe-182">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="bfabe-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="bfabe-183">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="bfabe-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
