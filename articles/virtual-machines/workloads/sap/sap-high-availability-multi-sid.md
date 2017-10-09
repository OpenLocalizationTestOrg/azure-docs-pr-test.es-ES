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
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="ffa96-103">Creación de una configuración de varios SID de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="ffa96-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="ffa96-104">En septiembre de 2016, Microsoft publicó una característica con la que puede administrar varias direcciones IP virtuales mediante un equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa96-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="ffa96-105">Esta funcionalidad ya existe en el equilibrador de carga externo Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="ffa96-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="ffa96-106">Si tiene una implementación de SAP, puede usar un toocreate de equilibrador de carga interno una configuración de clúster de Windows para SAP ASCS/SCS, tal como se documenta en hello [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="ffa96-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="ffa96-107">En este artículo se centra en cómo toomove configuración de una única ASCS/SCS instalación tooan SAP multi-SID instalando adicionales SAP ASCS/SCS instancias en clúster en un clúster de clústeres de conmutación por error de servidor de Windows (WSFC) existente.</span><span class="sxs-lookup"><span data-stu-id="ffa96-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="ffa96-108">Cuando se complete este proceso, habrá configurado un clúster de varios SID de SAP.</span><span class="sxs-lookup"><span data-stu-id="ffa96-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ffa96-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ffa96-109">Prerequisites</span></span>
<span data-ttu-id="ffa96-110">Ya ha configurado un clúster de WSFC que se usa para una instancia de SAP ASCS/SCS, según lo descrito en hello [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows] [ sap-ha-guide] y como se muestra en este diagrama.</span><span class="sxs-lookup"><span data-stu-id="ffa96-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Instancia de ASCS/SCS de SAP de alta disponibilidad][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="ffa96-112">Arquitectura de destino</span><span class="sxs-lookup"><span data-stu-id="ffa96-112">Target architecture</span></span>

<span data-ttu-id="ffa96-113">Hello objetivo es tooinstall varios ABAP de SAP ASCS o SCS de SAP Java en clúster instancias Hola mismo clúster de WSFC, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="ffa96-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Varias instancias en clúster ASCS/SCS de SAP en Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="ffa96-115">Hay un toohello limitar el número de direcciones IP de front-end privada para cada equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa96-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="ffa96-116">número máximo de Hola de instancias de SAP ASCS/SCS en un clúster de WSFC es toohello igual número máximo de IP privadas de front-end para cada equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa96-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="ffa96-117">Para obtener información sobre los límites del equilibrador de carga, consulte IP de front-end privada por equilibrador de carga en [Límites de redes - Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="ffa96-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="ffa96-118">perspectiva completa de Hello con dos sistemas SAP de alta disponibilidad sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ffa96-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![Configuración de varios SID de alta disponibilidad de SAP con dos sistemas SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="ffa96-120">el programa de instalación de Hello debe cumplir Hola condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffa96-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="ffa96-121">Hello SAP ASCS/SCS instancias deben compartir Hola mismo clúster de WSFC.</span><span class="sxs-lookup"><span data-stu-id="ffa96-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="ffa96-122">Cada SID de DBMS tiene su propio clúster de WSFC dedicado.</span><span class="sxs-lookup"><span data-stu-id="ffa96-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="ffa96-123">Servidores de aplicaciones de SAP que pertenecen el sistema SAP tooone SID deben tener sus propias máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="ffa96-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="ffa96-124">Preparar la infraestructura de Hola</span><span class="sxs-lookup"><span data-stu-id="ffa96-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="ffa96-125">tooprepare la infraestructura, puede instalar una instancia de SAP ASCS/SCS adicional con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffa96-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="ffa96-126">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="ffa96-126">Parameter name</span></span> | <span data-ttu-id="ffa96-127">Valor</span><span class="sxs-lookup"><span data-stu-id="ffa96-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ffa96-128">SID de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="ffa96-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="ffa96-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="ffa96-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="ffa96-130">Equilibrador de carga interno de DBMS de SAP</span><span class="sxs-lookup"><span data-stu-id="ffa96-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="ffa96-131">PR5</span><span class="sxs-lookup"><span data-stu-id="ffa96-131">PR5</span></span> |
| <span data-ttu-id="ffa96-132">Nombre de host virtual de SAP</span><span class="sxs-lookup"><span data-stu-id="ffa96-132">SAP virtual host name</span></span> | <span data-ttu-id="ffa96-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="ffa96-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="ffa96-134">Dirección IP del host virtual de ASCS/SCS de SAP (dirección IP adicional de Azure Load Balancer)</span><span class="sxs-lookup"><span data-stu-id="ffa96-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="ffa96-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="ffa96-135">10.0.0.50</span></span> |
| <span data-ttu-id="ffa96-136">Número de instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="ffa96-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="ffa96-137">50</span><span class="sxs-lookup"><span data-stu-id="ffa96-137">50</span></span> |
| <span data-ttu-id="ffa96-138">Puerto de sondeo de ILB para instancia adicional de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="ffa96-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="ffa96-139">62350</span><span class="sxs-lookup"><span data-stu-id="ffa96-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="ffa96-140">Para las instancias en clúster ASCS/SCS de SAP, cada dirección IP requiere un puerto de sondeo específico.</span><span class="sxs-lookup"><span data-stu-id="ffa96-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="ffa96-141">Por ejemplo, si una dirección IP en un equilibrador de carga interno de Azure usa el puerto de sondeo 62300, no puede usarlo ninguna otra dirección IP de ese equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="ffa96-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="ffa96-142">Para nuestro objetivo, dado que el puerto de sondeo 62300 está reservado, estamos usando el puerto de sondeo 62350.</span><span class="sxs-lookup"><span data-stu-id="ffa96-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="ffa96-143">Puede instalar instancias adicionales de SAP ASCS/SCS Hola existente clúster de WSFC con dos nodos:</span><span class="sxs-lookup"><span data-stu-id="ffa96-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="ffa96-144">Rol de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ffa96-144">Virtual machine role</span></span> | <span data-ttu-id="ffa96-145">Nombre de host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ffa96-145">Virtual machine host name</span></span> | <span data-ttu-id="ffa96-146">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="ffa96-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffa96-147">Primer nodo del clúster de la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="ffa96-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="ffa96-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="ffa96-148">pr1-ascs-0</span></span> |<span data-ttu-id="ffa96-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="ffa96-149">10.0.0.10</span></span> |
| <span data-ttu-id="ffa96-150">Segundo nodo del clúster de la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="ffa96-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="ffa96-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="ffa96-151">pr1-ascs-1</span></span> |<span data-ttu-id="ffa96-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="ffa96-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="ffa96-153">Crear un nombre de host virtual para la instancia de SAP ASCS/SCS de hello en clúster en el servidor DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="ffa96-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="ffa96-154">Puede crear una entrada DNS para el nombre de host virtual Hola de instancia de hello ASCS/SCS mediante Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffa96-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="ffa96-155">Nuevo nombre de host virtual de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="ffa96-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="ffa96-156">Dirección IP asociada</span><span class="sxs-lookup"><span data-stu-id="ffa96-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="ffa96-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="ffa96-157">pr5-sap-cl</span></span> |<span data-ttu-id="ffa96-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="ffa96-158">10.0.0.50</span></span> |

<span data-ttu-id="ffa96-159">Hola nuevo nombre de host y dirección IP se muestran en hello Administrador de DNS, como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="ffa96-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Lista de administrador de DNS resaltado Hola definido por entrada DNS para el nombre virtual del nuevo clúster SAP ASCS/SCS de Hola y dirección TCP/IP][sap-ha-guide-figure-6004]

<span data-ttu-id="ffa96-161">procedimiento de Hola para crear una entrada DNS también se describe detalladamente en hello principal [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="ffa96-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="ffa96-162">Hello nueva dirección IP que se asigna nombre a un host de virtual toohello de instancia adicional de ASCS/SCS de hello debe ser Hola igual a la nueva dirección IP Hola que asigna toohello equilibrador de carga de Azure de SAP.</span><span class="sxs-lookup"><span data-stu-id="ffa96-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="ffa96-163">En nuestro escenario, la dirección IP de hello es 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="ffa96-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="ffa96-164">Agregar un equilibrador de carga interno de Azure existente y tooan con dirección IP mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa96-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="ffa96-165">toocreate más de una instancia de SAP ASCS/SCS en Hola WSFC mismo clúster, use PowerShell tooadd una tooan de dirección IP existente equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa96-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="ffa96-166">Cada dirección IP requiere sus propias reglas de equilibrio de carga, puerto de sondeo, grupo de IP de front-end y grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="ffa96-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="ffa96-167">Hello siguiente script agrega un nueva IP dirección tooan equilibrador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="ffa96-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="ffa96-168">Actualice las variables de PowerShell de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="ffa96-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="ffa96-169">script de Hola creará necesarias todas las reglas de equilibrio de carga para todos los puertos de SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="ffa96-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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
<span data-ttu-id="ffa96-170">Después de ejecuta script de Hola, Hola resultados se muestran en Hola portal de Azure, como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="ffa96-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Nuevo grupo de IP de front-end en hello portal de Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="ffa96-172">Agregar discos toocluster máquinas y configurar el disco del recurso compartido de clúster de hello SIOS</span><span class="sxs-lookup"><span data-stu-id="ffa96-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="ffa96-173">Debe agregar un nuevo disco compartido de clúster para una nueva instancia adicional ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="ffa96-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="ffa96-174">Para Windows Server 2012 R2, disco de recurso compartido de clúster WSFC de hello actualmente en uso es la solución de software de SIOS DataKeeper de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffa96-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="ffa96-175">Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffa96-175">Do hello following:</span></span>
1. <span data-ttu-id="ffa96-176">Agregar otro disco o los discos de Hola mismo tamaño (cuál tiene toostripe) tooeach de hello nodos de clúster y darles formato.</span><span class="sxs-lookup"><span data-stu-id="ffa96-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="ffa96-177">Configure la replicación de almacenamiento con SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="ffa96-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="ffa96-178">Este procedimiento se da por supuesto que ya ha instalado SIOS DataKeeper de máquinas del clúster WSFC Hola.</span><span class="sxs-lookup"><span data-stu-id="ffa96-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="ffa96-179">Si se ha instalado, ahora debe configurar la replicación entre máquinas Hola.</span><span class="sxs-lookup"><span data-stu-id="ffa96-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="ffa96-180">Hola proceso se describe detalladamente en hello principal [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="ffa96-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper sincrónica de creación de reflejo de disco de recurso compartido de SAP ASCS/SCS nuevo Hola][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="ffa96-182">Implementación de máquinas virtuales para servidores de aplicaciones SAP y clústeres de DBMS</span><span class="sxs-lookup"><span data-stu-id="ffa96-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="ffa96-183">preparar la infraestructura toocomplete hello para el segundo sistema de SAP hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffa96-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="ffa96-184">Implementar máquinas virtuales dedicadas para servidores de aplicaciones de SAP y colocarlas en el propio grupo de disponibilidad dedicado</span><span class="sxs-lookup"><span data-stu-id="ffa96-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="ffa96-185">Implementar máquinas virtuales dedicadas para el clúster de DBMS y colocarlas en el propio grupo de disponibilidad dedicado</span><span class="sxs-lookup"><span data-stu-id="ffa96-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="ffa96-186">Instalar el segundo sistema de SAP NetWeaver de SID2 Hola</span><span class="sxs-lookup"><span data-stu-id="ffa96-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="ffa96-187">completar el proceso de instalar un segundo sistema SAP SID2 Hola se describe en hello principal [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="ffa96-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="ffa96-188">procedimiento de alto nivel de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="ffa96-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="ffa96-189">[Instalar el primer nodo de clúster de hello SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="ffa96-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="ffa96-190">En este paso, va a instalar SAP con una instancia ASCS/SCS de alta disponibilidad en hello **nodo de clúster de WSFC existente 1**.</span><span class="sxs-lookup"><span data-stu-id="ffa96-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="ffa96-191">[Modificar perfil SAP de Hola de instancia ASCS/SCS de hello][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="ffa96-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="ffa96-192">[Configuración de un puerto de sondeo][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="ffa96-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="ffa96-193">En este paso, va a configurar un puerto de sondeo SAP-SID2-IP del recurso de clúster de SAP mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa96-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="ffa96-194">Esta configuración se ejecuta en uno de los nodos del clúster de SAP ASCS/SCS Hola.</span><span class="sxs-lookup"><span data-stu-id="ffa96-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="ffa96-195">[Instalación de instancia de base de datos de hello] [sap-ha-guía-9.2].</span><span class="sxs-lookup"><span data-stu-id="ffa96-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="ffa96-196">En este paso, va a instalar DBMS en un clúster WSFC específico.</span><span class="sxs-lookup"><span data-stu-id="ffa96-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="ffa96-197">[Instalación de segundo nodo de clúster Hola] [sap-ha-guía-9.3].</span><span class="sxs-lookup"><span data-stu-id="ffa96-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="ffa96-198">En este paso, va a instalar SAP con una instancia ASCS/SCS de alta disponibilidad en el nodo de clúster WSFC existente de hello 2.</span><span class="sxs-lookup"><span data-stu-id="ffa96-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="ffa96-199">Abrir los puertos de Firewall de Windows para la instancia de SAP ASCS/SCS de Hola y ProbePort.</span><span class="sxs-lookup"><span data-stu-id="ffa96-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="ffa96-200">En ambos nodos del clúster usados para la instancia ASCS/SCS de SAP, abra todos los puertos de Firewall de Windows usados por los puertos ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="ffa96-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="ffa96-201">Estos puertos se enumeran en hello [guía para alta disponibilidad SAP NetWeaver en máquinas virtuales de Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="ffa96-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="ffa96-202">Abrir Hola carga interno de Azure equilibrador puerto de sondeo, que es 62350 en nuestro escenario.</span><span class="sxs-lookup"><span data-stu-id="ffa96-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="ffa96-203">[Cambiar tipo de inicio de Hola de instancia de servicio de SAP ERS Windows hello][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="ffa96-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="ffa96-204">[Instalar el servidor principal de la aplicación de hello SAP] [ sap-ha-guide-9.5] en hello nuevo dedicado de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ffa96-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="ffa96-205">[Instalar servidor de aplicaciones adicionales de SAP de hello] [ sap-ha-guide-9.6] en hello nuevo dedicado de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ffa96-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="ffa96-206">[Probar la replicación de SIOS y conmutación por error de hello SAP ASCS/SCS instancia][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="ffa96-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa96-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ffa96-207">Next steps</span></span>

- <span data-ttu-id="ffa96-208">[Límites de redes - Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="ffa96-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="ffa96-209">[Varias IP virtuales para Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="ffa96-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="ffa96-210">[Guía de alta disponibilidad para SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="ffa96-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
