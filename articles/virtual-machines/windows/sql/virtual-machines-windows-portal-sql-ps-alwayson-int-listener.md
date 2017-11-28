---
title: "aaaConfigure siempre en grupo de agentes de escucha disponibilidad – Microsoft Azure | Documentos de Microsoft"
description: "Configurar los agentes de escucha del grupo de disponibilidad en el modelo de Azure Resource Manager hello, usando un equilibrador de carga interno con una o más direcciones IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="b43c5-103">Configuración de uno o varios agentes de escucha de grupo de disponibilidad AlwaysOn: Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b43c5-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="b43c5-104">En este tema se muestra cómo llevar a cabo dos tareas:</span><span class="sxs-lookup"><span data-stu-id="b43c5-104">This topic shows how to:</span></span>

* <span data-ttu-id="b43c5-105">Crear un equilibrador de carga interno para grupos de disponibilidad de SQL Server mediante cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b43c5-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="b43c5-106">Agregar adicional IP direcciones tooa equilibrador de carga de más de un grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="b43c5-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="b43c5-107">Un agente de escucha del grupo de disponibilidad es un nombre de red virtual que los clientes conectan toofor acceso de base de datos.</span><span class="sxs-lookup"><span data-stu-id="b43c5-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="b43c5-108">En máquinas virtuales de Azure, un equilibrador de carga contiene la dirección IP de hello para el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="b43c5-109">rutas de equilibrador de carga de Hello tráfico toohello instancia de SQL Server que está escuchando en el puerto de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="b43c5-110">Normalmente, un grupo de disponibilidad usa un equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="b43c5-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="b43c5-111">Un equilibrador de carga interno de Azure puede hospedar una o varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="b43c5-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="b43c5-112">Cada una usa un puerto de sondeo específico.</span><span class="sxs-lookup"><span data-stu-id="b43c5-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="b43c5-113">Este documento se muestra cómo toouse PowerShell toocreate un equilibrador de carga, o agregar direcciones IP tooan equilibrador de carga existente para los grupos de disponibilidad de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b43c5-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="b43c5-114">Hola capacidad tooassign varios equilibrador de carga interno de tooan de direcciones IP tooAzure nueva y solo está disponible en el modelo de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b43c5-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="b43c5-115">toocomplete esta tarea, deberá toohave un grupo de disponibilidad de SQL Server implementado en máquinas virtuales de Azure en el modelo de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b43c5-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="b43c5-116">Las máquinas virtuales de SQL Server debe pertenecer toohello mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="b43c5-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="b43c5-117">Puede usar hello [plantilla Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically crear grupo de disponibilidad de hello en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b43c5-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="b43c5-118">Esta plantilla crea automáticamente el grupo de disponibilidad de hello, incluidos el equilibrador de carga interno de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b43c5-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="b43c5-119">Si lo prefiere, puede [configurar manualmente un grupo de disponibilidad AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="b43c5-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="b43c5-120">En este tema, es necesario que los grupos de disponibilidad ya estén configurados.</span><span class="sxs-lookup"><span data-stu-id="b43c5-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="b43c5-121">Temas relacionados:</span><span class="sxs-lookup"><span data-stu-id="b43c5-121">Related topics include:</span></span>

* [<span data-ttu-id="b43c5-122">Configuración de Grupos de disponibilidad AlwaysOn en la máquina virtual de Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="b43c5-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="b43c5-123">Configuración de una conexión entre dos redes virtuales mediante Azure Resource Manager y PowerShell</span><span class="sxs-lookup"><span data-stu-id="b43c5-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="b43c5-124">Configurar Firewall de Windows hello</span><span class="sxs-lookup"><span data-stu-id="b43c5-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="b43c5-125">Configurar el acceso de SQL Server de tooallow de Firewall de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b43c5-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="b43c5-126">las reglas de firewall de Hello permiten los puertos de toohello de las conexiones TCP utilizan por instancia de SQL Server de Hola y sondeo del agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="b43c5-127">Para instrucciones detalladas, consulte [Configurar Firewall de Windows para el acceso al motor de base de datos](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="b43c5-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="b43c5-128">Crear una regla de entrada para hello puerto de SQL Server y para el puerto de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="b43c5-129">Script de ejemplo: Crear un equilibrador de carga interno con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b43c5-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="b43c5-130">Si ha creado el grupo de disponibilidad con hello [plantilla Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), equilibrador de carga interno de hello ya se ha creado.</span><span class="sxs-lookup"><span data-stu-id="b43c5-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="b43c5-131">Hello siguiente script de PowerShell crea un equilibrador de carga interno, configura las reglas de equilibrio de carga de Hola y establece una dirección IP para el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="b43c5-132">script de Hola toorun, abra Windows PowerShell ISE y pegue el script de Hola en panel de scripts de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="b43c5-133">Use `Login-AzureRMAccount` toolog en tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="b43c5-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="b43c5-134">Si tiene varias suscripciones de Azure, use `Select-AzureRmSubscription ` suscripción de hello tooset.</span><span class="sxs-lookup"><span data-stu-id="b43c5-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="b43c5-135"><a name="Add-IP"></a>Script de ejemplo: agregar un equilibrador de carga existente de tooan de dirección IP con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b43c5-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="b43c5-136">toouse más de un grupo de disponibilidad, agregue un equilibrador de carga de toohello de dirección IP adicional.</span><span class="sxs-lookup"><span data-stu-id="b43c5-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="b43c5-137">Cada dirección IP requiere su regla de equilibrio de carga, puerto de sondeo y puerto de front-end propios.</span><span class="sxs-lookup"><span data-stu-id="b43c5-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="b43c5-138">Hola front-end Hola puerto es que las aplicaciones utilizan la instancia de SQL Server toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b43c5-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="b43c5-139">Direcciones IP para diferentes grupos de disponibilidad pueden use Hola mismo puerto front-end.</span><span class="sxs-lookup"><span data-stu-id="b43c5-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="b43c5-140">Para los grupos de disponibilidad de SQL Server, cada dirección IP requiere un puerto de sondeo específico.</span><span class="sxs-lookup"><span data-stu-id="b43c5-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="b43c5-141">Por ejemplo, si una dirección IP en un equilibrador de carga utiliza el puerto de sondeo 59999, no puede usarlo ninguna otra dirección IP de ese equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="b43c5-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="b43c5-142">Para información sobre los límites del equilibrador de carga, consulte **IP de front-end privada por equilibrador de carga** en [Límites de redes - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b43c5-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="b43c5-143">Para información acerca de los límites de los grupos de disponibilidad, consulte [Restricciones (grupos de disponibilidad)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="b43c5-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="b43c5-144">Hello siguiente script agrega un nueva IP dirección tooan equilibrador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="b43c5-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="b43c5-145">Hola ILB usa el puerto de escucha de Hola para puerto front-end de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="b43c5-146">Este puerto puede ser Hola que SQL Server está escuchando.</span><span class="sxs-lookup"><span data-stu-id="b43c5-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="b43c5-147">Para las instancias predeterminadas de SQL Server, el puerto de hello es 1433.</span><span class="sxs-lookup"><span data-stu-id="b43c5-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="b43c5-148">regla para un grupo de disponibilidad de equilibrio de carga de Hello requiere una dirección IP flotante (direct server devuelto) por lo que es el puerto de back-end de Hola Hola igual como puerto front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="b43c5-149">Actualice las variables de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="b43c5-149">Update hello variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a><span data-ttu-id="b43c5-150">Configurar el agente de escucha de Hola</span><span class="sxs-lookup"><span data-stu-id="b43c5-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="b43c5-151">Establecer el puerto de escucha de hello en SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b43c5-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="b43c5-152">Inicie SQL Server Management Studio y conéctese toohello de réplica principal.</span><span class="sxs-lookup"><span data-stu-id="b43c5-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="b43c5-153">Navegue demasiado**alta disponibilidad de AlwaysOn** | **grupos de disponibilidad** | **los agentes de escucha del grupo de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="b43c5-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="b43c5-154">Ahora debería ver el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="b43c5-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="b43c5-155">Haga clic en nombre de agente de escucha de Hola y haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b43c5-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="b43c5-156">Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (1433 pasaba Hola valor predeterminado), a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b43c5-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="b43c5-157">El agente de escucha de prueba Hola conexión toohello</span><span class="sxs-lookup"><span data-stu-id="b43c5-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="b43c5-158">conexión de Hola tootest:</span><span class="sxs-lookup"><span data-stu-id="b43c5-158">tootest hello connection:</span></span>

1. <span data-ttu-id="b43c5-159">RDP tooa SQL Server que se encuentra en hello mismo virtual de red, pero no no réplica Hola propio.</span><span class="sxs-lookup"><span data-stu-id="b43c5-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="b43c5-160">Esto puede ser Hola a otro servidor SQL Server en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="b43c5-161">Use **sqlcmd** conexión de utilidad tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="b43c5-162">Por ejemplo, Establece la siguiente secuencia de comandos de hello un **sqlcmd** réplica principal de conexión toohello a través de agente de escucha de hello con autenticación de Windows:</span><span class="sxs-lookup"><span data-stu-id="b43c5-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="b43c5-163">Si el agente de escucha de hello usa un puerto distinto de hello predeterminado (1433) de puerto, especifique el puerto hello en la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b43c5-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="b43c5-164">Por ejemplo, hello siguiente comando sqlcmd conecta tooa escucha en el puerto 1435:</span><span class="sxs-lookup"><span data-stu-id="b43c5-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="b43c5-165">Hola conexión SQLCMD conecta automáticamente toowhichever instancia de réplica principal de Hola de hosts de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b43c5-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="b43c5-166">Asegúrese de que especifica el puerto de hello está abierto en firewall de Hola de ambos servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b43c5-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="b43c5-167">Ambos servidores requieren una regla de entrada para el puerto TCP que usa hello.</span><span class="sxs-lookup"><span data-stu-id="b43c5-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="b43c5-168">Consulte [Agregar o editar regla de firewall](http://technet.microsoft.com/library/cc753558.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="b43c5-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="b43c5-169">Pautas y limitaciones</span><span class="sxs-lookup"><span data-stu-id="b43c5-169">Guidelines and limitations</span></span>
<span data-ttu-id="b43c5-170">Tenga en cuenta Hola siguiendo las directrices sobre el agente de escucha de grupo de disponibilidad en Azure con el equilibrador de carga interno:</span><span class="sxs-lookup"><span data-stu-id="b43c5-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="b43c5-171">Con un equilibrador de carga interno, solo se acceder a agente de escucha de Hola desde dentro de hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="b43c5-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="b43c5-172">Para obtener más información</span><span class="sxs-lookup"><span data-stu-id="b43c5-172">For more information</span></span>
<span data-ttu-id="b43c5-173">Para más información, consulte [Configuración manual de grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="b43c5-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="b43c5-174">Cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b43c5-174">PowerShell cmdlets</span></span>
<span data-ttu-id="b43c5-175">Usar hello después toocreate de cmdlets de PowerShell un equilibrador de carga interno para máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b43c5-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="b43c5-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) crea un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="b43c5-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="b43c5-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) crea una configuración IP de front-end para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="b43c5-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="b43c5-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) crea una configuración de regla para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="b43c5-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="b43c5-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) crea una configuración de grupo de direcciones de back-end para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="b43c5-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="b43c5-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) crea una configuración de sondeo para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="b43c5-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="b43c5-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) quita un equilibrador de carga de un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b43c5-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
