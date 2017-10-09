---
title: "aaaCreate una configuración de múltiples SID de SAP en Azure | Documentos de Microsoft"
description: "Configuración de múltiples SID de guía toohigh disponibilidad SAP NetWeaver en máquinas virtuales de Windows"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>Creación de una configuración de varios SID de SAP NetWeaver

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

En septiembre de 2016, Microsoft publicó una característica con la que puede administrar varias direcciones IP virtuales mediante un equilibrador de carga interno de Azure. Esta funcionalidad ya existe en el equilibrador de carga externo Azure Hola.

Si tiene una implementación de SAP, puede usar un toocreate de equilibrador de carga interno una configuración de clúster de Windows para SAP ASCS/SCS, tal como se documenta en hello [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows] [ sap-ha-guide].

En este artículo se centra en cómo toomove configuración de una única ASCS/SCS instalación tooan SAP multi-SID instalando adicionales SAP ASCS/SCS instancias en clúster en un clúster de clústeres de conmutación por error de servidor de Windows (WSFC) existente. Cuando se complete este proceso, habrá configurado un clúster de varios SID de SAP.


## <a name="prerequisites"></a>Requisitos previos
Ya ha configurado un clúster de WSFC que se usa para una instancia de SAP ASCS/SCS, según lo descrito en hello [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows] [ sap-ha-guide] y como se muestra en este diagrama.

![Instancia de ASCS/SCS de SAP de alta disponibilidad][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>Arquitectura de destino

Hello objetivo es tooinstall varios ABAP de SAP ASCS o SCS de SAP Java en clúster instancias Hola mismo clúster de WSFC, como se muestra aquí:

![Varias instancias en clúster ASCS/SCS de SAP en Azure][sap-ha-guide-figure-6002]

> [!NOTE]
>Hay un toohello limitar el número de direcciones IP de front-end privada para cada equilibrador de carga interno de Azure.
>
>número máximo de Hola de instancias de SAP ASCS/SCS en un clúster de WSFC es toohello igual número máximo de IP privadas de front-end para cada equilibrador de carga interno de Azure.
>

Para obtener información sobre los límites del equilibrador de carga, consulte IP de front-end privada por equilibrador de carga en [Límites de redes - Azure Resource Manager][networking-limits-azure-resource-manager].

perspectiva completa de Hello con dos sistemas SAP de alta disponibilidad sería similar al siguiente:

![Configuración de varios SID de alta disponibilidad de SAP con dos sistemas SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> el programa de instalación de Hello debe cumplir Hola condiciones siguientes:
> - Hello SAP ASCS/SCS instancias deben compartir Hola mismo clúster de WSFC.
> - Cada SID de DBMS tiene su propio clúster de WSFC dedicado.
> - Servidores de aplicaciones de SAP que pertenecen el sistema SAP tooone SID deben tener sus propias máquinas virtuales dedicadas.


## <a name="prepare-hello-infrastructure"></a>Preparar la infraestructura de Hola
tooprepare la infraestructura, puede instalar una instancia de SAP ASCS/SCS adicional con hello parámetros siguientes:

| Nombre de parámetro | Valor |
| --- | --- |
| SID de ASCS/SCS de SAP |pr1-lb-ascs |
| Equilibrador de carga interno de DBMS de SAP | PR5 |
| Nombre de host virtual de SAP | pr5-sap-cl |
| Dirección IP del host virtual de ASCS/SCS de SAP (dirección IP adicional de Azure Load Balancer) | 10.0.0.50 |
| Número de instancia de ASCS/SCS de SAP | 50 |
| Puerto de sondeo de ILB para instancia adicional de ASCS/SCS de SAP | 62350 |

> [!NOTE]
> Para las instancias en clúster ASCS/SCS de SAP, cada dirección IP requiere un puerto de sondeo específico. Por ejemplo, si una dirección IP en un equilibrador de carga interno de Azure usa el puerto de sondeo 62300, no puede usarlo ninguna otra dirección IP de ese equilibrador de carga.
>
>Para nuestro objetivo, dado que el puerto de sondeo 62300 está reservado, estamos usando el puerto de sondeo 62350.

Puede instalar instancias adicionales de SAP ASCS/SCS Hola existente clúster de WSFC con dos nodos:

| Rol de máquina virtual | Nombre de host de máquina virtual | Dirección IP estática |
| --- | --- | --- |
| Primer nodo del clúster de la instancia de ASCS/SCS |pr1-ascs-0 |10.0.0.10 |
| Segundo nodo del clúster de la instancia de ASCS/SCS |pr1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Crear un nombre de host virtual para la instancia de SAP ASCS/SCS de hello en clúster en el servidor DNS de Hola

Puede crear una entrada DNS para el nombre de host virtual Hola de instancia de hello ASCS/SCS mediante Hola parámetros siguientes:

| Nuevo nombre de host virtual de ASCS/SCS de SAP | Dirección IP asociada |
| --- | --- | --- |
|pr5-sap-cl |10.0.0.50 |

Hola nuevo nombre de host y dirección IP se muestran en hello Administrador de DNS, como se muestra en la siguiente captura de pantalla de hello:

![Lista de administrador de DNS resaltado Hola definido por entrada DNS para el nombre virtual del nuevo clúster SAP ASCS/SCS de Hola y dirección TCP/IP][sap-ha-guide-figure-6004]

procedimiento de Hola para crear una entrada DNS también se describe detalladamente en hello principal [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-9.1.1].

> [!NOTE]
> Hello nueva dirección IP que se asigna nombre a un host de virtual toohello de instancia adicional de ASCS/SCS de hello debe ser Hola igual a la nueva dirección IP Hola que asigna toohello equilibrador de carga de Azure de SAP.
>
>En nuestro escenario, la dirección IP de hello es 10.0.0.50.

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>Agregar un equilibrador de carga interno de Azure existente y tooan con dirección IP mediante PowerShell

toocreate más de una instancia de SAP ASCS/SCS en Hola WSFC mismo clúster, use PowerShell tooadd una tooan de dirección IP existente equilibrador de carga interno de Azure. Cada dirección IP requiere sus propias reglas de equilibrio de carga, puerto de sondeo, grupo de IP de front-end y grupo de back-end.

Hello siguiente script agrega un nueva IP dirección tooan equilibrador de carga existente. Actualice las variables de PowerShell de Hola para su entorno. script de Hola creará necesarias todas las reglas de equilibrio de carga para todos los puertos de SAP ASCS/SCS.

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
Después de ejecuta script de Hola, Hola resultados se muestran en Hola portal de Azure, como se muestra en la siguiente captura de pantalla de hello:

![Nuevo grupo de IP de front-end en hello portal de Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>Agregar discos toocluster máquinas y configurar el disco del recurso compartido de clúster de hello SIOS

Debe agregar un nuevo disco compartido de clúster para una nueva instancia adicional ASCS/SCS de SAP. Para Windows Server 2012 R2, disco de recurso compartido de clúster WSFC de hello actualmente en uso es la solución de software de SIOS DataKeeper de Hola.

Hola siguientes:
1. Agregar otro disco o los discos de Hola mismo tamaño (cuál tiene toostripe) tooeach de hello nodos de clúster y darles formato.
2. Configure la replicación de almacenamiento con SIOS DataKeeper.

Este procedimiento se da por supuesto que ya ha instalado SIOS DataKeeper de máquinas del clúster WSFC Hola. Si se ha instalado, ahora debe configurar la replicación entre máquinas Hola. Hola proceso se describe detalladamente en hello principal [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-8.12.3.3].  

![DataKeeper sincrónica de creación de reflejo de disco de recurso compartido de SAP ASCS/SCS nuevo Hola][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>Implementación de máquinas virtuales para servidores de aplicaciones SAP y clústeres de DBMS

preparar la infraestructura toocomplete hello para el segundo sistema de SAP hello, Hola siguientes:

1. Implementar máquinas virtuales dedicadas para servidores de aplicaciones de SAP y colocarlas en el propio grupo de disponibilidad dedicado
2. Implementar máquinas virtuales dedicadas para el clúster de DBMS y colocarlas en el propio grupo de disponibilidad dedicado


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>Instalar el segundo sistema de SAP NetWeaver de SID2 Hola

completar el proceso de instalar un segundo sistema SAP SID2 Hola se describe en hello principal [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-9].

procedimiento de alto nivel de Hello es como sigue:

1. [Instalar el primer nodo de clúster de hello SAP][sap-ha-guide-9.1.2].  
 En este paso, va a instalar SAP con una instancia ASCS/SCS de alta disponibilidad en hello **nodo de clúster de WSFC existente 1**.

2. [Modificar perfil SAP de Hola de instancia ASCS/SCS de hello][sap-ha-guide-9.1.3].

3. [Configuración de un puerto de sondeo][sap-ha-guide-9.1.4].  
 En este paso, va a configurar un puerto de sondeo SAP-SID2-IP del recurso de clúster de SAP mediante PowerShell. Esta configuración se ejecuta en uno de los nodos del clúster de SAP ASCS/SCS Hola.

4. [Instalación de instancia de base de datos de hello] [sap-ha-guía-9.2].  
 En este paso, va a instalar DBMS en un clúster WSFC específico.

5. [Instalación de segundo nodo de clúster Hola] [sap-ha-guía-9.3].  
 En este paso, va a instalar SAP con una instancia ASCS/SCS de alta disponibilidad en el nodo de clúster WSFC existente de hello 2.

6. Abrir los puertos de Firewall de Windows para la instancia de SAP ASCS/SCS de Hola y ProbePort.  
 En ambos nodos del clúster usados para la instancia ASCS/SCS de SAP, abra todos los puertos de Firewall de Windows usados por los puertos ASCS/SCS de SAP. Estos puertos se enumeran en hello [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-8.8].  
 Abrir Hola carga interno de Azure equilibrador puerto de sondeo, que es 62350 en nuestro escenario.

7. [Cambiar tipo de inicio de Hola de instancia de servicio de SAP ERS Windows hello][sap-ha-guide-9.4].

8. [Instalar el servidor principal de la aplicación de hello SAP] [ sap-ha-guide-9.5] en hello nuevo dedicado de máquina virtual.

9. [Instalar servidor de aplicaciones adicionales de SAP de hello] [ sap-ha-guide-9.6] en hello nuevo dedicado de máquina virtual.

10. [Probar la replicación de SIOS y conmutación por error de hello SAP ASCS/SCS instancia][sap-ha-guide-10].

## <a name="next-steps"></a>Pasos siguientes

- [Límites de redes - Azure Resource Manager][networking-limits-azure-resource-manager]
- [Varias IP virtuales para Azure Load Balancer][load-balancer-multivip-overview]
- [Guía de alta disponibilidad para SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide]
