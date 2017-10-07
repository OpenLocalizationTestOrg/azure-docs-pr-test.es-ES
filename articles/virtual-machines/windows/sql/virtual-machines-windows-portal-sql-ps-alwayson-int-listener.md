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
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Configuración de uno o varios agentes de escucha de grupo de disponibilidad AlwaysOn: Resource Manager
En este tema se muestra cómo llevar a cabo dos tareas:

* Crear un equilibrador de carga interno para grupos de disponibilidad de SQL Server mediante cmdlets de PowerShell
* Agregar adicional IP direcciones tooa equilibrador de carga de más de un grupo de disponibilidad. 

Un agente de escucha del grupo de disponibilidad es un nombre de red virtual que los clientes conectan toofor acceso de base de datos. En máquinas virtuales de Azure, un equilibrador de carga contiene la dirección IP de hello para el agente de escucha de Hola. rutas de equilibrador de carga de Hello tráfico toohello instancia de SQL Server que está escuchando en el puerto de sondeo de Hola. Normalmente, un grupo de disponibilidad usa un equilibrador de carga interno. Un equilibrador de carga interno de Azure puede hospedar una o varias direcciones IP. Cada una usa un puerto de sondeo específico. Este documento se muestra cómo toouse PowerShell toocreate un equilibrador de carga, o agregar direcciones IP tooan equilibrador de carga existente para los grupos de disponibilidad de SQL Server. 

Hola capacidad tooassign varios equilibrador de carga interno de tooan de direcciones IP tooAzure nueva y solo está disponible en el modelo de administrador de recursos. toocomplete esta tarea, deberá toohave un grupo de disponibilidad de SQL Server implementado en máquinas virtuales de Azure en el modelo de administrador de recursos. Las máquinas virtuales de SQL Server debe pertenecer toohello mismo conjunto de disponibilidad. Puede usar hello [plantilla Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically crear grupo de disponibilidad de hello en el Administrador de recursos de Azure. Esta plantilla crea automáticamente el grupo de disponibilidad de hello, incluidos el equilibrador de carga interno de hello automáticamente. Si lo prefiere, puede [configurar manualmente un grupo de disponibilidad AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

En este tema, es necesario que los grupos de disponibilidad ya estén configurados.  

Temas relacionados:

* [Configuración de Grupos de disponibilidad AlwaysOn en la máquina virtual de Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configuración de una conexión entre dos redes virtuales mediante Azure Resource Manager y PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Configurar Firewall de Windows hello
Configurar el acceso de SQL Server de tooallow de Firewall de Windows hello. las reglas de firewall de Hello permiten los puertos de toohello de las conexiones TCP utilizan por instancia de SQL Server de Hola y sondeo del agente de escucha de Hola. Para instrucciones detalladas, consulte [Configurar Firewall de Windows para el acceso al motor de base de datos](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Crear una regla de entrada para hello puerto de SQL Server y para el puerto de sondeo de Hola.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Script de ejemplo: Crear un equilibrador de carga interno con PowerShell
> [!NOTE]
> Si ha creado el grupo de disponibilidad con hello [plantilla Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), equilibrador de carga interno de hello ya se ha creado. 
> 
> 

Hello siguiente script de PowerShell crea un equilibrador de carga interno, configura las reglas de equilibrio de carga de Hola y establece una dirección IP para el equilibrador de carga de Hola. script de Hola toorun, abra Windows PowerShell ISE y pegue el script de Hola en panel de scripts de Hola. Use `Login-AzureRMAccount` toolog en tooPowerShell. Si tiene varias suscripciones de Azure, use `Select-AzureRmSubscription ` suscripción de hello tooset. 

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

## <a name="Add-IP"></a>Script de ejemplo: agregar un equilibrador de carga existente de tooan de dirección IP con PowerShell
toouse más de un grupo de disponibilidad, agregue un equilibrador de carga de toohello de dirección IP adicional. Cada dirección IP requiere su regla de equilibrio de carga, puerto de sondeo y puerto de front-end propios.

Hola front-end Hola puerto es que las aplicaciones utilizan la instancia de SQL Server toohello tooconnect. Direcciones IP para diferentes grupos de disponibilidad pueden use Hola mismo puerto front-end.

> [!NOTE]
> Para los grupos de disponibilidad de SQL Server, cada dirección IP requiere un puerto de sondeo específico. Por ejemplo, si una dirección IP en un equilibrador de carga utiliza el puerto de sondeo 59999, no puede usarlo ninguna otra dirección IP de ese equilibrador de carga.

* Para información sobre los límites del equilibrador de carga, consulte **IP de front-end privada por equilibrador de carga** en [Límites de redes - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Para información acerca de los límites de los grupos de disponibilidad, consulte [Restricciones (grupos de disponibilidad)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Hello siguiente script agrega un nueva IP dirección tooan equilibrador de carga existente. Hola ILB usa el puerto de escucha de Hola para puerto front-end de equilibrio de carga de Hola. Este puerto puede ser Hola que SQL Server está escuchando. Para las instancias predeterminadas de SQL Server, el puerto de hello es 1433. regla para un grupo de disponibilidad de equilibrio de carga de Hello requiere una dirección IP flotante (direct server devuelto) por lo que es el puerto de back-end de Hola Hola igual como puerto front-end de Hola. Actualice las variables de Hola para su entorno. 

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

## <a name="configure-hello-listener"></a>Configurar el agente de escucha de Hola

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Establecer el puerto de escucha de hello en SQL Server Management Studio

1. Inicie SQL Server Management Studio y conéctese toohello de réplica principal.

1. Navegue demasiado**alta disponibilidad de AlwaysOn** | **grupos de disponibilidad** | **los agentes de escucha del grupo de disponibilidad**. 

1. Ahora debería ver el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error. Haga clic en nombre de agente de escucha de Hola y haga clic en **propiedades**.

1. Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (1433 pasaba Hola valor predeterminado), a continuación, haga clic en **Aceptar**.

## <a name="test-hello-connection-toohello-listener"></a>El agente de escucha de prueba Hola conexión toohello

conexión de Hola tootest:

1. RDP tooa SQL Server que se encuentra en hello mismo virtual de red, pero no no réplica Hola propio. Esto puede ser Hola a otro servidor SQL Server en clúster de Hola.

1. Use **sqlcmd** conexión de utilidad tootest Hola. Por ejemplo, Establece la siguiente secuencia de comandos de hello un **sqlcmd** réplica principal de conexión toohello a través de agente de escucha de hello con autenticación de Windows:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Si el agente de escucha de hello usa un puerto distinto de hello predeterminado (1433) de puerto, especifique el puerto hello en la cadena de conexión de Hola. Por ejemplo, hello siguiente comando sqlcmd conecta tooa escucha en el puerto 1435: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hola conexión SQLCMD conecta automáticamente toowhichever instancia de réplica principal de Hola de hosts de SQL Server. 

> [!NOTE]
> Asegúrese de que especifica el puerto de hello está abierto en firewall de Hola de ambos servidores SQL Server. Ambos servidores requieren una regla de entrada para el puerto TCP que usa hello. Consulte [Agregar o editar regla de firewall](http://technet.microsoft.com/library/cc753558.aspx) para más información. 
> 
> 

## <a name="guidelines-and-limitations"></a>Pautas y limitaciones
Tenga en cuenta Hola siguiendo las directrices sobre el agente de escucha de grupo de disponibilidad en Azure con el equilibrador de carga interno:

* Con un equilibrador de carga interno, solo se acceder a agente de escucha de Hola desde dentro de hello misma red virtual.


## <a name="for-more-information"></a>Para obtener más información
Para más información, consulte [Configuración manual de grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>Cmdlets de PowerShell
Usar hello después toocreate de cmdlets de PowerShell un equilibrador de carga interno para máquinas virtuales de Azure.

* [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) crea un equilibrador de carga. 
* [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) crea una configuración IP de front-end para un equilibrador de carga. 
* [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) crea una configuración de regla para un equilibrador de carga. 
* [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) crea una configuración de grupo de direcciones de back-end para un equilibrador de carga. 
* [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) crea una configuración de sondeo para un equilibrador de carga.
* [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) quita un equilibrador de carga de un grupo de recursos de Azure.
