---
title: aaaLoad equilibrio en varias configuraciones de IP en Azure | Documentos de Microsoft
description: Equilibrio de carga entre las configuraciones de IP principales y secundarias.
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="01030-103">Equilibrio de carga en varias configuraciones de IP mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="01030-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01030-104">Portal</span><span class="sxs-lookup"><span data-stu-id="01030-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="01030-105">CLI</span><span class="sxs-lookup"><span data-stu-id="01030-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="01030-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01030-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="01030-107">Este artículo describe cómo aborda toouse equilibrador de carga de Azure con varias IP en una interfaz de red secundaria (NIC).</span><span class="sxs-lookup"><span data-stu-id="01030-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="01030-108">En este escenario, tenemos dos máquinas virtuales que ejecutan Windows. Cada una de ellas cuenta con una NIC principal y otra secundaria.</span><span class="sxs-lookup"><span data-stu-id="01030-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="01030-109">Cada uno de hello secundaria NIC tienen dos configuraciones de IP.</span><span class="sxs-lookup"><span data-stu-id="01030-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="01030-110">Cada máquina virtual hospeda dos sitios web: contoso.com y fabrikam.com. Cada sitio Web está enlazado tooone Hola de configuraciones de IP en la NIC de hello secundaria.</span><span class="sxs-lookup"><span data-stu-id="01030-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="01030-111">Utilizamos el equilibrador de carga Azure tooexpose dos front-end direcciones IP, una para cada sitio Web, toodistribute tráfico toohello respectivo configuración IP para el sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="01030-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="01030-112">Este escenario utiliza Hola el mismo número de puerto a través de front-ends, así como las direcciones IP de back-end del grupo.</span><span class="sxs-lookup"><span data-stu-id="01030-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Imagen del escenario de equilibrio de carga](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="01030-114">Saldo de tooload de pasos en varias configuraciones de IP</span><span class="sxs-lookup"><span data-stu-id="01030-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="01030-115">Siga los pasos de hello debajo de escenario de hello tooachieve descrito en este artículo:</span><span class="sxs-lookup"><span data-stu-id="01030-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="01030-116">Instale Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01030-116">Install Azure PowerShell.</span></span> <span data-ttu-id="01030-117">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="01030-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="01030-118">Crear un grupo de recursos mediante Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="01030-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="01030-119">Para más información, consulte el [Paso 2: Creación de un grupo de recursos](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01030-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="01030-120">[Crear un conjunto de disponibilidad](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="01030-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="01030-121">En este escenario, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="01030-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="01030-122">Siga las instrucciones pasos 3 a 5 [crear una VM de Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artículo creación de hello tooprepare de una máquina virtual con una NIC único.</span><span class="sxs-lookup"><span data-stu-id="01030-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="01030-123">Ejecute paso 6.1 y utilice el siguiente hello en lugar del paso 6.2:</span><span class="sxs-lookup"><span data-stu-id="01030-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="01030-124">Después, complete los pasos 6.3 a 6.8 de [Creación de una máquina virtual Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01030-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="01030-125">Agregue un segundo tooeach de configuración de IP de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="01030-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="01030-126">Siga las instrucciones de hello en [asignar varias direcciones IP toovirtual máquinas](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artículo.</span><span class="sxs-lookup"><span data-stu-id="01030-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="01030-127">Usar hello siguientes opciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="01030-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="01030-128">No es necesario tooassociate Hola secundaria las configuraciones IP con direcciones IP públicas para la finalidad de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="01030-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="01030-129">Editar parte de asociación de hello comando tooremove Hola pública IP.</span><span class="sxs-lookup"><span data-stu-id="01030-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="01030-130">Complete de nuevo los pasos 4 a 6 de este artículo para VM2.</span><span class="sxs-lookup"><span data-stu-id="01030-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="01030-131">Ser seguro tooreplace Hola VM nombre tooVM2 cuando haga esto.</span><span class="sxs-lookup"><span data-stu-id="01030-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="01030-132">Tenga en cuenta que no es necesario toocreate una red virtual para hello segunda máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01030-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="01030-133">Según sus necesidades de uso, puede crear o no una nueva subred.</span><span class="sxs-lookup"><span data-stu-id="01030-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="01030-134">Crear dos direcciones IP públicas y almacenarlos en variables apropiadas Hola tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="01030-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="01030-135">Cree dos configuraciones de IP de front-end:</span><span class="sxs-lookup"><span data-stu-id="01030-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="01030-136">Cree los grupos de direcciones de back-end, un sondeo y las reglas de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="01030-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="01030-137">Una vez que tenga estos recursos creados, cree el equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="01030-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="01030-138">Agregar Hola segundo back-end dirección front-end y grupo de IP configuration tooyour recién creado equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="01030-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="01030-139">comandos de Hello siguiente obtener NIC de hello y, a continuación, agregar que ambas configuraciones IP de cada grupo de direcciones secundaria de back-end toohello NIC de hello equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="01030-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="01030-140">Por último, debe configurar el dirección IP de DNS recursos registros toopoint toohello respectivos front-end de hello equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="01030-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="01030-141">Puede hospedar los dominios en Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="01030-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="01030-142">Para más información sobre el uso de Azure DNS con Load Balancer, consulte [Uso de Azure DNS con otros servicios de Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="01030-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01030-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01030-143">Next steps</span></span>
- <span data-ttu-id="01030-144">Obtener más información acerca de cómo Equilibrio de carga de toocombine services en Azure en [con servicios de equilibrio de carga en Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="01030-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="01030-145">Obtenga información acerca de cómo puede usar varios tipos de registros de Azure toomanage y solucionar problemas de equilibrador de carga en [análisis de registros para el equilibrador de carga de Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="01030-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
