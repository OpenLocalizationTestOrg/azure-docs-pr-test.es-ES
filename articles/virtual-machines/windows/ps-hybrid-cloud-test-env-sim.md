---
title: "entorno de prueba de nube híbrida de aaaSimulated | Documentos de Microsoft"
description: "Cree un entorno de nube híbrida simulado para profesionales de TI o pruebas de desarrollo con dos redes virtuales de Azure y una conexión de red virtual a red virtual."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="2aaf8-103">Configuración de un entorno de nube híbrida simulado para pruebas</span><span class="sxs-lookup"><span data-stu-id="2aaf8-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="2aaf8-104">Este artículo le guiará en el proceso de creación de un entorno de nube híbrida simulado con Microsoft Azure mediante dos redes virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="2aaf8-105">Esta es la configuración resultante de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="2aaf8-106">Esto simula un entorno de producción en la nube híbrida y consta de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2aaf8-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="2aaf8-107">Una red simulada y simplificado local hospedada en una red virtual (red virtual de hello práctica de prueba).</span><span class="sxs-lookup"><span data-stu-id="2aaf8-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="2aaf8-108">Una red virtual simulada entre locales hospedada en Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="2aaf8-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="2aaf8-109">Una conexión de red virtual a red virtual entre redes virtuales Hola dos.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="2aaf8-110">Un controlador de dominio secundario en la red virtual de hello TestVNET.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="2aaf8-111">Esto proporciona una base y un punto de partida común desde el que puede:</span><span class="sxs-lookup"><span data-stu-id="2aaf8-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="2aaf8-112">Desarrollar y probar las aplicaciones en un entorno de nube híbrida simulado.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="2aaf8-113">Crear configuraciones de pruebas de equipos, algunas dentro de la red virtual de hello práctica de prueba y otras en red virtual hello TestVNET, toosimulate híbrida basada en la nube TI las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="2aaf8-114">Hay cuatro toosetting fases principales en este entorno de prueba de nube híbrida:</span><span class="sxs-lookup"><span data-stu-id="2aaf8-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="2aaf8-115">Configurar red virtual de hello práctica de prueba.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="2aaf8-116">Crear red virtual entre entornos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="2aaf8-117">Crear la conexión de VPN de red virtual a red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="2aaf8-118">Configuración de DC2.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-118">Configure DC2.</span></span> 

<span data-ttu-id="2aaf8-119">Esta configuración requiere una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="2aaf8-120">Si tiene una suscripción de MSDN o de Visual Studio, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="2aaf8-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="2aaf8-121">Las máquinas virtuales y las puertas de enlace de redes virtuales en Azure incurren en un coste económico constante cuando se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="2aaf8-122">Este costo se factura en su suscripción de pago o MSDN.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="2aaf8-123">Una puerta de enlace de VPN de Azure se implementa como un conjunto de dos máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="2aaf8-124">los costos de hello toominimize, crear el entorno de prueba de Hola y realizar las pruebas y demostración necesarios lo más rápido posible.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="2aaf8-125">Fase 1: Configurar red virtual de hello práctica de prueba</span><span class="sxs-lookup"><span data-stu-id="2aaf8-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="2aaf8-126">Utilice instrucciones de Hola Hola [entorno de prueba de configuración de Base](https://technet.microsoft.com/library/mt771177.aspx) tema tooconfigure Hola DC1, APP1 y CLIENT1 equipos Hola red virtual de Azure denominado práctica de prueba.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="2aaf8-127">Después, inicie un símbolo del sistema de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="2aaf8-128">Hola siguientes conjuntos de comandos usa Azure PowerShell 1.0 y versiones posterior.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="2aaf8-129">Inicie sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="2aaf8-130">Obtiene el nombre de la suscripción con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="2aaf8-131">Establezca su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-131">Set your Azure subscription.</span></span> <span data-ttu-id="2aaf8-132">Use Hola misma suscripción utilizada toobuild de la configuración base en la fase 1.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="2aaf8-133">Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con el nombre correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="2aaf8-134">A continuación, agregar una puerta de enlace subred toohello práctica de prueba red virtual de la configuración base, que será usado toohost Hola puerta de enlace de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="2aaf8-135">A continuación, solicitar pública IP dirección tooassign toohello puerta de enlace de red virtual de hello práctica de prueba.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="2aaf8-136">A continuación, cree la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="2aaf8-137">Tenga en cuenta que las nuevas puertas de enlace pueden tardar 20 minutos o más toocreate.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="2aaf8-138">En hello portal de Azure en el equipo local, conéctese tooDC1 con las credenciales de CORP\User1 Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="2aaf8-139">dominio CORP hello tooconfigure para que los usuarios y equipos de usan su controlador de dominio local para la autenticación, ejecute estos comandos desde un símbolo de Windows PowerShell de nivel de administrador en DC1.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="2aaf8-140">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="2aaf8-141">Fase 2: Crear red virtual de hello TestVNET</span><span class="sxs-lookup"><span data-stu-id="2aaf8-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="2aaf8-142">En primer lugar, crear red virtual de hello TestVNET y protéjala con un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="2aaf8-143">A continuación, la solicitud una toobe de dirección IP pública asignada toohello puerta de enlace de red virtual de hello TestVNET y crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="2aaf8-144">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="2aaf8-145">Fase 3: Crear la conexión de red virtual a red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="2aaf8-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="2aaf8-146">En primer lugar, solicite una clave previamente compartida aleatoria criptográficamente segura de 32 caracteres al administrador de red o de seguridad.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="2aaf8-147">Como alternativa, use la información de hello en [crear una cadena aleatoria de una clave previamente compartida IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain una clave previamente compartida.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="2aaf8-148">A continuación, use estas conexiones de VPN de red virtual a red virtual de comandos toocreate hello, lo que pueden tardar algún tiempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="2aaf8-149">Después de unos minutos, se debe establecer la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="2aaf8-150">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="2aaf8-151">Fase 4: configuración de DC2</span><span class="sxs-lookup"><span data-stu-id="2aaf8-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="2aaf8-152">Primero, cree una máquina virtual para DC2.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="2aaf8-153">Ejecute estos comandos en línea de comandos de PowerShell de Azure de hello en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="2aaf8-154">A continuación, conectar toohello DC2 máquina virtual de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="2aaf8-155">A continuación, configure un tráfico de tooallow de regla de Firewall de Windows para probar la conectividad básica.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="2aaf8-156">Desde un símbolo del sistema de Windows PowerShell con nivel de administrador en DC2, ejecute estos comandos.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="2aaf8-157">comando ping de Hello debe producir cuatro respuestas correctas de dirección IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="2aaf8-158">Esto es una prueba de tráfico a través de hello conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="2aaf8-159">A continuación, agregue Hola disco de datos adicionales en DC2 como un volumen nuevo con una letra de unidad de hello F:.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="2aaf8-160">En el panel izquierdo del administrador del servidor de hello, haga clic en **File and Storage Services**y, a continuación, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="2aaf8-161">En panel de contenido de hello, Hola **discos** grupo, haga clic en **disco 2** (con hello **partición** establecido demasiado**desconocido**).</span><span class="sxs-lookup"><span data-stu-id="2aaf8-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="2aaf8-162">Haga clic en **Tareas** y luego haga clic en **Nuevo volumen**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="2aaf8-163">En hello antes de comenzar la página del Asistente para nuevo volumen hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="2aaf8-164">En el servidor seleccione Hola de Hola y página de disco, haga clic en **disco 2**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="2aaf8-165">Cuando se le solicite, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="2aaf8-166">En especificar el tamaño de Hola de página de volumen de Hola Hola, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="2aaf8-167">En hello asignar tooa unidad carpeta o letra de página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="2aaf8-168">En la página Configuración del sistema seleccione archivo hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="2aaf8-169">En la página Confirmar selecciones de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="2aaf8-170">Cuando haya terminado, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-170">When complete, click **Close**.</span></span>

<span data-ttu-id="2aaf8-171">A continuación, configure DC2 como un controlador de dominio de réplica para el dominio de corp.contoso.com Hola.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="2aaf8-172">Ejecutar estos comandos desde la línea de comandos de Windows PowerShell de hello en DC2.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="2aaf8-173">Tenga en cuenta que toosupply solicitada ambos Hola CORP\User1 contraseña y una contraseña de modo de restauración de servicios de directorio (DSRM) y toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="2aaf8-174">Ahora que hello TestVNET red virtual no tiene su propio servidor DNS (DC2), debe configurar toouse de red virtual de hello TestVNET este servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="2aaf8-175">En panel izquierdo de Hola de hello portal de Azure, haga clic en el icono de redes virtuales de hello y, a continuación, haga clic en **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="2aaf8-176">En hello **configuración** , haga clic en **servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="2aaf8-177">En **servidor DNS principal**, tipo **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="2aaf8-178">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-178">Click **Save**.</span></span>

<span data-ttu-id="2aaf8-179">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="2aaf8-180">Su entorno de nube híbrida simulado ya está listo para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="2aaf8-181">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="2aaf8-181">Next step</span></span>
* <span data-ttu-id="2aaf8-182">Configure una [aplicación de línea de negocio web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en este entorno.</span><span class="sxs-lookup"><span data-stu-id="2aaf8-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

