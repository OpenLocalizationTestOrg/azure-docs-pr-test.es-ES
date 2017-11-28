---
title: "Creación de un equilibrador de carga con conexión a Internet de Azure: PowerShell | Microsoft Docs"
description: Aprenda a crear un equilibrador de carga accesible desde Internet en Resource Manager con PowerShell
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
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="249af-103"><a name="get-started"></a>Creación de un equilibrador de carga orientado a Internet en Resource Manager mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="249af-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="249af-104">Portal</span><span class="sxs-lookup"><span data-stu-id="249af-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="249af-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="249af-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="249af-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="249af-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="249af-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="249af-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="249af-108">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="249af-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="249af-109">También puede [aprender a crear un equilibrador de carga con acceso desde Internet mediante el modelo de implementación clásica](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="249af-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="249af-110">Implementación de la solución mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="249af-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="249af-111">Los siguientes procedimientos explican cómo crear un equilibrador de carga accesible desde Internet mediante Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="249af-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="249af-112">Con Azure Resource Manager, cada recurso se crea y configura de forma individual, y luego se juntan para crear un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="249af-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="249af-113">Para implementar un equilibrador de carga, debe crear y configurar los siguientes objetos:</span><span class="sxs-lookup"><span data-stu-id="249af-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="249af-114">Configuración de direcciones IP front-end: contiene direcciones IP públicas (PIP) para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="249af-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="249af-115">Grupo de direcciones de back-end: contiene interfaces de red (NIC) para que las máquinas virtuales reciban tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="249af-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="249af-116">Reglas de equilibrio de carga: contiene reglas que asignan un puerto público en el equilibrador de carga a un puerto del grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="249af-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="249af-117">Reglas NAT de entrada: contiene reglas que asignan un puerto público en el equilibrador de carga a un puerto de una máquina virtual específica en el grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="249af-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="249af-118">Sondeos: contiene sondeos de estado que se usan para comprobar la disponibilidad de las instancias de máquina virtual del grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="249af-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="249af-119">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="249af-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="249af-120">Configuración de PowerShell para usar Resource Manager</span><span class="sxs-lookup"><span data-stu-id="249af-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="249af-121">Asegúrese de que tiene la última versión de producción del módulo Azure Resource Manager para PowerShell:</span><span class="sxs-lookup"><span data-stu-id="249af-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="249af-122">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="249af-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="249af-123">Escriba sus credenciales cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="249af-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="249af-124">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="249af-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="249af-125">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="249af-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="249af-126">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="249af-126">Create a resource group.</span></span> <span data-ttu-id="249af-127">(Si utiliza un grupo de recursos existente, puede omitir este paso).</span><span class="sxs-lookup"><span data-stu-id="249af-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="249af-128">Creación de una red virtual y una dirección IP pública para el grupo de direcciones IP front-end</span><span class="sxs-lookup"><span data-stu-id="249af-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="249af-129">Cree una subred y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="249af-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="249af-130">Cree un recurso de dirección IP pública de Azure, llamado **PublicIP**, para que lo use un grupo de direcciones IP front-end con el nombre DNS **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="249af-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="249af-131">El siguiente comando usa el tipo de asignación estática.</span><span class="sxs-lookup"><span data-stu-id="249af-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="249af-132">El equilibrador de carga usa la etiqueta de dominio de la dirección IP pública como prefijo para su FQDN.</span><span class="sxs-lookup"><span data-stu-id="249af-132">The load balancer uses the domain label of the public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="249af-133">Esto es diferente del modelo de implementación clásica, que usa el servicio en la nube como FQDN del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="249af-133">This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.</span></span>
   > <span data-ttu-id="249af-134">En este ejemplo, el FQDN es **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="249af-134">In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="249af-135">Creación de un grupo de direcciones IP front-end y un grupo de direcciones back-end</span><span class="sxs-lookup"><span data-stu-id="249af-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="249af-136">Cree un grupo de direcciones IP front-end llamado **LB-Frontend** que use el recurso **PublicIp**.</span><span class="sxs-lookup"><span data-stu-id="249af-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="249af-137">Cree un grupo de direcciones de back-end llamado **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="249af-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="249af-138">Creación de reglas NAT, una regla de equilibrador de carga, un sondeo y un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="249af-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="249af-139">En este ejemplo se crean los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="249af-139">This example creates the following items:</span></span>

* <span data-ttu-id="249af-140">Una regla NAT para trasladar todo el tráfico entrante del puerto 3441 al puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="249af-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="249af-141">Una regla NAT para trasladar todo el tráfico entrante del puerto 3442 al puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="249af-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="249af-142">Una regla de sondeo para comprobar el estado de mantenimiento en una página llamada **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="249af-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="249af-143">Una regla de equilibrador de carga para equilibrar todo el tráfico entrante del puerto 80 al puerto 80 en las direcciones del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="249af-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="249af-144">Un equilibrador de carga que usa todos estos objetos.</span><span class="sxs-lookup"><span data-stu-id="249af-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="249af-145">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="249af-145">Use these steps:</span></span>

1. <span data-ttu-id="249af-146">Cree las reglas NAT.</span><span class="sxs-lookup"><span data-stu-id="249af-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="249af-147">Cree un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="249af-147">Create a health probe.</span></span> <span data-ttu-id="249af-148">Hay dos formas de configurar un sondeo:</span><span class="sxs-lookup"><span data-stu-id="249af-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="249af-149">Sondeo HTTP</span><span class="sxs-lookup"><span data-stu-id="249af-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="249af-150">Sondeo TCP</span><span class="sxs-lookup"><span data-stu-id="249af-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="249af-151">Cree una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="249af-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="249af-152">Cree el equilibrador de carga mediante los objetos creados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="249af-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="249af-153">Cree tarjetas NIC</span><span class="sxs-lookup"><span data-stu-id="249af-153">Create NICs</span></span>

<span data-ttu-id="249af-154">Cree interfaces de red (o modifique las existentes) y asócielas a reglas NAT, reglas de equilibrador de carga y sondeos:</span><span class="sxs-lookup"><span data-stu-id="249af-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="249af-155">Obtenga la red virtual y una subred de red virtual, donde deben crearse las NIC.</span><span class="sxs-lookup"><span data-stu-id="249af-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="249af-156">Cree una NIC llamada **lb-nic1-be**y asóciela con la primera regla NAT y el primer (y único) grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="249af-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="249af-157">Cree una NIC llamada **lb-nic2-be**y asóciela con la segunda regla NAT y el primer (y único) grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="249af-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="249af-158">Compruebe las tarjetas NIC.</span><span class="sxs-lookup"><span data-stu-id="249af-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="249af-159">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="249af-159">Expected output:</span></span>

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

5. <span data-ttu-id="249af-160">Use el cmdlet `Add-AzureRmVMNetworkInterface` para asignar las tarjetas NIC a distintas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="249af-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="249af-161">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="249af-161">Create a virtual machine</span></span>

<span data-ttu-id="249af-162">Para instrucciones sobre cómo crear una máquina virtual y asignar una NIC, consulte el artículo sobre cómo [crear una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="249af-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="249af-163">Adición de la interfaz de red al equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="249af-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="249af-164">Recupere el equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="249af-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="249af-165">Cargue el recurso de equilibrador de carga en una variable (si no lo ha hecho todavía).</span><span class="sxs-lookup"><span data-stu-id="249af-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="249af-166">La variable se denomina **$lb**. Use los mismos nombres del recurso de equilibrador de carga que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="249af-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="249af-167">Cargue la configuración de back-end en una variable.</span><span class="sxs-lookup"><span data-stu-id="249af-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="249af-168">Cargue la interfaz de red ya creada en una variable.</span><span class="sxs-lookup"><span data-stu-id="249af-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="249af-169">El nombre de la variable es **$nic**.</span><span class="sxs-lookup"><span data-stu-id="249af-169">The variable name is **$nic**.</span></span> <span data-ttu-id="249af-170">El nombre de la interfaz de red es el mismo que el del ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="249af-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="249af-171">Cambie la configuración de back-end en la interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="249af-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="249af-172">Guarde el objeto de interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="249af-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="249af-173">Después de agregar una interfaz de red al grupo de back-end del equilibrador de carga, comienza la recepción del tráfico de red según la reglas de equilibrio de carga para ese recurso de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="249af-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="249af-174">Actualización de un equilibrador de carga existente</span><span class="sxs-lookup"><span data-stu-id="249af-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="249af-175">Con el equilibrador de carga del ejemplo anterior, asigne un objeto de equilibrador de carga a la variable **$slb** con `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="249af-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="249af-176">En el ejemplo siguiente, agregará una nueva regla NAT de entrada, mediante el puerto 81 en el grupo de front-end y el puerto 8181 en el grupo de back-end, a un equilibrador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="249af-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="249af-177">Guarde la nueva configuración mediante `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="249af-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="249af-178">Elimine un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="249af-178">Remove a load balancer</span></span>

<span data-ttu-id="249af-179">Use el comando`Remove-AzureLoadBalancer` para eliminar un equilibrador de carga creado previamente denominado **NRP-LB** en un grupo de recursos llamado **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="249af-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="249af-180">Puede usar el modificador opcional **-Force** para evitar la solicitud de eliminación.</span><span class="sxs-lookup"><span data-stu-id="249af-180">You can use the optional switch **-Force** to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="249af-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="249af-181">Next steps</span></span>

[<span data-ttu-id="249af-182">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="249af-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="249af-183">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="249af-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="249af-184">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="249af-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
