---
title: "Creación de una configuración de varios SID de SAP en Azure | Microsoft Docs"
description: "Guía de alta disponibilidad para la configuración de varios SID de SAP NetWeaver en máquinas virtuales Windows"
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
ms.openlocfilehash: b48df78df9f53ac7bf0804f55a8d36a2fe2f86b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="2e578-103">Creación de una configuración de varios SID de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="2e578-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="2e578-104">En septiembre de 2016, Microsoft publicó una característica con la que puede administrar varias direcciones IP virtuales mediante un equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e578-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="2e578-105">Esta funcionalidad ya existe en el equilibrador de carga externo de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e578-105">This functionality already exists in the Azure external load balancer.</span></span>

<span data-ttu-id="2e578-106">Si tiene una implementación de SAP, puede usar un equilibrador de carga interno para crear una configuración de clúster de Windows para ASCS/SCS de SAP, tal y como se describe en la [guía de alta disponibilidad de SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="2e578-106">If you have an SAP deployment, you can use an internal load balancer to create a Windows cluster configuration for SAP ASCS/SCS, as documented in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="2e578-107">En este artículo nos centraremos en cómo pasar de una sola instalación ASCS/SCS de este tipo a una configuración de varios SID de SAP mediante la instalación de instancias en clúster ASCS/SCS de SAP adicionales en un clúster de servidor de conmutación por error de Windows (WSFC) existente.</span><span class="sxs-lookup"><span data-stu-id="2e578-107">This article focuses on how to move from a single ASCS/SCS installation to an SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="2e578-108">Cuando se complete este proceso, habrá configurado un clúster de varios SID de SAP.</span><span class="sxs-lookup"><span data-stu-id="2e578-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2e578-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2e578-109">Prerequisites</span></span>
<span data-ttu-id="2e578-110">Ya ha configurado un clúster de WSFC que se usa para una instancia de ASCS/SCS de SAP, tal como se describe en la [guía de alta disponibilidad SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide] y se muestra en este diagrama.</span><span class="sxs-lookup"><span data-stu-id="2e578-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Instancia de ASCS/SCS de SAP de alta disponibilidad][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="2e578-112">Arquitectura de destino</span><span class="sxs-lookup"><span data-stu-id="2e578-112">Target architecture</span></span>

<span data-ttu-id="2e578-113">El objetivo es poder instalar varias instancias en clúster SAP ABAP ASCS o SAP Java SCS en el mismo clúster de WSFC:</span><span class="sxs-lookup"><span data-stu-id="2e578-113">The goal is to install multiple SAP ABAP ASCS or SAP Java SCS clustered instances in the same WSFC cluster, as illustrated here:</span></span>

![Varias instancias en clúster ASCS/SCS de SAP en Azure][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="2e578-115">Hay un límite en el número de direcciones IP de front-end privadas por cada equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e578-115">There is a limit to the number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="2e578-116">El número máximo de instancias ASCS/SCS de SAP en un clúster de WSFC es igual al número máximo de IP de front-end privadas por equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e578-116">The maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal to the maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="2e578-117">Para obtener información sobre los límites del equilibrador de carga, consulte IP de front-end privada por equilibrador de carga en [Límites de redes - Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="2e578-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="2e578-118">La visión global con la perspectiva completa con dos sistemas SAP de alta disponibilidad sería esta:</span><span class="sxs-lookup"><span data-stu-id="2e578-118">The complete landscape with two high-availability SAP systems would look like this:</span></span>

![Configuración de varios SID de alta disponibilidad de SAP con dos sistemas SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="2e578-120">Debe cumplir las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="2e578-120">The setup must meet the following conditions:</span></span>
> - <span data-ttu-id="2e578-121">Las instancias ASCS/SCS de SAP deben compartir el mismo clúster de WSFC.</span><span class="sxs-lookup"><span data-stu-id="2e578-121">The SAP ASCS/SCS instances must share the same WSFC cluster.</span></span>
> - <span data-ttu-id="2e578-122">Cada SID de DBMS tiene su propio clúster de WSFC dedicado.</span><span class="sxs-lookup"><span data-stu-id="2e578-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="2e578-123">Los servidores de aplicaciones de SAP que pertenecen a un SID del sistema SAP tienen sus propias máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="2e578-123">SAP application servers that belong to one SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-the-infrastructure"></a><span data-ttu-id="2e578-124">Preparación de la infraestructura</span><span class="sxs-lookup"><span data-stu-id="2e578-124">Prepare the infrastructure</span></span>
<span data-ttu-id="2e578-125">Para preparar la infraestructura, puede instalar una instancia de ASCS/SCS de SAP adicionales con los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="2e578-125">To prepare your infrastructure, you can install an additional SAP ASCS/SCS instance with the following parameters:</span></span>

| <span data-ttu-id="2e578-126">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2e578-126">Parameter name</span></span> | <span data-ttu-id="2e578-127">Valor</span><span class="sxs-lookup"><span data-stu-id="2e578-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2e578-128">SID de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="2e578-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="2e578-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="2e578-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="2e578-130">Equilibrador de carga interno de DBMS de SAP</span><span class="sxs-lookup"><span data-stu-id="2e578-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="2e578-131">PR5</span><span class="sxs-lookup"><span data-stu-id="2e578-131">PR5</span></span> |
| <span data-ttu-id="2e578-132">Nombre de host virtual de SAP</span><span class="sxs-lookup"><span data-stu-id="2e578-132">SAP virtual host name</span></span> | <span data-ttu-id="2e578-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="2e578-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="2e578-134">Dirección IP del host virtual de ASCS/SCS de SAP (dirección IP adicional de Azure Load Balancer)</span><span class="sxs-lookup"><span data-stu-id="2e578-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="2e578-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="2e578-135">10.0.0.50</span></span> |
| <span data-ttu-id="2e578-136">Número de instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="2e578-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="2e578-137">50</span><span class="sxs-lookup"><span data-stu-id="2e578-137">50</span></span> |
| <span data-ttu-id="2e578-138">Puerto de sondeo de ILB para instancia adicional de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="2e578-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="2e578-139">62350</span><span class="sxs-lookup"><span data-stu-id="2e578-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="2e578-140">Para las instancias en clúster ASCS/SCS de SAP, cada dirección IP requiere un puerto de sondeo específico.</span><span class="sxs-lookup"><span data-stu-id="2e578-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="2e578-141">Por ejemplo, si una dirección IP en un equilibrador de carga interno de Azure usa el puerto de sondeo 62300, no puede usarlo ninguna otra dirección IP de ese equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="2e578-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="2e578-142">Para nuestro objetivo, dado que el puerto de sondeo 62300 está reservado, estamos usando el puerto de sondeo 62350.</span><span class="sxs-lookup"><span data-stu-id="2e578-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="2e578-143">Instalará la instancia adicional ASCS/SCS de SAP en el clúster de WSFC existente con dos nodos:</span><span class="sxs-lookup"><span data-stu-id="2e578-143">You can install additional SAP ASCS/SCS instances in the existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="2e578-144">Rol de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2e578-144">Virtual machine role</span></span> | <span data-ttu-id="2e578-145">Nombre de host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2e578-145">Virtual machine host name</span></span> | <span data-ttu-id="2e578-146">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="2e578-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e578-147">Primer nodo del clúster de la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="2e578-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="2e578-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="2e578-148">pr1-ascs-0</span></span> |<span data-ttu-id="2e578-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="2e578-149">10.0.0.10</span></span> |
| <span data-ttu-id="2e578-150">Segundo nodo del clúster de la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="2e578-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="2e578-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="2e578-151">pr1-ascs-1</span></span> |<span data-ttu-id="2e578-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="2e578-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a><span data-ttu-id="2e578-153">Creación de un nombre de host virtual para la instancia de ASCS/SCS de SAP en clúster en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="2e578-153">Create a virtual host name for the clustered SAP ASCS/SCS instance on the DNS server</span></span>

<span data-ttu-id="2e578-154">Puede crear una entrada DNS para el nombre de host virtual de la instancia de ASCS/SCS con los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="2e578-154">You can create a DNS entry for the virtual host name of the ASCS/SCS instance by using the following parameters:</span></span>

| <span data-ttu-id="2e578-155">Nuevo nombre de host virtual de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="2e578-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="2e578-156">Dirección IP asociada</span><span class="sxs-lookup"><span data-stu-id="2e578-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="2e578-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="2e578-157">pr5-sap-cl</span></span> |<span data-ttu-id="2e578-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="2e578-158">10.0.0.50</span></span> |

<span data-ttu-id="2e578-159">El nuevo nombre de host y la dirección IP se muestran en el Administrador de DNS, como se muestra en la captura de pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="2e578-159">The new host name and IP address are displayed in the DNS Manager, as shown in the following screenshot:</span></span>

![El Administrador de DNS destaca la entrada DNS para el nombre virtual del clúster de ASCS/SCS de SAP y la dirección TCP/IP.][sap-ha-guide-figure-6004]

<span data-ttu-id="2e578-161">El procedimiento de creación de una entrada DNS también se describe en [Guía de alta disponibilidad de SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="2e578-161">The procedure for creating a DNS entry is also described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="2e578-162">La dirección IP que asigna al nombre de host virtual de la instancia de ASCS/SCS adicional debe ser la misma que la nueva dirección IP que asignó a Azure Load Balancer para SAP.</span><span class="sxs-lookup"><span data-stu-id="2e578-162">The new IP address that you assign to the virtual host name of the additional ASCS/SCS instance must be the same as the new IP address that you assigned to the SAP Azure load balancer.</span></span>
>
><span data-ttu-id="2e578-163">En nuestro escenario, la dirección IP es 10.0.0.50.</span><span class="sxs-lookup"><span data-stu-id="2e578-163">In our scenario, the IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="2e578-164">Adición de una dirección IP a un equilibrador de carga interno de Azure existente con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e578-164">Add an IP address to an existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="2e578-165">Para crear más de una instancia de ASCS/SCS de SAP en el mismo clúster de WSFC, utilice PowerShell para agregar una dirección IP adicional a un equilibrador de carga interno de Azure existente.</span><span class="sxs-lookup"><span data-stu-id="2e578-165">To create more than one SAP ASCS/SCS instance in the same WSFC cluster, use PowerShell to add an IP address to an existing Azure internal load balancer.</span></span> <span data-ttu-id="2e578-166">Cada dirección IP requiere sus propias reglas de equilibrio de carga, puerto de sondeo, grupo de IP de front-end y grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="2e578-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="2e578-167">El script siguiente agrega una nueva dirección IP a un equilibrador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="2e578-167">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="2e578-168">Actualice las variables de PowerShell de su entorno.</span><span class="sxs-lookup"><span data-stu-id="2e578-168">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="2e578-169">El script creará todas las reglas de equilibrio de carga necesarias para todos los puertos de ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="2e578-169">The script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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

# Get the Azure VNet and subnet
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

# Assign VM NICs to backend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="2e578-170">Cuando se haya ejecutado el script, los resultados se muestran en Azure Portal, como se muestra en la captura de pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="2e578-170">After the script has run, the results are displayed in the Azure portal, as shown in the following screenshot:</span></span>

![Nuevo grupo de IP de front-end en Azure Portal][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a><span data-ttu-id="2e578-172">Adición de máquinas de clúster y configuración de discos compartidos de clúster de SIOS</span><span class="sxs-lookup"><span data-stu-id="2e578-172">Add disks to cluster machines, and configure the SIOS cluster share disk</span></span>

<span data-ttu-id="2e578-173">Debe agregar un nuevo disco compartido de clúster para una nueva instancia adicional ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="2e578-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="2e578-174">Para Windows Server 2012 R2, el disco compartido de clúster de WSFC que se usa actualmente es la solución de software SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="2e578-174">For Windows Server 2012 R2, the WSFC cluster share disk currently in use is the SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="2e578-175">Haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2e578-175">Do the following:</span></span>
1. <span data-ttu-id="2e578-176">Agregue discos adicionales o del mismo tamaño (que deba seccionar) con el mismo tamaño a cada uno de los nodos del clúster y formatéelos.</span><span class="sxs-lookup"><span data-stu-id="2e578-176">Add an additional disk or disks of the same size (which you need to stripe) to each of the cluster nodes, and format them.</span></span>
2. <span data-ttu-id="2e578-177">Configure la replicación de almacenamiento con SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="2e578-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="2e578-178">Este procedimiento da por supuesto que ya ha instalado SIOS DataKeeper en los equipos del clúster WSFC.</span><span class="sxs-lookup"><span data-stu-id="2e578-178">This procedure assumes that you have already installed SIOS DataKeeper on the WSFC cluster machines.</span></span> <span data-ttu-id="2e578-179">Si se ha instalado, ahora debe configurar la replicación entre las máquinas.</span><span class="sxs-lookup"><span data-stu-id="2e578-179">If you have installed it, you must now configure replication between the machines.</span></span> <span data-ttu-id="2e578-180">El procedimiento se describe detalladamente en la [Guía de alta disponibilidad de SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="2e578-180">The process is described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![El reflejo sincrónico de DataKeeper para el disco compartido de ASCS/SCS de SAP][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="2e578-182">Implementación de máquinas virtuales para servidores de aplicaciones SAP y clústeres de DBMS</span><span class="sxs-lookup"><span data-stu-id="2e578-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="2e578-183">Con el fin de finalizar la preparación de la infraestructura para el segundo sistema SAP, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2e578-183">To complete the infrastructure preparation for the second SAP system, do the following:</span></span>

1. <span data-ttu-id="2e578-184">Implementar máquinas virtuales dedicadas para servidores de aplicaciones de SAP y colocarlas en el propio grupo de disponibilidad dedicado</span><span class="sxs-lookup"><span data-stu-id="2e578-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="2e578-185">Implementar máquinas virtuales dedicadas para el clúster de DBMS y colocarlas en el propio grupo de disponibilidad dedicado</span><span class="sxs-lookup"><span data-stu-id="2e578-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-the-second-sap-sid2-netweaver-system"></a><span data-ttu-id="2e578-186">Instalar el segundo sistema SAP SID2 NetWeaver</span><span class="sxs-lookup"><span data-stu-id="2e578-186">Install the second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="2e578-187">El procedimiento completo de instalar un segundo sistema SID2 de SAP se describe detalladamente en la [Guía de alta disponibilidad de SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="2e578-187">The complete process of installing a second SAP SID2 system is described in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="2e578-188">El procedimiento general es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="2e578-188">The high-level procedure is as follows:</span></span>

1. <span data-ttu-id="2e578-189">[Instalación del primer nodo de clúster de SAP][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="2e578-189">[Install the SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="2e578-190">En este paso, instalará SAP con una instancia de ASCS/SCS de alta disponibilidad en el **nodo 1 del clúster de WSFC existente**.</span><span class="sxs-lookup"><span data-stu-id="2e578-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="2e578-191">[Modificación del perfil SAP de la instancia de ASCS/SCS][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="2e578-191">[Modify the SAP profile of the ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="2e578-192">[Configuración de un puerto de sondeo][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="2e578-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="2e578-193">En este paso, va a configurar un puerto de sondeo SAP-SID2-IP del recurso de clúster de SAP mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e578-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="2e578-194">Ejecute esta configuración en uno de los nodos del clúster ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="2e578-194">Execute this configuration on one of the SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="2e578-195">[Instalación de la instancia de base de datos][sap-ha-guide-9.2].</span><span class="sxs-lookup"><span data-stu-id="2e578-195">[Install the database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="2e578-196">En este paso, va a instalar DBMS en un clúster WSFC específico.</span><span class="sxs-lookup"><span data-stu-id="2e578-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="2e578-197">[Instalación del segundo nodo del clúster][sap-ha-guide-9.3].</span><span class="sxs-lookup"><span data-stu-id="2e578-197">[Install the second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="2e578-198">En este paso, instalará SAP con una instancia de ASCS/SCS de alta disponibilidad en el nodo 2 del clúster de WSFC existente.</span><span class="sxs-lookup"><span data-stu-id="2e578-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="2e578-199">Abra los puertos de Firewall de Windows de la instancia ASCS/SCS de SAP y el puerto de sondeo.</span><span class="sxs-lookup"><span data-stu-id="2e578-199">Open Windows Firewall ports for the SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="2e578-200">En ambos nodos del clúster usados para la instancia ASCS/SCS de SAP, abra todos los puertos de Firewall de Windows usados por los puertos ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="2e578-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="2e578-201">Estos puertos se enumeran en la [Guía de alta disponibilidad de SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="2e578-201">These ports are listed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="2e578-202">Además, abra el puerto de sondeo del equilibrador de carga interno de Azure, que en nuestro caso es 62350.</span><span class="sxs-lookup"><span data-stu-id="2e578-202">Also open the Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="2e578-203">[Cambio del tipo de inicio del servicio de Windows para la instancia de ERS de SAP][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="2e578-203">[Change the start type of the SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="2e578-204">[Instalación del servidor de aplicaciones principal de SAP][sap-ha-guide-9.5] en la nueva máquina virtual dedicada.</span><span class="sxs-lookup"><span data-stu-id="2e578-204">[Install the SAP primary application server][sap-ha-guide-9.5] on the new dedicated VM.</span></span>

9. <span data-ttu-id="2e578-205">[Instalación del servidor de aplicaciones adicional de SAP][sap-ha-guide-9.6] en la nueva máquina virtual dedicada.</span><span class="sxs-lookup"><span data-stu-id="2e578-205">[Install the SAP additional application server][sap-ha-guide-9.6] on the new dedicated VM.</span></span>

10. <span data-ttu-id="2e578-206">[Prueba de la conmutación por error de la instancia de ASCS/SCS de SAP y de la replicación de SIOS][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="2e578-206">[Test the SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e578-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2e578-207">Next steps</span></span>

- <span data-ttu-id="2e578-208">[Límites de redes - Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="2e578-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="2e578-209">[Varias IP virtuales para Azure Load Balancer][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="2e578-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="2e578-210">[Guía de alta disponibilidad para SAP NetWeaver en máquinas virtuales Windows][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="2e578-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
